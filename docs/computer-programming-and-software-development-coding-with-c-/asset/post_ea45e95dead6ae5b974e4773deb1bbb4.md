
defined in our main method, that variable is automatically scoped to just this method. Remember, by default, variables are only available in the code block they're created in and any nested blocks. Our report methods down below are entirely different methods, not just nested code blocks. So for them to be able to use this variable, we have to pass it as a parameter. So, let's copy and paste the survey results into each of these parentheses like so. At first, Visual Studio will complain to us that this is not acceptable. Well, that's because the signatures for these methods do not currently accept a parameter. So further down in our report methods, we need to add that new parameter to the method definition. On this GenerateWinner report, let's add the SurveyResults as a parameter and name that parameter results or something similar.

```
public static void GenerateWinnerEmails(SurveyResults results)...
public static void GenerateCommentsReport(SurveyResults results)...
public static void GenerateTasksReport(SurveyResults results)...
```

Once we have that in place, we can then copy it and add it as a parameter to our other two methods. This will get rid of the original errors up top, but we do still have some errors throughout our app with all these red lines under our old Q1Results references.

```
Console.WriteLine(Environment.NewLine + "Selected Winners Output:");
while (selectedEmails.Count < 2 && counter < Q1Results.Responses.Count)
{
    var currentItem = Q1Results.Responses[counter];
```

We have to change all of those references to instead use the results variable that is passed into the method. Remember, we are no longer using this static data. We want to perform our logic on the survey results that are dynamically provided as a parameter. An easy way to accomplish this is just through find and replace. So, let's hit Ctrl+F to bring up the search box and then click the arrow on the left to expand this to include the replace feature. In the first input, let's type Q1Results., and that will find all the references to our old class, and then in the replace, just type results., which will update all those references to use our new variable when we click replace. Our program file here is now set up much better. We no longer use hard coded, data. Instead, we dynamically read data in from a file, store it in a variable, and pass it down into methods that will use it to perform logic. This setup is closer to what you would want to use in a real app. If you do not understand every aspect or step of this process, that's totally fine for this book.

![](img/0155736aec718cf18821e9f10a5d308d_607_0.png)

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        bool quitApp = false;

        do
        {
            Console.WriteLine("Please specify a report to run (rewards, comments, tasks, quit):");
            var selectedReport = Console.ReadLine();

            Console.WriteLine("Please specify which quarter of data: (q1, q2)");
            var selectedData = Console.ReadLine();

            var surveyResults = JsonConvert.DeserializeObject<SurveyResults>
                (File.ReadAllText($"data/{selectedData}.json"));

            switch (selectedReport)
            {
                case "rewards":
                    GenerateWinnerEmails(surveyResults);
                    break;
                case "comments":
                    GenerateCommentsReport(surveyResults);
                    break;
            }
        }
    }
}
```
```

The key concept here is that we're now able to use user input to control our program flow and select which file to read in and use

to our app as more results come in, and the user would be able to keep running different reports. This is a much more flexible and useful solution than what we had before. Next, let's start to talk about some additional more advanced features of selection statements that we can apply to our app.

## Chapter 15 How to Explore Advanced Selection Statement Features

As you start to work with selection statements in more depth, you'll find there are some alternative syntaxes or additional features for these statements and the expressions that they utilize. Let's say we have a simple if/else statement that conditionally assigns a value to a discount code variable.

```
double discountRate;

if (product.Category == "Coffee")
{
    discountRate = .25
}
else
{
    discountRate = .33
}
```

If the category is Coffee, the discount rate is .25, or 25%, and for other categories, it's 33%. While this code is technically fine, but it also creates about 10 lines of code for a simple conditional

assignment. These scenarios can be streamlined using a C# feature called ternary statements. Ternaries allow us to place a Boolean expression on the right side of a variable assignment, followed by a conditional operator.

```
var discountRate = product.Category == "Coffee" ? .25 : .33;
```

The conditional operator is a pair of question mark and colon symbols, and it's also referred to as a ternary operator. The value that's placed right after the question mark is assigned to the variable if the Boolean expression is true, while the value after the colon is assigned if it's false. You can also substitute calls to methods for the static values seen here.

```
var discountRate = product.Category == "Coffee" ?
GetDiscount("Coffee") : GetDiscount("Other");
```

This essentially allows us to write simple if/else statements in a single line of code. And this brings us to an important point about ternary statements. These statements are primarily intended for assigning or selecting values, not for traditional program flow. Although they can conditionally select methods to run, those methods must also return a value to be assigned. Ternaries cannot select more complex or branching blocks of code to run, like a traditional if/else statement could. Switch statements also provide shortcuts when assigning values to a variable. So in this case, we are using a switch statement to check the friendly name of a product and then assigning a category id for it to a variable.

```
int categoryId;
switch (productName)
{
    case "Granola":
        categoryId = 1;
        break;
    case "Latte":
        categoryId = 2;
        break;
}
```

Well, this index could be greatly simplified using the switch expression syntax. This option defines an expression to match a set of patterns against. Those patterns use the C# lambda syntax to return a value if a match is found, such as the if productName here matches Granola. This code is much simpler and more compact, and that makes it easy to use in different parts of our app.

```
int discountId = 25;
switch (discountId)
{
    case int id when id < 10:
        // returns false
        break;
    case int id when id < 10 && id > 20:
        // returns false
        break;
    case int id when id > 20 && id < 30:
        // returns true, code section would execute
        break;
}
```

We can declare a local variable for that case statement that makes a copy of the switch expression value. So in this case, the discount id would be copied to id, and then we use that as part of another expression. If that nested expression evaluates to true, the corresponding switch section will run. The last feature of switch statements I want to mention is their support for tight matching. Now this topic is a bit more advanced and requires a decent understanding of the C# type system, so we are going to spend minimal time on it in this book.

```
Shape myShape = new Rectangle() { width = 20 };
switch (myShape)
{
    case Square s when shape.width < 10:
    // returns false
    break;
    case Rectangle r when shape.width > 10:
    // returns true
    break;
    case Circle c when c.diameter > 10:
    // returns false
    break;
}
```

For now, just be aware that we can test whether a switch expression can be converted to a certain type. So for example, here we are verifying that a shape is of a certain type and that its dimensions are of a certain size. Just keep this feature in mind as you start to explore more advanced C# features later on. Let's start to explore some of these concepts. At the bottom of our tasks report, we created this switch statement that creates tasks based on the area that needs the most improvement.
