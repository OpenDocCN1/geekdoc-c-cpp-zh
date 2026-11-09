```
```java
public int getFee() {
    int fee = 0;
    if (getType() == REGULAR)
        fee += applyGracePeriod(150, days, 3);
    else
        fee += getDays() * 100;
    return fee;
}

public int getPoints() {
    int points = 0;
    if (getType() == REGULAR)
        points += applyGracePeriod(1, days, 3);
    else
        points++;
    return points;
}

private static int applyGracePeriod(int amount, int days, int grace)
{
    if (days > grace)
        return amount + amount * (days - grace);
    return amount;
}
```
```

Those ugly if statements need to be gotten rid of. Every new type of video is going to mean another clause in those statements. Let’s head that off with some subclasses and polymorphism.

First, there’s the abstract `Movie` class. It’s got the `applyGracePeriod` utility and two abstract functions to get the fee and the points.

[Click here to view code image](#)

```
```java
public abstract class Movie {
    private String title;

    public Movie(String title) {
```
```