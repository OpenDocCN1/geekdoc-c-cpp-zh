less than or greater than, this approach is beneficial. If the values are equal the function will return 0. If the first one is less, it will return a negative value. If the first one is greater it will return a positive value. We will see this type of usage of comparison functions in later chapters.

The strength of this approach using a second function argument for comparison is that is makes the sort more flexible. For example, in either of the above examples we could have sorted the numbers from greatest to least instead of least to greatest by simply passing in >_ instead of <_. In addition, it truly places no limitations on the type A. This allows you to sort things according to any sort order you want. For example, if you had a type for students you might want to sort by last name in some contexts or by grade in others. This approach would allow you to do that because the sort order is not attached to the object type. The downside of this approach is that the person calling the sort method has to write a comparison function each time they want to use it. In the examples above that was not a big deal because we had simply comparisons. However, there are times when that will not be the case.

# 19.4.3 Type Bounds

As we just saw, a normal type parameter, like [A], is treated like Any when we use objects of that type in code. While this is a very common usage, there are certainly times when you want to limit what types can be used in a type parameter so that you can safely call methods other than the small set that are available with Any. The way you do this is to put bounds on the type.

The most common form of this is putting an upper bounds on a type. This is done with the <: symbol. To understand why you might want to do this, let’s consider an example using code that we had before with fruit. The function, makeBreakfastShake that we wrote at the beginning of the chapter only used a single piece of fruit. This is not how it normally works. You would want to be able to include multiple pieces of fruit, perhaps of different types. A common example would be a shake with both bananas and strawberries. To do that, you might consider having code like this where you pass in an Array[Fruit].

```
def makeBreakfastShake(fruits:Array[Fruit]) {
  for(fruit <- fruits) {
    if(!fruit.canEatSkin) {
      fruit.peel
    }
    blender += fruit
  }
  blender += juice
  blender += ice
  blender.blend
}
```

This code probably looks fine to you and in many situations it will work. However, it is not perfect. Here is an example of where it runs into problems.

```
scala> val berries = Array(new Strawberry,new Strawberry)
berries: Array[Strawberry] = Array(Strawberry@51d36f77, Strawberry@103b1799)

scala> makeBreakfastShake(berries)
<console>:16: error: type mismatch;
found   : Array[Strawberry]
required: Array[Fruit]
```