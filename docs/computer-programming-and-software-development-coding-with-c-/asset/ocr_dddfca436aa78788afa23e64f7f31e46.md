# Chapter 11 Working with While Statements

Let's see how we can use a while loop to accomplish another objective of our app. So let's say that the marketing team would like to pick two people to give away a free gift card to. The drink of the month was a cappuccino, so they want to pick the first two responses who selected that as their favorite product. So essentially, we want to loop through our survey responses until we find the first two people who meet this criteria. This criteria is subtly different from our previous loops. We only want to iterate through our responses until some specific criteria is met, and then we can forget about the rest of the items. With our previous loops, we specifically wanted to process every single item. There are a variety of ways to accomplish this in C#, but let's see how to do this using a while loop. Above our existing code, let's create some spaces with a few new lines and then start to type out our new loop with the while keyword.

```
static void Main(string[] args)
{
    var selectedEmails = new List<string>();
    int counter = 0;
    while (selectedEmails.Count < 2 && counter < Q1Results.Responses.Count)
    {
        var currentItem = Q1Results.Responses[counter];
        if (currentItem.FavoriteProduct == "Cappucino")
        {
            selectedEmails.Add(currentItem.EmailAddress);
            Console.WriteLine(currentItem.EmailAddress);
        }
        counter++;
    }
    GenerateTasksReport();
    GenerateCommentsReport();
```