```
cout << "Adding 500 to myScore\n";
myScore += 500;
cout << "myScore is: " << myScore << "\n";
cout << "mikesScore is: " << mikesScore << "\n\n";

cout << "Adding 500 to mikesScore\n";
mikesScore += 500;
cout << "myScore is: " << myScore << "\n";
cout << "mikesScore is: " << mikesScore << "\n\n";

return 0;
}
```

# Creating References

The first thing I do in main() is create a variable to hold my score.

```
int myScore = 1000;
```

Then I create a reference that refers to myScore.

```
int& mikesScore = myScore; //create a reference
```

The preceding line declares and initializes mikesScore, a reference that refers to myScore. mikesScore is an alias for myScore. mikesScore does not hold its own int value; it's simply another way to get at the int value that myScore holds.

To declare and initialize a reference, start with the type of value to which the reference will refer, followed by the reference operator (&), followed by the reference name, followed by =, followed by the variable to which the reference will refer.

> Trick
> 
> Sometimes programmers prefix a reference name with the letter "r" to remind them that they're working with a reference. A programmer might include the following lines:
> 
> int playerScore = 1000;
> int& rScore = playerScore;

One way to understand references is to think of them as nicknames. For example, suppose you've got a friend named Eugene, and he (understandably) asks to be called by a nickname—Gibby (not much of an improvement, but it's what Eugene