```
}
void Display()
{
    Console.WriteLine(a + b);
}
}
class Program
{
    static void Main(string[] args)
    {
        Class2 cl = new Class2();
        Console.Write("The output is : ");
        cl.Display();
    }
}
}
```

# Programming Exercises

12.1 Create a class named Number to hold one integer value. Include a constructor to display the message "object is created" and a destructor to display the message "object is destroyed". Write a program to demonstrate the creation and destruction of Number objects.

12.2 Rewrite the program in Exercise 12.1 by adding a Set method to provide a value to the data member and a Get method to display the value stored in the object. Demonstrate your program by storing an integer value, say 2002, and display the same.

12.3 Rewrite the program in Exercise 12.2 by replacing the Set method by a constructor.

12.4 Rewrite the program in Exercise 12.2 by replacing the Set and Get methods by a property.

12.5 Create a class named Integer to hold two integer values. Design a method Swap that could take two integer objects as parameters and swap their contents. Write a Main program to implement the class Integer and the method Swap.

+   12.6 Design a class named Date with the following members:
+   - Data members day, month and year
+   - A constructor to provide values to the data members (using three parameters)
+   - A method to display the date in the format day/month/year (Example: 15/8/1945 for August 15, 1945)
+   Write a program to implement the class Date.

12.7 Add to the class designed in Exercise 12.6 another constructor which takes only one parameter that represents the date in the form of a long integer, like 19450815 for the date 15/8/1945 and assigns suitable values for the year, month and day members. Also modify the Main program to demonstrate the use of both the constructors. Use a suitable algorithm to convert the long integer 19450815 into year, month and day.

+   12.8 Define a Time class containing the following members:
+   - Two integer data members minutes and hours
+   - Two overloaded constructors
+   - One method to display the class data members
+   One of the constructors take two integer parameters to assign values to two data members and the other constructor takes one integer parameter representing total number of minutes and converts it into hours and minutes
+   Write a complete program to verify the operation of the constructors and the method.