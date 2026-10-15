Another way to fix this problem, let me roll the method and variable back to float. Another way would be to force this conversion and say okay, C#, I know what I'm doing. Do as I say. Just force the conversion of this expression from double to float. That's called a cast.

```
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    float temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
    return temperatureCelsius;
}
```

In fact, if I hover over this error and ask C# to show me a list of fixes for the error, that's what it will propose. Add an explicit cast. And you learn how it cast works in the C# type system training. But for now, we won't do this. We want to use a cast because we have yet another way to fix this code that is quicker and easier than either adding a cast or upgrading the method to return a double. And that is let's go to the root of the issue. That is the fact that this number is interpreted as a double. And let's say look, C#, this number is not a double. It's a float. And we can do it by simply adding this f after the number. Now this is the literal value for the float 1.8, not double 1.8. So now we divide float by float. That gives us a float. And we can assign it to a float variable. And finally, this code is 100% valid C#. There are no remaining errors.

```
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    float temperatureCelsius = (temperatureFahrenheit - 32) / 1.8f;
    return temperatureCelsius;
}
```