# Formatting Numeric Output

be integers; therefore; you will store values in int variables. You will store the fat percentage in a double variable, because its value will be a real number. Figure 5-31 shows the input, processing, and output items from the IPO chart, with the corresponding C++ instructions. Pay particular attention to the shaded statement, which calculates the percentage. The statement uses static_cast operator to convert the integers stored in the fatCals and totalCals variables to double before performing the division operation. As you learned in Chapter 4, the static_cast operator ensures that the quotient when dividing one int by another is a real number rather an integer. Although the statement converts the contents of int variables to double, recall that only one of the integers involved in a division operation needs to be converted. As a result, you can also write the division part of the statement as static_cast<double>(fatCals) / totalCals / static_cast<double>(totalCals).

# IPO chart information

# C++ instructions

total calories

grams of fat

```
int totalCals = 0;
int fatGrams = 0;
```

# Processing

none

# Output

fat calories

fat percentage (0 decimal places)

```
int fatCals = 0;
double fatPercent = 0.0;
```

# Algorithm

+   1. enter the total calories and grams of fat

```
cout << "Total calories: \
```

+   2. if (both the total calories and grams of fat are greater than equal to zero)

calculate calories by multiplying grams of fat by

```
fatCals = fatGrams * 9;
```

calculate fat percentage by dividing fat calories and then multiplying the result by 100

```
fatPercent =
static_cast<double>(fatCals) /
static_cast<double>(totalCals)
* 100;
```

display fat calories and fat percentage

```
cout << "Fat calories: ""
fatCals << endl;
cout << fixed << setprecision(0);
cout << "Fat percentage: ""
fatPercent << "%%"\ << endl;
```

```
}
else
```

display an error message

```
cout << "Input error" << endl;
//end if
```

Figure 5-31 IPO chart information and C++ instructions for the health club problem

![](bbox=[0.935, 0.187, 0.977, 0.207])