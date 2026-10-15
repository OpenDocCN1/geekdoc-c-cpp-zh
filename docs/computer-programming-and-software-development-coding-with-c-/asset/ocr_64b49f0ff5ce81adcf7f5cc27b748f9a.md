because that condition check happens after the loop runs. With a standard while loop, that check happens before the loop runs.

```
do {
    // Statements to execute
}
while (someValue == true)
```

This type of loop is useful in certain niche situations, but it's fairly rare to see in applications, so we will not spend a lot of time with it in this book. One other feature of loops to be aware of is the break keyword. You might remember this word from our switch statements. Break allows us to short circuit a loop and jump out of that statement and back into normal program flow, regardless of whether the loop condition has been reached or not.

```
foreach (var customer in mailingList)
{
    break;
    SendEmail(customer);
}
```