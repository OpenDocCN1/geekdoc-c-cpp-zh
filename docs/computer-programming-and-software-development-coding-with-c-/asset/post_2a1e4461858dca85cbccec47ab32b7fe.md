
One issue with foreach loops is that we cannot modify the size of the original collection while we are looping through it. So if we start with 100 customers to loop through, we have to keep that same 100 set. Because the counting and incrementing is handled for us in the background by C#, it will not adapt to a change in the size of the collection. This is a fairly uncommon requirement in the first place, but it's good to be aware of. The next type of loop is called a while loop, and it comes with a matching keyword again.

```
while ((line = file.ReadLine()) != null)
{

WriteToProductTable(line);

}
```

While loops simply execute a block of code over and over, as long as some Boolean expression evaluates to true. These types of loops are really useful when you have no idea how many times the block of code must run. For example, let's say we have to read in a text file, and that contains an unknown number of rows of product data. We could use a while loop to check if we have reached the end of the file every time another row is processed. While loops are also often used in interfaces or games. So, for instance, while a controller button is pressed, a game character might continue to run forward or while an arrow key is held down, a graph will progressively draw more information. These are scenarios where the number of times the code has to execute is very dynamic, or constantly changing. The last type of loop is called a do-while loop. This type of loop is almost identical to a while loop, with one important distinction. A do-while loop will always execute at least once, even if the condition being evaluated results to false, because that condition check happens after the loop runs. With a standard while loop, that check happens before the loop runs.

```
do {
    // Statements to execute
}
while (someValue == true)
```

This type of loop is useful in certain niche situations, but it's fairly rare to see in applications, so we will not spend a lot of time with it in this book. One other feature of loops to be aware of is the break keyword. You might remember this word from our switch statements. Break allows us to short circuit a loop and jump out of that statement and back into normal program flow, regardless of whether the loop condition has been reached or not.

```
foreach (var customer in mailingList)
{
    break;
    SendEmail(customer);
}
```

So in this example, our customers would never be sent an email, since the code breaks out of it before that method below it is ever called. I also want to very quickly mention LINQ in case you may have heard of it. LINQ stands for language integrated query, and it provides some powerful options for filtering and iterating over data in C#. Some of our examples could be easily implemented through LINQ, however, LINQ is a sizable topic of its own and there are other C# book on this topic in detail, so we will not be discussing it in this more beginner level course. LINQ is my personal favorite feature of C#, though, so I encourage you to go and explore this great topic more on your own. For now though, let's start to explore how to use additional types of loops in our app.

Let's see how to use a foreach loop as a simple option for processing sets of data. In the previous module, we briefly explored this area to improve property on our set of data. This mobile app value is what the majority of users selected as the area could improve on the most. Well, in order to come up with actionable ideas, would like to find all of the comments from people who selected mobile app as their area to improve. So back in our Program file, let's see how to use a foreach loop to accomplish this. Let's step down a few lines below our for loop and then create a second loop using the foreach keyword. Inside of our parentheses we can simply type var response in Q1Results.Responses. Behind the scenes, C# will automatically iterate over every item in the responses list and assign the current iteration item to this response variable. Next, let's drop down into our code block, and in here we can add another nested if statement. This time we can say if response.AreaToImprove == Q1Results.AreaToImprove, and that will

filter our responses down to only those items that match the aggregate AreaToImprove score. Then in our nested code block, let's again write out those comments to the console.

![](img/0155736aec718cf18821e9f10a5d308d_578_0.png)

For this example, I have intentionally chosen a scenario that is very similar to our previous loop so we can appreciate just how much simpler the foreach syntax is. We do not have to worry about managing incrementer variables or accessing dictionary items using an index or manually creating a CurrentItem variable for readability or any of those sorts of tasks. In C# apps, foreach loops are by far the most common type of loop you'll see because they are extremely easy to use for simply iterating over collections. Let's temporarily comment out this first loop, and this way we can debug our new one in isolation. You can do that using the Comment button at the top of Visual Studio or just using the keyboard shortcut Ctrl+K/Ctrl+C. Commented out code does not execute when the app runs. Then let's set a breakpoint at the start of our new loop and start the app.

```
foreach (var response in Q1Results.Responses)
{
    if (response.AreaToImprove == Q1Results.AreaToImprove)
    {
        Console.WriteLine(response.Comments);
    }
}

public static void GenerateTasksReport()
{
    var tasks = new List<string>();
```

After a moment, we'll pause on our new foreach loop. As we step through this code, we first land on our collection and then a local variable is set for the first item in that list. And as we continue to step through this, that response variable is continually reassigned to the next item in our list. Some of those responses match the area to improve that we're looking for, and those items will be written out to the console as we iterate through this. So just click through the remaining items or remove the breakpoint and hit Continue to jump ahead and see the final results printed in the app. So now we've seen how to streamline iterations using a foreach loop. In order to keep our code organized, let's package up these loops that find problematic comments into their own method, just like we did with our tasks report. So let's highlight these two loops and then and choose Actions, Extract method. Then, let's name this new method something like GenerateCommentsReport, and this will just help keep our main method more manageable as we continue.

```
class Program
{
    static void Main(string[] args)
    {
        GenerateTasksReport();
        GenerateCommentsReport();
    }

    private static void GenerateCommentsReport()
    {
        for (var i = 0; i < Q1Results.Responses.Count; i++)
        {
            var currentResponse = Q1Results.Responses[i];

            if (currentResponse.WouldRecommend < 7.0)
            {
                Console.WriteLine(currentResponse.Comments);
            }
        }
    }
```

In the next chapter, let's continue our work with loops, but let's see how to use a different type of loop to solve a different type of problem.

## Chapter 11 Working with While Statements

Let's see how we can use a while loop to accomplish another objective of our app. So let's say that the marketing team would like to pick two people to give away a free gift card to. The drink of the month was a cappuccino, so they want to pick the first two responses who selected that as their favorite product. So essentially, we want to loop through our survey responses until we find the first two people who meet this criteria. This criteria is subtly different from our previous loops. We only want to iterate through our responses until some specific criteria is met, and then we can forget about the rest of the items. With our previous loops, we specifically wanted to process every single item. There are a variety of ways to accomplish this in C#, but let's see how to do this using a while loop. Above our existing code, let's create some spaces with a few new lines and then start to type out our new loop with the while keyword.

```
static void Main(string[] args)
{
    var selectedEmails = new List<string>();
    int counter = 0;
    while (selectedEmails.Count < 2 && counter < Q1Results.Responses.Count)
    {
        var currentItem = Q1Results.Responses[counter];
        if (currentItem.FavoriteProduct == "Cappuccino")
        {
            selectedEmails.Add(currentItem.EmailAddress);
            Console.WriteLine(currentItem.EmailAddress);
        }
        counter++;
    }
    GenerateTasksReport();
    GenerateCommentsReport();
```
