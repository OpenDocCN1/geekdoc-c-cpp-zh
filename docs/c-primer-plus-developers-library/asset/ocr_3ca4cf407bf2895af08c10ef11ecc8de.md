```
public:
    const char * what() { return "bad arguments to gmean()"; }
...
};
```

If you don’t want to handle these derived exceptions differently from one another, you can catch them with the same base-class handler:

```
try {
...
}
catch(std::exception & e)
{
    cout << e.what() << endl;
...
}
```

Or you could catch the different types separately.
The C++ library defines many exception types based on `exception`.

# The stdexcept Exception Classes

The stdexcept header file defines several more exception classes. First, the file defines the logic_error and runtime_error classes, both of which derive publicly from exception:

```
class logic_error : public exception {
public:
    explicit logic_error(const string& what_arg);
...
};
```

```
class domain_error : public logic_error {
public:
    explicit domain_error(const string& what_arg);
...
};
```

Note that the constructors take a string object as an argument; this argument provides the character data returned as a C-style string by the `what()` method.

These two new classes serve, in turn, as bases for two families of derived classes. The logic_error family describes, as you might expect, typical logic errors. In principle, sound programming could avoid such errors, but in practice, such errors might show up. The name of each class indicates the sort of error it is intended to report:

+   - domain_error
+   - invalid_argument
+   - length_error
+   - out_of_bounds