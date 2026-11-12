> Note: Axioms for the ADT stack
> (new Stack()).isEmpty() = true
> (new Stack()).pop() = false
> (new Stack()).peek() = error
> (aStack.push(item)).isEmpty() = false
> (aStack.push(item)).peek() = item
> (aStack.push(item)).pop() = true

# ## 6.2 Simple Uses of a Stack

Once you have satisfactorily specified the behavior of an ADT, you can design applications that access and manipulate the ADT's data solely in terms of its operations and without regard for its implementation. Thus, we can use the operations of the ADT stack even though we have not discussed their implementations yet. This section presents two rather simple examples for which the LIFO property of stacks is appropriate.

![](bbox=[0.79, 0.26, 0.92, 0.33])

# ### 6.2.1 Checking for Balanced Braces

C++ uses curly braces, “{” and “}”, to delimit groups of statements. For example, braces begin and end a method’s body. If you treat a C++ program as a string of characters, you can use a stack to verify that a program contains balanced braces. For example, the braces in the string

```
abc{defg{ijk{l{mn}}op}qr
```

are balanced, while the braces in the string

```
abc{def}}{ghij{kl}m
```

are not balanced. You can check whether a string contains balanced braces by traversing it from left to right. As you move from left to right, you match each successive close brace “}” with the most recently encountered unmatched open brace “{”; that is, the “{” must be to the left of the current “}”. The braces are balanced if

+   1. Each time you encounter a “{”, it matches an already encountered “}”.
+   2. When you reach the end of the string, you have matched each “{”.

The solution requires that you keep track of each unmatched “{” and discard one each time you encounter a “}”. One way to perform this task is to push each “{” encountered onto a stack and pop one off each time you encounter a “}”. Thus, a first-draft pseudocode solution is

Requirements for balanced braces

```
for (each character in a string)
{
    if (the character is a '{')
        aStack.push('{')
    else if (the character is a '}')
        aStack.pop()
}
```

Initial draft of a solution

Although this solution correctly keeps track of braces, missing from it are the checks that conditions 1 and 2 are met—that is, that the braces are indeed balanced. To verify condition 1 when a “}” is encountered, you must check to see whether the stack is empty before popping from it. If it is empty,