
# Introduction to Programming and Problem-Solving Using Scala

numerical operations between a Double and an Int automatically convert the Int to a Double and result in a Double.

## 5.4 Abstraction

What if, instead of taking the sum of a bunch of user inputs, we want to take a product? What would we change in sumCount to make it productAndCount? The obvious change is that we change addition to multiplication in the recursive bunch of the if. A less obvious change is that we also need the base case to return 1 instead of 0. So our modified function might look like this.

```scala
def productAndCount():(Int,Int) = {
 val n = readLine()
  if (n!="quit") {
    val (s,c) = productAndCount()
    (s*n.toInt, c+1)
  } else {
    (1, 0)
  }
}
```

This is almost exactly the same as what we had before. We just called it a different name and changed two characters in it. This copying of code where make minor changes is something that is generally frowned upon. You might say that it does not smell right. There are many reasons why you would want to avoid this type of thing. First, what happens if your first version had a bug? Well, you have duplicated it and when you figure out something is wrong you want a bit to fix it in multiple places. A second problem is closely related to this, which is the situation where you realize you want a bit more functionality so you need to add something. Now you have multiple versions to add that into. In, it makes the code base harder to work with. Longer code means more places can be messed up and more code to go through when there is a problem. For this reason, we strive to reduce code duplication. How do we do this is to include abstraction. We look for ways to make the original code more flexible so we can do everything we want. Abstraction is one of the most important tools in Computer Science and we are here to start with a simple example.

In order to abstract these functions to make them into one, we focus on the things that were different between them and ask if there is a way to pass that information as arguments to a function that will do that. For this, changing of the name is not important. What is important that we changed the operation we were doing and the base value that was returned. That value is easy to deal with. We simply pass an argument to the method that is the value returned at the base. That might look like this.

```scala
def inputAndCount(base:Int): (Int,Int) = {
 val n = readLine()
  if (n!="quit") {
    val (s,c) = inputAndCount(base)
    (s*n.toInt, c+1)
  } else {
    (base, 0)
  }
}
```

> ³In deed, the term "smell" is the actual terminology used in the field of refactoring for things in code that are not quite right and should be fixed.

The argument base is passed through the recursion and is also returned to the base case. However, this version is stuck with multiplication so we have not gained all that much.

Dealing with the multiplication is a bit harder. For that we need to think about multiplication and addition really and how they are used here. Both multiplication and addition are operators. They take two operands and give us a back value. When described that way, we can see they are like functions. We need a function that takes two Ints and returns an Int. That function could be multiplication or addition then the inputCount function be flexible enough to handle either a sum or a product. It might look like this:

```scala
def inputCount(base:Int, func:(Int,Int)->Int):(Int,Int) = {
 val n = readLine()
  if(n="") {
    val (s,c) = inputCount(base,func)
    func(s,n.toInt, c+1)
  } else {
    (base, 0)
  }
}
```

The second argument to inputCount, which is called func, has a more complex type. It is a function. Type that takes two Ints as arguments and returns an Int. As base, we pass func through the recursive call. We also used func in place of the * or the + in the first element of the return in the recursive case. Now instead of doing s.n.toInt or s.n.toInt, we are doing func(s,n.toInt). What that depends on the function that is passed

To make sure this process need to see it in action. Let us doing a sum and, easiest to understand syntax. We define a function that does addition and pass that in. For the input we use the numbers 3, 4, and 5 followed by "quit". Those values are not shown by the REPL

```scala
scala def add(x:Int,y:Int):Int = x+y
add:(x:Int,y:Int)Int
```

```scala
inputCount(0,add)
res3:(Int,Int) = (12,3)
```

In the call to inputCount we used the add func, which was defined above it, as the second argument. Using a function in this way forces us to do a lot of typing. This is exactly how Scala includes function literals. You will recall from chapter 4 that a function allows us to define a function on the fly in Scala. The normal syntax for this looks lot like the function in the definition of inputCount. It uses a => between the parameters and the body of the function. Using a literal we could use inputCount without defining the function. It looks like this:

```scala
inputCount(0,(x,y) => x+y)
res4:(Int,Int) = (12,3)
```

# Introduction to Programming and Problem-Solving Using Scala

One thing to notice about this is that we did not specify the types on x and y. Because Scala knows the second argument to inputCount is a function that takes Int. If you remember back to section 4.5 on function literals, there is an even shorter syntax for declaring them. This syntax uses _ as a placeholder. This can only work in certain situations.

```scala
inputCount(0,_)
res5:(Int,Int) = (12,3)
```

Of course, the reason for doing this was that we could also do products without having to write a function. The product function differed from the sum function in that the base case was 1 instead of 0. If we make those two changes to what we did above, we will see that we have a single function that can either sum or product.

```scala
inputCount(1,_)
res6:(Int,Int) = (60,3)
```

Not only did we succeed, we did so in a way that feels satisfying to us. Why? Because our abstraction is created in a minimal way and only the essential variations have we expressed. We do not have to do a lot of typing just to use the abstraction. It is not much longer to call inputCount than it was to call sum or productCount. The inputCount function is what we call a higher order function. That is because it is a function that uses other functions to operate. We provide it with a function to help it do its job. This type of construct has been found mostly in functional languages. With the addition of lambda expressions, mainstream languages also allows this type of functionality.

You might say you had to duplicate the code to prevent that? Is this really all that smell? The answer, with a sum and a product, is "no". A single code duplication is not the end of the world. However, if I ask you to complete versions that return the minimum or the maximum, what do you do? Without the abstraction, you get to copy and paste two versions of the code and make similar minor changes to them. With the abstraction, you just call it with different arguments. The question of whether it is worth it to abstract really depends on how much you expect in the future. If the abstraction does not take much effort it is probably worth doing to start with because it is often hard to predict if you will need to extend something in the future. You might not feel this what we do in this, but it becomes very significant in professional development when you are not told up front exactly is wanted of you and when you are, the customer is to change their mind later in the process.
