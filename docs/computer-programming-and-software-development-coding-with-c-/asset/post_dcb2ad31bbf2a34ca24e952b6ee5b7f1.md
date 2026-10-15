
Response Percentage: 0.65
Unanswered Surveys: 175
Overall Score: 7.5

We should quickly see the output for all three statement calculations printed in our console. This gives us a good idea of how to work with simple statements and expressions; however, there are some larger concepts at work here as well.

// Calculated Values:
double responseRate = QIResults.NumberResponded / QIResults.NumberSurveyed;
double unansweredCount = QIResults.NumberSurveyed - QIResults.NumberResponded;
double overallScore = (QIResults.ServiceScore + QIResults.CoffeeScore + QIResults.FoodScore + QIResults.

Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
Console.WriteLine($"Overall Score: {overallScore}");

What we've done so far is created three different statements that produce calculated values. In fact, at the top of our statements here, I'll just add in a comment that groups these as calculated values. As we'll see throughout the book, arithmetic expressions like these can impact program flow in a really big way by helping us make decisions or triggering branching paths and so on. For example, maybe if the response rate of our survey is above a certain percentage, we take one action versus another. Next, let's explore statements that use other types of expressions and build on these concepts.

# Chapter 5 How to Make Logical Comparisons with Statements

Let's look at how to write statements that perform different types of logical comparisons. So let's say the marketing team sent over some additional questions for us about the survey data. They would like to know if the coffee quality score was higher than the food score since that's really the heart of the business. They would also like to know whether customers are likely to recommend the Company to their friends and family. Finally, the director personally would like to know if the least favorite product is granola and the favorite product is cappuccino since those are her personal preferences as well. You may have noticed that all of these questions involve comparisons, and you'd be right. Comparisons can be done using expressions, and they're critical building blocks of program flow and statements. For this chapter, I have stubbed out a bit of starting code for us below our previous work.

```
bool higherCoffeeScore;
bool customersRecommend;
bool noGranolaYesCappucino;

Console.WriteLine($"Coffee Score Higher Than Food: {higherCoffeeScore}");
Console.WriteLine($"Customers Would Recommend Us: {customersRecommend}");
Console.WriteLine($"Hate Granola, Love Cappucino: {noGranolaYesCappucino}");
```

We simply have a few variables declared to highlight the task objectives and a few lines to print out the results of those variables. Visual Studio will complain at the moment that our variables have no value using these red squiggly lines, but that's okay for us at the moment. By now, we already know how to write these types of statements, so let's focus instead on writing statements with new

types of expressions. So first, let's check if the coffee score is higher than the food score.

```
bool higherCoffeeScore = QIResults.CoffeeScore > QIResults.FoodScore;
bool customersRecommend = QIResults.WouldRecommend >= 7;
bool noGranolaYesCappucino = QIResults.LeastFavoriteProduct == "Granola" && QIResults.FavoriteProduct == "Cappuccino";
```

For this, we can simply type an equal sign out and then QIResults.CoffeeScore and then use the greater than comparison operator and add QIResults.FoodScore on the other side. The greater than operator ensures this expression will evaluate to true or false depending on if the coffee score was indeed higher. Comparison operators are a powerful tool for influencing program flow, as we'll see later. Next, let's check if the customers are likely to recommend the Company to their friends. We're going to say that a score of 7 or higher means yes since it's ranked out of 10. For this, we can use another familiar type of comparison operator called the greater than or equal to. So for this statement, let's add an equals after our WouldRecommend variable and then say QIResults.RecommendScore is greater than or equal to 7. Finally, let's check the least and most popular products. So after our third variable, let's access the QIResults.LeastFavorite product and then add the double equals operator, which performs comparison and not assignment like our single equals operator, and then just type out a string of Granola. We also want to verify that the most popular product is cappuccino. To check that two conditions are true, we can use the double ampersand sign, which represents and logic. After that, we can type out another comparison, so QIResults.FavoriteProduct == Cappuccino. Now we have a statement that performs multiple comparison checks at once. So if both sides of an and operator are true, the statement

will assign a true value to our variable. However, if one or both sides of an and comparison are false, the statement will assign a value of false to the variable. We already have our Console.WriteLine statements defined at the bottom of our method that print out these variables, so let's just run the app and see what happens. After a moment, we should see our complete result set, including our new comparison values down at the bottom.

```
Response Percentage: 0.65
Unanswered Surveys: 175
Overall Score: 7.5
Coffee Score Higher Than Food: True
Customers Would Recommend Us: False
Hate Granola, Love Cappuccino: True
```

All of these variables hold true or false values since the expressions we used evaluate to Booleans instead of numbers like our previous work. Back in our code, I want to reiterate that the statements and expressions we have written here are another core building block for program flow. Later, we'll see how true and false computations can influence flow in a big way. So just like we labeled this first set of statements as calculated values, we can also label the second set as logical comparisons. Together, these are two essential building blocks for manipulating program flow, as we'll see in a moment. As a side note, I also do want to mention that there are better ways to check for equality between strings and C# than this simplistic approach. I have chosen this approach because it more clearly depicts different types of operators and expressions. Next, let's revisit our work thus far more specifically in the context of program flow.

We have spent quite a bit of time working with statements in the last several chapters. As we start to transition into the next module, let's return our focus specifically to program flow. So, let's make sure we understand the current flow of our app statements and how that

will evolve ahead. We now have a dozen or so statements that execute in order from top to bottom without any variability. Our program flow is entirely sequential, and we can actually prove that using the Visual Studio debugging tools. I am going to assume you have at least basic familiarity with debugging in an IDE like Visual Studio. As a quick reminder, the debugger allows us to step through our code one line at a time as it executes. It also lets us inspect the state of variables and other context data along the way. We'll be using this tool throughout the book to walk through our program flow, so let's place a breakpoint to the left of line 10, which will tell the debugger where to initially pause so we can inspect our code.

![](img/0155736aec718cf18821e9f10a5d308d_535_0.png)

Next, let's run our app, and after this launches, we should land on the line of code where we set that point. This yellow highlighted bar indicates the next line of code that will be executed in our program flow.

![](img/0155736aec718cf18821e9f10a5d308d_535_1.png)

At the top of Visual Studio, we use our debugging controls to step through our app one line at a time. So as I click the step over arrow, we will slowly move from one line to the next in order.

![](img/0155736aec718cf18821e9f10a5d308d_535_2.png)
