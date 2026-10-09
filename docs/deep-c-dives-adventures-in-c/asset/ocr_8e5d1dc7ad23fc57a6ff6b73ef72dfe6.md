Notice that you cannot have a pointer to a bit field, but you can have a pointer to the struct that has the bit fields. This is often useful when you want to map a bit field to a hardware port or register.
Bit fields seem like a great idea, but their big disadvantage is that different compilers implement bit fields in different ways. For these reasons many programmers recommend avoiding the use of bit fields and implementing the bit operations using logic.

# Some Examples

# Count the Bits

Bit manipulation has a fascination that will keep many a programmer occupied for hours when they could be doing something more useful. To see why it is addictive, consider the following simple problem – count the number of bits set to one in a bit pattern. The direct way of doing the job is to use shifting and test each bit that is shifted out.

```
```
unsigned value = 0x55;
int count = 0;
for(int i = 0;i < 16;i++){
    if(value & 0x01) count++;
    value >>= 1;
}
```
```

Simple and direct, but not the only way. The best known solution is due to Brian Kernighan:

```
```
unsigned value = 0x55;
int count = 0;
while(value){
    value &= value-1;
    count++;
}
```
```

Why does this works?
The reason it counts the one bits can be understood by working out what happens the first time through the loop. If `value` ends in a `1` subtracting one removes it, e.g `101 - 1 = 100` ANDED with the original gives `100`. If `value` ends in a `0` then subtracting one has to borrow from higher-order bits. In fact, it borrows from the first high-order bit that is a `1`. For example, `100 - 1` has to borrow from the third bit in the pattern and the result is `011`, which when ANDED with the `100` gives `000` and the loop ends.
You can see that each time the subtraction causes a borrow from the first `1` bit to the right and this removes it from `value` and the AND removes the lower-order bits that result from the subtraction – hence the loop repeats the number of times that there are one bits in the bit pattern.