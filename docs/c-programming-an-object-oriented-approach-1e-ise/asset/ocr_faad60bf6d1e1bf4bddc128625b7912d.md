We can have one or more default parameters with predefined values in a function declaration.

Function overloading provides several definitions for a function with the same name but with different *signatures*, which means a different number of parameters, or different types of parameters, or both. The return type of a function is not part of its signature.

Scope and lifetime are two concepts that affect the design and use of functions. Scope defines where in the source code a named entity is visible. An entity in a program has a lifetime: It is born and it dies.

# Problems

**PR-1.** Find the signature associated with each of the following function declarations:

```
```cpp
int firstFunction (int x, float y, int z);
void secondFunction (int x, boolean y);
void thirdFunction (double x, double y);
void fourthFunction ();
```
```

**PR-2.** Given the declaration of the following two functions, determine if they are overloaded versions of each other.

```
```cpp
int fun (int x, int y);
void fun (int a, int b);
```
```

**PR-3.** Given the declaration of the following two functions, determine if they are overloaded versions of each other.

```
```cpp
int fun (int x, int y);
void fun (float a, float b);
```
```

**PR-4.** Given the declaration of the following two functions, determine if they are overloaded versions of each other.

```
```cpp
int fun (int x, int y, int z);
float fun (int a, int b);
```
```

**PR-5.** Given the declaration of the following two functions, determine if they are overloaded versions of each other.

```
```cpp
int functionOne (int x, int y);
int functionTwo (int a, int b);
```
```

**PR-6.** Given the declaration of the following two functions, determine if they are overloaded versions of each other.

```
```cpp
int fun ();
float fun ();
```
```

**PR-7.** Find the valid function declarations among the following:

```
```cpp
a. float one (int a, int b);
b. boolean two (int a, int b);
c. float (int a, int b);
d. void three (void);
e. int ();
```
```