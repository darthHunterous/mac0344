# MAC0344 - Lista 04
## Édio Cerati Neto - NUSP 9762678

### Questão 01
* Para um dado de 7 bits com um código de Hamming de 11 bits, teremos 4 bits adicionais distribuídos de acordo com potências de 2 contidas até 11, ou seja: x1, x2, x4 e x8 precisam ser determinados
<table style="text-align:center">
    <tr>
        <th>1 a 11 em binário</th>
        <th>8 4 2 1</th>
    </tr>
        <td>1</td>
        <td>0 0 0 1</td>
    <tr>
    </tr>
        <td>2</td>
        <td>0 0 1 0</td>
    <tr>
        <td>3</td>
        <td>0 0 1 1</td>
    </tr>
    <tr>
        <td>4</td>
        <td>0 1 0 0</td>
    </tr>
    <tr>
        <td>5</td>
        <td>0 1 0 1</td>
    </tr>
    <tr>
        <td>6</td>
        <td>0 1 1 0</td>
    </tr>
    <tr>
        <td>7</td>
        <td>0 1 1 1</td>
    </tr>
    <tr>
        <td>8</td>
        <td>1 0 0 0</td>
    </tr>
    <tr>
        <td>9</td>
        <td>1 0 0 1</td>
    </tr>
    <tr>
        <td>10</td>
        <td>1 0 1 0</td>
    </tr>
    <tr>
        <td>11</td>
        <td>1 0 1 1</td>
    </tr>
</table>

* De acordo com a tabela acima, segue que podemos obter os valores de x1, x2, x4 e x8 com:
    * x1 = x3 &xoplus; x5 &xoplus; x7 &xoplus; x9 &xoplus; x11
    * x2 = x3 &xoplus; x6 &xoplus; x7 &xoplus; x10 &xoplus; x11
    * x4 = x5 &xoplus; x6 &xoplus; x7
    * x8 = x9 &xoplus; x10 &xoplus; x11
* Com o dado de 7 bits original 1100101 segue:
<table style="text-align:center">
    <tr>
        <th>x1</th>
        <th>x2</th>
        <th>x3</th>
        <th>x4</th>
        <th>x5</th>
        <th>x6</th>
        <th>x7</th>
        <th>x8</th>
        <th>x9</th>
        <th>x10</th>
        <th>x11</th>
    </tr>
    <tr>
        <td>?</td>
        <td>?</td>
        <td>1</td>
        <td>?</td>
        <td>1</td>
        <td>0</td>
        <td>0</td>
        <td>?</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
    </tr>
</table>

* Portanto:
    * x1 = 1 &xoplus; 1 &xoplus; 0 &xoplus; 1 &xoplus; 1 = 0
    * x2 = 1 &xoplus; 0 &xoplus; 0 &xoplus; 0 &xoplus; 1 = 0
    * x4 = 1 &xoplus; 0 &xoplus; 0  = 1
    * x8 = 1 &xoplus; 0 &xoplus; 1 = 0

* **Código de Hamming resultante:**
    * `00111000101`


### Questão 02
* Devemos calcular os 4 bits de paridade para o código lido da memória `00110000101`: k1, k2, k3 e k4
* Da tabela feita na Questão 01, podemos obter os bits de paridade da seguinte maneira:
    * k1 = y1 &xoplus; y3 &xoplus; y5 &xoplus; y7 &xoplus; y9 &xoplus; y11
    * k2 = y2 &xoplus; y3 &xoplus; y6 &xoplus; y7 &xoplus; y10 &xoplus; y11
    * k3 = y4 &xoplus; y5 &xoplus; y6 &xoplus; y7
    * k4 = y8 &xoplus; y9 &xoplus; y10 &xoplus; y11
* Logo:
    * k1 = 0 &xoplus; 1 &xoplus; 0 &xoplus; 0 &xoplus; 1 &xoplus; 1 = 1
    * k2 = 0 &xoplus; 1 &xoplus; 0 &xoplus; 0 &xoplus; 0 &xoplus; 1 = 0
    * k3 = 1 &xoplus; 0 &xoplus; 0 &xoplus; 0 = 1
    * k4 = 0 &xoplus; 1 &xoplus; 0 &xoplus; 1 = 0
* Como k4k3k2k1 = 0101, há um erro e ele se encontra em y5: 0011**0**000101 (em negrito)
* Corrigindo o erro, obtemos o valor esperado, mesmo da questão 01:
    * `00111000101`
