```
double CelsiusToFahr(double Celsius) //Function header.
{
//Declare local variables.
double temp;
//Convert from degrees Celsius to degrees Fahrenheit.
temp = (9.0/5.0)*celsius + 32.0;
return temp;
}
```

Notice that the function CelsiusToFahr() includes no input statements and no output statements, only the statements required to perform the temperature conversion and to return the new value. The input and output is performed in main(). We will now provide a partial program trace for program chapter6_1, beginning with the fin >> cels; statement.

# Program Trace

![](bbox=[0.22, 0.38, 0.93, 0.56])

# Function Definition

+   - function header
+   - parameter list
+   - function body

As we look more closely at the functions we have defined thus far in the text, we see that a function definition consists of a **function header** followed by a statement block. A function header defines the type of value that is returned by the function: int form () and double for CelsiusToFahr() in the example given in the previous section. If a function does not return a value, the return type is void. The function name and a **parameter list** follow the return type. Note that the parameter list may be empty as in our definition of main(). The general form of a function definition is

```
return_type function_name(parameter list)
{
declarations;
statements;
}
```

The parameter list represents the information passed to the function; if there are no input parameters the parameter list can be omitted. However, the function name must always be followed by a set of parentheses, as we do when defining int main(). Additional objects used by a function are defined in the statement block that defines the **function body**.

![](bbox=[0.13, 0.85, 0.2, 0.91])

A function name should be selected to help document the purpose of the function. Comments should also be included within the function to further describe the purpose of