arguments.

```
// zero initialization of the string to the empty string
std::string msg {};
```

Brace initialization has the added benefit of disallowing type conversions that are narrowing. This means that if we try to use brace initialization to initialize a variable with a value that it cannot safely hold, the compiler will throw a warning or an error.

Floating-point to integer conversions are always narrowing — even 5.0 to 5.

```
// error: narrowing initialization: trying to convert a float type
// type to an int type
```

```
int width { 4.0 };
```

The best practise is to always initialize variables. But sometimes, in order to save CPU cycles, we can leave variables uninitialized.

The use of brace initialization forces value initialization. A variable that is initialized with {} is set to the zero value for the type of the variable (for example, nullptr if it is a pointer:

```
string s;
string s {};
// s has an undefined value
// s is initialized to the empty string
```

```
int j;
int j {};
// j has an undefined value
// j is initialized by 0
```

```
int* p;
int* p {};
// p has undefined value
// p is initialized to nullptr
```

# The Meaning Of Return {

Consider the function declaration: