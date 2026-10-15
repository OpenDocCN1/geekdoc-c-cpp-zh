```
for ( int i = 1;  i < 6;  i++ )
{
    WakeUp();
    GoToWork();
    MakeDinner();
    Relax();
}
```

![](bbox=[0.56, 0.12, 0.64, 0.17])

![](bbox=[0.55, 0.18, 0.65, 0.23])

![](bbox=[0.56, 0.24, 0.64, 0.28])

![](bbox=[0.55, 0.3, 0.65, 0.35])

That would make days So, first we initialize an integer as 1 to represent Monday. Then we check if that integer is less than 6 to ensure we have not reached the weekend or Saturday yet. We also increment the i variable by one every time the day's activities repeat. So after they run 5 times, i will become 6, which means that the loop condition will evaluate to false and the loop will stop. Let's see how to apply these types of concepts to our own app next.

Let's explore how to use a standard for loop to process a set of data in our app. For this chapter, there are some changes to our Q1Results dataset, so let's revisit that file for a moment. Now up until this point, we have worked with aggregated scores and data. In other words, these were the total average scores for all of the people who responded to the survey. However, this type of data is not all that useful when working with loops and iterations.