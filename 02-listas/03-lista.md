# MAC0344 - Lista 03

## Édio Cerati Neto - NUSP 9762678

### Questão 01

* Instruções com Dependência Verdadeira:
  * 1 &rarr;<sup>v</sup> 3
  * 2 &rarr;<sup>v</sup> 3
  * 4 &rarr;<sup>v</sup> 5
* Instruções com Anti-Dependência:
  * 1 &rarr;<sup>anti</sup> 2
  * 3 &rarr;<sup>anti</sup> 4
* Instruções com Dependência de Saída:
  * 2 &rarr;<sup>saida</sup> 4

### Questão 02

```asm
1: B1 = B
2: A = B1 + 2
3: B2 = C
4: E = A + B2
5: B = 0
6: F = B + 1
```
