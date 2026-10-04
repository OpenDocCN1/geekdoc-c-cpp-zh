There is a workaround that lets you pass a literal by reference. The trick is to add const in front of the reference parameter. This tells the compiler: "I don’t need to copy this data, and I won’t modify it. It will stay constant." This is called passing by const reference. Passing by const reference lets you avoid unnecessary copying and can help optimize code when you’re dealing with large data.

Another way const can be used is when you have a variable that you want to assign a value to and you know that the value will never change. In that case, you can declare it

to be a const variable when you declare and initialize it. You just write const in front of the type. Declaring a variable to be constant ensures that the intent of the variable—as an unchanging value—is maintained.

The use of pass by reference is also a way, in effect, of returning more than one value. Ordinarily, a function can only have one return type, but if you have multiple parameters that are passed by reference, you can use that to modify the values of each of them. In this way, a function can return multiple values—by modifying multiple arguments.

> When you’re deciding when to overload functions, when to pass by value, and when to pass by reference, a good rule of thumb is to pass by value as a default, unless you have a good reason not to. That way, you’re less likely to have errors or run into problems.

# READINGS

+   a Stroustrup, Programming Principles and Practice Using C++, section 8.5.

b Lippman, Lajoie, and Moo, C++ Primer, sections 6.2, 6.4, 6.5, and 6.6.

# Exercise Solution

Here’s what the header could look like. (Note that the order of parameters is up to you.)

```
1  // Program 13_9
2  // Passing by Reference - Incomplete program
3  #include<iostream>
4  #include<string>
5  using namespace std;
6
7  void search_and_replace(string& main_string, string word_to_find, string replacement) {
8      // Manipulate main_string here
9  }
10
11 int main() {
12     string long_document;
13     // Assign something to long_document here
14     search_and_replace(long_document, "Robert", "Bob");
15 }
```

Click here to go back to the exercise.