# Self-Test Exercises

+   1. What is a pointer in C++?

+   2. Give at least three uses of the * operator. Name and describe each use.

+   3. What is the output produced by the following code?

```
int *p1, *p2;
p1 = new int;
p2 = new int;
*p1 = 10;
*p2 = 20;
cout << *p1 << " " " << *p2 << endl;
p1 = p2;
cout << *p1 << " " " << *p2 << endl;
*p1 = 30;
cout << *p1 << " " " << *p2 << endl;
```

How would the output change if you were to replace

+   *p1 = 30;

with the following?

+   *p2 = 30;

+   4. What is the output produced by the following code?

```
int *p1, *p2;
p1 = new int;
p2 = new int;
*p1 = 10;
*p2 = 20;
cout << *p1 << " " " << *p2 << endl;
*p1 = *p2; //This is different from Exercise 3
cout << *p1 << " " " << *p2 << endl;
*p1 = 30;
cout << *p1 << " " " << *p2 << endl;
```

# Basic Memory Management

A special area of memory, called the frestore or the heap, is reserved for dynamically allocated variables. Any dynamic variable created by a program consumes some of the memory in the frestore. If your program creates too many dynamic variables, it will consume all the memory in the frestore. If happens, any additional calls to new will fail. What happens when you use new after you have exhausted all the memory in the frestore (all the memory reserved for dynamically allocated variables) will depend on how up-to-date your compiler is. With earlier C++ compilers, if