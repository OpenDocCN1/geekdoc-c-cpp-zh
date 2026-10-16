```
livesLeft = startingLives;
}
```

In both methods, we have a parameter that has an identical name to the instance variable. Using the ‘this’ keyword, we access the name variable for the class. When we only say ‘name’, it is the parameter that we are referring to, So, using this.name = name, takes the name parameter value, passes to the constructor, and assigns the value to the name instance variable.

Ok, that’s enough of that for now, let’s get to our class.

# Adding Methods

What we need to sort out now is which methods we might want to be defined by the class. We could decide that we want to get the name of the current player; we might want their current score, and we might want to add points. We might also be looking for a way of making that player lose a life, lose all their lives so they are ‘killed’ off, and to determine how many lives they have left.

Using the code below, we can add a method for each of these:

```
public string GetName()
{
    return name;
}
```

```
public int GetScore()
{
    return score;
}
```