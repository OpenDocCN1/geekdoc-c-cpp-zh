type string. Unfortunately, the compiler initially accepts this, but complains when name is used.

If you have C++11 or higher, you should get into the habit of always initializing variables with the brackets or the equals sign.

There is another variant that has the same effect:

```
std::string name = "";
```

Use this notation if you want to perform the initialization with an initialization list; in this case, this is a list with only one element—namely, the empty string "". As it is optional during initialization, this notation almost always corresponds to std::string name(""). To keep clear, however, I recommend only using this notation specifically for the initialization list.

# 6.1.2 Functions and Methods

You have seen that you can create string variables in this way—for example:

+   * std::string name; Or std::string name(); creates an empty string.

+   * std::string name = "value"; Or std::string name("value") creates a string from a literal.

Instead of "value", you can also use a different string—that is, copy a different character sequence into a string. In the documentation for string, you will find further options for initialization and even more functions