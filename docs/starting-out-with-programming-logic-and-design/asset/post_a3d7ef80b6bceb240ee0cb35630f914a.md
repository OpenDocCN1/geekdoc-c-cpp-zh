
# Recursion

- 13.1 Introduction to Recursion
- 13.2 Problem Solving with Recursion
- 13.3 Examples of Recursive Algorithms

## 13.1 Introduction to Recursion

> CONCEPT: A recursive module is a module that calls itself.

You have seen instances of modules calling other modules. In a program, the main module might call module A, which then might call module B. It's also possible for a module to call itself. A module that calls itself is known as a recursive module. For example, look at the message module shown in Program 13-1.

# Program 13-1

```
Module main()
  Call message()
  End Module

Module message()
  Display "This is a recursive module."
  Call message()
  End Module
```

# Program Output

```
This is a recursive module.
This is a recursive module.
This is a recursive module.
This is a recursive module.
...and this output repeats infinitely!
```

The message module displays the string "This is a recursive module." and then calls itself. Each time it calls itself, the cycle is repeated. Can you see a problem with the module? There's no way to stop the recursive calls. This module is like an infinite loop because there is no code to stop it from repeating.

Like a loop, a recursive module must have some way to control the number of times it repeats. The pseudocode in Program 13-2 shows a modified version of the message module. In this program, the message module receives an Integer that specifies the number of times the module should display the message.

# Program 13-2

```
Module main()
  // By passing the argument 5 to the message module,
  // we are telling it to display the message
  // five times.
  Call message(5)
End Module

Module message(Integer times)
  If times > 0
    Display "This is a recursive module."
    Call message(times - 1)
  End If
End Module
```

# Program Output

This is a recursive module.
This is a recursive module.
This is a recursive module.
This is a recursive module.
This is a recursive module.

The message module in this program contains an If-Then statement (in lines 9 through 12) that controls the recursion. As long as the times parameter is greater than zero, the message "This is a recursive module." is displayed, and then the module calls itself again. Each time it calls itself, it passes times - 1 as the argument.

The main module calls the message module passing the argument 5. The first time the module is called, the If-Then statement displays the message and then calls itself with 4 as the argument. Figure 13-1 illustrates this.

# Figure 13-1 First two calls of the module

![](img/c939132f78787c7f339c6977b3fc8c85_524_0.png)

## 13.1 Introduction to Recursion

The diagram shown in Figure 13-1 illustrates two separate calls of the module. Each time the module is called, a new instance of the times parameter is created in memory. The first time the module is called, the times parameter is set to 5. When the module calls itself, an instance of the times parameter is created, and the value 4 is passed into it. This cycle repeats until finally, zero is passed as an argument to the module. This is illustrated in Figure 13-2.

# Figure 13-2 Six calls to the message module

![](img/c939132f78787c7f339c6977b3fc8c85_525_0.png)

As you can see in the figure, the module is called six times. The first time it is called from the main module, and the other five times it calls itself. The number of times a module calls itself is known as the depth of recursion. In this example, the depth of recursion is five. When the module reaches its sixth call, the times parameter is set to 0. At that point, the If-Then statement's conditional expression is false, the module returns. Control of the program returns from the sixth instance of the module to the point in the fifth instance directly after the recursive module call. This is illustrated in Figure 13-3.

- If the problem can be solved without recursion, then the module solves it and returns
- If the problem cannot be solved now, then the module reduces it to a smaller but similar problem and calls itself to solve the smaller problem

## 13.2 Problem Solving with Recursion

In order to apply this approach, first, we identify at least one case in which the problem can be solved without recursion. This is known as the *base case*. Second, we determine a way to solve the problem in all other circumstances using recursion. This is called the *recursive case*. In the recursive case, we must always reduce the problem to a smaller version of the original problem. By reducing the problem with each recursive call, the base case will eventually be reached and the recursion will stop.

# Using Recursion to Calculate the Factorial of a Number

The previous examples demonstrated recursive modules. Most programming languages also allow you to create recursive functions. Let's take an example from mathematics to examine an application of recursive functions. In mathematics, the notation $n!$ represents the factorial of the number $n$. The factorial of a nonnegative number can be defined by the following rules:

- If $n=0$ then $n! = 1$
- If $n>0$ then $n! = 1 \times 2 \times 3 \times \dots \times n$

Let's replace the notation $n!$ with factorial$(n)$, which looks a bit more like computer code, and rewrite these rules as:

- If $n=0$ then factorial$(n) = 1$
- If $n>0$ then factorial$(n) = 1 \times 2 \times 3 \times \dots \times n$

These rules state that when $n=0$, its factorial is 1. When $n$ is greater than 0, its factorial is the product of all the positive integers from 1 up to $n$. For instance, factorial(6) is calculated as $1 \times 2 \times 3 \times 4 \times 5 \times 6$.

When designing a recursive algorithm to calculate the factorial of any number, we first identify the base case, which is the part of the calculation that we solve without recursion. That is the case where $n$ is equal to 0 as follows:

- If $n=0$ then factorial$(n) = 1$

This tells how to solve the problem when $n$ is equal to 0, but what do we do when $n$ is greater than 0? That is the recursive case, or the part of the problem that we use recursion to solve. This is how we express:

- If $n>0$ then factorial$(n) = n \times factorial$(n-1)$

This states that if $n$ is greater than 0, the factorial of $n$ is $n$ times the factorial of $n-1$. Notice how the recursive call works on a reduced version of the problem, $n-1$. So, our recursive rule for calculating the factorial of a number might look like this:

- If $n=0$ then factorial$(n) = 1$
- If $n>0$ then factorial$(n) = n \times factorial$(n-1)$

The pseudocode in Program 13-3 shows how we might design a factorial function in a program.

# Program 13-3

# Program Output (with Input Shown in Bold)

Enter a nonnegative integer.
4 [Enter]
The factorial of 4 is 24

In the sample run of the program, the factorial function is called with the argument 4 passed into n. Because n is not equal to 0, the If statement's Else clause executes the following statement:

Return n * factorial(n - 1)
Although this is a Return statement, it does not immediately return. Before the return value can be determined, the value of factorial(n - 1) must be determined. The factorial function is called recursively until the fifth call, in which the n parameter will be set to zero. Figure 13-4 illustrates the value of n and the return value during each call of the function.

# Figure 13-4 The value of n and the return value during each call of the function

The function is first called
from the main function.

![](img/c939132f78787c7f339c6977b3fc8c85_529_0.png)

The second through fifth
calls are recursive.

![](img/c939132f78787c7f339c6977b3fc8c85_529_1.png)

![](img/c939132f78787c7f339c6977b3fc8c85_529_2.png)

![](img/c939132f78787c7f339c6977b3fc8c85_529_3.png)

![](img/c939132f78787c7f339c6977b3fc8c85_529_4.png)

The figure illustrates why a recursive algorithm must reduce the problem with each recursive call. Eventually, the recursion has to stop in order for a solution to be reached.

If each recursive call works on a smaller version of the problem, the recursive calls work toward the base case. The base case does not require recursion, so it stops the chain of recursive calls.

Usually, a problem is reduced by making the value of one or more parameters smaller with each recursive call. In our factorial function, the value of the parameter n gets closer to 0 with each recursive call. When the parameter reaches 0, the function returns a value without making another recursive call.
