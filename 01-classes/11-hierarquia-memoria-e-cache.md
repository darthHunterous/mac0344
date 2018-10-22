# Aulas 11 e 12 - Hierarquia de Memória e Memória Cache
### Hierarquia de Memória
* **Características**
    * Custo
    * Capacidade
    * Velocidade
* Memória rápida: custosa e baixa capacidade
* **Hierarquia**
    * Registradores: memórias rápidas dentro do processador
    * Níveis de memória cache (on-chip L1, off-chip L2, etc)
    * Memória principal (RAM)
    * Memória externa ou secundária (discos)
    * Armazenamento remoto (web)

### Memória Cache
* Níveis de cache: L1, L2, L3
    * L1 tem menor capacidade mas maior velocidade
* **Cache hit**: quando um dado buscado pelo processador já está no cache, caso contrário, **cache miss** (necessário buscar na memória ou disco)
* Ao acessar um dado na memória, um bloco inteiro (geralmente 64 bytes) é trazido ao cache
    * **Prefetching:** acesso de blocos vizinhos para uso futuro
    * No próximo uso do dado, ele já estará no cache, de acesso rápido
    * **Analogia com supermercado:** se falta ovo (dado) na cozinha (processador), vai-se ao supermercado (memória), comprando uma dúzia (prefetching) e deixando na geladeira (cache) para os próximos usos

### Cache no i7
* 8x 32k L1, 4x 256k L2 e 8 MB L3
    * L3 cache é conhecido como LL ou Last Level cache

### Latência em Ciclos
* Registrador: 1 ciclo
* L1 cache: 4 ciclos
* L2 cache: 11 ciclos
* L3 cache: 39 ciclos
* RAM: 107 ciclos
* Disco: milhões de ciclos

### Evolução do uso de Cache
* VAX-11/780 (1978): 16 KB L1
* IBM 3090 (1985): 128 KB L1
* Pentium (1993): 8 KB L1 + 256 KB L2
* Itanium (2001): 16 KB L1 + 96 KB L2 + 4 MB L3
* IBM Power6 (2007): 64 KB L1 + 4 MB L2 + 32 MB L3
* IBM Power9 - 24 cores (2017): (32 KB I + 64 KB D) L1 por núcleo + 512 KB L2 por núcleo + 120 MB L3 por chip

### Organização do Cache
* Contém L linhas
* Cada linha contém tag, bloco de palavras da memória e bits de controle
    * A tag contém informações sobre o endereço do bloco na memória
    * Bit de controle informa se a linha foi modificada depois de ser carregada no cache
* Em um processador multicore, L1 e L2 ficam dentro de cada core, enquanto L3 é compartilhada por todos
* Ao ler uma palavra da memória, o processador checa se o bloco está presente no cache. Em caso positivo (**cache hit**) o dado é fornecido sem acessar a memória, em caso de **cache miss**, o bloco da memória é lido e armazenado no cache
    * **Hit ratio:** razão entre o número de cache hit e o número de buscas no cache
* **Localidade:** ao armazenar um bloco na memória, é provável que haverá futuras referências

### Cache - Função de Mapeamento
* Há menos linhas de memória cache do que blocos de memória totais
* **Funções de Mapeamento:**
    * Direto
    * Associativo
    * Associativo por conjunto

### Mapeamento direto
* Blocos mapeados um a um em sequência modular, com `i = j mod L`
    * i = número da linha do cache
    * j = número do bloco de memória
    * L = número total de linhas no cache
* **Exemplo**
    * B = 2<sup>s</sup>
    * L = 2<sup>r</sup>
    * O bloco zero é mapeado à linha zero do cache, o mesmo valendo até o bloco L-1 para a linha L-1
    * O bloco L é mapeado à linha zero e, sucessivamente, L+1 à linha 1
    * Logo, bastam `s-r` bits para identificar qual bloco está mapeado em uma dada linha
        * Supondo s = 5 (32 blocos de memória) e r = 2 (cache de 4 linhas)
        * Linha 0: **000**00 **001**00 **010**00 **011**00 **100**00 **101**00 **110**00 **111**00
        * Linha 1: **000**01 **001**01 **010**01 **011**01 **100**01 **101**01 **110**01 **111**01
        * Linha 2: **000**10 **001**10 **010**10 **011**10 **100**10 **101**10 **110**10 **111**10
        * Linha 3: **000**11 **001**11 **010**11 **011**11 **100**11 **101**11 **110**11 **111**11
        * São necessários apenas os 3 bits em negrito (s - r) para identificar qual bloco está mapeado em cada linha
* **Desvantagem de Mapeamento Direto:** cada bloco é mapeado a uma posição fica, logo, se o programa repetidamente faz referência a palavras em dois blocos distintos mapeados à mesma posição do cache, tais blocos são introduzidos e retirados continuamente (**thrashing**, que resulta em grande número de hit miss, baixo hit ratio)
* **Aliviar thrashing:** anotar quais blocos são retirados e necessários logo em seguida, criando um "cache vítima" (de 4 a 16 linhas) onde se colocam tais blocos

### Mapeamento Associativo
* Blocos de memória podem ser carregados em qualquer linha do cache
* Se a memória tem B = 2<sup>s</sup> blocos, o campo tag de s bits informa o bloco carregado na linha, portanto, para determinar se um bloco está no cache, as tags de todas as linhas são examinadas simultaneamente (**acesso associativo**)
* **Desvantagem:** complexidade de circuitaria para comparar tags em paralelo
* **Algoritmo de substituição:** determina qual linha deve receber um novo bloco que precisa ser carregado no cache cheio
    * Um exemplo comum é o **LRU (Least Recently Used)**, que se vale da linha menos usada para substituição

### Mapeamento Associativo por Conjunto
* Une vantagens do mapeamento direto com o associativo, reduzindo as desvantagens de ambos
* Cache composto por **v** conjuntos, cada um com **L** linhas. Seja **i** o número do conjunto em que o bloco será colocado e **j** o número do bloco de memória. **i** é obtido por `i = j mod v`
    * Dentro do conjunto **i**, o bloco **j** pode ser colocado em qualquer linha do cache por acesso associativo para verificar a presença ou não do bloco
* Melhoria do hit ratio: duas linhas em cada conjunto (L = 2)
    * Two-way set-associative cache

### Algoritmo de Substituição no Cache
* Em mapeamento direto, há apenas uma linha possível
* Para mapeamento associativo ou associativo por conjunto, utiliza-se um algoritmo de substituição implementado em hardware (maior velocidade) para escolher qual bloco deve ser substituído pelo novo
* **LRU - Least Recently Used:** substituição do bloco no cache que está mais tempo sem ser referenciado
    * Mais efetivo
    * No cache associativo, mantém-se lista de índices das linhas do cache. Ao se referenciar uma linha, ela move-se à frente
    * Para um novo bloco, a linha ao final é substituída
* **Algoritmo pseudo-LRU**
    * Em cada linha de cache mantém-se um **Use bit**
    * Ao carregar um bloco de memória numa linha do cache, o **Use bit** recebe zero
    * Ao se referenciar uma linha, **Use bit** recebe um
    * Ao se carregar um novo bloco no cache, escolhe-se uma linha com **Use bit** zero
    * Algoritmo eficiente para o *two-way set-associative cache*

### Cache Write Through e Write Back
* Casos a considerar ao substituir uma linha no cache
    * Se a linha não foi alterada, pode ser simplesmente substituída
    * Se houve operação de escrita na linha do cache, o bloco correspondente na memória deve ser atualizado
* Escritas em linhas do cache podem gerar inconsistência de dados com a memória, há duas técnicas para resolver
    * **Write Through:** toda escrita ao cache é feito também na memória
    * **Write Back:** escritas se dão apenas no cache, mas toda vez que isso ocorre, um **dirty bit** indica que a linha foi alterada. Antes de efetuar a substituição da linha do cache, se o dirty bit está ativo, o bloco correspondente na memória é atualizado para garantir a consistência

### Informações Extras
* [Writing Cache Friendly Code](http://web.cecs.pdx.edu/~jrb/cs201/lectures/cache.friendly.code.pdf)