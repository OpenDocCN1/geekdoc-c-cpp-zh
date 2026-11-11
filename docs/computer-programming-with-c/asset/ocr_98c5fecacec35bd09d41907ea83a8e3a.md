Figure 7.27 gives the complete execution of the statement

```
`m =max( max( max ( a,b ) , max(c,d) ) , max(e,f ) ) ;`
```

After the execution of the statement, the value of variable `m` will be initialized to `30` which is the maximum of the six numbers.

![](bbox=[0.52, 0.12, 0.93, 0.42])

**Figure 7.27:** Execution of nested calls to max( )

# ## 7.6 Passing Array as an Argument to the Function

It is possible to pass array as an argument to the function. Let `a` be an array of size `n` created in the `main()` function. We create a function `max()` which accepts an array as an argument and returns the maximum element from the array back to the caller.

When defining the function `max()`, we create an array `p` which is of type 'float' as a formal argument along with the integer `n`. Note that we should not specify the size of the formal array `p` because the array `p` will be the exact image of the actual argument `a` passed to it by the 'calling' function. Hence, the size of the array `p` will be same as the size of the array `a`. In this case, since the size of array `a` is 100, size of `p` will also be 100. The function `max()` will find the maximum of all the elements in the array passed to it and return a resultant 'maximum value' back to the 'calling' function.

The function `max()` takes the following two arguments:

+   1. **Array of floats:** This is the array which stores the actual data.
+   2. **Integer n:** Although the size of the array `a` is 100, all 100 elements of `a` are not valid. As seen in `main()`, only `n` elements in `a` are valid, containing actual user inputs. As `n` is a local variable of `main()`, there is no way for function `max()` to determine how many elements in `a` are valid user inputs. Hence, we pass `n` as an argument from `main()` to `f1()` so that `f1()` knows the exact value of `n`.

Further, the function `max()` returns a floating point result, which is the maximum of `n` elements in the array. Hence, the function `max()` must be prototyped as

```
`float max(float [ ] , int );`
```

The logic to find the maximum of `n` elements from the array is same as discussed in Chapter 6, section 6.2.4. Given below is the full source code to find the maximum of `n` numbers using the function `max()`.