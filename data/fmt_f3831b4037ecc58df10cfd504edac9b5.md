
假设市场部门想知道所有四个主要类别的总体平均分。目前我们只有单个分数，如果能有一个总体平均值来跟踪，那就太好了。那么，让我们切换回`Program.cs`中的`Main`方法。在现有计算的下方，我们先声明另一个变量。这个变量也需要存储一个小数值，所以让我们再次使用`double`数据类型，并将其命名为`overallScore`。要计算总体得分，我们必须将四个单独分数相加，然后除以总类别数，就像任何其他标准数学平均值一样。因此，在`overallScore`的分号前，让我们开始访问不同的类别。让我们输入`Q1Results.ServiceScore`，然后使用加号运算符加上`Q1.CoffeeScore`，再加`Q1.FoodScore`，最后加上`Q1.PriceScore`。我们还必须将这些项目的总和除以`4`，才能得到平均值。C#遵循数学运算顺序，就像任何其他编程语言一样。因此在这种情况下，除法实际上会先执行，然后其他所有分数才会相加。这肯定不是我们想要的结果。我们可以通过简单地将加法括在一组括号中来修复这个问题，这将确保分数在除法之前相加。最后，让我们复制一条`Console.WriteLine`语句并粘贴到底部。我们可以将标签改为 Overall Score，然后传入匹配的变量。一切就绪后，让我们运行应用，看看会得到什么结果。

```
Response Percentage: 0.65
Unanswered Surveys: 175
Overall Score: 7.5
```

We should quickly see the output for all three statement calculations printed in our console. This gives us a good idea of how to work with simple statements and expressions; however, there are some larger concepts at work here as well.

```
// Calculated Values:
double responseRate = QIResults.NumberResponded / QIResults.NumberSurveyed;
double unansweredCount = QIResults.NumberSurveyed - QIResults.NumberResponded;
double overallScore = (QIResults.ServiceScore + QIResults.CoffeeScore + QIResults.FoodScore + QIResults.

Console.WriteLine($"Response Percentage: {responseRate}");
Console.WriteLine($"Unanswered Surveys: {unansweredCount}");
Console.WriteLine($"Overall Score: {overallScore}");
```

What we've done so far is created three different statements that produce calculated values. In fact, at the top of our statements here, I'll just add in a comment that groups these as calculated values. As we'll see throughout the book, arithmetic expressions like these can impact program flow in a really big way by helping us make decisions or triggering branching paths and so on. For example, maybe if the response rate of our survey is above a certain percentage, we take one action versus another. Next, let's explore statements that use other types of expressions and build on these concepts.

### Chapter 5 How to Make Logical Comparisons with Statements

Let's look at how to write statements that perform different types of logical comparisons. So let's say the marketing team sent over some additional questions for us about the survey data. They would like to know if the coffee quality score was higher than the food score since that's really the heart of the business. They would also like to know whether customers are likely to recommend the Company to their friends and family. Finally, the director personally would like to know if the least favorite product is granola and the favorite product is cappuccino since those are her personal preferences as well. You may have noticed that all of these questions involve comparisons, and you'd be right. Comparisons can be done using expressions, and they're critical building blocks of program flow and statements. For this chapter, I have stubbed out a bit of starting code for us below our previous work.

```
bool higherCoffeeScore;
bool customersRecommend;
bool noGranolaYesCappucino;

Console.WriteLine($"Coffee Score Higher Than Food: {higherCoffeeScore}");
Console.WriteLine($"Customers Would Recommend Us: {customersRecommend}");
Console.WriteLine($"Hate Granola, Love Cappucino: {noGranolaYesCappucino}");
```

We simply have a few variables declared to highlight the task objectives and a few lines to print out the results of those variables. Visual Studio will complain at the moment that our variables have no value using these red squiggly lines, but that's okay for us at the moment. By now, we already know how to write these types of statements, so let's focus instead on writing statements with new types of expressions. So first, let's check if the coffee score is higher than the food score.

```
bool higherCoffeeScore = QIResults.CoffeeScore > QIResults.FoodScore;
bool customersRecommend = QIResults.WouldRecommend >= 7;
bool noGranolaYesCappucino = QIResults.LeastFavoriteProduct == "Granola" && QIResults.FavoriteProduct == "Cappuccino";
```

For this, we can simply type an equal sign out and then `QIResults.CoffeeScore` and then use the greater than comparison operator and add `QIResults.FoodScore` on the other side. The greater than operator ensures this expression will evaluate to `true` or `false` depending on if the coffee score was indeed higher. Comparison operators are a powerful tool for influencing program flow, as we'll see later. Next, let's check if the customers are likely to recommend the Company to their friends. We're going to say that a score of 7 or higher means yes since it's ranked out of 10. For this, we can use another familiar type of comparison operator called the greater than or equal to. So for this statement, let's add an equals after our `WouldRecommend` variable and then say `QIResults.RecommendScore` is greater than or equal to 7. Finally, let's check the least and most popular products. So after our third variable, let's access the `QIResults.LeastFavorite` product and then add the double equals operator, which performs comparison and not assignment like our single equals operator, and then just type out a string of `Granola`. We also want to verify that the most popular product is `Cappuccino`. To check that two conditions are true, we can use the double ampersand sign, which represents and logic. After that, we can type out another comparison, so `QIResults.FavoriteProduct == Cappuccino`. Now we have a statement that performs multiple comparison checks at once. So if both sides of an and operator are true, the statement will assign a true value to our variable. However, if one or both sides of an and comparison are false, the statement will assign a value of false to the variable. We already have our `Console.WriteLine` statements defined at the bottom of our method that print out these variables, so let's just run the app and see what happens. After a moment, we should see our complete result set, including our new comparison values down at the bottom.

```
Response Percentage: 0.65
Unanswered Surveys: 175
Overall Score: 7.5
Coffee Score Higher Than Food: True
Customers Would Recommend Us: False
Hate Granola, Love Cappuccino: True
```
