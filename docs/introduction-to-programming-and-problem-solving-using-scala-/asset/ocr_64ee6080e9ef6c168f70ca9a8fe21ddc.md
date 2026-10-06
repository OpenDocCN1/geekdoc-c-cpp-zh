# Arrays and Lists in Scala

```
scala Array[Int]("Does","this","work")
<console>:6: error: type mismatch;
found: java.lang.String("Does")
required: Int Array[Int]("Does","this","work")
```

```
<console>:6: error: type mismatch;
found: java.lang.String("this")
required: Int Array[Int]("Does","this","work")
```

```
<console>:6: error: type mismatch;
found: java.lang.String("work")
required: Int Array[Int]("Does","this","work")
```

# 6.2 Using Arrays

Now you know one way to make arrays, but what can you do with them? The first things we need to be able to get the values stored in the array and change the values stored in the array. This is done by following the name of the array with parentheses and a number that is the index of the thing we want. Arrays, like with most things in modern programming languages, are zero indexed. The first element in the array is at index zero, and if there are N things in the array, the last one is at index N-1. Here is an example.

```
scala var arr=Array(7,4,6,3,9,1)
arr: Array[Int] = Array(7, 4, 6, 3, 9, 1)
```

```
scala arr(0)
res5: Int = 7
```

```
scala arr(1)
res6: Int = 4
```

```
scala arr(5)
res7: Int = 1
```

The first statement creates a new variable arr that is an array of integers and gives that array six values to store. The next three commands basically pull out values from that array. The expression arr(0) gets the first elements, arr(1) gets the second, and arr(5) gets the last.

What goes in the parentheses does not have to be a simple integer. It can be any expression of type Int. You could do something much more complex to pull out a value.