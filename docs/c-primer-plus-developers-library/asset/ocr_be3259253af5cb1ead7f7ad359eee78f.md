# C++11 List Initialization

With C++11, can you use the list-initialization syntax with classes? Yes, you can, providing the brace contents match the argument list of a constructor:

```
Stock hot_tip = {"Derivatives Plus Plus", 100, 45.0};
Stock jock {"Sport Age Storage, Inc"};
Stock temp {};
```

The braced lists in the first two declarations match the following constructor:

```
Stock::Stock(const std::string & co, long n = 0, double pr = 0.0);
```

Therefore, that constructor will be used to create the two objects. For jock, the default values of 0 and 0.0 will be used for the second and third arguments. The third declaration matches the default constructor, so temp is constructed using it.

In addition, C++11 offers a class called std::initializer_list that can be used as a type for a function or method parameter. This class can represent a list of arbitrary length, providing all the entries are of the same type or can be converted to the same type. Chapter 16, “The string Class and the Standard Template Library,” will return to this topic.

# const Member Functions

Consider the following code snippet:

```
const Stock land = Stock("Kludgehorn Properties");
land.show();
```

With current C++, the compiler should object to the second line. Why? Because the code for show() fails to guarantee that it won’t modify the invoking object, which, because it is const, should not be altered. We’ve solved this kind of problem before by declaring a function’s argument to be a const reference or a pointer to const. But there’s a syntax problem: The show() method doesn’t have any arguments for const to qualify. Instead, the object it uses is provided implicitly by the method invocation. What is needed is a new syntax, one that says a function promises not to modify the invoking object. The C++ solution is to place the const keyword after the function parentheses. That is, the show() declaration should look like this:

```
void show() const;        // promises not to change invoking object
```

Similarly, the beginning of the function definition should look like this:

```
void stock::show() const   // promises not to change invoking object
```

Class functions declared and defined this way are called const member functions. Just as you should use const references and pointers as formal function arguments whenever appropriate, you should make class methods const whenever they don’t modify the invoking object. We’ll follow this rule from here on out.