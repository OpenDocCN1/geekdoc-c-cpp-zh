The call is ambiguous because 2.0 is the best match for the first argument of pow(double ,double) and 2 is the best match for the second argument of pow(int,int).

# 12.3.5 Manual Overload Resolution

Declaring too few (or too many) overloaded versions of a function can lead to ambiguities. For example:

```
void f1(char);
void f1(long);
void f2(char*); void f2(int*);
```

```
void k(int i) {
f1(i); // ambiguous: f1(char) or f1(long)?
f2(0); // ambiguous: f2(char*) or f2(int*)?
}
```

Where possible, consider the set of overloaded versions of a function as a whole and see if it makes sense according to the semantics of the function. Often the problem can be solved by adding a version that resolves ambiguities. For example, adding

```
inline void f1(int n) { f1(long(n)); }
```

would resolve all ambiguities similar to f1(i) in favor of the larger type long int.
One can also add an explicit type conversion to resolve a specific call. For example:

```
f2(static_cast<int*>(0));
```

However, this is most often simply an ugly stopgap. Soon another similar call will be made and have to be dealt with.
Some C++ novices get irritated by the ambiguity errors reported by the compiler. More experienced programmers appreciate these error messages as useful indicators of design errors.

# 12.4 Pre- and Postconditions

Every function has some expectations on its arguments. Some of these expectations are expressed in the argument types, but others depend on the actual values passed and on relationships among

argument values. The compiler and linker can ensure that arguments are of the right types, but it is up to the programmer to decide what to do about “bad” argument values. We call logical criteria that are supposed to hold when a function is called preconditions, and logical criteria that are supposed to hold when a function returns its postconditions. For example:

```
int area(int len, int wid)
/*
calculate the area of a rectangle
precondition: len and wid are positive
postcondition: the returnvalue is positive
```