
enough that you can have confidence in their performance. For example, the following is a possible stub for the function unitPrice:

```
//A stub. The final function definition must still be written.
double unitPrice(int diameter, double price)
{
    return (9.99);//Not correct but good enough for a stub.
}
```

## Display 4.9 Driver Program (part 1 of 2)

```
1
2 //Driver program for the function unitPrice.
3 #include <iostream>
4 using namespace std;
5
double unitPrice(int diameter, double price);
6 //Returns the price per square inch of a pizza.
7 //Precondition: The diameter parameter is the diameter of the pizza
8 //in inches. The price parameter is the price of the pizza.
9
10 int main( )
11 {
12     double diameter, price;
13     char ans;
14
15     do
16     {
17         cout << "Enter diameter and price:\n";
18         cin >> diameter >> price;
19         cout << "unit Price is $"
20             << unitPrice(diameter, price) << endl;
21
22         cout << "Test again? (y/n)";
23         cin >> ans;
24         cout << endl;
25     } while (ans == 'y' || ans == 'Y');
26
27     return 0;
28 }
29
double unitPrice(int diameter, double price)
30 {
31     const double PI = 3.14159;
32     double radius, area;
33
34     radius = diameter/static_cast<double>(2);
35     area = PI * radius * radius;
36     return (price/area);
37 }
```

## Display 4.9 Driver Program (part 2 of 2)

Sample Dialogue

```
Enter diameter and price:
13 14.75
Unit price is: $0.111126
Test again? (y/n): y

Enter diameter and price:
2 3.15
Unit price is: $1.00268
Test again? (y/n): n
```

Using a program outline with stubs allows you to test and then flesh out the basic program outline, rather than write a completely new program to test each function. For this reason, a program outline with stubs is usually the most efficient method of testing. A common approach is to use driver programs to test some basic functions, such as input and output, and then use a program with stubs to test the remaining functions. The stubs are replaced by functions one at a time: One stub is replaced by a complete function and tested; once that function is fully tested, another stub is replaced by a full function definition, and so forth, until the final program is produced.

## The Fundamental Rule for Testing Functions

> Every function should be tested in a program in which every other function in that program has already been fully tested and debugged.

## Self-Test Exercises

- 11. What is the fundamental rule for testing functions? Why is this a good way to test functions?
- 12. What is a driver program?
- 13. What is a stub?
- 14. Write a stub for the function whose declaration is given next. Do not write a whole program, only the stub that would go in a program. (Hint: It will be very short.)

```
double rainProb(double pressure, double humidity, double temp);
//Precondition: pressure is the barometric pressure in inches
//of mercury, humidity is the relative humidity as a
//percentage, and temp is the temperature in degrees
//Fahrenheit. Returns the probability of rain, which is a
//number between 0 and 1. 0 means no chance of rain, 1 means
//rain is 100% certain.
```

- 3. 10 20 30
- 1 2 3
- 1 20 3

- 4. Enter two integers: 5 10
- In reverse order the numbers are: 5 5

```
5. void zeroBoth(int& n1, int& n2)
{
    n1 = 0;
    n2 = 0;
}
```

```
6. void addTax(double taxRate, double& cost)
{
    cost = cost + (taxRate/100.0)*cost;
}
```

The division by 100 is to convert a percentage to a fraction. For example, 10% is 10/100.0, or one-tenth of the cost.

- 7. par1Value in function call = 111
- par2Ref in function call = 222
- n1 after function call = 1
- n2 after function call = 2

8. The one with one parameter would be used because the function call has only one parameter.

9. The first one would be used because it is an exact match, namely, two parameters of type double.

10. This cannot be done (at least not in any nice way). The natural ways to represent a square and a round pizza are the same. Each is naturally represented as one number, which is the radius for a round pizza and the length of a side for a square pizza. In either case the function unitPrice would need to have one formal parameter of type double for the price and one formal parameter of type int for the size (either radius or side). Thus, the two function declarations would have the same number and types of formal parameters. (Specifically, they would both have one formal parameter of type double and one formal parameter of type int.) Thus, the compiler would not be able to decide which definition to use. You can still defeat this evil pizza parlor's strategy by defining two functions, but they will need to have different names.

11. The fundamental rule for testing functions is that every function should be tested in a program in which every other function in that program has already been fully tested and debugged. This is a good way to test a function because if you follow this rule, then when you find a bug, you will know which function contains the bug.

12. A driver program is a program written for the sole purpose of testing a function.

13. A stub is a simplified version of a function that is used in place of the function so that other functions can be tested.

```
14. //THIS IS JUST A STUB.
double rainProb(double pressure,
    double humidity, double temp)
{
    return 0.25; //Not correct,
                //but good enough for some testing.
}
```

## Programming Projects

- 1. Write a program that converts from 24-hour notation to 12-hour notation. For example, it should convert 14:25 to 2:25 P.M. The input is given as two integers. There should be at least three functions: one for input, one to do the conversion, and one for output. Record the A.M./P.M. information as a value of type char, 'A' for A.M. and 'P' for P.M. Thus, the function for doing the conversions will have a call-by-reference formal parameter of type char to record whether it is A.M. or P.M. (The function will have other parameters as well.) Include a loop that lets the user repeat this computation for new input values again and again until the user says he or she wants to end the program.

- 2. The area of a circle can be calculated using the formula

A = πr²

where r is the radius of the circle, and π is the ratio of the circle's circumference to its diameter. The circumference can be calculated using the formula

C = πd

where d is the diameter of the circle, whose value is twice that of the radius. Write a void function that takes the radius of the circle, and two reference parameters to compute the area and the circumference. Use a value of 3.14159 for π.

- 3. You have a voucher for a bakery, which you redeem to buy baked goods of your choice. The value of the voucher is fixed and the total bill of the items selected should not exceed the voucher value. If the voucher has any value left after the purchase, then it cannot be utilized again. Write a program that displays 4 items and their prices as a menu and then reads the value of the voucher.
Write a function, with parameters itemCode and voucherValue passed by reference, that deducts the price of an item from the voucher value only if the item's value is less than or equal to the voucher value. Use a loop to invoke the above function as many times as required until the value of the voucher is less than or equal to the cheapest item on the menu.
Finally, display the calculated sum of the prices of the items selected, and the unutilized balance on the voucher after purchase.

4. Write a program that will read in a length in feet and inches and output the equivalent length in meters and centimeters. Use at least three functions: one for input, one or more for calculating, and one for output. Include a loop that lets the user repeat this computation for new input values until the user says he or she wants to end the program. There are 0.3048 meters in a foot, 100 centimeters in a meter, and 12 inches in a foot.

5. Write a program like that of the previous exercise that converts from meters and centimeters into feet and inches. Use functions for the subtasks.

6. (You should do the previous two programming projects before doing this one.) Write a program that combines the functions in the previous two programming projects. The program asks the user if he or she wants to convert from feet and inches to meters and centimeters or from meters and centimeters to feet and inches. The program then performs the desired conversion. Have the user respond by typing the integer 1 for one type of conversion and 2 for the other. The program reads the user's answer and then executes an if-else statement. Each branch of the if-else statement will be a function call. The two functions called in the if-else statement will have function definitions that are very similar to the programs for the previous two programming projects. Thus, they will be fairly complicated function definitions that call other functions. Include a loop that lets the user repeat this computation for new input values until the user says he or she wants to end the program.

7. Write a program that will read a weight in pounds and ounces and will output the equivalent weight in kilograms and grams. Use at least three functions: one for input, one or more for calculating, and one for output. Include a loop that lets the user repeat this computation for new input values until the user says he or she wants to end the program. There are 2.2046 pounds in a kilogram, 1000 grams in a kilogram, and 16 ounces in a pound.

8. Write a program like that of the previous exercise that converts from kilograms and grams into pounds and ounces. Use functions for the subtasks.

9. (You should do the previous two programming projects before doing this one.) Write a program that combines the functions of the previous two programming projects. The program asks the user if he or she wants to convert from pounds and ounces to kilograms and grams or from kilograms and grams to pounds and ounces. The program then performs the desired conversion. Have the user respond by typing the integer 1 for one type of conversion and 2 for the other. The
