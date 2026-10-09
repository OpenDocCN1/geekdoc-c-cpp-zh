Strictly speaking, when you only have one statement in a group you can omit the curly brackets. For example, you could finish the code with just

```
```
} else
    cout << "You failed :-\n";
return 0;
```
```

However, it is generally accepted that code with curly brackets throughout is easier to read. So you should always include them.

C++ doesn't care much where you put spaces in your code. However, if you space your code nicely it can be much easier to read. Different authors have different preferences for how to format curly brackets. We will write our curly brackets so that the \{ appears at the end of a line, the \} appears at the beginning of the line, and everything inside the brackets is indented. You will see different conventions in other books. It doesn't matter what convention you choose, but it does make your code more readable if you pick a convention and stick to it.

# 1.7 Exercises

1.7.1 If a company has revenue $r$ and costs $c$, then its gross profits, $g$, are given by $g = r - c$. If it has made a positive gross profit, suppose that a tax of $tg$ must be paid where $t$ is the tax rate. On the other hand, if the company has made a loss, no tax is payable. The net profit is equal to the gross profit with tax paid subtracted.

Write a program called **ProfitCalculator**, which prompts the user for the revenue, the costs, and the tax rate, and then prints out the gross profit and the net profit.

Write two versions, one using single letter variable names and one using long variable names such as **grossProfit**. Note that in C++ variable names can't contain spaces. This is why we use capitals in this way. This way of writing variable names as all one word with capitals in the middle is called *camel case*. The reason is because the word has now got a hump like a camel.

Do you prefer the code with long variable names or single letter names? Which of the two versions would be easier for someone else to understand?