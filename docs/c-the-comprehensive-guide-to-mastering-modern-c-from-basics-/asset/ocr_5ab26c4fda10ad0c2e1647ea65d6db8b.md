You have already seen some functions, and you have already written some of them yourself—primarily the main() function, because you can't do without main(). In this chapter, I want to explain the possibilities you have with functions, especially when you write them yourself.

A function is something that you can call from another location. Functions can also have a return value. A function that does not have a return value is said to return void. In addition to calculating the return value, parameters can also be changed if you allow it. A function can also have side effects, meaning it can additionally change other objects in the program.

# 7.1 Declaration and Definition of a Function

When you write a function and immediately specify what its program code looks like—that is, with the instructions in the curly brackets—then this is the definition of the function:

```
int addTwo(int a, int b) {
  return a + b;
}
```

However, you can also first tell the compiler that a certain function exists somewhere; where exactly, it should figure out later. Then you omit the brackets and only name the function header—and you have a declaration: