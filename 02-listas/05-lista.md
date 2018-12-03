# MAC0344 - Lista 05
## Édio Cerati Neto - NUSP 9762678

```
21: mar := 0; sp = lshift(sp+sp); rd
22: sp = lshift(sp+sp); rd
23: ac := mbr; sp = sp+ac;
24: alu := sp; if z goto 26
25: ac := 0; goto 0
26: ac := ac+1; goto 0
```