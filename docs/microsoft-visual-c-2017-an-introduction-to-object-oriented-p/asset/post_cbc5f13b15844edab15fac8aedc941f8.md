
## CHAPTER 7 Using Methods

Instead of storing a method's returned value in a variable, you can use it directly, as in statements that produce output or perform arithmetic such as the following:

```csharp
WriteLine("My gross pay is {0}");
CalPay(myHours,myRate).ToString("C");
double tax = CalPay(myHours,myRate) * TAX_RATE;
```

In the first statement, the call to the CalPay() method is made within the WriteLine() method call. Because CalPay() returns a double, you can use the method CalPay() in the same statement you would use a double value. The method call CalPay() has a double data type in the same way you would use double variable does.

As an additional example, suppose that you have a method GetPrice() that accepts an item number and returns its price. The header is as follows:

```csharp
private static double GetPrice(int itemNumber)
```

Further suppose that you want to ask the user to enter an item number from the keyboard so you can pass it to the GetPrice() method. You can get the value from the store, using a string, convert the string to an integer, pass the integer to the GetPrice() method, and store the returned value in a variable named price in four or five statements. Or you can use the following:

```csharp
price = GetPrice(Convert.ToInt32(ReadLine()));
```

This statement contains a method call to ReadLine() within a method call to Convert.ToInt32(), within a method call to GetPrice(). When method calls are placed inside other method calls, the calls are nested method calls. When you write a statement with three nested method calls as in the previous statement, the innermost method executes first. Its return value is used as an argument to the intermediate method, and its return value is used as an argument to the outer method. There is no limit to how “deep” you go with nested method calls.

> The system keeps track of where return after a method call in an area of memory called the stack. Another area of memory called the heap is where memory is allocated while a program is executing.

## Writing a Method That Returns a Boolean Value

When a method returns a value that is type bool, the method call can be used anywhere you can use a boolean expression. For example, suppose you have written a method named isPreferredCustomer() that returns a boolean value indicating whether a customer is a preferred customer who qualifies for a discount. Then you can write if statement such as the following:

```csharp
if(isPreferredCustomer())
    price = price - DISCOUNT;
```

## Writing Methods That Return a Value

In Chapter 4 you learned about effects and how they affect compound Boolean expressions. When you use Boolean methods, you must be especially careful not to cause unintended effects. For example, consider the if statement, in which the intention is to set a delivery fee to 0 if the isPreferredCustomer() and isLocalCustomer() methods return true:

```csharp
if(isPreferredCustomer() && isLocalCustomer())
    deliveryFee = 0;
```

If the localCustomer() method should perform some dense task—for displaying a customer's status or applying a custom discount to the price—then you might not achieve the desired results. By short-circuit evaluation, if the isPreferredCustomer() method returns false, the localCustomer() method never executes. If it is your intention, using methods in this way is fine, but always consider any unintended effects.

## Analyzing a Built-In Method

C# provides you with many predefined methods such as WriteLine() and ReadLine(). In Chapter 2, you learned about C#'s arithmetic operators, such as + and *, and you learned C# provides no exponential operator. Instead, to raise a number to a power, you can use the built-in Pow() method. For example, to raise 2 to the third power (2 * 2 * 2) and store the answer in the variable result, you can write a program that includes the following statement: double result = Math.Pow(2.0, 3.0);

From this, you know the following about the Pow() method:

- It is in the Math class because the class name and a dot precede the method call.
- It is public because you can write a program that uses it.
- It is static because it is used with it its class name and a dot, without any object.
- It accepts two double parameters.
- It returns a double or a type that can be promoted automatically to a double (such as an int) because its answer is stored in a double.

Although you know many facts about the Pow() method, you do not know how its instructions are carried out internally. In good object-oriented style, its implementation is hidden.

## CHAPTER 7 Using Methods

## TWO TRUTHS & A LIE

## Writing a Method That Returns a Value

- 1. A method can return, at most, one value to a method that calls it.
- 2. The data type used in a method's return statement must be the same as the return type declared in the method's header.
- 3. If a method returns a value and you call the method, you must store the value in a variable that has the same data type as the method's parameter variable needs to be capable of accepting the method's returned type. variable does not have to match any parameter's value, the storage variable. Furthermore, if you assign the returned value to a storage variable, that you will typically want to use the returned value, but you are not required to use the method. The false statement is #3. If a method returns a value and you call the method.

## You Do It: Writing a Method That Receives Parameters and Returns a Value

Next, you write a method named CalPhoneCallPrice() that both receives parameters and returns a value. The purpose of the method is to accept the length of a phone call in minutes and the rate charged per minute and to calculate the price of a call, assuming each call includes a 25-cent charge in addition to the per-minute charge. After writing the CalPhoneCallPrice() method, you write a Main() method that calls the CalPhoneCallPrice() method using four different sets of data as arguments.

- 1. Start a program named PhoneCall by typing a using statement, class header, and opening brace:

```csharp
using static System.Console;
class PhoneCall
{
```

2. Type the following CalcPhoneCallPrice() method. The method is declared as static because it will be called by a static Main() without creating an object. The method receives an integer and a double as parameters. The fee for a call is calculated as 0.25 plus the minutes times the rate minute. The method returns the call fee to the calling method.

```csharp
private static double CalcPhoneCallPrice(int minutes, double rate)
{
    const double BASE_FEE = 0.25;
    double callFee;
    callFee = BASE_FEE + minutes * rate;
    return callFee;
}
```

3. Add the Main() method header for the PhoneCall class. Begin the method by declaring two arrays; one contains two lengths, and the other contains two rates. You will use all the possible combinations of call lengths and rates to test the CalcPhoneCallPrice() method. Also, declare a double named priceOfCall that will hold the result of a calculated price.

```csharp
static void Main()
{
    int[] callLengths = {2, 5};
    double[] rates = {0.03, 0.12};
    double priceOfCall;
}
```

4. Add a statement that displays call headings under which you can list combinations of call lengths, rates, and prices. The three column headings are right-aligned, each in a field 10 wide.

```csharp
WriteLine("{0, 10}{1, 10}{2, 10}",
"Minutes", "Rate", "Price");
```

5. Add a pair of nested loops that pass each callLength and rate to the CalcPhoneCallPrice() method in turn. As each pair is passed, the result is stored in the priceOfCall variable, and the details are displayed. Using the nested loops you allow to pass each combination of call time and rate so that multiple possibilities for the values can be tested conveniently.

```csharp
for(int x = 0; x < callLengths.Length; ++x)
{
    for(int y = 0; y < rates.Length; ++y)
    {
        priceOfCall = CalcPhoneCallPrice(callLengths[x],
        rates[y]);
        WriteLine("{0, 10}{1, 10}{2, 10}",
        callLengths[x], rates[y], priceOfCall.ToString("C"));
    }
}
```

6. Add a closing brace for the Main() method and another for the PhoneCall class.

7. Save the file, and compile and run the program. The output looks like Figure 7-16. It shows how a single method can produce a variety of results when you use different values for the arguments.

| Minutes | Rate | Price |
| :--- | :--- | :--- |
| 2 | 0.03 | $0.31 |
| 2 | 0.12 | $0.49 |
| 5 | 0.03 | $0.40 |
| 5 | 0.12 | $0.85 |

Figure 7-16 Output of the PhoneCall program
