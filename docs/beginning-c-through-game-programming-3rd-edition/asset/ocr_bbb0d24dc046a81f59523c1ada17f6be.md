![](bbox=[0.115, 0.105, 0.835, 0.385])

# Figure 1.6

Each variable is altered in a different way.

```
int main()
{
    unsigned int score = 5000;
    cout << "score: " << score << endl;

    //altering the value of a variable
    score = score + 100;
    cout << "score: " << score << endl;

    //combined assignment operator
    score += 100;
    cout << "score: " << score << endl;

    //increment operators
    int lives = 3;
    ++lives;
    cout << "lives: "   << lives << endl;

    lives = 3;
    lives++;
    cout << "lives: "   << lives << endl;
```