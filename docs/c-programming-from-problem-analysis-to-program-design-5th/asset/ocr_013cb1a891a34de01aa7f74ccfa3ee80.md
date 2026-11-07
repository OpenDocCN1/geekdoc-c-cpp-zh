```
```cpp
xClass ();
xClass (int, double);
private:
    int u;
    double w;
};
```
```

and assume that the following statement is in a user program:

```
```cpp
xClass x;
```
```

+   a. How many members does **class** xClass have?
+   
+   b. How many *private* members does **class** xClass have?
+   
+   c. How many constructors does **class** xClass have?
+   
+   d. Write the definition of the member function `func` so that `u` is set to 10 and `w` is set to 15.3.
+   
+   e. Write the definition of the member function `print` that prints the contents of `u` and `w`.
+   
+   f. Write the definition of the default constructor of the **class** xClass so that the *private* member variables are initialized to 0.
+   
+   g. Write a C++ statement that prints the values of the member variables of the object `x`.
+   
+   h. Write a C++ statement that declares an object `t` of type xClass and initializes the member variables of `t` to 20 and 35.0, respectively.

4. Consider the definition of the following class:

```
```cpp
class CC
{
public :
    CC();                 //Line 1
    CC(int);              //Line 2
    CC(int, int);         //Line 3
    CC(double, int);      //Line 4
    .
    .
    .
private:
    int u;
    double v;
};
```
```

+   a. Give the line number containing the constructor that is executed in each of the following declarations.
+   
+      i. `CC one;`
+   
+      ii. `CC two(5, 6);`
+   
+      iii. `CC three(3.5, 8);`