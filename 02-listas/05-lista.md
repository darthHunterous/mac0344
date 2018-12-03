# MAC0344 - Lista 05
## Édio Cerati Neto - NUSP 9762678

```
21: mar := 0; sp = lshift(sp+sp); rd
22: sp = lshift(sp+sp); rd
23: ac := mbr; sp = sp+ac; if z goto 25
24: ac := 0; goto 0
25: ac := ac+1; goto 0
```