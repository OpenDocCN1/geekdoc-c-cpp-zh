# DISPLAY 4.10 Buying Pizza (part 2 of 2)

```
47 }
48 
49 double unitPrice(int diameter, double price)
50 {
51     const double PI = 3.14159;
52     double radius, area;
53 
54     radius = diameter/static_cast<double>(2);
55     area = PI * radius * radius;
56     return (price/area);
57 }
58
```

# Sample Dialogue

```
Welcome to the Pizza Consumers Union.
Enter diameter of a small pizza (in inches): 10
Enter the price of a small pizza: $7.50
Enter diameter of a large pizza (in inches): 13
Enter the price of a large pizza: $14.75
Small pizza:
Diameter = 10 inches
Price = $7.50 Per square inch = $0.10
Large pizza:
Diameter = 13 inches
Price = $14.75 Per square inch = $0.11
The small one is the better buy.
Buon Appetito!
```

sense to buy a 2-inch pizza, but it can still be used as an easy test case for this program. It is an easy test case because it is easy to compute the answer by hand. Let’s calculate the cost per square inch of a 2-inch pizza that sells for $3.14. Since the diameter is 2 inches, the radius is 1 inch. The area of a pizza with radius 1 is 3.14159 * 1², which is 3.14159. If we divide this into the price of $3.14, we find that the price per square inch is 3.14/3.14159, which is approximately $1.00. Of course, this is an absurd size for a pizza and an absurd price for such a small pizza, but it is easy to determine the value that the function unitPrice should return for these arguments.

Having checked your program on this one case, you can have more confidence in it, but you still cannot be certain your program is correct. An incorrect program can sometimes give the correct answer, even though it will give incorrect answers on some other inputs. You may have tested an