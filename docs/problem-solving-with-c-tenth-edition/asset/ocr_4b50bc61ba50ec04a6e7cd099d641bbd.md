```
//Precondition: If n < 0, then x is not 0.
//Returns x to the power n.

(Hint: x⁻ⁿ is equal to 1/(xⁿ).)
```

# 14.3 THINKING RECURSIVELY

> There are two kinds of people in the world: those who divide the world into two kinds of people and those who do not.
> 
> — ANONYMOUS

# Recursive Design Techniques

When defining and using recursive functions you do not want to be continually aware of the stack and the suspended computations. The power of recursion comes from the fact that you can ignore that detail and let the computer do the bookkeeping for you. Consider the example of the function power in Display 14.3. The way to think of the definition of power is as follows:

```
power(x, n) returns power(x, n − 1) * x
```

Since xⁿ is equal to xⁿ⁻¹ * x, this is the correct value to return, provided that the computation will always reach a stopping case and will correctly compute the stopping case. So after checking that the recursive part of the definition is correct, all you need check is that the chain of recursive calls will always reach a stopping case and that the stopping case always returns the correct value.

When you design a recursive function, you need not trace out the entire sequence of recursive calls for the instances of that function in your program. If the function returns a value, all that you need do is confirm that the following three properties are satisfied:

+   1. There is no infinite recursion. (A recursive call may lead to another recursive call and that may lead to another and so forth, but every such chain of recursive calls eventually reaches a stopping case.)
+   
+   2. Each stopping case returns the correct value for that case.
+   
+   3. For the cases that involve recursion: If all recursive calls return the correct value, then the final value returned by the function is the correct value.

For example, consider the function power in Display 14.3:

+   1. There is no infinite recursion: The second argument to power(x,n) is decreased by 1 in each recursive call, so any chain of recursive calls must eventually reach the case power(x,0), which is the stopping case. Thus, there is no infinite recursion.

![](bbox=[0.789, 0.581, 0.891, 0.626])