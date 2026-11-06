Use an `istringstream` to convert the numbers inside a string to integers or floating-point numbers.

Next, simply use the `>>` operator to read the month name, the day, the comma separator, and the year:

```
string month;
int day;
string comma;
int year;
strm >> month >> day >> comma >> year;
```

Now month is "January", day is 24, and year is 1973. Note that this input statement yields day and year as *integers*. Had we taken the string apart with `substr`, we would have obtained only strings, not numbers.

In fact, converting strings that contain digits to their integer values is such a common operation that it is useful to write a helper function for this purpose:

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

For example, `string_to_int("1973")` is the *integer* 1973.

By writing to a string stream, you can convert integers or floating-point numbers to strings. First construct an `ostringstream` object:

```
ostringstream strm;
```

Use an `ostringstream` to convert numeric values to strings.

Next, use the `<<` operator to add a number to the stream. The number is converted into a sequence of characters:

```
strm << fixed << setprecision(5) << 10.0 / 3;
```

Now the stream contains the string "3.33333". To obtain that string from the stream, call the `str` member function:

```
string output = strm.str();
```

You can build up more complex strings in the same way. Here we build a data string of the month, day, and year:

```
string month = "January";
int day = 24;
int year = 1973;
ostringstream strm;
strm << month << " " << day << ", " << year;
string output = strm.str();
```

Now output is the string "January 24, 1973". Note that we converted the *integers* day and year into a string. Again, converting an integer into a string is such a common operation that is useful to have a helper function for it:

```
string int_to_string(int n)
{
    ostringstream strm;
    strm << n;
    return strm.str();
}
```

For example, `int_to_string(1973)` is the string "1973".