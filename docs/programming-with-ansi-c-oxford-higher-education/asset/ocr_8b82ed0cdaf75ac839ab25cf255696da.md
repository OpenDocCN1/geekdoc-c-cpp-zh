```
void main()
{
    Time Time1(12,15,15);
    /* Second constructor with MIL is used here */
    cout << "Time number 1 \n";
    Time1.ShowTime();
}
```

An MIL appears in between the header and the body, starting with a colon.

The initialization list has been used in the second constructor for the Time class to initialize the Time object. Earlier, the same was done using assignment statements in the constructor body. Let us compare the two methods syntactically. The earlier approach was as follows:

```
Time(int TempHours, int TempMinutes, int TempSeconds)
{
    Hours = TempHours;
    Minutes = TempMinutes;
    Seconds = TempSeconds;
}
```

The MIL approach is as follows:

```
Time(int TempHours, int TempMinutes, int TempSeconds)
:Hours(TempHours),
Minutes(TempMinutes),
Seconds(TempSeconds)
{ } // the empty body
```

Syntactically, the MIL appears in between the body of the constructor and the header. It starts with a colon (:) and has all the initializations separated by a comma. The initialization has the normal syntax of initialization, that is, Variable(value) for initializing a variable with a value. In the given example, both the approaches yield the same result.

# Need for Initialization List

However, it is not true that both these approaches always yield the same result. There are some cases where the use of the second approach is a must (or is better). The difference between assignment and initialization has already been elaborated in Section 5.11.1. The assignment statements in the function body invoke the assignment operator whereas the MIL invokes initialization. The following sub-sections discuss the advantages of using the MIL approach.

# Readability

When the MIL is used in a constructor function, it is separated from the rest of the code, and thus, the program becomes more readable. (There is an argument against this. Those who are new to C++ claim that the syntax of the MIL is a bit cryptic and one can easily misunderstand it for a function call.) MIL has not been used in the examples in this book, but its use is advisable while writing commercial programs.

# Efficiency

The MIL is more efficient in certain cases. Consider the following program.