
```csharp
class Temperature
{
    static FahrenheitToCelsius(temperatureFahrenheit)
    {
        temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
        return temperatureCelsius;
    }
}
```

So to recap, this is the definition of the class. This is the body of the class, and notice the curly braces again. And inside the class, this is the definition of a method, that is C#'s own spin on the function. Now this code won't compile yet. It's still not valid C#. It's missing something important that we'll see in a moment. But eventually, once we are done making this valid C#, we'll be able to call this method by writing this, name of the class dot name of the method and then the argument in parentheses like 32. And this call, for example, would result in the temperature of 0 degrees Celsius. I have to give you a little heads up at this point. From this example, you see that we created this class Temperature just to contain the method FahrenheitToCelsius because the method cannot exist on its own without a class. But just be aware that this isn't the entire story about classes. As it turns out, classes are much more than just bundles of static methods. They are actually one of the central concepts in C#. They are the foundation of programming. But that is a topic for another day. We don't want to open that can of worms in this training, so we'll treat classes as just things that contain static methods. Just know that as you learn more C#, you'll also unlock the full power of classes. So coming back to our example, we took steps to convert this function to C#, but I told you that this isn't valid C# syntax yet. Let's try it actually. I have the Hello World example from before here.

Same code as before. I just changed the size of the fonts to make it more readable. And if I copy this method and paste it into Visual Studio right inside the class that we already have here, there. See these red squiggles?

```csharp
static FahrenheitToCelsius(temperatureFahrenheit)
{
    temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
    return temperatureCelsius;
}
```

They mean that this code is invalid for the C# compiler, and that's because this code is still missing one thing.

## Chapter 3 Juggling Types

This code doesn't work yet because it's missing one crucial piece of information, and that is the types of things. C# really cares about types, so let's fix the types in this code. First, we say that this static method takes an argument called temperatureFahrenheit, but we don't specify the type of this argument.

```csharp
static FahrenheitToCelsius(float temperatureFahrenheit)
{
    float temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
    return temperatureCelsius;
}
```

Is it a string, a number? If it's a number, is it integer or a floating point number? We need to decide. In this case, we are talking about temperatures that might have decimal digits, so we probably want a floating point number. C# has two floating point types, float and double. Float is the regular one, so to say, and double takes twice as many bytes and gives you extra precision. Both these types are based on types defined by .NET platform. All the types in C# rely on .NET types. So don’t be surprised if you see a similar set of types in other .NET languages, maybe with different names. So, coming back to this code, should this argument be a float or a double? In our case, we probably don’t need the extra precision, so a float should be enough. We can declare that this argument is a float, like this. And you see that the red squiggle under the argument went away. Likewise, this variable also has a type. It should also be a float, so let's specify that. One less error. And also, this entire method has a type.

```csharp
float temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
```

You see, if I hover with the cursor over the name of the method, Visual Studio tells me method must have a return type and currently doesn't. The type of a method is the same as the type of the value returned from the method. So in this case, it's float. We must declare it in front of the method name like this. And this fixes a few more errors. We need to declare the type of all methods in C# with the exclusion of methods that don't return anything. And in that case, we use the keyword void like this to mean this method doesn't have a type because it doesn't return a value. But in general, like in this case, we do have a type. There is one last error in this code, and, once again, it's a problem with types. This one is pretty subtle. Let's look at the types involved in this calculation. This value is a float, remember, and we subtract 32 from it. If we just write 32 like this, this number has no decimal part, so it's an integer value. In C#, the type for integers is called int. So we are subtracting an int from a float. And that's okay because C# just takes the int and converts it to a float, so it becomes 32.0. C# can do that automatically because we are not going to lose any information by upgrading an int to a float. It's a safe conversion.

```csharp
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    double temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
    return temperatureCelsius;
}
```

So we are subtracting a float from a float, and the result is another float. But now, we divide this float by this other number. And the problem we are having is that this number written like this is not a float. It's a double, which you'll remember is more precise than a float and contains more information. A float would be more than precise enough to represent this number, but that doesn't matter. C#'s syntax rules say that when I write a decimal number like here, then it's a double by default. This 1.8 is a literal for a double as it's called. So now we have a float divided by a double that results in a double, and we try to assign that double to a float. And that's when the error happens. We cannot assign a double to a float because we potentially lose information by doing that, so this conversion cannot happen automatically. Note that I said potentially. It doesn't matter which exact numbers are involved and whether or not we actually lose precision. C# won't let us shoehorn a more precise type into a less precise type period. So how do we fix this? There are a few ways. One is to upgrade this variable to a double like this. But if we do this, we just shift the problem to another place because now we cannot return this variable from this method because we said that the method is a float. So now we have to upgrade the entire method to a double, and that fixes the problem for good.

```csharp
static double FahrenheitToCelsius(float temperatureFahrenheit)
{
    double temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
    return temperatureCelsius;
}
```

Another way to fix this problem, let me roll the method and variable back to float. Another way would be to force this conversion and say okay, C#, I know what I'm doing. Do as I say. Just force the conversion of this expression from double to float. That's called a cast.

```csharp
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    float temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
    return temperatureCelsius;
}
```

In fact, if I hover over this error and ask C# to show me a list of fixes for the error, that's what it will propose. Add an explicit cast. And you learn how a cast works in the C# type system training. But for now, we won't do this. We won't use a cast because we have yet another way to fix this code that is quicker and easier than either adding a cast or upgrading the method to return a double. And that is, let's go to the root of the issue. That is the fact that this number is interpreted as a double. And let's say look, C#, this number is not a double. It's a float. And we can do it by simply adding this f after the number. Now this is the literal value for the float 1.8, not double 1.8. So now we divide float by float. That gives us a float. And we can assign it to a float variable. And finally, this code is 100% valid C#. There are no remaining errors.

```csharp
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    float temperatureCelsius = (temperatureFahrenheit - 32) / 1.8f;
    return temperatureCelsius;
}
```
