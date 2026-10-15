Single line statements are simple. They're just one line of code that executes a task and ends with a semicolon. Each of the lines here is a statement, and together they form the logic of a complete function. Multiline or composite statements are a bit more interesting.

```
if (todayIsMonday)
{
    sendReminderEmails();
    submitTimesheets();
    orderMoreCoffee();
```

These statements utilize additional embedded statements or blocks of code to execute that are defined with opening and closing curly braces. Curly braces are used throughout C# to mark the beginning and end of scopes or definitions, such as a method or a class. These blocks of code can contain a list of nested statements to perform additional logic. Composite statements usually leverage special C# keywords, which is something we'll get into later. There are many types of statements. For this book, we are interested in the most essential statements that can significantly impact program flow. First, we will focus mostly on simpler types of statements and related expressions. Next, we will explore how those concepts tie into selection statements to impact program flow and then the same for iteration statements later on. Finally, we will bring together many of these concepts to look at additional ways to manage flow. So, let's start by looking a little more closely at some single line, simpler statements.