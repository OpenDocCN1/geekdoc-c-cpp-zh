
```
def countUnder(nPnts:Int,xmin:Double, xmax:Double, ymin:Double, ymax:Double,f: Double=>Double):Int
```

This function should generate the specified number of random points in the rectangle with the given bounds and return how many of them were below the curve defined by the function f. Note that you can get a random number in the range [min, max) with code like this.

```
val r = min+math.random()*(max-min)
```

You want to do this for the x and y axes.

To estimate π use a function of √1−x² with x and y in the range of [0,1). The full rectangle has an area of 1 while the area under the curve is π/4. If you multiply the fraction of points under the curve by 4, you get an estimate of pi.

In addition to printing out your estimate of π, you should print out an estimate of ∫₀^π (sin x²)²

for the same number of random points.

8. If you did project 1 (p.108), you can now add another option to it. Write a function that takes a rational number as an (Int,Int) and returns an (Int,Int) where all common factors have been removed so that it is in the lowest form.

With that added in, write a script that uses a recursive function to do calculations on rational numbers. The script presents the user with a menu with options for add, subtract, multiply, divide, and quit. If one of the first four options is selected, it should ask for a fraction and perform that operation between the “current” fraction and the one entered. When the program starts, the “current” value will be 1/1 represented by (1,1). After each operation you print the new current value, making sure it is always in the lowest form.

The website provides additional exercises and projects with data files that you can process using input redirection.

## Chapter 7

## Arrays and Lists in Scala

- 7.1 Making Arrays ......................................................... 136
- 7.2 Using Arrays ........................................................... 137
- 7.3 Lists ............................................................... 140
- 7.4 Standard Methods ...................................................... 143
- 7.4.1 Basic Methods ....................................................... 143
- 7.4.2 Higher-Order Methods ................................................ 146
- 7.4.3 Combinatorial/Iterator Methods ...................................... 151
- 7.5 A World of Types ....................................................... 153
- 7.5.1 The Option Type ..................................................... 154
- 7.5.2 Parametric Functions ................................................ 154
- 7.5.3 Subtyping ........................................................... 156
- 7.6 Variable Length Argument Lists ......................................... 156
- 7.7 Mutability and Aliasing ................................................ 159
- 7.8 Basic Argument Passing ................................................. 162
- 7.9 Pass-By-Name ........................................................... 165
- 7.10 Fill and Tabulate ..................................................... 167
- 7.11 Complete Grades Script/Software Development ........................... 168
- 7.12 End of Chapter Material ............................................... 173
- 7.12.1 Problem-Solving Approach ........................................... 173
- 7.12.2 Summary of Concepts ............................................... 173
- 7.12.3 Self-Directed Study ................................................ 174
- 7.12.4 Exercises .......................................................... 175
- 7.12.5 Projects ........................................................... 177

Adding conditionals and logic expanded our capabilities dramatically. Combining it with recursion gives us the ability to do almost anything we want. Technically, we have full computing power. However, there are some ideas that are challenging to express with what we currently know and there are better ways to say them in Scala and programming languages in general.

One of these ideas is the ability to refer to many different objects. In chapter 3 we gained the ability to refer to objects by names with val and var declarations. Using those, we could make as many names as we want and hard code in references to them. We could even have big match statements that allow us to select particular variables based on some value. These approaches are verbose and not particularly useful. In this chapter we will begin learning about COLLECTIONS in Scala. Collections are types that allow us to store and look up many different values using a single name. Most of this chapter will focus on the most basic types, ARRAYS and LISTS. They are two different types that on the surface seem to provide similar functionality, but we will see later on that they are actually very different.

Such forcing has to match what you pass in. As you can see below, Scala will not allow you to do this for an invalid conversion.

```
scala> Array[Int]("Does","this","work")
<console>:6: error: type mismatch;
found   : java.lang.String("Does")
required: Int Array[Int]("Does","this","work")
<console>:6: error: type mismatch;
found   : java.lang.String("this")
required: Int Array[Int]("Does","this","work")
<console>:6: error: type mismatch;
found   : java.lang.String("work")
required: Int Array[Int]("Does","this","work")
```

We can also make arrays that have the default initial value. This is helpful for making larger arrays. It is not unusual for arrays to have thousands or even millions of elements. We certainly do not want to have to type in values for those by hand. Here is the syntax for that.

```
scala> new Array[Int](101) res7: Array[Int] = Array(0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0)
```

The default value for numeric types is zero. The default for the **Boolean** type is **false**. For most other types, many of which we have not learned about, the default is **null**.¹

### 7.2 Using Arrays

So now you know how to make arrays, but what can you do with them? The first things we need to be able to do are get the values stored in the array and change the values stored in the array. This is done by following the name of the array with parentheses and a number that is the index of the thing we want. Arrays, like with most things in most modern programming languages, are zero indexed. So the first element in the array is at index zero and if there are N things in the array, the last one is at index N-1. Here is an example.

```
scala> val arr=Array(7,4,6,3,9,1)
arr: Array[Int] = Array(7, 4, 6, 3, 9, 1)
```

```
scala> arr(0)
res8: Int = 7
```

```
scala> arr(1)
```

```
res9: Int = 4
```

```
scala> arr(5)
res10: Int = 1
```

The first statement creates a new variable named arr that is an array of integers and gives that array six values to store. The next three commands basically pull out values from that array. The expression arr(0) gets the first elements, arr(1) gets the second, and arr(5) gets the last.

What goes in the parentheses does not have to be a simple integer either. It can be any expression of type Int. You could do something much more complex to pull out a value.

```
scala> val i=2
i: Int = 2
```

```
scala> arr(2*i-2)
res12: Int = 6
```

The same type of expression can also be used in an assignment expression. So we can alter the values that are stored in an array as we see in the following example.

```
scala> arr(4)=99
```

```
scala> arr
res13: Array[Int] = Array(7, 4, 6, 3, 99, 1)
```

Here we see how we can use assignment to change the value of one of the elements of the array. This might surprise you because we originally declared arr to be a val. Previously we said that you can not change what is referred to by a variable that is created with val. This does not actually break that rule. You see, the name arr still refers to the same array. What has changed is the value in the array. An analogy might be that an array is a house and the values are the people in it. The variable arr refers to a particular house. People might come and go from the house, but the house itself is the same. We can demonstrate this by trying to change what array the variable arr references.

```
scala> arr=Array(2,7,5)
<console>:6: error: reassignment to val
      arr=Array(2,7,5)
```

We call the Array type a MUTABLE type because the values in it can be changed. Types whose internal values can’t be changed are called IMMUTABLE types. This distinction is very significant to us in Scala and in programming in general, as it alters how we deal with data. We will talk more about it because the List type, which we will also look at in this chapter, happens to be immutable. Indeed, all of the types that we have seen so far are immutable. Once they are created, the values they have never change. The Array is our first example of something that is mutable.

Not everything about an array can be changed. As we have seen, we can change the values stored in an array. However, we can not change how many things are stored in an array. The number of things an array holds can be called the length or the size of the array. In fact, the Array type has methods called length and size which give us this information.

```
scala> arr.length
res5: Int = 6
```

> ¹The value null represents an invalid reference or a reference to nothing. Trying to do something with a null value will cause an error. For this reason, we will typically avoid this approach to making arrays. We will generally prefer to use `Array.fill` or `Array.tabulate`, which will be introduced later in this chapter.
