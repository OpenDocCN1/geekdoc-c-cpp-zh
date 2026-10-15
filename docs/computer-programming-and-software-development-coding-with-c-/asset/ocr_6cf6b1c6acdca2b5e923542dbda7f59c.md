# Chapter 4 Static Typing & Built-in Types

We just learned that C# is fussy about types. It wants to know the type of everything upfront, variables, the arguments of methods, the return values. Not all languages work like that. For example, if you take this method and convert it to JavaScript, it's quite similar.

```
C#
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    float temperatureCelsius = (temperatureFahrenheit - 32) / 1.8f;
    return temperatureCelsius;
}
```

```
JavaScript
function FahrenheitToCelsius(temperatureFahrenheit)
{
    temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
    return temperatureCelsius;
}
```

It's almost spot differences. But if you do mark the differences, you see that they are mostly about types. Languages like JavaScript where you don't declare types are called dynamically typed. And the languages like C# where you do have to declare types are called statically typed. You can also just call them static and dynamic for short. Which one is better, static typing or dynamic typing? That's a debate in programming, and I'll carefully avoid that debate here because I think it depends on what you want to do. Dynamic static languages are both useful in their own ways. However, we've already