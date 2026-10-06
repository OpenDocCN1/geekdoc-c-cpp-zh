The first message statement sends the setNumerator: message to myFraction. The argument that is supplied is the value 1. Control is then sent to the setNumerator: method defined for your Fraction class. The Objective-C system knows that it is the method from this class to use because it knows that myFraction is an object from the Fraction class.

Inside the setNumerator: method, the passed value of 1 is stored inside the variable n. The single program line in that stores that value in the instance variable numerator. So you have effectively set the numerator of myFraction to 1.

The message that invokes the setDenominator: method on myFraction follows next. The argument of 3 is assigned to the variable d inside the setDenominator: method. This value is then stored inside the denominator instance variable, completing the assignment of the value 1/3 to myFraction. Now you're ready to display the value of your fraction, which you do with the following lines of code from Program 3.2:

```
// Display the fraction using the print method

NSLog("@ value of myFraction is:");
[myFraction print];
```

The NSLog call simply displays the following text:

The value of myFraction is:

The following message expression invokes the print method:

```
[myFraction print];
```

Inside the print method, the values of the instance variables numerator and denominator are displayed, separated by a slash