When we do bit-wise operations we simply take the bits in the same position and do the specified operations on them to get the bits in the result. To see how this works let us run through a set of examples on the binary operators where we use the four bit numbers 1100 and 1010.

```
1100
& 1010
------
1000
```

```
1100
| 1010
------
1110
```

```
1100
^ 1010
------
0110
```

Negation is pretty straightforward: ~1001=0110. Of course, these bit combinations all have numeric decimal values. We can put commands into Scala to do these same things. Our first value is 12 and our second is 10. The value we took the negation of is 9. Here are the operations performed in Scala. Check that they match the answers we got.

```
scala> 12 & 10
res3: Int = 8
```

```
scala> 12 | 10
res4: Int = 14
```

```
scala> 12 ^ 10
res5: Int = 6
```

```
scala> ~9
res6: Int = -10
```

The last one is interesting. When you check if it makes sense, remember that negative values are represented using two's complement and an Int has 32 bits.

While on the topic of bit-wise operations there are two others that are worth mentioning. They are left-shift and right-shift and are written in Scala as << and >>. These operators shift the bits in an integer value the specified number of positions. If you think about the meaning of bits, this is like multiplying or dividing by powers of two in the same way that adding zeros to the end of a decimal number is the same as multiplying by ten. Some simple examples show you how we can use this to get powers of two.

```
scala> 1 << 0
res7: Int = 1
```

```
scala> 1 << 1
res8: Int = 2
```

```
scala> 1 << 2
res9: Int = 4
```