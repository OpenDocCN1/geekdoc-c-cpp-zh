# // PERFORMING OUT-OF-BOUNDS CHECKS

In terms of addressing individual elements inside the overall data structure, vectors can be used like arrays. You've seen several examples where square brackets are used to access individual elements. In all of the loops that print out elements in the last several examples, you have accessed elements with square brackets.

But there is a problem you have to be careful to avoid accessing array elements: the array-of-bounds error, which occurs when you access elements that have not been allocated to the array or vector.

When you use at instead of square brackets, it will automatically check the bounds of the array. If you try to access an element that should not exist, you will get an exception, which is an error code. And if you have an exception in a situation like this, the program will just stop. If you access memory that it shouldn't, let set values in memory that it shouldn't, and won't print out your memory values containing nonsense.

Accessing elements of a vector using square brackets works just like arrays—good and bad. On the good side, it's efficient, and you can access the next element directly. Because all the data is allocated in one continuous block of memory, it's easy for the computer to process it efficiently.

In Program 8_13, you have a vector that has been initialized with 3 elements, having the values 1, 2, and 3. However, in the loop that you print out the elements, you are printing v[3] and v[4], which don't really exist.

```
// Program 8_13
// Vector ERROR indexing out of bounds
#include <iostream>
```

```
int main() {
  vector<int> v = {1, 2, 3};
  for (int i = 0; i < 5; i++) {
    cout << v.at(i) << " ";
  }
  cout << endl;
}
```

Just like arrays, the code lets you do this; there's nothing stopping you from doing it. But when you run the code, who knows what you'll get? In general, those nonexistent elements will have whatever value left in memory location, and you have no guarantee what that is!

But with vectors, there is a way to avoid this from error occurring: Instead of accessing elements using square brackets, you can use the member function at.

```
#include <vector>
```

To use this method, you use the vector name, followed by a period, and then the number of the element you want to access in parentheses. This is basically the code from before, but now you are using .at and parentheses, rather than square brackets, to access the element.

When you run this code, you get an output of 3 elements. You have for loop, in which you try to print each element, from 0 to 4, from a vector of size 3. Printing out elements 0, 1, and 2 are fine. However, when you try to print v[3], that will be out of bounds. Because you're using the at function instead of square brackets, the program will stop at this point. It will exit with an exception code.

using namespace std;

Lecture 08 | Vectors for Safe and Flexible Data Storage