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

### RAID 0