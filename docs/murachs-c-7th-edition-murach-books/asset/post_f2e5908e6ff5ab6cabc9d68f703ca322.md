
## How to work with tuples

C# 7.0 introduced a new feature called *tuples* that lets you define simple data structures. Tuples are similar to enumerations, except the *members* of a tuple are public variables instead of constants. In the topics that follow, you’ll learn the basic skills for creating tuples and referring to their members. You’ll also learn how to use a tuple as the return type for a method.

### How to create tuples and refer to their members

Figure 6-7 shows different ways that you can create tuples. The first example shows how to create an *unnamed tuple*. To do that, you code the var keyword as the tuple type, followed by the name of the variable that will store the tuple. Then, you assign values for the members of the tuple by coding the values in parentheses and separating them with commas.

When you use this technique, the types of the members are inferred from the values that are assigned to them. In this example, that means that the first member is given a type of string and the second member is given a type of int. In addition, the members of an unnamed tuple are given default names of Item1, Item2, and so on. Then, you can refer to a member of the tuple using its default name. To do that, you code the name of the tuple variable, followed by a dot operator and the name of the member.

In most cases, you’ll want to create a *named tuple* by assigning your own names to the members of the tuple. The second example shows two ways to do that. First you can specify a member name by coding the name and a colon before the member value. When you use this technique, the types of the members are inferred from the values that are assigned to them, just as they are when you create an unnamed tuple.

Second, you can declare the data types for the members explicitly. To do that, you code the type and name for each member before the name of the tuple variable, you separate the members with commas, and you enclose them with parentheses.

To refer to a member of a named tuple, you code the name of the tuple variable followed by the dot operator just like you do for an unnamed tuple. Instead of coding the default names, though, you can code the names you specified. These names act as synonyms for the default names and make it easier to refer to the members.

Notice in both of these examples that the names of the tuple members use Pascal notation (each word starts with an uppercase character). This is a common coding practice, since the members are public variables.

The third example in this figure shows another way to create a tuple that was introduced with C# 7.1. Here, the member values are specified using variable names instead of literals. When you use this technique, the members are given the same names as the variables. Because of that, the member names use Camel notation (first word starts with a lowercase character, all words after that start with an uppercase character). Then, you can refer to the members using those names.

### How to create and work with an unnamed tuple

### How to create a tuple with two members

```
var person = ("Anne Boehm", 62);
```

### How to refer to the members of the tuple

```
person.Item1
person.Item2
```

### How to create and work with a named tuple

### How to create a tuple with two members

```
var person = (Name: "Anne Boehm", Age: 62);
```

### How to create the tuple and declare its member types

```
(string Name, int Age) person = ("Anne Boehm", 62);
```

### How to refer to the members of the tuple

```
person.Name
person.Age
```

### How to create a tuple using variable names (C# 7.1 and later)

### How to create a tuple with two members

```
string name = "Anne Boehm";
int age = 62;
var person = (name, age);
```

### How to refer to the members of the tuple

```
person.name
person.age
```

### Description

- *Tuples* are a new feature of C# 7.0 that lets you define simple data structures that contain two or more data items called *members*.
- Tuples can be used in place of classes and structures when you just need to work with a group of public variables, or *fields*. See chapter 12 for more information on working with classes, structures, and fields.
- When you create a tuple, you must assign a value to each member. You can do that using any of the techniques shown above.
- An *unnamed tuple* is a tuple whose members don’t have names. You can refer to the members of an unnamed tuple using the default names Item1, Item2, and so on.
- A *named tuple* is assigned synonyms that can be used in place of the default names.
- To refer to a member of a tuple, you code the name of the tuple, followed by the dot operator and the name of the member.

### How to use a tuple as the return type for a method

Earlier in this chapter, you learned how to use out parameters to return values from a method to the calling code. When you use out parameters, you can return one or more values. However, this isn’t the recommended way to return multiple values from a method. A better way is to use tuples as shown in figure 6-8.

This figure starts by showing a version of the CalculateFutureValue() method that returns a tuple. Here, the return type is coded as a tuple that contains two members. The first member is a decimal named FutureValue that will store the future value that’s calculated by the method, and the second member is a decimal that will store the total amount of interest that’s included in the future value.

To return a tuple from a method, you code a return statement as shown here. This return statement includes the names of the variables that contain the values you want to return. These variables must be enclosed in parentheses and separated by commas, and they must be coded in the same sequence as the members of the tuple for the return type. Their data types must also correspond to member types of the tuple.

Next, this figure shows two ways that you can call the CalculateFutureValue() method. First, you can declare the data types and names for the members of the tuple and then assign the result of the method to the tuple. When you do that, the values in the tuple that’s returned by the method are assigned to the corresponding members of the tuple in the calling code. This is referred to as deconstructing the tuple. Note that when you use this technique, you don’t have to name the tuple in the calling code. If you don’t, you can refer to its members directly by name.

Second, you can use the var keyword to create a tuple variable in the calling code. Then, the data types of the tuple members are inferred from the tuple that’s returned by the method. In that case, you must refer to the members of the tuple using the name of the tuple variable.

Although it’s not shown here, you should know that you can use a discard if you don’t need one or more of the values that are returned by a tuple. For example, suppose you need just the future value that’s returned by the method in this figure and not the total interest. In that case, you could call the method like this:

```
(decimal FutureValue, _) = this.CalculateFutureValue(
    monthlyInvestment, monthlyInterestRate, months);
```

Then, the second value that’s returned by the tuple is discarded instead of being stored in a variable.

Although tuples provide an easy and efficient way to return multiple values from a method, you should know that you can accomplish the same thing using a class or structure. You’ll learn more about that in chapter 12. For now, you should realize that classes and structures can contain members like properties and methods that you can’t include in tuples. If you need to return a type from a method that contains these members, then, you’ll need to use a class or structure.

### A CalculateFutureValue() method that returns a tuple

```
private (decimal FutureValue, decimal TotalInterest)
    CalculateFutureValue(decimal monthlyInvestment,
    decimal monthlyInterestRate, int months)
{
    decimal futureValue = 0m;
    decimal totalInterest = 0m;
    decimal monthlyInterest = 0m;
    for (int i = 0; i < months; i++)
    {
        monthlyInterest = (futureValue + monthlyInvestment)
            * monthlyInterestRate;
        totalInterest += monthlyInterest;
        futureValue += monthlyInvestment + monthlyInterest;
    }
    return (futureValue, totalInterest);
}
```

### A statement that calls the method and deconstructs the tuple

```
(decimal FutureValue, decimal TotalInterest) =
    this.CalculateFutureValue(monthlyInvestment, monthlyInterestRate,
    months);
```

### Two statements that refer to the members of the tuple

```
txtFutureValue.Text = FutureValue.ToString("c");
txtTotalInterest.Text = TotalInterest.ToString("c");
```

### A statement that calls the method and assigns the tuple to a variable

```
var calculations = this.CalculateFutureValue(
    monthlyInvestment, monthlyInterestRate, months);
```

### Two statements that refer to the members of the tuple

```
txtFutureValue.Text = calculations.FutureValue.ToString("c");
txtTotalInterest.Text = calculations.TotalInterest.ToString("c");
```

### Description

- To define a tuple as the return type for a method, you define its members by enclosing them in parentheses and separating them with commas.
- To return a tuple from a method, you code the variables that store the values of the members on the return statement. To do that, you enclose the variables in parentheses and separate them with commas.
- To call a method that returns a tuple, you can declare each member of the tuple and then assign the result of the method to the tuple. This is referred to as deconstructing the tuple because the value of each member that’s returned is assigned to a separate variable.
- You can also assign a tuple that’s returned by a method to a single variable. Then, the members of the tuple have the same names as the members of the return type, and you can refer to those members through the tuple variable.
