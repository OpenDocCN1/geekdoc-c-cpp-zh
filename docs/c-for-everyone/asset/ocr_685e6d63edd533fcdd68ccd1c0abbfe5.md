Table 2 summarizes the stream manipulators. Note that all manipulators set the state of the stream object for all subsequent operations, with the exception of `setw`. After each output operation, the field width is reset to 0. To use any of these manipulators, include the `<iomanip>` header.

# **SELF CHECK**

![](bbox=[0.124, 0.19, 0.28, 0.262])

+   11. What is the output of the following statement?
+   
+       ```cpp
+       cout << fixed << 123456.0;
+       ```

+   12. How do you change the statement so that the result is 123456.00?

+   13. What is the output of the following statement?
+   
+       ```cpp
+       cout << setw(8) << setfill('0') << 123456;
+       ```

+   14. What is the output of the following statement?
+   
+       ```cpp
+       cout << setw(2) << setfill('0') << 123456;
+       ```

+   15. Why doesn't the following statement sequence line up the numbers?
+   
+       ```cpp
+       cout << setw(10) << setprecision(2) << fixed << 1.234 << endl << 56.7;
+       ```

**Practice It** Now you can try these exercises at the end of the chapter: R8.7, R8.8, P8.18.

# ## 8.4 String Streams

In the preceding sections, you saw how file streams read characters from a file and write characters to a file. The `istringstream` class reads characters from a string, and the `ostringstream` class writes characters to a string. That doesn't sound so exciting—we already know how to access and change the characters of a string. However, the string stream classes have the same **interface** as the other stream classes. In particular, you can use the familiar `>>` and `<<` operators to read and write numbers that are contained in strings. For that reason, the `istringstream` and `ostringstream` classes are called **adapters**—they adapt strings to the stream interface. Include the `<sstream>` header when you use string streams.

Here is a typical example. Suppose the string `date` contains a date such as "January 24, 1973", and we want to separate it into month, day, and year. First, construct an `istringstream` object. Then use the `str` function to set the stream to the string that you want to read:

```
```cpp
istringstream strm;
strm.str("January 24, 1973");
```
```

![](bbox=[0.629, 0.798, 0.825, 0.906])

*Like an adapter that converts your power plugs to international outlets, the string stream adapters allow you to access strings as streams.*