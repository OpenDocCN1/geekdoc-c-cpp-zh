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