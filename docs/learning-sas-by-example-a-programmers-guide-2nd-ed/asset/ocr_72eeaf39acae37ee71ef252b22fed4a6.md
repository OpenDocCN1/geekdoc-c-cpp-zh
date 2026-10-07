# 210 Learning SAS as Example: A Programmer's Guide, Second Edition

The variables Celsius1–Celsius24 are created by the ARRAY statement. Inside the DO loop, you convert each of the 24-Fahrenheit temperatures to Celsius. Data set Temp contains all 24 Fahrenheit and 24-Celsius temperatures. If you want to list a variable list in an ARRAY statement and include the number of elements following the array, SAS automatically creates variable names for you, using the array name as the base and adding the numbers from 1 to n, where n is the number of elements in the array. In this program, SAS creates the variables Fahrenheit1–Fahrenheit24. You could have used this feature for the Celsius array as well.

# 13.6 Changing the Array Bounds

By default, SAS numbers the elements of an array starting from 1. There are times when it is useful to specify the beginning and ending values of the array elements. For example, if you have variables Income2010 to Income2017, it would be nice to have the array elements start with 2010 and end with 2017.

The program that follows an array of the eight income values, using the values of 2010 and 2017 as the array bounds, and computes the taxes for each of the eight years:

# Program 13.6: Changing the Array Bounds

```
data Account;
  input ID Income2010-Income2017;
  array Income[2010:2017] Income2010-Income2017;
  array Taxes[2010:2017] Taxes2010-Taxes2017;
  do Year = 2010 to 2017
    Taxes{Year} = .25*Income{Year};
  end;
  format Income2010-Income2017 Taxes2010-Taxes2017 dollar10.

datalines;
  01 45000 47500 48000 48000 52000 53000 55000
  02 67130 68000 72000 65000 52000 49000 40100
;
```

In this program, you specify the lower and upper bounds in the brackets the array name and separate them with a colon.

# 13.7 Temporary Arrays

You can create an array that has only elements and no variables! As strange as this sounds, elements of temporary arrays are great places to store values or perform table lookups. If you want, you can assign the array elements initial values when you create the temporary array. Alternatively, you can load values into the temporary array in the DATA step. Either way, the values in the temporary array are automatically retained (that is, they are not set to missing values when the DATA step iterates). Thus, they are useful places to store values that you need during the execution of the DATA step.

We start out with an example that uses a temporary array to store the correct answer for each of 10 questions on a multiple-choice quiz. You can then score the quiz using the temporary array as the answer. Here is the program: