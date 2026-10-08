But couldn't the compiler see that \textbf{iac} has just 20 elements so that \textbf{iac[200]} is an error? A compiler could, but as far as we know no production compiler does. The problem is that keeping track of array bounds at compile time is impossible in general, and catching errors in the simplest cases (like the one above) only is not very helpful.

# ### 18.6.1 Pointers to array elements

A pointer can point to an element of an array. Consider:

```
```cpp
double ad[10];
double* p = &ad[5];
// point to ad[5]
```
```

We now have a pointer \textbf{p} to the \textbf{double} known as \textbf{ad[5]}:

![](bbox=[0.159, 0.367, 0.73, 0.481])

We can subscript and dereference that pointer:

```
```cpp
*p = 7;
p[2] = 6;
p[-3] = 9;
```
```

We get

![](bbox=[0.159, 0.645, 0.73, 0.761])

That is, we can subscript the pointer with both positive and negative numbers. As long as the resulting element is in range, all is well. However, access outside the range of the array pointed into is illegal (as with free-store-allocated arrays; see §17.4.3). Typically, access outside an array is not detected by the compiler and (sooner or later) is disastrous.