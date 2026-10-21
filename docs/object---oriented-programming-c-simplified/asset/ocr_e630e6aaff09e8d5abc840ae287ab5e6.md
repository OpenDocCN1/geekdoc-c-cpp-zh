object has a **streambuf**-derived object attached, and the two classes work together; the istream class does the formatting, and the **streambuf** class does the low-level buffered input. The class provides number of methods for input handling such as **get, getline, read, peek, gcount, ignore, eatwhite, putback etc.** This class also contains overloaded **extraction operator >>** for handling all data types such as **int, signed int, char, long, double, float, long double**. The extraction operator is also overloaded for handling **streambuf and istream** types of objects.

# 3. istream_withassign Class

The **istream_withassign** class is a variant **istream** that allows object assignment. The predefined object cin is an object of this class and thus may be reassigned at run time to a different **istream** class.

# 4. ostream_withassign Class

The **ostream_withassign** class is variant of **ostream** that allows object assignment. The predefined object **cout, cerr and clog** are objects of this class and thus may be reassigned at run time to a different **ostream object.**

# 11.3 UNFORMATTED INPUT/OUTPUT

Until now is all the program with the help of cin and cout we have taking input without making use of any formatting function. Thus, general syntax of using data as input and output is as follows :

```
cin >> data1 >> data2 >> data3 >> ........................... >> data n;
cout << data1 << data2 << data3 << ........................... << data n;
```

Where **data1, data2....** Are variables of **int, char, float** etc.

Here data is scanned as it is input and similarly it is displayed as it. This is because the operator **>> and <<** overloaded for all the basic types like **int, char, unsigned, float** etc.

In case of string data the input breaks at occurrence of very first white space character like tab or space. Similarly for reading **int, float** etc., input must match the type of variable in which you are accepting it.

Before discussing how to format data for input and output we first see few functions for input and output character, scanning and printing strings.

# 1. The get Function

This function is used to scan a single character from the keyboard. There are two different syntaxes of using get function.

+   (a) void cin.get(char);
+   (b) char cin.get();

In the first syntax get function takes an argument of type char. This is used as :

```
char x;
cin.get(x);
```