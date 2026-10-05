```
/* input */
input(name, birthYear);
/* calculations */
// ...
}
```

# Listing 6.1 Some possible uses of strings.

You can do all kinds of things with variables of type string. You can use functions that take a string as a parameter, such as std::getline with std::getline(std::cin, name). In addition, each string variable has methods that you call with the dot , such as name.length() in the if. Methods are special functions that always work on one of the variables with which they were called using dot notation.

You can see at the beginning 6.1.1 Initialization of main() how to define a string. Because it is not a built-in type, it is also initialized even though no = or similar have been specified. In this case, the following variants are equivalent:

```
std::string name;
std::string name();
std::string name("");
std::string name(""");
std::string name = "";
```

Here, however, only the first two variants are completely identical. As a complex data type, string has a constructor—a special function that serves the specific purpose of initializing a new variable. If you do not specify an initialization, the constructor with no