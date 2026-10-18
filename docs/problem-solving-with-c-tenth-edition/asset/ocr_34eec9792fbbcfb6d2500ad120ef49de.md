Member functions that allow you to change the values of the private member variables of a class are called mutator functions. Although this is not required by the C++ language, the names of mutator functions normally include the word set.

It is important to always include accessor and mutator functions with each class definition so that you can change the data stored in an object.

# SELF-TEST EXERCISES

14. The private member function DayOfYear::checkDate in Display 10.4 allows some illegal dates to get through, such as February 30. Redefine the member function DayOfYear::checkDate so that it ends the program whenever it finds any illegal date. Allow February to contain 29 days, so you account for leap years. (Hint: This is a bit tedious and the function definition is a bit long, but it is not very difficult.)

15. Suppose your program contains the following class definition:

```
class Automobile
{
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

and suppose the main part of your program contains the following declaration and that the program somehow sets the values of all the member variables to some values:

```
Automobile hyundai, jaguar;
```

Which of the following statements are then allowed in the main part of your program?

```
hyundai.price = 4999.99;
jaguar.setPrice(30000.97);
double aPrice, aProfit;
aPrice = jaguar.getPrice();
aProfit = jaguar.getProfit();
aProfit = hyundai.getProfit();
```