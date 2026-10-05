# 7.2 Function Type

Just like almost everything else in C++, a function has a type. This type determines how you call the function and what you can do with the result. The type of a function consists of the types of the parameters and the return type.

So the functions

```
bool print(std::string arg1, int arg2);
```

and

```
bool formatIntoToString(std::string format, int value);
```

have the same type. The exact type is something composite—in this case:

```
std::function<bool(std::string, int)>
```

You see that in this notation, the return type bool is directly behind the angle bracket, and the parameter types are in parenthesis inside the angle brackets. function is just a tool from the standard library and my preferred C++ notation, which I understand better than the actual type in C form—that is:

```
bool(*)(std::string, int);
```