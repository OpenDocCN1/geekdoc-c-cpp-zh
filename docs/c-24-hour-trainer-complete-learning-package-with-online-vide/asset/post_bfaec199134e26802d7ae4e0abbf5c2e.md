
## IF-ELSE STATEMENTS

The previous example set shipping to a default value and then changed it if total was at least $100. Another way to think about this problem is to imagine taking one of two actions depending on total’s value. If total is less than $100, the program should set shipping to $5. Otherwise the program should set shipping to $0.

The if-else construct lets a program follow this approach, taking one of two actions depending on some condition.

The syntax for if-else is:

```csharp
if (condition)
    statementsIfTrue;
else
    statementsIfFalse;
```

If *condition* is true, the first block *statementsIfTrue* executes. Otherwise (if *condition* is false) the second block *statementsIfFalse* executes.

Using the else keyword, the preceding code could be rewritten like this:

```csharp
decimal shipping;
if (total < 100)
    shipping = 5M;      // Shipping is $5 if total < 100.
else
    shipping = 0M;      // Shipping is free if total >= 100.
```

You can use braces to make either the if or else part of the if-else statement execute more than one command.

## CASCADING IF STATEMENTS

The if-else construct performs one of two actions depending on whether the condition is true or false. Sometimes a program needs to check several conditions to decide what to do.

For example, suppose an order entry program calculates shipping charges depending on the total purchase amount according to this schedule:

- If total < $20, shipping is $5.00.
- Otherwise, if total < $50, shipping is $7.50.
- Otherwise, if total < $75, shipping is $10.00.
- Otherwise, shipping is free.

You can make a program perform each of these tests one after another by making a second if statement be the else part of a first if statement. The following code shows how you can calculate shipping according to the preceding schedule:

```csharp
decimal shipping;
if (total < 20)
{
    shipping = 5M;
}
else if (total < 50)
{
    shipping = 7.5M;
}
else if (total < 75)
{
    shipping = 10M;
}
else
{
    shipping = 0M;
}
```

When the program encounters a cascading series of if statements, it executes each in turn until it finds one with a true condition. It then skips the rest because they are all part of the current if statement's else block.

For example, consider the previous code and suppose total is $60. The code evaluates the first condition and decides that (total < 20) is false, so it does not execute the first code block.

The program skips to the else statement and executes the next if test. The program decides that (total < 50) is also not true, so it skips to this if statement's else block.

The program executes the third if test and finds that (total < 75) is true so it executes the statement shipping = 10M.

Because the program found an if statement with a true condition, it skips the following else statement, so it passes over any other if statements that follow without evaluating their conditions.

## NESTED IF STATEMENTS

Another common arrangement of if statements nests one within another. The inner if statement is executed only if the first statement's condition allows the program to reach it.

For example, suppose you charge customers 5 percent state sales tax. If a customer lives within your county, you also charge a county transportation tax. Finally, if the customer also lives within city limits, you charge a city sales tax. (Taxes where I live are at least this confusing.)

The following code performs these checks, where the variables inCounty and inCity indicate whether the customer lives within the county and city:

```csharp
if (inCounty)
{
    if (inCity)
    {
```

```csharp
...
    default:
        statementsDefault;
        break;
}
```

Here testValue is the value that you are testing. The values value1, value2, and so on are the values to which you are comparing testValue. The statements1, statements2, and so on are the blocks of statements that you want to execute for each case. The other pieces (switch, case, break, and default) are keywords that you must type as they appear here.

If you include the optional default section, its statements execute if no other case applies. Actually the case statements are optional, too, although it would be strange to not use any.

Note that a case's code block doesn't need to include any statements other than break. You can use that to make the code take no action when a particular case occurs.

For example, suppose you build a form where the user selects a hotel from a ComboBox. The program uses that selection to initialize an enumerated variable named hotelChoice. The following code sets the lodgingPrice variable depending on which hotel the user selected:

```csharp
decimal lodgingPrice;
switch (hotelChoice)
{
    case HotelChoice.LuxuryLodge:
        lodgingPrice = 45;
        break;

    case HotelChoice.HamiltonArms:
        lodgingPrice = 80;
        break;

    case HotelChoice.InvernessInn:
        lodgingPrice = 165;
        break;

    default:
        MessageBox.Show("Please select a hotel");
        lodgingPrice = 0;
        break;
}
```

The case statements check for the three expected choices and sets lodgingPrice to the appropriate value. If the user doesn't select any hotel, the default section's code displays a message box and sets lodgingPrice to 0 to indicate a problem.

A switch statement is most robust (less prone to bugs and crashes) if its cases can handle every possible comparison value. That makes them work very well with enumerated types because you can list every possible value. In contrast, you can't include a case statement for every possible integer value (unless you include several billion lines of code), so case statements can't check every possible integer value.

Even if the `case` statements check every possible value in an enumeration, it's a good practice to include a `default` section just in case another value sneaks into the code. For example, a bug in the code could convert an integer into an enumeration value that doesn't exist, or you could later add a new value to the enumeration and forget to add a corresponding `case` statement. In those cases, the default statement can catch the bug, take some default action, and possibly warn you that something is wrong.

When you use a `switch` statement with other data types, be sure to consider unexpected values, particularly if the user typed in the value. For example, don't assume the user will always enter a valid string. Allowing the user to select a string from a `ComboBox` is safer, but you should still include a `default` statement.

## TRY IT

In this Try It, you build the Order Form program shown in Figure 18-1. The program uses a cascading series of `if` statements to calculate shipping cost based on the subtotal.

### Lesson Requirements

In this lesson, you:

- Build the form shown in Figure 18-1.
- Write the code for the Calculate button so it calculates the subtotal, sales tax, shipping, and grand total. The sales tax should be 7 percent of the subtotal. Shipping should be $5 if subtotal < $20, $7.50 if subtotal < $50, $10 if subtotal < $75, and free if subtotal ≥ $75.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_308_0.png)

FIGURE 18-1

**NOTE** You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

### Hints

- Make the sales tax rate a constant, giving it the most limited scope you can.

### Step-by-Step

- Build the form shown in Figure 18-1.
    - 1. This is relatively straightforward.
- Write the code for the Calculate button so it calculates the subtotal, sales tax, shipping, and grand total. The sales tax should be 7 percent of the subtotal. Shipping should be $5 if subtotal < $20, $7.50 if subtotal < $50, $10 if subtotal < $75, and free if subtotal ≥ $75.
    - 1. Calculate the total costs for each of the four items. Add them together to get the subtotal.
    - 2. Calculate sales tax by multiplying the tax rate by the subtotal.
    - 3. Use a series of cascading if-else statements to calculate the shipping cost based on the subtotal as in the following code:
    - 4. Add the subtotal, tax, and shipping cost to get the grand total.
    - 5. Display the results.

```csharp
// Calculate shipping cost.
decimal shipping;
if (subtotal < 20)
{
    shipping = 5;
}
else if (subtotal < 50)
{
    shipping = 7.5m;
}
else if (subtotal < 75)
{
    shipping = 10;
}
else
{
    shipping = 0;
}
```

## EXERCISES

- 1. Build the Conference Coster program shown in Figure 18-2.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_309_0.png)

FIGURE 18-2

When the user clicks the Calculate button, first check each ListBox's SelectedIndex property. If any SelectedIndex is less than zero (indicating the user didn't make a choice), display an error message and use the return keyword to stop calculating.
