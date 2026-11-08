```
```cpp
void show_error(std::string message)
{
    std::cout << message << std::endl;
}
```
```

You specify the default argument value like this:

```
```cpp
void show_error(std::string message = "Program Error");
```
```

If both are separate, you need to specify default values in the function prototype and not in the function definition. The reason is that when resolving the function calls, the compiler needs to know whether a given number of arguments is acceptable.

To output the default message, you call such functions without the corresponding argument:

```
```cpp
show_error();        // Outputs "Program Error"
```
```

To output a particular message, you specify the argument:

```
```cpp
show_error("Nothing works!");
```
```

In the previous example, the parameter was passed by value. Of course, you can also specify default values for parameters that are passed by reference-to-const in the same manner:

```
```cpp
void show_error(const std::string& message = "Program Error");  // Better...
```
```

From what you learned in the previous section, it also should come as no surprise that default values for which the implicit conversion requires the creation of a temporary object—as is in our example—are illegal for reference-to-non-const parameters. Hence, the following should not compile:

```
```cpp
void show_error(std::string& message = "Program Error");  /* Does not compile */
```
```

Specifying default parameter values can make functions simpler to use. Naturally, you aren't limited to just one parameter with a default value.

> > **Note**  We will have more to say about implicit argument conversions of string literals to temporary string objects in Chapter 9. Spoiler alert: The performance of reference-to-const-string parameters will turn out to be suboptimal in general, precisely because they sometimes require the creation of such temporary string objects.

# ## Multiple Default Parameter Values

All function parameters that have default values must be placed together at the end of the parameter list. When an argument is omitted in a function call, all subsequent arguments in the list must also be omitted. Thus, parameters with default values should be sequenced from the least likely to be omitted to the most likely at the end. These rules are necessary for the compiler to be able to process function calls.