One of the ways you can help keep your code neat, organized, and modular (reusable) is to use functions in your code. Additionally, they help make your code smaller by making certain sections reusable. Functions are like tools that were created to serve a particular function, as the name suggests.

While we have already encountered a few user-defined functions, we will cover them in greater detail now and explain some of the features we may have glossed over when we encountered them last time. Let's look at the declaration of a function now:

```
float employeeEarnings (float hoursWorked, float payRate) {
```

```
float result;// this will be the value we return when this function is called. It should match the datatype before our function name.
```

```
result = hoursWorked * payRate
```

```
return result//  return tells the function to send a value back once to where it was called
```

```
}
```

This function clearly takes two arguments, hoursWorked, and payRate, both of which are ‘floats.’ It does some simple math on them and then returns a float as a value. Return means to terminate the function and send back whatever value is placed after the word return, usually a variable, as the result of some calculations.

Let's see us call this function now to get an employee's earnings:

```
void loop () {
```

```
floathoursWorked = 37.5;
```

```
float payRate= 18.50;
```

```
float result = employeeEarnings (hoursWorked, payRate)
```

```
// result will be 693.75
```

First, the function must be declared outside of any other functions. This means