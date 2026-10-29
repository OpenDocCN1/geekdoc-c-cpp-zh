```
if (a == b)
    cout << "Dates a and b are the same." << endl;
else
    cout << "Dates a and b are not the same." << endl;
if (a == c)
    cout << "Dates a and c are the same." << endl;
else
    cout << "Dates a and c are not the same." << endl;
return 0;
}
```

The following output is produced by Program 11.1:

```
Dates a and b are not the same.
Dates a and c are the same.
```

The first new feature shown in Program 11.1 is the declaration and implementation of the operator== function. Except for its name, this operator function is constructed in the same manner as any other class method: It's declared in the class declaration section and defined in the class implementation section.

The second new feature is how the function is called. Operator functions can be called by using their associated symbols. Because operator functions are true functions, however, the traditional method of calling them can also be used—specifying the function name and including appropriate arguments. Therefore, instead of being called by the expression a == b in Program 11.1, the call a.operator==(b) could have been used.

Now see how to create another operator for the Date class—an addition operator. As before, creating this operator requires specifying three items:

+   - The name of the operator function
+   - The processing the function is to perform
+   - The data type, if any, the function is to return

Clearly, for addition you would use the addition symbol with the operator function name: operator+. Having selected the function's name, you must then determine what you want this function to do with Date objects. As noted, adding two dates makes no sense. Adding an integer to a date is meaningful, however, when the integer represents the number of days before or after a given date. The sum of an integer and a Date object is simply another Date object, which should be returned by the addition operation. Therefore, the following prototype is suitable for the addition function:

```
Date operator+(int);
```

This prototype, included in the class declaration section, specifies adding an integer to a class object and returning a Date object. Therefore, if a is a Date object, the function call a.operator+(284), or its more common alternative, a + 284, should cause the number 284 to be added to a's date value correctly.

Next, you must construct the function to accomplish this task, which requires selecting a calendar convention first. For simplicity, adopt the financial date convention of each month