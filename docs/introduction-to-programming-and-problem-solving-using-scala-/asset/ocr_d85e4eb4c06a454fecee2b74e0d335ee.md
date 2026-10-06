# Introduction to Programming and Problem-Solving Using Scala

```
scala fact(10)
res2: Int = 3628800
```

```
scala fact(15)
res3: Int = 2004310016
```

```
scala fact(20)
res4: Int = -2102132376
```

The first two show that the factorial function grows very quickly. Indeed, programs that do factorial are referred to as intractable because you cannot use them for even size problems. The third example though shows else interesting. The value of 20! would be quite large. It certainly should not be. What is going on here?

If you remember back to chapter 2, we talked about how numbers are represented on computers. Integers are represented by a finite number of bits. As a result, they can only get so large. The bit in representation in Scala are 32 bits for Int. If we changed our function just a bit to Long we could get 64 bits. Let's see that here in action.

```
scala def fact(n:Long):Long = if (n<2) il else fact*(n-1)
fact: (n:Long)Long
```

```
scala fact(20)
res5: Long = 24329900817640000
```

```
scala fact(30)
res6: Long = -87645798698847253504
```

The 64 bits in a Long are enough to store 20!, but they fall short of 30! If we give up the speed of using the number types wired into the computer, we can represent much larger numbers. We can then be limited by the amount of memory in the computer. That is a value not measured in bits, but in bytes. By doing this, we use the BigInt.

The BigInt provides us with arbitrary precision arithmetic. This does at the cost of speed and memory. You do not want to use BigInt unless you really need it. However, it can be fun to play with a function like factorial which has the possibility of getting quite large. Let us redefine our function using this type and see how it works.

```
scala def fact(n:BigInt):BigInt = if (n<2) il else fact*(n-1)
fact: (n:BigInt)BigInt
```

```
scala fact(150)
res8: BigInt = 26525289812190158636304800000000
8254883733813792192485539312654748867511145371078787468524024626
6625019864504663559941952206526774925290957335789292355729044494624
72405146970221184437126675500000000000000000000000000000
```

Not only can this version take the factorial of 30, but it can go to much larger values as we see here. There are not many applications that need these types of numbers, but those that benefit greatly from this type of functionality.

Now that we have beaten factorial, it is probably time to move on a different