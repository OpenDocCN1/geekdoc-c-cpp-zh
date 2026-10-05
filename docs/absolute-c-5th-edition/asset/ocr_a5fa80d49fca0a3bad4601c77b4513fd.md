# CHAPTER 4 Parameters and Overloading

Display 4.5 Buying Pizza (part 3 of 3)

```
else
    cout << "The small one is the better buy.\n";
    cout << "Buon Appetito!\n";
}

double unitPrice(int diameter, double price)
{
    const double PI = 3.14159;
    double radius, area;

radius = diameter/static_cast<double>(2);
area = PI * radius * radius;
return (price/area);
```

Sample Dialogue

Welcome to the Pizza Consumers Union.
Enter diameter of a small pizza (in inches): 10
Enter the price of a small pizza: $7.50
Enterter diameter of a large pizza (in inches): 13
Enter the price of a large pizza: $14.75
Small pizza:
Diameter = 10 inches
Price = $7.50 Per square inch = $0.10
Large pizza:
Diameter = 13 inches
Price = $14.75 Per square inch = $0.11
The small one is the better buy.
Buon Appetito!