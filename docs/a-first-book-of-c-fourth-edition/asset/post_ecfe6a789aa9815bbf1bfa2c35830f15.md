
3. (Practice)  
   a. Construct a class implementation section for the constructor and `showData()` member methods corresponding to the class declaration created for Exercise 2a.  
   b. Construct a class implementation section for the constructor and `showData()` methods corresponding to the class declaration created for Exercise 2b.  
   c. Construct a class implementation section for the constructor and `showData()` methods corresponding to the class declaration created for Exercise 2c.  
   d. Construct a class implementation section for the constructor and `showData()` methods corresponding to the class declaration created for Exercise 2d.

4. (Program)  
   a. Include the class declaration and implementation sections prepared for Exercises 2a and 3a in a complete working program.  
   b. Include the class declaration and implementation sections prepared for Exercises 2b and 3b in a complete working program.  
   c. Include the class declaration and implementation sections prepared for Exercises 2c and 3c in a complete working program.  
   d. Include the class declaration and implementation sections prepared for Exercises 2d and 3d in a complete working program.

5. (Desk check) Determine the errors in the following class declaration section:

```
class Employee
{
public:
    int empnum;
    char code;
private:
    class(int = 0);
    void showemp(int, char);
};
```

6. (Modify)  
   a. Add another member method named `convert()` to Program 10.1 that does the following: The method should access the month, year, and day data members and display and then return an integer calculated as year × 10000 + month × 100 + day. For example, if the date is 4/1/2014, the returned value is 20140401. (Dates in this form are useful when performing sorts because placing the numbers in numerical order automatically places the corresponding dates in chronological order.)  
   b. Include the modified Date class constructed for Exercise 6a in a complete C++ program.

7. (Modify)  
   a. Add to Program 10.1's class definition an additional member method named `leapyr()` that returns a true if the year is a leap year and a false if it's not a leap year. A leap year is any year that's evenly divisible by 4 but not by 100, with the exception that all years evenly divisible by 400 are leap years. For example, the year 1996 is a leap year because it's evenly divisible by 4 and not evenly divisible by 100. The year 2000 is a leap year because it's evenly divisible by 400.  
   b. Include the class definition constructed for Exercise 7a in a complete C++ program. The `main()` function should display the message "The year is a leap year" or the message "The year is not a leap year" (depending on the Date object's year value).

## Chapter 10

## Creating Your Own Classes

8. (Modify)  
   a. Add a member method named `dayOfWeek()` to Program 10.1's class definition that determines the day of the week for any Date object. An algorithm for determining the day of the week, known as Zeller's algorithm, is the following:

   ```text
   If mm is less than 3
       mm = mm + 12 and yyyy = yyyy - 1
   Endif
   Set century = int(yyyy/100)
   Set year = yyyy % 100
   Set T = dd + int(26 * (mm + 1)/10) + year + int(year / 4)
           int(century / 4) - 2 * century
   Set DayOfWeek = T % 7
   If DayOfWeek is less than 0
       DayOfWeek = DayOfWeek + 7
   Endif
   ```

   Using this algorithm, the variable `DayOfWeek` has a value of 0 if the date is a Saturday, 1 if a Sunday, and so forth.

   b. Include the class definition constructed for Exercise 8a in a complete C++ program. The `main()` function should display the name of the day (Sun, Mon, Tue, and so on) for the Date object being tested.

9. (Program)  
   a. Construct a class named `Rectangle` that has double-precision data members named length and width. The class should have member methods named `perimeter()` and `area()` to calculate a rectangle's perimeter and area, a member method named `setData()` to set a rectangle's length and width, and a member method named `showData()` that displays a rectangle's length, width, perimeter, and area.

   b. Include the `Rectangle` class constructed in Exercise 9a in a working C++ program.

10. (Modify)  
    a. Modify the Date class defined in Program 10.1 to include a `nextDay()` method that increments a date by one day. Test your method to ensure that it increments days into a new month and into a new year correctly.

    b. Modify the Date class defined in Program 10.1 to include a `priorDay()` method that decrements a date by one day. Test your method to ensure that it decrements days into a prior month and into a prior year correctly.

11. (Modify) Modify the Date class in Program 10.1 to contain a method that compares two Date objects and returns the larger of the two. The method should be written according to the following algorithm:

    **Accept two Date values as parameters**

    **Determine the later date by using the following procedure:**
    - Convert each date into an integer value having the form `yyyymmdd`
      - (This can be accomplished with the formula `year * 10000 + month * 100 + day`)
    - Compare the corresponding integers for each date
    - The larger integer corresponds to the later date
    - Return the later date

## 10.3 Constructors

As you learned in Section 10.2, a constructor method is any method with the same name as its class. Multiple constructors can be defined for each class, as long as they can be distinguished by the number and types of their parameters.

A constructor's intended purpose is to initialize a new object's data members. Depending on the number and types of supplied arguments, one constructor method is called automatically each time an object is created. If no constructor method is written, the compiler supplies a default constructor. In addition to its initialization role, a constructor method can perform other tasks when it's called and be written in a variety of ways. This section explains possible variations of constructor methods and introduces another method, the destructor, which is called automatically whenever an object goes out of existence.

The following code example shows the general format of a constructor method:

```
className::className(parameter list)
{
    // method body
}
```

As this format shows, a constructor must have the following:

- The same name as the class to which it belongs
- No return type (not even void)

If you don't include a constructor in your class definition, the compiler supplies a do-nothing default one for you. For example, examine the following class declaration:

```
// class declaration section
class Date
{
    private:
        int month, day, year;
    public:
        void setDate(int, int, int);
        void showDate(void);
};
```

Because no user-defined constructor has been declared, the compiler creates a default constructor. For the Date class, this default constructor is equivalent to `Date::Date(void) { }`—that is, the compiler-supplied default constructor expects no parameters and has an empty body. Clearly, this default constructor isn't very useful, but it does exist if no other constructor is declared.

The term default constructor is used often in C++ and refers to any constructor that doesn't require arguments when it's called. The reason it doesn't require arguments is that no arguments are declared, as with the compiler-supplied default, or all arguments have been given default values. For example, `Date(int mm = 7, int dd = 4, int yyyy = 2012)` is a valid prototype for a default constructor. Each argument has been given a default value, and an object can be declared as type Date without supplying any further arguments. Using this default constructor, the declaration `Date a;` initializes the a object with the default values 7, 4, and 2012.

### Point of Information

### Constructors

A constructor is any method with the same name as its class. Its main purpose is to initialize an object's member variables when an object is created, so a constructor is called automatically when an object is declared.

A class can have multiple constructors if each constructor can be distinguished by having a different formal parameter list. A compiler error results when unique identification of a constructor isn't possible. If no constructor is provided, the compiler supplies a do-nothing default constructor.

Every constructor method must be declared with no return type (not even void). Because they're methods, constructors can also be called in nondeclaration statements. When used in this manner, the method call requires parentheses following the constructor name, even if no parameters are used. However, when used in a declaration, parentheses must not be included for a constructor. For example, the declaration `Date a();` is incorrect. The correct declaration is `Date a;`. When parameters are used, however, they must be enclosed in parentheses in both declaration and nondeclaration statements. Default parameter values should be included in the constructor's prototype.

To verify that a constructor method is called automatically when a new object is created, examine Program 10.2. Notice that in the implementation section, the constructor uses cout to display the message "Created a new date object with data values". Therefore, whenever the constructor is called, this message is displayed. Because the `main()` function creates three objects, the constructor is called three times, and the message is displayed three times.

The following output is produced when Program 10.2 runs:

```
Created a new date object with data values 7, 4, 2012
Created a new date object with data values 7, 4, 2012
Created a new date object with data values 4, 1, 2009
```

Although any legitimate C++ statement can be used in a constructor method, such as the cout statement in Program 10.2, it's best to keep constructors simple and use them only for initializing purposes. One further point needs to be made about the constructor in Program 10.2. According to C++ rules, object members are initialized in the order they're declared in the class declaration section, not in the order they might appear in the method's definition in the implementation section. Usually, this order isn't an issue, unless one data member is initialized by using another data member's value.
