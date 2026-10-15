
If we pause at line 15, at this point only the response rate has been written to our console. We can confirm that by checking our app window real quick. The response percentage is indeed printed out, but the other values are not displayed yet. This reassures us that these lines are written out as they are sequentially processed by our app. Back on our debugging controls, let's continue to step through this one line at a time until there are no more lines to process. We can then double check our app window again to see if the rest of our results have been printed out, and of course there they are.

```
Response Percentage: 0.65
Unanswered Surveys: 175
Overall Score: 7.5
Coffee Score Higher Than Food: True
Customers Would Recommend Us: False
Hate Granola, Love Cappucino: True
```

So this is perhaps the simplest possible example of program flow. Our code simply executes one line after the other in order until there are no lines left to process. These are also all single line statements, so every line of code we process also represents one statement. Over the next few chapters, we'll explore special types of multiline block statements that are specifically designed to influence this program flow. This will allow us to create much more interesting flows than what we've observed here. As we move further into the book, it's important that we understand a few key concepts. Program flow represents the order in which our code or statements are executed. Simple programs often execute code sequentially from start to finish while complex programs contain branching paths based on various conditions. Statements are the smallest complete instructions for our applications. They are simple building blocks we can combine in all sorts of ways to accomplish complex tasks. Statements can

also influence program flow and the order or conditions in which other statements run. These statements are written using a combination of C# keywords and expressions. Some special types of statements even have their own reserved keywords, such as if and else. Expressions are composed of operators and operands, such as when two variables are added together. The variables would be the operands and the addition sign would be the operator that acts on them. Statements can be used to control program flow directly or indirectly. Single line statements often influence program flow more indirectly by calculating values and making logical comparisons. Multiline statements allow us to manipulate program flow more directly, so let's look at those more closely in the next chapter, starting with selection statements.

## Chapter 6 How to Explore Selection Statements

At this point, we've written some simple statements and we understand their relationship to program flow. Now let's start to explore special types of statements that can control program flow more directly, starting with selection statements. Selection statements are the most common type of statement you'll use to control program flow. These statements allow you to execute different branches of code depending on specific conditions. There are two types of selection statements in C#. The first are if/else statements, which can select blocks of code to execute based on the result of a Boolean expression. The second are switch statements, and these execute sections of code based on pattern matches to a given expression. If/else statements are slightly more straightforward, so let's discuss those first. The if/else statement is the most essential tool in C# for making decisions.

```
if (currentDay == "Monday")
{
    sendEmailReminder();
}
```

Before, we discussed that statements are written using keywords and expressions, and selection statements are no different. This statement begins with the special if keyword followed by an expression that's wrapped in parentheses. This expression must evaluate to a Boolean

true or false value. We then define a block of code that will execute if that expression is true. Remember, multiline statements like this can define the start and end of blocks of code using opening and closing curly braces. If the result is false, the code inside of our curly braces is never executed and the program flow moves on. Previously, we examine different types of expressions that calculate values or result in true or false Booleans.

```
if (priceScore > serviceScore)
{
    // Do something
}

if (productCategory == "Coffee")
{
    // Do something
}

if ((responseCount / surveyCount) > .5)
{
    // Do something
}
```

Well, now we can see how these expressions really come into play with selection statements and program flow. If statements can use

comparison expressions to decide whether to execute a block of code. They can also use equality checks to decide since these expressions also result in a Boolean value. They can even calculate values using expressions in order to make more specific decisions. If statements can also optionally be paired with an else block.

```
```text
if (productCategory == "Coffee")
{
    // Do something
}
else
{
    // Otherwise do something else
}
```
```

The else block will only execute when the first if expression evaluates to false. You can think of this as an either/or type of decision making. In this case, the first if block will only execute if the value stored inside of the product category is coffee; otherwise, the statements inside of the else block will execute instead. We can also add additional branches of logic to these statements by using the else/if syntax.

```
if (productCategory == "Coffee")
{
    // Do something
}
else if (productCategory == "Food")
{
    // Do something
}
else
{
    // Do something else
}
```

So in this example, if the product category is coffee, the first block will execute and the blocks below it will be skipped by program flow. If the product category is not coffee, the else/if expression will be evaluated instead. If the category is food, that second block will execute and the else block at the bottom will be skipped again. However, if the product category is not coffee or food, this final else block will execute as a fallback regardless of what the category value is. Let's look at an example of how to work with these types of statements in our code project. Let's see how we can start to use

selection statements to control program flow in our app. We created various expressions to calculate interesting data points or answer certain questions. Rather than just computing and printing out these values to the console, let's start to rework this code to actually make decisions. Let's say the marketing team would like to create a list of tasks for their staff to work on based on some of these values and comparisons.

```
class Program
{
    static void Main(string[] args)
    {
        // Calculated Values
        double responseRate = QIResults.NumberResponded / QIResults.NumberSurveyed;
        double unansweredCount = QIResults.NumberSurveyed - QIResults.NumberResponded;
        double overallScore = (QIResults.ServiceScore + QIResults.CoffeeScore + QIResults.FoodScore + QIResults.Price...)

        Console.WriteLine($"Response Percentage: {responseRate}");
        Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
        Console.WriteLine($"Overall Score: {overallScore}");

        // Logical comparisons
        bool isCoffeeScoreLower = QIResults.CoffeeScore < QIResults.FoodScore;
        bool customersRecommend = QIResults.WouldRecommend >= 7;
        bool noGranolaYesCappucino = QIResults.LeastFavoriteProduct == "Granola" && QIResults.FavoriteProduct == "Ca..."

        Console.WriteLine($"Coffee Score Higher Than Food: {isCoffeeScoreLower}");
        Console.WriteLine($"Customers Would Recommend Us: {customersRecommend}");
        Console.WriteLine($"Hate Granola, Love Cappucino: {noGranolaYesCappucino}");
    }
}
```

So to start with, we no longer need these lines of code that simply write out values to the console, so let's delete those entirely.

```
class Program
{
    static void Main(string[] args)
    {
        // Calculated Values
        double responseRate = QIResults.NumberResponded / QIResults.NumberSurveyed;
        double unansweredCount = QIResults.NumberSurveyed - QIResults.NumberResponded;
        double overallScore = (QIResults.ServiceScore + QIResults.CoffeeScore + QIResults.FoodScore + QIResults.Price...)

        // Logical comparisons
        bool isCoffeeScoreLower = QIResults.CoffeeScore < QIResults.FoodScore;
    }
}
```

Next, although all of these variables provide useful examples of expressions, we don't need this many of them to build out a few
