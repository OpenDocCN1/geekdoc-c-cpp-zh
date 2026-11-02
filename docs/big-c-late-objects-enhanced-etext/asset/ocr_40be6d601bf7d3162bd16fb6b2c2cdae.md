# 8.4 Parsing and Formatting Strings

In the preceding sections, you saw how file streams read characters from a file and write characters to a file. The istream class reads characters from a string, and the ostringstream class writes characters to a string. That doesn't sound so exciting—we already know how to access and change the characters of a string. However, the string stream classes have the same public interface as the other stream classes. In particular, you can use the familiar >> and << operators to read and write numbers that are contained in strings. For that reason, the istringstream and ostringstream classes are called adapters—they adapt strings to the stream interface. Include the <sstream> header when you use string streams.

![](bbox=[0.78, 0.18, 0.95, 0.38])

© iStockphoto.
Like an adapter that converts your power plugs to international outlets, the string stream adapters allow you to access strings as streams.

Use an istringstream to convert the numbers inside a string to integers or floating-point numbers.

Here is a typical example. Suppose the string date contains a date such as "January 24, 1973", and we want to separate it into month, day, and year. First, construct an istringstream object. Then use the str function to set the stream to the string that you want to read:

```
istringstream strm;
strm.str("January 24, 1973");
```

Next, simply use the >> operator to read the month name, the day, the comma separator, and the year:

```
string month;
int day;
string comma;
int year;
strm >> month >> day >> comma >> year;
```

Now month is "January", day is 24, and year is 1973. Note that this input statement yields day and year as integers. Had we taken the string apart with substr, we would have obtained only strings, not numbers.

If you only need to convert a single string to its int or double value, you can instead use the functions stoi and stod:

```
string year = "1973";
int y = stoi(year); // Sets y to the integer 1973
```

These functions are available since C++ 11. If you have an older version of C++, use a helper function for this purpose:

```
int string_to_int(string s)
{
    istringstream strm;
    strm.str(s);
    int n = 0;
    strm >> n;
    return n;
}
```