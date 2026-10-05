# Classes 263

getMonthNumber and getDay are accessor functions. The accessor functions need literally return the values of each member variable, which they must return something equivalent to those values. For example, for a class like DayOfYear, you might have an accessor function return the name of the month as some sort of string value, rather than the number as a number.

Mutator functions allow you to change the data. In Display 6.4, the two functions named are set functions. It is traditional to use names that include the word get for accessor functions and names that include the word set for mutator functions. (The functions input and output in Display 6.4 are really mutator and accessor functions, respectively, but I/O is such a special case that they are usually just I/O functions rather than accessor or mutator functions.)

Your classes should always provide an adequate collection of accessor and mutator functions.

It may seem that accessor and mutator functions define the purpose of making variables private, but that is not. Notice the mutator function set in Display 6.4. It will not allow you to set the month member variable to 13 or any number that does not represent a month. Similarly, it will not allow you to set the day member variable to any number that is not in the range 1 to 31 (inclusive). The variables could set the data to values that do not make sense for a date. (As it is, you can still set the data to values that do not represent a real date, such as February 31, but it would be easy to exclude these dates. We did not exclude these dates to keep the example simple.) With mutator functions, you can control and filter changes to the data.

# Self-Test Exercises

+   12. Suppose your program contains the following class definition,

```
class Automobile {
public:
    void setPrice(double newPrice);
    void setProfit(double newProfit);
    double getPrice();
private:
    double price;
    double profit;
    double getProfit();
};
```

and suppose the main function of your program contains the following declaration and that the program somehow sets the values of all member variables to some values:

Automobile hyundai, jaguar; (continued)

![](bbox=[0.052, 0.576, 0.172, 0.592])