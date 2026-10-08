```
bitset<9> bs3 = ~bs1;
bitset<9> bs4 = bs1&bs3;
bitset<9> bs5 = bs1<<2;
```

// complement: bs3=="001110000"
// all zeros
// shift left: bs5 = "000111100"