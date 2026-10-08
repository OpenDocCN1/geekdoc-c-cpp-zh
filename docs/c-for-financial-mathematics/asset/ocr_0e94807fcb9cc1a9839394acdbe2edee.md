as a parameter and a function that takes a pointer as a parameter. Here is a function that adds up a sequence of `length` numbers which start at the memory location `toSum`.

```
```
int sumUsingPointer( int* toSum, int length ) {
    int sum = 0;
    for (int i=0; i<length; i++) {
        sum+=toSum[i];
    }
    return sum;
}
```
```

The code here is identical to that with arrays except that we declare the type using `*` rather than `[]`. In particular, notice that you have to pass the length as well as the pointer.

There isn't a lot wrong with this code. Nevertheless, an experienced C++ programmer might choose to write this as follows:

```
```
int sumUsingForAndPlusPlus(int* begin, int n) {
    int sum = 0;
    int* end = begin + n;
    for (int* ptr = begin; ptr != end; ptr++) {
        sum += *ptr;
    }
    return sum;
}
```
```

This code is hard to follow if you are new to C++. But because it follows certain programming conventions, it does become easy to understand with a little practice.

We call the first memory location `begin`. We call the memory location immediately after the last element `end`. In the `for` loop we move the variable `ptr` through the values from `begin` up to, but not including, `end`. At each stage of the loop we add to `sum` the value pointed to by `ptr`.

There are two reasons why an experienced programmer might prefer this version of the code:

+   (i) The code is completely standardised and therefore easy to read once you are used to it. `begin` is a standard name for a pointer as is `end`. This means that the reader can understand the `for` loop at a glance. This is the purpose of for loops: they shout out “boring looping code” so you can focus on the interesting bit in the middle of the loop and ignore the rest. Later in the book we will discuss a C++ concept called iterators that allows this pointer code to be generalised to many different kinds of data structures. See Chapter 18.

+   (ii) This code may be slightly faster. We only perform one addition per loop,