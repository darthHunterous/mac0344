# Aula 17 - Memória Externa

* **1956 - IBM 305**
    * Primeiro disco magnético de cabeça móvel
    * RAMAC - Random Access Method of Access and Control
    * Uma tonelada
    * Alugado por 250 mil dólares ao ano
    * Capacidade de 5 MB

### Disco Magnético
* Fatias circulares de substrato formado por alumínio ou vidro coberto por camada magnética
* Disco dividido em **trilhas**, organizadas em **setores**
* **Setor:** tipicamente 512 bytes de dados mais alguns de controle
* **Cabeça de Leitura/Gravação Móvel:** posiciona-se primeiro em cima da trilha desejada antes de efetuar o acesso
* **Cabeça Fixa:** em discos mais modernos, há uma cabeça em cima de cada trilha, evitando movimentações desnecessárias

### Desempenho do Disco Magnético
* **Seek Time:** tempo de posicionamento da cabeça móvel em cima da trilha desejada
    * De 3 a 12 ms
* **Latência Rotacional:** tempo para que o setor desejado chegue abaixo da cabeça quando a trilha já está posicionada
    * De 4 a 8 ms
* **Tempo de Acesso:** soma do Seek Time com a Latência Rotacional
    * Tempo que leva para que a cabeça esteja pronta para acessar o setor
    * Tempo médio de acesso: seek time + 0.5 \* r
        * r é velocidade em rotações por segundo
* **Tempo de Transferência:** depende da quantidade de bytes a serem acessados

### RAID - Redundant Array of Independent Disks
* Aceso a disco magnético leva 10 ms ou mais
* Melhorias no desempenho do disco magnético são menores que no desempenho de processadores ou da memória interna
    * Levou a desenvolver **arranjos de múltiplos discos** operando independentemente e em paralelo
* Demandas separadas de entrada e saída podem ser atendidas em paralelo, desde que os dados residam em discos separados
* Uma mesma requisição de entrada e saída pode ser paralelizada desde que os blocos de dados estejam distribuídos em vários discos
* **RAID:** conjunto de discos físicos vistos pelo SO como uma unidade lógica
    * Dados distribuídos em múltiplos discos para viabilizar acesso simultâneo
    * Múltiplas cabeças aumentam a vazão de transferência, porém também a probabilidade de falhas
    * Redundância de dados permite a recuperação em caso de falhas
    * Existem 7 níveis de RAID, de RAID 0 a RAID 6

### RAID 0 - Sem redundância, com rodízio de strips
* Sem redundância
* Distribui blocos de dados logicamente contíguos (**strips**) com rodízio (**round robin**) em **n** discos
    * strip *i* armazenado no disco *i* mod *n*
* Permite acesso paralelo de strips diferentes sequenciais pois ficam em discos diferentes, por exemplo strip 0 e strip 1
    * Exemplo de organização em 4 discos
        ```
        DISCO 00: DISCO 01: DISCO 02: DISCO 03:

        strip 00, strip 01, strip 02, strip 03
        strip 04, strip 05, strip 06, strip 07
        strip 08, strip 09, strip 10, strip 11 
        strip 12, strip 13, strip 14, strip 15
        ```
* **Número mínimo de discos:** 2
* **Eficiência de espaço:** 1
* **Tolerância a erros:** sem
* **Performance de leitura e escrita:** n<sup>x</sup>

### RAID 1 - Redundância por duplicação (Mirroring)
* Duplica cada strip em dois discos, custo como desvantagem
* Recuperação de erro: quando um disco falha, busca-se o dado no disco que o espelha
* Escrita deve ser feita em ambos os discos
* **Número mínimo de discos:** 2
* **Eficiência de espaço:** <sup>1</sup>/<sub>n</sub>
* **Tolerância a falhas:** n-1 falhas de discos
* **Performance de leitura:** n<sup>x</sup>
* **Performance de escrita:** 1<sup>x</sup>

### RAID 2 - Redundância com Hamming Code
* Todos discos com a cabeça na mesma posição
* Strips pequenos (a nível de byte ou palavra)
* **Hamming Code estendido:** correção de erro de 1 bit e detecção de 2 bits
* Menos discos que RAID 1: discos redundantes proporcionais a log da quantidade de discos de dados
* RAID 2 é utilizado quando há erros frequentes
* **Exemplo de organização**
    * Para strips equivalentes nos discos de 0 a 3: de b0 a b3, temos em 3 discos redundantes, strips equivalentes f0(b), f1(b) e f2(b) (mesmo posicionamento horizontal de strip)
* **Número mínimo de discos:** 3
* **Eficiência de espaço:** 1 - <sup>1</sup>/<sub>n</sub> \* log<sub>2</sub>(n-1)
* **Tolerância a erros:** um disco
* **Performance de leitura e escrita:** varia

### RAID 3 - Redundância com bit de paridade
* Todos os discos com a cabeça na mesma posição
* Strip a nível de byte
* Apenas um disco redundante, contendo o **bit paridade** dos bits correspondentes no discos de dados
* Se um disco falha, ele pode ser substituído por um novo, cujo conteúdo é obtido com **XOR** de todos bits dos discos de dados e do disco redundante (Válido de RAID 3 a 6)
* **Exemplo de organização**
    * Para strips equivalentes de b0 a b3 nos discos 0 a 3, temos no disco redundante o bit paridade de b0 a b3, ou seja, P(b)
* **Número mínimo de discos:** 3
* **Eficiência de espaço:** 1 - <sup>1</sup>/<sub>n</sub>
* **Tolerância a erros:** um disco
* **Performance de leitura e escrita:** (n-1)<sup>x</sup>

### RAID 4 - Paridade a nível de bloco
* Em RAID 4 a 6, discos operam independentemente
* Pedido de acesso a dados podem ser paralelizados
* Os strips são blocos grandes
* Um disco redundante com bits de paridade dos blocos correspondentes
* Ao escrever um bit nos discos de dados, faz-se necessária a atualização do bit paridade
    * Se o novo bit escrito é igual ao antigo, o bit de paridade também é igual. Caso contrário, é o complemento da paridade antiga
* **Exemplo de organização:**
    * (Blocos verticalmente alinhados dentro de cada disco)
    ```
    DISCO 00: DISCO 01: DISCO 02: DISCO 03: DISCO RD:

    bloco 00, bloco 01, bloco 02, bloco 03, P(00-03)
    bloco 04, bloco 05, bloco 06, bloco 07, P(04-07)
    bloco 08, bloco 09, bloco 10, bloco 11, P(08-11)
    bloco 12, bloco 13, bloco 14, bloco 15, P(12-15)
    ```
    * R é o disco redundante, Pr a paridade
* **Número mínimo de discos:** 3
* **Eficiência de espaço:** 1 - <sup>1</sup>/<sub>n</sub>
* **Tolerância a erros:** um disco
* **Performance de leitura:** 1 - (1-r)<sup>n</sup> - n \* r \* (1-r)<sup>n</sup>
* **Performance de escrita:** (n-1)<sup>x</sup>

### RAID 5- Paridade a nível de bloco distribuído
* No RAID 4, o disco redudante pode se tornar gargalo, já que toda escrita envolve ele
* Em RAID 5, aplica-se rodízio (**round robin**) aos blocos de paridade entre os discos de dados
* **Exemplo de organização:**
    ```
    DISCO 00: DISCO 01: DISCO 02: DISCO 03: DISCO 04:

    bloco 00, bloco 01, bloco 02, bloco 03, P(00-03)
    bloco 04, bloco 05, bloco 06, P(04-07), bloco 07
    bloco 08, bloco 09, P(08-11), bloco 10, bloco 11
    bloco 12, P(12-15), bloco 13, bloco 14, bloco 15
    P(16-19), bloco 16, bloco 17, bloco 18, bloco 19
    ```
* **Número mínimo de discos:** 3
* **Eficiência de espaço:** 1 - <sup>1</sup>/<sub>n</sub>
* **Tolerância a erros:** um disco
* **Performance de leitura:** n<sup>x</sup>
* **Performance de escrita:** (n-1)<sup>x</sup>

### RAID 6 - Redundância Dual
* Redundância dual: dois cálculos diferentes para verificação de paridade
    * Bit paridade por XOR
    * Outro cálculo como Reed-Solomon
* Com dois cálculos, torna-se possível recuperar a falha de dois discos
* **Exemplo de organização**
    ```
    DISCO 00: DISCO 01: DISCO 02: DISCO 03: DISCO 04: DISCO 05:

    bloco 00, bloco 01, bloco 02, bloco 03, P(00-03), Q(00-03)
    bloco 04, bloco 05, bloco 06, P(04-07), Q(04-07), bloco 07
    bloco 08, bloco 09, P(08-11), Q(08-11), bloco 10, bloco 11
    bloco 12, P(12-15), Q(12-15), bloco 13, bloco 14, bloco 15
    ```
* **Número mínimo de discos:** 4
* **Eficiência de espaço:** 1 - <sup>2</sup>/<sub>n</sub>
* **Tolerância a erros:** dois discos
* **Performance de leitura:** n<sup>x</sup>
* **Performance de escrita:** (n-2)<sup>x</sup>

### HD vs SSD
* **SSD - Solid State Drive**: memória flash como memória externa
* SSD mais rápido do que HD, porém mais caro
* HD tem bom desempenho quando arquivos grandes ficam em blocos contíguos. Com tempo de uso, tais arquivos grandes podem ser alocados em blocos não contíguos, fragmentando o HD
    * Fragmentação não ocorre com SSD
* SSD não tem partes móveis, portanto não é vulnerável a choques mecânicos como HD
* **Histórico**
    * Setembro de 2005: Samsung lança SSD de 16 GB, NAND Flash
    * Março de 2007: SanDisk lança SSD de 32 GB, 100x mais rápido
    * 2009: Kingston DataTraveler, de 256 GB
    * 2013: Kingston DataTraveler HyperX Predator, USB 3.0 e 1 TB
        * Em 2015, custava U$ 772,74 na Amazon
        * Dimensões: 2,8 x 1,1 x 0,8 polegadas
    * Agosto de 2015: na Flash Memory Summit, Samsung anuncia SSD de 16 TB, PM1633a
        * Demonstrou um servidor com 48 desses drivers, 758 TB
    * Agosto de 2016: na Flash Memory Summit, Samsung anuncia SSD de 60 TB
    * Março de 2018: Nimbus Data ExaDrive DC 100, SSD de 100TB
* SSDs tipicamente custam U$ 500 por TB