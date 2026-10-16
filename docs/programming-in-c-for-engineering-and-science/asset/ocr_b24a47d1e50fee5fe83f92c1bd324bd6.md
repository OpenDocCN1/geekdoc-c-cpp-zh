```
cout << tempCelsius << " degrees Celsius is equivalent to "
    << tempFahrenheit << " degrees Fahrenheit\n";
cout <<"\nEnter a Celsius temperature (< -273.15 to stop): ";
cin >> tempCelsius;
}
}

double celsiusToFahrenheit(double tempCels) // function definition
{
    return 1.8 * tempCels + 32;
}
```

The program in Example 6.2 produces exactly the same output as that in Example 6.1, but the flow of execution is very different. Here the Celsius-to-Fahrenheit conversion is performed using a function that is defined following the main function. The following diagram illustrates the flow of control in this new program.

![](bbox=[0.15, 0.48, 0.85, 0.78])

Execution of the program starts at the beginning of main() and proceeds in the usual manner (1), until it reaches the call to function celsiusToFahrenheit() (2). At that time, the function's argument tempCelsius is evaluated (3) and copied into the parameter tempCels in the function celsiusToFahrenheit() (4). Control is transferred from the main function to the function celsiusToFahrenheit(), which begins executing (5). The expression

```
1.8 * tempCels + 32.0
```

> See the text's website (given in the Preface) about why we speak of function "calls" and "libraries."