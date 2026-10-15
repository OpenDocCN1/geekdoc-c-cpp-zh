
It's a bad practice to just put everything at the code block, since that can cause readability issues and produce unexpected bugs when too many pieces of code are modifying the same variables. We will start to explore more of these concerns or ideas in the next chapter. Before we get there, though, let's wrap up by reviewing a few key concepts. Let's review some small changes to our application that will organize it more effectively for the rest of the book. So up to this point, we have used a combination of console outputs and lists to manage the data items we are working with.

```
{
    var comments = new List<string>();

    Console.WriteLine(Environment.NewLine + "Comments Output:");
    for (var i = 0; i < Q1Results.Responses.Count; i++)
    {
        var currentResponse = Q1Results.Responses[i];

        if (currentResponse.wouldRecommend < 7.0)
        {
            Console.WriteLine(currentResponse.Comments);
            comments.Add(currentResponse.Comments);
        }
    }

    foreach (var response in Q1Results.Responses)
    {
        if (response.AreaToImprove == Q1Results.AreaToImprove)
        {
            Console.WriteLine(response.Comments);
            comments.Add(response.Comments);
        }
    }

    File.WriteAllLines("CommentsReport.csv", comments);
}
```

For the end state of this module, I have made a few small cleanup changes to our project to standardize these approaches across our methods, so if we look through here carefully, each report will now output its results to the console along with a header description of that report. Each report will also store any relevant items in a list, such as a list of tasks or comments like we started earlier. That way when we run the reports, we can see the results output in our console, but we also have an list of those items to work with. This second point is important, because it allows us to do other things with our data. On each report, I have added a line of code at the bottom that says File.WriteAllLines, and then I provide a name for a file, as well as a list of items for that report. This line of code uses the C# file helper class to write this data out to a file on our file system. Working with files is not really a focus of this book, so we do not need to spend a lot of time on this code, except to understand the basics of what it does. This setup is valuable to us because it means that the outputs of our reports can be accessed outside of our app by other people. So, for example, someone could run this report and then take the generated text file and email it to someone else. The files are saved as CSVs, so they can be opened as rows easily in something like Excel. Later in the book, we'll see how to control which reports get generated based on user input.

```
class Program
{
    static void Main(string[] args)
    {
        GenerateWinnerEmails();

        GenerateTasksReport();

        GenerateCommentsReport();
    }

    public static void GenerateWinnerEmails() { ... }

    public static void GenerateCommentsReport() { ... }

    public static void GenerateTasksReport() { ... }
}
```

So if I collapse all three of our reports, and you can do that with the Ctrl+M, O keyboard shortcut, we still have a clean Main method to work with that just runs all these reports in a row, but now we'll get a consistent output across all of them. Let's start our app at the top of Visual Studio to see what happens now. So after a moment we should see our data results output to the console, which is certainly helpful while we're working. We can see the tasks, improvement concepts, and selected rewards members that we set up in the earlier modules. However, our app now also outputs these results as files. Those files are located in our project directory on the file system. So over in our Solution Explorer, let's on our project node and say Open Folder in File Explorer, which is a useful shortcut. In the root directory here, let's navigate down through the bin folder and then all the way into our .net5.0 folder. This is the directory our app actually executes out of, which we can see with our Reports.exe file here. However, we also now have three report files such as this TasksReport.csv. Let's to open that in Excel, and we'll discover the list of tasks that people should take action on from our app. These files could then be sent around and used however needed. We could also add more reports to our app in the future that output other files, and polish up the formats and data inside of them, and so on. So, again, managing file outputs is not a huge focus of our app, since we are more interested in the program flow to get to that point; however, this general setup provides a clean starting point for some of the concepts later in this book, and a good place for us to close out this module.

Iteration statements are a powerful tool for controlling program flow. They allow us to repeat a block of code many times, often to iterate over a set of data. There are several different types of loops in C# that each provide different features to handle different situations or objectives. For loops are perhaps the most classic type of loop. They generally initialize an incrementer variable, which is used in a conditional check to repeat a block of code a given number of times. Foreach loops provide a streamlined alternative to for loops with a slightly reduced feature set, but much simpler syntax. While loops are a very flexible, more manual approach to loops. They allow us to repeatedly execute a block of code as long as a given expression evaluates to true. We also have the do while loop, which is a variation of the while loop that is guaranteed to execute at least once. Finally, it's important to understand the nuances of variable scope. At the most basic level, just remember that variables can be used inside of the code block that they are declared in, as well as any nested code blocks. They must also be declared above the code that utilizes them. In the next chapter, let's explore a few more advanced features of statements and additional application program flow considerations.

## Chapter 12 How to Explore Additional Program Flows

Let's start to bring together many of the concepts of this book to achieve some larger goals. There are really two main areas we want to focus on to round out our discussion. First, we'll explore more ways to control program flow across our application as a whole. We've written a fair amount of code up to this point, so we want to take a step back and explore how to start managing this larger setup. Then later on, we'll wrap up the book by discussing a few more advanced features of selection statements and their relationship to program flow. These more advanced features can be very useful in specific situations. To expand on our first goal, most of our work with program flow in this book has centered around individual methods or specific statement examples, create this task, or print out this message, and other tasks. As we start to build more substantial apps, we must understand how to control program flow between larger pieces of our apps and in a wider variety of situations. We want to influence program flow at the macro level across multiple methods and code files or classes. We also want our program flow to adapt to user input and more dynamic data. Let's start to explore how to accomplish some of these goals next.

### Controlling Flow through User Input

Let's see how to make our app more interactive by collecting user input and using that to influence program flow. Back in Visual Studio, right now in the Main method we are simply calling our three reporting methods sequentially.

```
static void Main(string[] args)
{
    GenerateWinnerEmails();
    GenerateTasksReport();
    GenerateCommentsReport();
}
```

Although these methods have branching logic inside of them, at the application level they still just execute one after the other. Well, what if we wanted to make this more dynamic? What if we wanted the user of the app to be able to choose which report will run? This is really easy to do in a C# console app using a basic selection statement. So at the top of our Main method, let's add a couple statements to capture the user input and store it in a variable.

```
Console.WriteLine("Please specify a report to run (rewards, comments, tasks):");
var selectedReport = Console.ReadLine();

switch (selectedReport)
{
    case "rewards":
        GenerateWinnerEmails();
        break;
    case "comments":
        GenerateCommentsReport();
        break;
    case "tasks":
        GenerateTasksReport();
        break;
    default:
        Console.WriteLine("Sorry, that's not a valid option.");
        break;
}
```

First, let's inform the user that they actually can select a report in the first place, so we can say something like Console.WriteLine, Please specify a report to run, and then in parentheses just give
