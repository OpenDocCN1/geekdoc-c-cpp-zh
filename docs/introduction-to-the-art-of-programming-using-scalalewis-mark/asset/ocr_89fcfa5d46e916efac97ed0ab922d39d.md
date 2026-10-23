```
8841761993739701954543616000000
304888344611713860501504000000
10888869450418352160768000000
403291461126605635584000000
15511210043330985984000000
620448401733239439360000
25852016738884976640000
1124000727777607680000
51090942171709440000
2432902008176640000
121645100408832000
6402373705728000
355687428096000
20922789888000
1307674368000
```

```
scala> for(i <- 30 to 15 by -1 par) println(fact(i))
1124000727777607680000
51090942171709440000
2432902008176640000
265252859812191058636308480000000
121645100408832000
6402373705728000
403291461126605635584000000
355687428096000
15511210043330985984000000
20922789888000
620448401733239439360000
304888344611713860501504000000
25852016738884976640000
10888869450418352160768000000
1307674368000
8841761993739701954543616000000
```

The factorial on BigInt is used in part because it is fairly slow. In the first version, everything runs in the way that you expect and the values of 30! down to 15! are printed in order. With the addition of par, the values are no longer printed in order. Instead, the work is broken up into different threads and each each value prints after it has been calculated. The biggest values take longer to calculate so they are not the first ones to print.

While you can use this to speed things up, it has to be done with care. To get some idea of why this is, consider the following few lines typed into the REPL.

```
scala> var count = 0
count: Int = 0
```

```
scala> for(i <- 1 to 1000000 par) count +=1
```

```
scala> count
res0: Int = 930420
```

At the end of this, count should be 1000000, but it is not. It is about 70000 shy of that. Were you to do this on your own machine, you would certainly get a different