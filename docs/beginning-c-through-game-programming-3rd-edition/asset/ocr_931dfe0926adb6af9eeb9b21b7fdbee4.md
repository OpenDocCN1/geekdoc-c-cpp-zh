```
if (false)
{
    cout << "This is never displayed.\n\n";
}

int score = 1000;

if (score)
{
    cout << "At least you didn't score zero.\n\n";
}

if (score >= 250)
{
    cout << "You scored 250 or more. Decent.\n\n";
}

if (score >= 500)
{
    cout << "You scored 500 or more. Nice.\n\n";

    if (score >= 1000)
    {
        cout << "You scored 1000 or more. Impressive!\n";
    }
}

return 0;
}
```

# Testing true and false

In the first if statement I test true. Because true is, well, true, the program displays the message, “This is always displayed.”

```
if (true)
{
    cout << "This is always displayed.\n\n";
}
```

In the next if statement I test false. Because false isn’t true, the program doesn’t display the message, “This is never displayed.”