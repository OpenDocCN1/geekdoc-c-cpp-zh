
```cpp
vector<Number> allNumbers;
vector<Number*> primes;
// _
for(Number &z : allNumbers)
    if(isPrime(z, primes))
        primes.push_back(&z); // store address
return primes; // Pointers to function-local objects
}
```

**Listing 20.9** Do not return addresses of function-local objects.

## 20.7 C-Arrays

With vector and array, you already have very good options for storing multiple similar elements in sequence. But sometimes you need to go back to the basics, and in this case, that means C-arrays.

In principle, a C-array is the same as a raw pointer with the additional information of a size. While a pointer points to a single value, a C-array points to the beginning of several consecutive values:

```cpp
int value = 42;
int* pointer = &value; // points to a single int
int array[10] = {1,2,3,4,5,6,7,8,9,10}; // C-array of 10 int values
```

Now array has type int[10], and you can iterate over all elements using the range-based for loop:

```cpp
for(int val : carray)
  cout << val;
```

You can also read the fifth element or write to the eighth element. It should be noted that, as with vector and array, the index of the elements starts at zero:

```cpp
int x = carray[4]; // get the 5th element
carray[7] = 12; // write to the 8th element
```

How a C-array works with raw pointers is a bit trickier. For example, you can implicitly convert any C-array to a simple pointer of the same type. This gives you an int*:

```cpp
int* ptr = carray;
```

This ptr points to carry[0]. So with *ptr = 99, you set carry[0] = 99;

### 20.7.1 Calculating with Pointers

When a raw pointer points to a C-array, you, can perform arithmetic with this pointer. For example, use the ++ -- operations as well as + and - like you would with an integer.

```cpp
// https://godbolt.org/z/a5b6gMo9h
#include <iostream>
int main() {
    int carry[10] = { 1, 1 }; // initialized to {1,1,0,0,0,0,0,0,0,0};
    int* end = carry+10; // pointer past the last element
    for(int* p = carry+2; p != end; ++p) {
        *p = *(p-1) + *(p-2); // adds the previous two
    }
    for(int const* p=carry; p != end; ++p) {
        std::cout << *p << " ";
        std::cout << "\n";
    }
}
```

**Listing 20.10** With raw pointers pointing to a C-array, you can perform arithmetic.

This program outputs 1 1 2 3 5 8 13 21 34 55. How does that work? First, the program initializes array with two ones, followed by as many zeros as needed. **Warning:** If you dot specify an initialization, the C-array contains random values—for example:

```cpp
int carray[10]; // C-array remains uninitialized
```

With carray+10, you initialize end so that it is a pointer **behind** the last element of the C-array. It is a common convention in C and C++ to remember the end of a range, rather than pointing to the last element itself. The side effect is that the difference between the two `carray` and end pointers is exactly the number of elements in between: ((end-carray)=10) is true.

Then initialize the `int* p` for the loop with `carray+2`, thus pointing to the first element after the two ones in `carray`. This should be the first position you want to write to. For each iteration of the loop, advance `p` by one position in the C-array. However, you need to check the `for` loop after each increment to see if `p != end` checks if `p` is not yet pointing to the element after the C-array, which would signify the end of the loop. Thus, during the loop, `p` points to `carray+2`, `carray+3`, `carray+4`, ... up to `carray+9`, to execute the loop body. The final increment advances `p` to `carray+10`, which represents the loop's termination condition.

In the loop body, you write to `*p`, which means what `carray+2` to `carray+9` refer to sequentially. What do you write? Well, `*(p-1) + *(p-2)` for the sum of the two previous elements—for the first iteration, effectively:

```cpp
*p = *(p-1) + *(p-2); // in the first loop iteration, p = carray+2, so:
*(carray+2) = *(carray+2-1) + *(carray+2-2); // which is:
```

```cpp
(carray+2) = *(carray+1) + *(carray+0); // which is:
carray[2] = carray[1] + carray[0]; // so:
carray[2] = 1 + 1;
```

You have learned about the different notations. *(carray+x) is equivalent to carray[x].

In the second loop iteration, when p = carray+3, it ultimately results in

```cpp
carray[3] = carray[2] + carray[1]; // that is:
carray[3] = 2 + 1;
```

and so on and for so, until the entire carray overwritten to {1, 1, 2, 3, 5, 8, 13, 21, 34, 55}.

You have seen that you can iterate over a C-Array with the range-based for loop. You can do this because, unlike a raw pointer int*, a C-Array carries its size. Unfortunately, as soon as you pass C-Array to a function, its size is lost—it decays to a simple pointer of the same type.

 20.7.2 Decay of C-Arrays

```cpp
// https://godbolt.org/z/a5b6gMo9h
#include <iostream>
int main() {
    int carry[10] = { 1, 1 }; // initialized to {1,1,0,0,0,0,0,0,0,0};
    int* end = carry+10; // pointer past the last element
    for(int* p = carry+2; p != end; ++p) {
        *p = *(p-1) + *(p-2); // adds the previous two
    }
    for(int const* p=carry; p != end; ++p) {
        std::cout << *p << " ";
        std::cout << "\n";
    }
}
```

**Listing 20.10** With raw pointers pointing to a C-array, you can perform arithmetic.

```cpp
With carray+10, you initialize end so that it is a pointer **behind** the last element of the C-array. It is a common convention in C and C++ to remember the end of a range, rather than pointing to the last element itself. The side effect is that the difference between the two `carray` and end pointers is exactly the number of elements in between: ((end-carray)=10) is true.

Then initialize the `int* p` for the loop with `carray+2`, thus pointing to the first element after the two ones in `carray`. This should be the first position you want to write to. For each iteration of the loop, advance `p` by one position in the C-array. However, you need to check the `for` loop after each increment to see if `p != end` checks if `p` is not yet pointing to the element after the C-array, which would signify the end of the loop. Thus, during the loop, `p` points to `carray+2`, `carray+3`, `carray+4`, ... up to `carray+9`, to execute the loop body. The final increment advances `p` to `carray+10`, which represents the loop's termination condition.

In the loop body, you write to `*p`, which means what `carray+2` to `carray+9` refer to sequentially. What do you write? Well, `*(p-1) + *(p-2)` for the sum of the two previous elements—for the first iteration, effectively:

```cpp
*p = *(p-1) + *(p-2); // in the first loop iteration, p = carray+2, so:
*(carray+2) = *(carray+2-1) + *(carray+2-2); // which is:
```

```cpp
(carray+2) = *(carray+1) + *(carray+0); // which is:
carray[2] = carray[1] + carray[0]; // so:
carray[2] = 1 + 1;
```

You have learned about the different notations. *(carray+x) is equivalent to carray[x].

In the second loop iteration, when p = carray+3, it ultimately results in

```cpp
carray[3] = carray[2] + carray[1]; // that is:
carray[3] = 2 + 1;
```

and so on and for so, until the entire carray overwritten to {1, 1, 2, 3, 5, 8, 13, 21, 34, 55}.

You have seen that you can iterate over a C-Array with the range-based for loop. You can do this because, unlike a raw pointer int*, a C-Array carries its size. Unfortunately, as soon as you pass C-Array to a function, its size is lost—it decays to a simple pointer of the same type.

```cpp
int carray[10]; // C-array remains uninitialized
```

### 20.7.3 Dynamic C-Arrays

When you need a C-array whose size is determined at runtime, you can use the `new[]` operator. This returns a pointer to the first element of the dynamically allocated array on the heap. You must also use `delete[]` to free the memory.

```cpp
int size;
cin >> size;
int* dynamicArray = new int[size];
// ... use dynamicArray
delete[] dynamicArray;
```

Just like static C-arrays, dynamic C-arrays do not carry their size. You must keep track of the size yourself.
