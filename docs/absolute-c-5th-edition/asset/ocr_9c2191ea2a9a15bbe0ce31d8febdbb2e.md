# Programming Projects

40. This solution remembers the highest score and name seen so far and outputs it after
the loop is over.

```
fstream inputStream;

inputStream.open("player.txt");
int numScores;
int highScore = -1;
string highName = ""
inputStream >> numScores;
for (int i = 0; i < numScores; i++))
{
    string name;
    int score;
    inputStream >> name;
    inputStream >> score;
    if (score > highScore)
{
        highScore = score;
        highName = name;
    }
}
inputStream.close();
cout << highName << " has the high score of "
" << highScore << endl;
```

# Programming Projects

Visit www.myprogramminglab.com to complete select exercises online and get instant
feedback.

+   1. It is difficult to make a budget that spans years, because prices are not
stable. If your company needs 200 pencils per year, you cannot simply use this
year's price as the cost of pencils two years from now. Because of inflation the
cost is likely to be higher than it is today. Write a program to gauge the expected
c of an item in a specified number of years. The program asks for the cost of
item, the number of years from now that the item will be purchased, and the
rate of inflation. The program outputs the estimated cost of the item after
t specified period. Have the user enter the cost as a percentage, such
as 5.6 (percent). Your program should then convert the percentage to a decimal
fraction, and should use a loop to estimate the price adjusted for
inflation. (Hint: Use a loop).

![](bbox=[0.068, 0.563, 0.181, 0.581])