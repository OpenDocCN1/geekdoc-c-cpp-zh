# **Chapter 15**

# ### `underflow_error()`

This class defines the type of objects thrown as exceptions to emphasize the arithmetic underflow errors. It is designed in such a way that apart from the elements of the standard library, any program can throw it as an exception. This class may be defined as follows:

```
class underflow_error : public runtime_error
{
public:
    explicit underflow_error (const string& what_arg);
};
```

# ### `ios_base::failure`

The standard exception class derives this embedded class, which serves as a base class for the objects thrown as exceptions by the member functions in the iostream hierarchy of classes. This class is defined within the std namespace as:

```
class ios_base::failure : public exception
{
public:
    explicit failure (const string& msg);
    virtual ~failure();
    virtual const char* what() const throw();
};
```

The value of string received as the msg parameter in the constructor explicit failure (const string& msg) is internally stored and its C-string equivalent is returned by subsequent calls to what(). It effectively calls its parent class' constructor (exception::exception). The destructor virtual ~failure() has no operation. The declaration virtual const char* what() const returns the C-string value equivalent to the msg argument used on its construction.

Let’s now summarize the main points discussed in this chapter.

# ## Summary

In this chapter, we have learnt about I/O streams and exception handling. In I/O streams, we have discussed the advantages of the Stream classes, the Stream class hierarchy, explicit file opening and closing, disk I/O using member functions, random access, and manipulators. In exception handling, we have discussed error handling in C and C++, the throw statement, catching an exception, re-throwing an exception, handling derived class exception and the standard library exception hierarchy.

# ## Quick Revise

# ### Multiple Choice Questions

+   1. If a catch statement is written to catch the exception objects of a base class type, then it can also catch all the __________ derived from that base class.
+      i. Exceptions for objects
+      ii. Objects of classes
+      iii. Arguments
+      iv. Errors