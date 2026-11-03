```
}/*End of switch*/
common statements;
break;
default:
    break;
}/*End of switch*/
```

Hopefully this will help lot of new programmers.

# 16.11 Avoid Pointer Dereference

We should always avoid pointer dereferencing in loop or while passing it as parameter. It creates lot of trouble in memory. Suppose it is used in loop then it will affect the efficiency. So better assign it to some temporary variable and then use that temporary variable in loop.

# 16.12 Prefer Pre Increment/Decrement to Post Increment/Decrement

We should prefer pre increment/decrement to post increment/decrement wherever both of them have been used for same work. In pre increment, it first increments the value and just copies to the variable location but in post increment it first copies the value to temporary variable, increments it and then copies the value to variable location. For a one time operation may be it will not affect but suppose this operation is in 1000 time loop then it will sure effect the efficiency. So it will always be better to use pre increment/decrement to get efficiency.

# 16.13 Prefer Array to Memory Allocation

Wherever possible we should use array instead of pointer with memory allocation. Accessing with array index is always fast compared to dynamic storage. Basically it depends on the requirement also. But if we are sure that we are not going to use storage more than particular size then we can prefer array for that particular size. Memory allocation and deallocation has some burden and in some circumstances it can be avoided with array. You can take example of creating stack or queue, which will be better with array instead of implementing with linked list when we know the size of stack and queue will not be more than particular size.

# 16.14 Use Array Style Code Rather Than Pointer

Pointer is special facility in C that distinguishes it from other languages. Effective use of pointer makes C language more efficient. But it also creates problem for compiler to optimize code. Pointer can read and write at any part of memory and it becomes difficult for compiler to optimize code which uses pointer. In some places we can use pointer as array. Like we can use ptr[0], ptr[1],...... which will make compiler's job easier for optimization.

# 16.15 Expression Order Understanding

In C we use lot of expressions in control statements and we also join more than one expressions by || or && operator. Let us take an example of || operator-
A || B
Here first A will be evaluated, if it's true then there is no need of evaluation of expression B and condition will become true. But if A is false then it will check for B, now if B is true then whole condition will become true otherwise it will be false. Suppose probability of expression A becoming true is very less and B becoming true is high then most of the time after evaluating expression A it will go for evaluation of B. So most of the time we are evaluating A unnecessarily. In this case, it would be better to put