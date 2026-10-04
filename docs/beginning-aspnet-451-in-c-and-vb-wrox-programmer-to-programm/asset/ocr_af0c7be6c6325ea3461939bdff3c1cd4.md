```
Case "/*"
result = myCalculator.Divide(value1, value2)
End Select
```

+   6. Save all your changes and open the page in the browser. The calculator still works as before; only this time the calculations are not carried out in the code's Code Behind, but by the Calculator class in the App_Code folder instead.

# How It Works

The file you created in the App_Code folder contains a class called Calculator. You learn more about the classes in the final section of this chapter, but now it's important to know that a class is a definition for an object that can expose methods you can call at runtime. In this case, the definition for the Calculator class contains four methods to perform arithmetic operations. These methods accept parameters for the left-hand and right-hand sides of the calculations. Each method simply carries out the requested calculation (Add, Subtract, and so on) and returns the result to the calling code.

The code in the CalculatorDemo.aspx page creates an instance of the Calculator class. That is, it creates an object in the computer's memory based on the class definition. To do this, it uses the New (in C#) keyword to create an instance of Calculator, which is then stored in the variable myCalculator. You learn more about the New keyword later in this chapter when objects are discussed. Note the data type of this variable is Calculator, the name of the class.

```
VB.NET
Dim myCalculator As New Calculator()
```

```
C#
Calculator myCalculator = new Calculator();
```

Once the Calculator instance is created, you can call its methods. Just as you saw earlier with other methods, the methods of the Calculator accept class parameters that are passed in by the calling code:

```
VB.NET
```

```
Case "*"
```