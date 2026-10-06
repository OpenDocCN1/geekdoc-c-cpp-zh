Things start to get more interesting when you define a sum function that takes two parameters. LISTING 1-66 shows the code definition and its execution result in FSI.

# LISTING 1-66 Defining a sum function that takes two parameters

```
// define a sum function that takes two parameters
let sum x y = x + y

// FSI execution result
val sum : int -> int -> int
```

sum is aried function. You can define this function as something that takes x as a parameter and returns a new function that takes a parameter called y. The beauty of this approach is that it enables you to define a new function based on an partially applied function. For example, the increaseOne function is really a sum function where y is always I. So you can rewrite the increaseOne as follows:

let increaseOne2 = sum 1

If you give 4 to this increaseOne2 function, the result will be 5. It is like passing 4 and 1 into the sum function.

```
increaseOne2 4    // returns 5
sum 4 1             // pass 4 and 1 into the sum function and yield 5
```

> Note You might be tempted to invoke this sum function with the following syntax: sum(4,1). If you do this, an error message will point out that the expression types of int*int. However, (4,1) is an F# type called a tuple. The code sum(4,1) is trying to pass a tuple type into sum, which confuses the F# compiler.

Now you can define your function using refactor and the conversion-task F# code, as shown in Listing 1-67.

# LISTING 1-67 Defining An F# function in the odd-number sum program

```
// define enum
type EvenOddFlagEnum =
  | Odd = 0x1
  | Even = 0x0

// define a function to check if the given number is odd or not
let checkOdd n = n && (int EvenOddFlagEnum.Odd) <> 0
```

![](bbox=[0.96, 0.523, 0.133, 0.563])