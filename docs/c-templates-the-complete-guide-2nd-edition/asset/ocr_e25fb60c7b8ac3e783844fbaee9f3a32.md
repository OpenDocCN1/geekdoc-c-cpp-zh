```
mid = (1+16+1)/2
    = 9
value = (16<9*9) ? Sqrt<16,1,8>::value
                : Sqrt<16,9,16>::value
    = (16<81) ? Sqrt<16,1,8>::value
                : Sqrt<16,9,16>::value
    = Sqrt<16,1,8>::value
```