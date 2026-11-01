
## EXERCISES

- 23.1 Extend the Ch23Ex06 example by adding a WebView control to the page BlankPage1 and use the Navigate method to show a web page of your choice. Add an event handler to the page that will navigate the webView to another web page when the app resumes from suspension.
- 23.2 If you want your app to work as a voice recorder, you must ensure that the app has access to the microphone on the device. How do you ensure that the app will not get an UnauthorizedAccessException when it tries to use the microphone on the device?
- 23.3 Many apps running on Windows Phone use a style of navigation known as Pivot. You can create Universal apps that use this style as well. Create an app that uses the Pivot control to display three views, one displaying a web page, another displaying the text “Hello Pivot!,” and the third showing the Wrox logo. You can find the logo here: http://media.wiley.com/assets/253/59/wrox_logo.gif

## WHAT YOU LEARNED IN THIS CHAPTER

| KEY CONCEPT | DESCRIPTION |
|---|---|
| Windows Universal App XAML | Windows Universal app XAML is used with C# to create the GUI for Windows Universal apps. It includes many of the same controls that you know from WPF, but some have changed, others are missing, and new controls have been introduced. |
| Visual State Manager | You saw how to use a Visual State Manager to change the look of your controls and pages simply by changing the visual state of the control. This leads to a lot less code in exchange for slightly more complex XAML. |
| App State | Windows Universal apps are suspended when the user switches to another app or to the desktop, so it's important to handle this suspension and save the app state when it happens. |
| App Store account | This account is used for deploying apps to the Windows Store. |
| Navigation | Navigation in Windows Universal apps is done in much the same way that it is in web applications, using method calls to move back and forth in the page structure. |

## APPENDIX

### Exercise Solutions

There are no exercises in Chapters 1 and 2.

### CHAPTER 3 SOLUTIONS

#### Exercise 1

```
super.smashing.great
```

#### Exercise 2

b), as it starts with a number, and e), as it contains a full stop.

#### Exercise 3

No, there is no theoretical limit to the size of a string that may be contained in a string variable.

#### Exercise 4

The * and / operators have the highest precedence here, followed by +, %, and finally +=. The precedence in the exercise can be illustrated using parentheses as follows:

```
resultVar += ((var1 * var2) + var3) % (var4 / var5);
```

#### Exercise 5

```
using static System.Console;
using static System.Convert;
static void Main(string[] args)
{
    int firstNumber, secondNumber, thirdNumber, fourthNumber;
    WriteLine("Give me a number:");
    firstNumber = ToInt32(ReadLine());
    WriteLine("Give me another number:");
    secondNumber = ToInt32(Console.ReadLine());
    WriteLine("Give me another number:");
    thirdNumber = ToInt32(ReadLine());
    WriteLine("Give me another number:");
    fourthNumber = ToInt32(ReadLine());
    WriteLine($"The product of {firstNumber}, {secondNumber}, " +
      $"{thirdNumber}, and {fourthNumber} is " +
      $"{firstNumber * secondNumber * thirdNumber * fourthNumber}.");
}
```

Note that Convert.ToInt32() is used here, which isn't covered in the chapter.

### CHAPTER 4 SOLUTIONS

#### Exercise 1

```
(var1 > 10) ^ (var2 > 10)
```

#### Exercise 2

```
using static System.Console;
using static System.Convert;
static void Main(string[] args)
{
    bool numbersOK = false;
    double var1, var2;
    var1 = 0;
    var2 = 0;
    while (!numbersOK)
    {
        WriteLine("Give me a number:");
        var1 = ToDouble(ReadLine());
        WriteLine("Give me another number:");
        var2 = ToDouble(ReadLine());
        if ((var1 > 10) && (var2 > 10))
        {
            numbersOK = true;
        }
        else
        {
            if ((var1 <= 10) && (var2 <= 10))
            {
                numbersOK = true;
            }
            else
            {
                WriteLine("Only one number may be greater than 10.");
            }
        }
    }
    WriteLine($"You entered {var1} and {var2}.");
}
```

#### Exercise 3

Yes, as the byte type can hold numbers between 0 and 255, so byte-based enumerations can hold 256 entries with individual values, or more if duplicate values are used for entries.

#### Exercise 4

The code will not compile, for the following reasons:

- End of statement semicolons are missing.
- Second line attempts to access a nonexistent sixth element of blab.
- Second line attempts to assign a string that isn't enclosed in double quotes.

#### Exercise 5

```
using static System.Console;
static void Main(string[] args)
{
    WriteLine("Enter a string:");
    string myString = ReadLine();
    string reversedString = "";
    for (int index = myString.Length - 1; index >= 0; index--)
    {
        reversedString += myString[index];
    }
    WriteLine($"Reversed: {reversedString}");
}
```

#### Exercise 6

```
using static System.Console;
static void Main(string[] args)
{
    WriteLine("Enter a string:");
    string myString = ReadLine();
    myString = myString.Replace("no", "yes");
    WriteLine($"Replaced \"no\" with \"yes\": {myString}");
}
```

#### Exercise 7

```
using static System.Console;
static void Main(string[] args)
{
    WriteLine("Enter a string:");
    string myString = ReadLine();
    myString = "\"" + myString.Replace(" ", "\"\" ") + "\"";
    WriteLine($"Added double quotes around words: {myString}");
}
```

Or using String.Split():

```
using static System.Console;
static void Main(string[] args)
{
    WriteLine("Enter a string:");
    string myString = ReadLine();
    string[] myWords = myString.Split(' ');
    WriteLine("Adding double quotes around words:");
    foreach (string myWord in myWords)
    {
        Write($"\"{myWord}\" ");
    }
}
```

### CHAPTER 6 SOLUTIONS

#### Exercise 1

The first function has a return type of bool, but doesn't return a bool value.

The second function has a params argument, but this argument isn't at the end of the argument list.

#### Exercise 2

```
using static System.Console;
static void Main(string[] args)
{
    if (args.Length != 2)
    {
        WriteLine("Two arguments required.");
        return;
    }
    string param1 = args[0];
    int param2 = ToInt32(args[1]);
    WriteLine($"String parameter: {param1}");
    WriteLine($"Integer parameter: {param2}");
}
```

Note that this answer contains code that checks that two arguments have been supplied, which wasn't part of the question but seems logical in this situation.

#### Exercise 3

```
using static System.Console;

class Program
{
    delegate string ReadLineDelegate();
    static void Main(string[] args)
    {
        ReadLineDelegate readline = new ReadLineDelegate(ReadLine);
        WriteLine("Type a string:");
        string userInput = readLine();
        WriteLine($"You typed: {userInput}");
    }
}
```

#### Exercise 4

![](img/cf72ea860016d2d680fc085fc06f265a_771_0.png)

FIGURE A-1

#### Exercise 5

```
static void ManipulateDrink(HotDrink drink)
{
    drink.AddMilk();
    drink.Drink();
    ICup cupInterface = (ICup)drink;
    cupInterface.Wash();
}
```

Note the explicit cast to ICup. This is necessary as HotDrink doesn't support the ICup interface, but you know that the two cup objects that might be passed to this function do. However, this is dangerous, as other classes deriving from HotDrink are possible, which might not support ICup, but could be passed to this function. To correct this, you should check to see if the interface is supported:

```
static void ManipulateDrink(HotDrink drink)
{
    drink.AddMilk();
    drink.Drink();
    if (drink is ICup)
    {
        ICup cupInterface = drink as ICup;
        cupInterface.Wash();
    }
}
```

The is and as operators used here are covered in Chapter 11.
