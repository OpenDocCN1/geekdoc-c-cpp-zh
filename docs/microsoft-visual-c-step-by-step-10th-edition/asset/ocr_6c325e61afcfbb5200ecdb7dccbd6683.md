```
class Example
{
    public static void MyOtherMethod(int parameter) { ... }
    public static void Main()
    {
        Hour lunch = new Hour(12);
        Example.MyOtherMethod(lunch); // implicit Hour to int conversion
    }
```

If the conversion operator had been declared with explicit, the preceding example would not have compiled because an explicit conversion operator requires a cast.

Click here to view code image

Example.MyOtherMethod(int lunch); // explicit Hour to int conversion

When should you declare a conversion operator as explicit or implicit? If a conversion is always safe, does not run the risk of losing information, and cannot throw an exception, it can be defined as an implicit conversion. Otherwise, it should be declared as an explicit conversion. Converting from an Hour to an int safe—every Hour has a corresponding int value—so it makes sense for it to be implicit. An operator that converts a string to an Hour should be explicit because not all strings represent valid Hours. (The string "7" is fine, but how would you convert the string Hello, World to an Hour?)

# Creating symmetric operators, revisited

Conversion operators provide an alternative way to resolve the problem of providing symmetric operators. For example, instead of providing three versions of operator + (Hour + Hour, Hour + int, and int + Hour) for the Hour structure, as shown earlier, you can provide a single version of operator + (that takes two Hour parameters) and an implicit int to Hour conversion, like this:

Click here to view code image