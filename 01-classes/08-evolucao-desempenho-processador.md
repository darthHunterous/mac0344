# Aula 08, 09, 10 - Evolução do Desempenho do Processador
* **Frequência do Relógio**
    * ENIAC (1946) - 100 kHz
    * AMD FX-9590 - 5 GHz
* Aumento da frequência do relógio acarreta maior dissipação de calor, limitando o aumento dela
* Evolução do desempenho do processador se explica pela evolução da tecnologia VLSI, aumentando o número de transistores em uma pastilha de silício
* **Lei de Moore:** o número de transistores em uma pastilha VLSI dobra a cada 18 meses
* Transistores menores significam maior capacidade e também maior velocidade
* Tecnlogia VLSI viabilizou a computação paralela
    * Limitada pela **Lei de Amdahl**
* **Melhorias visando desempenho:**
    * **Pipelining** de instruções
    * Processador **superescalar**
    * **Multicore**
<br><br>
* **Bottleneck (Gargalo) de Von Neumann**
    * Instruções e dados residem na memória e precisam ser buscadas e trazidas ao processador causando tal gargalo
<br><br>
* **Pipelining**
    * Semelhaça a uma linha de montagem
    * Execução de tarefas divididas em estágios
        * Estação separada para a execução de cada estágio
        * Pipelining possibilita a execução de diferentes estágios de tarefas ao mesmo tempo
        * Ao terminar o estágio de uma tarefa, cada estação passa a executar o mesmo estágio, porém da tarefa seguinte
        * A primeira tarefa leva tempo normal até sua conclusão, porém a partir de então, uma nova tarefa se conclui logo após cada estágio
<table>
    <tr>
        <th>Ciclo</th>
        <th>01</th>
        <th>02</th>
        <th>03</th>
        <th>04</th>
        <th>05</th>
        <th>06</th>
        <th>07</th>
        <th>08</th>
        <th>09</th>
        <th>10</th>
    </tr>
        <td>BUSCA INSTRUÇÃO</td>
        <td>i01</td>
        <td>i02</td>
        <td>i03</td>
        <td>i04</td>
        <td>i05</td>
        <td>i06</td>
        <td>i07</td>
        <td>i08</td>
        <td>i09</td>
        <td>i10</td>
    <tr>
        <td>DECODIFICAÇÃO</td>
        <td></td>
        <td>i01</td>
        <td>i02</td>
        <td>i03</td>
        <td>i04</td>
        <td>i05</td>
        <td>i06</td>
        <td>i07</td>
        <td>i08</td>
        <td>i09</td>
    </tr>
        <td>ENDEREÇO DO OPERANDO</td>
        <td></td>
        <td></td>
        <td>i01</td>
        <td>i02</td>
        <td>i03</td>
        <td>i04</td>
        <td>i05</td>
        <td>i06</td>
        <td>i07</td>
        <td>i08</td>
    <tr>
        <td>BUSCA OPERANDO</td>
        <td></td>
        <td></td>
        <td></td>
        <td>i01</td>
        <td>i02</td>
        <td>i03</td>
        <td>i04</td>
        <td>i05</td>
        <td>i06</td>
        <td>i07</td>
    </tr>
        <td>EXECUÇÃO</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>i01</td>
        <td>i02</td>
        <td>i03</td>
        <td>i04</td>
        <td>i05</td>
        <td>i06</td>
    <tr>
        <td>ESCRITA RESULTADO</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>i01</td>
        <td>i02</td>
        <td>i03</td>
        <td>i04</td>
        <td>i05</td>
    </tr>
</table>

* Em desvios (branches), pode ser necessário recomeçar a pipeline já preenchida
    * Ver **predição de desvio**
<br><br>
* **Pré-Busca de Instruções:**
    * Para manter o processador ocupado, instruções são pré-buscadas, ficando disponíveis assim que necessitam serem executadas
* **Predição de Desvios:**
    * Processador examina o código, buscando prever qual desvio é mais provável de ser executado em um **if**, baseado no histórico, já carregando as intruções referentes a esse trecho
    * Prevendo corretamente, economiza-se tempo pois as instruções já estarão disponíveis
<br><br>
* **Processador Superescalar:**
    * Múltiplas unidades de execução de instruções
        * Duas unidades para inteiros e duas para ponto flutuante
    * Paralelismo no nível de instrução
    * Limitação por dependência de dados
    * **Análise do Fluxo de Dados:** verificação de quais instruções dependem de resultados de outras
        * Permite escalonamento para execução fora de ordem, aproveitando os recursos de hardware
<br><br>
### Dependências de Dados:
* **Dependência Verdadeira (Dependência de Fluxo):**
    * Read-After-Write (RAW)
    * Quando uma instrução depende do resultado de outra
    * **Modelo**
        * A = ...
        * ... = A...
    * **Exemplo**
        * 1: A = A + 2
        * 2: B = 2 \* A
        * 3: C = B - A
    * 2 depende verdadeiramente de 1, 3 depende verdadeiramente de 1, 3 depende verdadeiramente de 2
        * 1 &rarr;<sup>v</sup> 2
        * 1 &rarr;<sup>v</sup> 3
        * 2 &rarr;<sup>v</sup> 3
* **Anti-Dependência**
    * Write-After-Read (WAR)
    * Quando uma instrução usa uma variável que depois será alterada, portanto a ordem de execução não pode ser alterada nem executada em paralelo
    * **Modelo**
        * ... = A...
        * A = ...
    * **Exemplo**
        * 1: B = A + 5
        * 2: A = 7
    * A instrução 1 anti-depende da instrução 2
        * 1 &rarr;<sup>anti</sup> 2
    * **Remoção:** através da renomeação de variáveis para permitir a execução em paralelo
        * **Exemplo** de instruções com anti-dependência
            * 1: B = A \* X + X / (Y - Z)
            * 2: A = X \* X / (Y + 30 \* Z)
        * Renomeando
            * 1: A1 = A
            * 2: B = A1 \* X + X / (Y - Z)
            * 3: A = X \* X / (Y + 30 \* Z)
        * A renomeação permite a execução de 2 e 3 em paralelo, porém introduz-se uma dependência verdadeira entre 1 e 2
* **Dependência de Saída:**
    * Write After Write (WAW)
    * Quando a ordem das instruções afeta o valor final da saída de uma variável
    * **Modelo**
        * A = ...
        * A = ...
    * **Exemplo**
        * 1: A = 0
        * 2: B = A + 5
        * 3: A = 7
    * Instrução 3 tem dependência de saída em relação à instrução 1
        * 1 &rarr;<sup>saida</sup> 3
    * A dependência de saída pode ser removida ao renomear as variáveis
        * 1: A1 = 0
        * 2: B = A1 + 5
        * 3: A = 7
<br><br>
* **Algoritmo de Tomasulo**
    * Permite a execução de instruções fora de ordem, aproveitando os múltiplos núcleos de processadores
    * Implementado em hardware, remove antidependências e dependências de saída renomeando registradores
    * Processador Superescalar é geralmente associado à arquitetura RISC
    * Algoritmo implementado em hardware no IBM 360/91, depois aplicado em outros processadores
    * Rastreia operando disponíveis para satisfazer dependências
    * **Passos**
        * Sequência de instruções carregadas na *instruction queue*
        * Usa um número de *reservation stations*
        * Pega uma instrução na fila e encontra uma estação livre para ela
        * Lê operandos nos registradores
        * Se um operando não se encontra no registrador, localiza a estação que irá produzi-lo
        * O passo acima renomeia o registrador, o ID da estação será o nome temporário
        * Monitora resultados, colocando-os nas estações que os esperam assim que produzidos
        * Quando todos os operandos da instrução estão disponíveis, envia-a para execução
<br><br>
* **VLIW - Very Large Instruction Word**
    * Processador superescalar com várias unidades funcionais, portanto para melhor explorá-las, afotam instruções longa (VLIWs)
    * Do bit zero ao 4 - Template (5 bits)
    * Do bit 5 ao 45 - Instruction Slot 0 (41 bits)
    * Do bit 46 ao 86 - Instruction Slot 1 (41 bits)
    * Do bit 87 ao 127 - Instruction Slot 2 (41 bits)
<br><br>
* **Execução Especulativa**
    * Com predição de desvio e análise do fluxo de dados, processadores executam instruções especulativamente antes que elas aparecem na sequência
    * Num desvio condicional, o processador pode especular que o ramo then será executado e já ir carregando tais instruções
    * Os resultados de execução especulativa são armazenados em locais temporários e validados depois
    * Ocupa o processador com a execução de instruções que provavelmente serão necessárias
<br><br>
* **Processador Multicore:** múltiplos núcleos em uma mesma pastilha
    * Cada núcleo contém todos componentes de um processador independente
    * Viável com o avanço da tecnlogia VLSI
    * **Speedup**: ganho obtido com o uso dos múltiplos processadores
        * tempo para execução sequencial com único processador sobre o tempo de execução em paralelo com n processadores
        * Idealmente pode se chegar ao valor n
        * Lei de Amdahl mostra o esperado na prática
* **Lei de Amdahl**
    * Programa onde uma fração **f** pode ser paralelizada e outra fração **(1 - f)** é apenas sequencial
    * Speedup = <sup>T<sub>1</sub></sup>/<sup>T<sub>n</sub></sup>
    * Speedup = T<sub>1</sub> / (T<sub>1</sub> \* (1 - f) + (T<sub>1</sub> \* f / n))
    * Speedup = 1 / [(1 - f) + f / n]
    * Para n &rarr; &infin;, o speedup é limitado por 1 / (1 - f)
    * Com f pequeno, o paralelismo maciço não surte muitos efeitos
    * **Exemplo**
        * Sendo 10% do código inerentemente serial, sua fração paralela é 90%
        * Executando tal código com 8 núcleos, temos um speedup de 4,7 vezes, ao invés do ideal 8 vezes mais rápido
    * Dadas tais conclusões pessimistas, frequentemente se usam os múltiplos processadores para executar programas independentes
<br><br>
### Paralelização de Laços
* Laços são boas oportunidades para execução em paralelo
* Certos métodos analisam vetores de dependências e buscam paralelismo em laços
<br><br>
* **Checagem de Aprendizado**
* 1 - Programar um computador com um só processador é mais fácil do que paralelizar o mesmo código para milhares de processadores
* 2 - Pipelining funciona melhor quando há poucos desvios na sequência de instruções
* 3 - Processador superescalar explora o paralelismo no nível de instruções
* 4 - O altíssimo desempenho também depende do algoritmo em si, um processador superescalar com milhares de unidades de execução não surtirá efeitos se o código for pouco paralelizável
* 5 - Sim, implementar vários núcleos em uma única pastilha é uma maneira de aumentar o desempenho sem alterar o clock
* 6 - Sim, A Lei de Amdahl mostra que nem todo problema pode ser resolvido de maneira satisfatória com um computador paralelo 