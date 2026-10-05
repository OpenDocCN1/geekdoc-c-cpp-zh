parameters is used. Since C++11, you can also construct with {...} so that {} makes the call of the constructor without parameters explicit. You can find out more about this in Chapter 12.

In the case of string, a constructor with no parameters initializes the variable with the empty string—that is, "". Therefore, calling the constructor with the empty string as parameter std::string name{""} effectively does the same thing.

During initialization, the equal sign = does not mean "assignment"; instead, the constructor is called with a parameter. std::string name = ""} therefore has the same effect as std::string name("").

Before C++11, the curly brackets were not available for initializing strings. The notation in the older standard was std::string name("").

> Attention When Initializing with Round Parenthesis without Parameters

You cannot use std::string name(); for initialization without parameters. In this case, always use the empty curly brackets—that is, std::string name{}, or before C++11, without brackets as std::string name;

The empty parentheses () unfortunately have a double meaning here as an an empty type list for a function declaration. The preceding function declares a function name without parameters with the return