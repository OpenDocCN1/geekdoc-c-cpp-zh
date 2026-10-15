
# Chapter 10 How to Find the Correct Method

We have already taken a first look at how we can pass data to our methods using parameters, but there are quite a few extra options to do this, so let's look at that next. Have seen that a method requires a name, a return type, and 0 or more parameters. When we ask C# to invoke a certain method, it'll start searching for the corresponding one. To search for the correct method, it doesn't just use the name. No, indeed a few things are considered to locate the correct method. The method name is, the first one. Then it'll also see if the call to the method is passing the same argument types as the method requires. The method may say it needs a string parameter, but if we try to invoke it passing an integer argument, C# won't match it. It is a good thing. It's a type safety of C# that will make sure at compile time that not only the name matches, but also the parameter types. Also, the number of parameters is taken into consideration when searching for the correct methods. In conclusion, we can say that three things are used to find the correct method, the method name, the parameter types, and the number of parameters. Only when this combination is found, C# will invoke the method. It also brings another thing here. It's this combination that needs to be unique, not just the name. Indeed, we can have multiple methods with the same name. As long as the combination stays unique within the class, we're good. The fact that multiple methods with the same name can exist within a class is called method overloading.

```
static void Main(string[] args)
{
    DisplaySum(3, 52);
}
```

The name can be the same, but either we need to define a different number of parameters or different parameter types or a combination of these two. I have two methods with the same name. Both are called DisplaySum. The first variation has to integer parameters.

```
public static void DisplaySum
(int a, int b)
{ ... }

public static void DisplaySum
(int a, int b, int c)
{ ... }
```

The second one has three. C# will accept this. These are now overloaded methods. And then now we invoke from the main DisplaySum, as you can see here, with just two parameters. The highlighted version is selected. C# will match this method, and this one only here, because of the number of parameters matching. Let us head back to Visual Studio and take a look at method overloading in action. When we asked C# to invoke the CalculateYearlyWage method, it actually searched for a method that

had that particular name, and it also had the same amount of parameters, and also the type of parameters needs to match. It is possible to actually create overloaded methods, methods with the same name, but then they need to contain either a different number of parameters or a different type of parameters. And that still gives C# the ability to distinguish which method you want to use. So let me show you method overloading for this.

```
static void Main(string[] args)
{
    int monthlyWage = 1234;
    int months = 12;

    int yearlyWage = CalculateYearlyWage(monthlyWage, months);

    Console.WriteLine($"Yearly wage (from main): {yearlyWage}");

    Console.ReadLine();
}

public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked)
{
    //Console.WriteLine($"Yearly wage: {monthlyWage * numberOfMonthsWorked}");
    if (numberOfMonthsWorked == 12)//Let's add a bonus month
        return monthlyWage * (numberOfMonthsWorked + 1);

    return monthlyWage * numberOfMonthsWorked;
}

public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked, int bonus)
{
    Console.WriteLine($"The yearly wage is: {monthlyWage * numberOfMonthsWorked + bonus}");
    return monthlyWage * numberOfMonthsWorked + bonus;
}
```

I'm going to bring in a second method with the same name. As you can see here, that's also CalculateYearlyWage. I also accept monthlyWage, and numberOfMonthsWorked, but now this one accepts a third parameter, bonus. The types of the parameters are the same, so we cannot just do this and have Visual Studio say, well, I already have a method with these parameters, so you cannot do that.

![](img/0155736aec718cf18821e9f10a5d308d_708_0.png)

I cannot distinguish between these two. But that's not what I was planning on doing; I actually added the third parameter, and that's okay for C#. So now just including a third parameter of type integer, in this case, bonus, and I used that inside of my method. So these two methods are not overloaded methods. They have the same name but a different number of parameters. But I can also do the same thing, but the difference now is that the parameter types are different, so they're now doubles.

![](img/0155736aec718cf18821e9f10a5d308d_708_1.png)

So at this point, C# can still distinguish between these three methods based on the parameters, the number of parameters, or the types of parameters that I'm passing it. So I'm going to go here, and I'm going to bring in a bonus. Let's set that to 1000. I'm going to change the method invocation as we already had, and I'm going to add bonus. You see automatically that Visual Studio is showing me these overloads.

```
0 references
public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked)
{
    //Console.WriteLine($"Yearly wage: {monthlyWage * numberOfMonthsWorked}");
    if (numberOfMonthsWorked == 12)//let's add a bonus month
        return monthlyWage * (numberOfMonthsWorked + 1);

    return monthlyWage * numberOfMonthsWorked;
}

1 reference
public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked, int bonus)
{
    Console.WriteLine($"The yearly wage is: {monthlyWage * numberOfMonthsWorked + bonus}");
    return monthlyWage * numberOfMonthsWorked + bonus;
}

0 references
public static double CalculateYearlyWage(double monthlyWage, double numberOfMonthsWorked, double bonus)
{
```

These are different overloads of the same method but with different parameter combinations, as you can see here. So what is now going to happen? Well, I'm going to show you which is actually invoked, so I'll put a couple of breakpoints, and then we'll run the application and we'll see which one gets hit.

```
//int yearlyWage = CalculateYearlyWage(monthlyWage, months, bonus);

//Console.WriteLine($"Yearly wage (from main): {yearlyWage}");

double monthlyWageDouble = 1500.0;
double monthsDouble = 12;
double bonusDouble = 1000;
double yearlyWageWithBonusDouble = CalculateYearlyWage(monthlyWageDouble, monthsDouble, bonusDouble);

Console.ReadLine();
}

0 references
public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked)
{
    //Console.WriteLine($"Yearly wage: {monthlyWage * numberOfMonthsWorked}");
    if (numberOfMonthsWorked == 12)//let's add a bonus month
        return monthlyWage * (numberOfMonthsWorked + 1);

    return monthlyWage * numberOfMonthsWorked;
}

0 references
public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked, int bonus)
{
    Console.WriteLine($"The yearly wage is: {monthlyWage * numberOfMonthsWorked + bonus}");
    return monthlyWage * numberOfMonthsWorked + bonus;
}

1 reference
public static double CalculateYearlyWage(double monthlyWage, double numberOfMonthsWorked, double bonus)
```

And you see that indeed the one with integer parameter types is being selected, is being used, and that's because I passed integer values over here. Now let me bring in a little bit of extra code here. I've now brought in double variants of our original parameters, and I'm now going to also calculate the yearly wage but now passing in these double families. Can you guess which one will be called? I think you do. Let's take a look. Indeed, based on the parameter types and also the number of parameters, C# has decided that this method needs to be invoked.

## Chapter 11 How to Pass Parameters by Value & Reference

In C#, it's possible to pass parameters to a method in two ways. So far, we've actually used the default, and that was by value. The second option is passing the parameters by reference, which will require us to use a new keyword, the ref keyword, on the parameters we want to pass this way. Let's explore these two options in more detail. As said, the default way of passing parameters is by value, and that's what we've used so far without giving it any attention, really. With this approach, when calling a method and passing it arguments, so values for the parameters, a copy is created for the method to work with. The method can do whatever it wants on these values. It's a working copy of the values, and thus the values in the caller aren't changed. They are not being touched. Say we have our AddTwoNumbers method again, and I have defined a to be 33 and b to be 44.

```
int a = 33;
int b = 44;

AddTwoNumbers(a, b);
```

I'm passing these to the AddTwoNumbers method. Essentially, a copy of these values is created, and that is passed to the method. If the method now changes the values, so here we're adding 10 to the b parameter, the original value of b, so in the caller, is not influenced. It keeps its original value, 44. The method works on a copy. That is passing by value. The second option to pass them is passing by reference.
