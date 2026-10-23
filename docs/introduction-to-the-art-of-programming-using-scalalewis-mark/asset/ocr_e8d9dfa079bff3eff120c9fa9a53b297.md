```
val (rest,last)=n.splitAt(n.lastIndexOf(’ ’)+1) last+"，"+rest } )
lnames: List[java.lang.String] = List(Lewis, Mark C. , Hughes, Jason C. , Stewart, Glen R. , Hogan, Jen )
```

So the use of map allowed us to complete a task in a quick and short way that could have taken us a fairly large amount of code using other approaches.

If you had a long list of these names, you might want to do something like find all the people who have last names beginning with a particular letter. For example, we might want to find everyone whose last names starts with an ‘H’. For this we would use the filter function. The filter function will select out values that satisfy some condition and give us a sequence with only those values.

```
scala> lnames.filter(_.startsWith("H"))
res48: List[java.lang.String] = List(Hughes, Jason C. , Hogan, Jen )
```

Thanks to filter and the startsWith method, this is a very simple one-liner.

There are some other methods that were not listed above because they take a bit more explanation. They should not be too hard to understand if you have followed up to this point because they do exactly what we did ourselves earlier in this chapter with the operateOnArray and operateOnList functions. We will start with the reduce methods, reduceLeft and reduceRight. These methods take a function that operates on two elements of the sequence and returns a value of that type. The reduce methods repeatedly apply the function to successive elements the same way the operateOnArray and operateOnList methods did. The difference between the two is whether they apply the operations moving from left to right or from right to left. If the operation is commutative, like addition or multiplication, then the order does not impact the result, only potentially the efficiency. For non-commutative operations it can matter. Here are a few examples using the lst variable that we defined earlier.

```
scala> lst.reduceLeft(_+_)
res49: Int = 30
```

```
scala> lst.reduceLeft(_*_)
res50: Int = 4536
```

```
scala> lst.reduceLeft(_- )
res51: Int = -16
```

```
scala> lst.reduceRight(_- )
res52: Int = 14
```

The first two calls do what we have seen before taking the sum and product of the list. The last two use a difference, which is not commutative, and show how the results of reduceLeft and reduceRight are different. The reduceLeft method gives us (((((7 − 4) − 6) − 3) − 9) − 1. The reduceRight method gives us 7 − (4 − (6 − (3 − (9 − 1))))).

In the last chapter we made a recursive method that could do these types of operations with user input. That differed from what we did in this chapter in that we had to pass in an extra value to use when the user terminated the recursion. We did not do anything special with that, but it could have opened other possibilities. The reduce operations have to operate on the element type of the collection for both arguments because that is what happens in the most deeply nested application. If we specify the base value, the function can take one argument of a different type than the elements in the sequence as long as it returns that type as well. If we say that the sequence has type A and we want a function