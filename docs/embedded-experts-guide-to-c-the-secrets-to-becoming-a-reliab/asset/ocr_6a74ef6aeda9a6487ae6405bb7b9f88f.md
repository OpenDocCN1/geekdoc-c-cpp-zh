result is mathematical nonsense, but it is the result according to the C Standard. Integer promotion rules apply to short and char types as well – but these will always be cast to a (signed) This can cause even more confusion – comparing a negative signed char to an unsigned char with the same underlying bit-pattern will show that the two are not equal, which is mathematically correct, but shows you can’t even rely on the bits being unchanged!

The lesson here is that you don’t mix signed and unsigned types – it will only cause you trouble. If you absolutely must do it then make the casts explicit rather than relying on the implicit casting that results from the integer promotion rules.

```
int oranges = -1;
unsigned int stop = 1;
/* Integer promotion causes odd behaviour:
 * This loop will never run! */
while (oranges < stop)
{
++oranges;
...;
}
```

Fig 1.4 - Integer Promotion can cause some very odd behaviour – comparisons between different sized integer types, or signed and unsigned types of the same size, can give strange results – such as causing a loop to terminate unexpectedly (or not run at all).

Less subtle examples of type safety violations also occur; many are the result of the versatility granted to the programmer by pointers. Probably