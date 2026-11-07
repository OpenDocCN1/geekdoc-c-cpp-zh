```
```cpp
cout << " player selects one of the objects Rock, "
     << "Paper, or Scissors." << endl;
cout << "The rules for winning the game are:" << endl;
cout << "1. If both players select the same object, it "
     << "is a tie." << endl;
cout << "2. Rock breaks Scissors: So player who selects "
     << "Rock wins." << endl;
cout << "3. Paper covers Rock: So player who selects "
     << "Paper wins." << endl;
cout << "4. Scissors cuts Paper: So player who selects "
     << "Scissors wins." << endl << endl;
cout << "Enter R or r to select Rock, P or p to select "
     << "Paper, and S or s to select Scissors." << endl;
}
```
```

**Function validSelection**: This function checks whether a player's selection is valid.

if selection is 'R' or 'r' or 'S' or 's' or 'P' or 'p', then
    it is a valid selection;
otherwise the selection is invalid.

Let’s use a switch statement to check for the valid selection. The definition of this function is:

```
```cpp
bool validSelection(char selection)
{
    switch (selection)
    {
    case 'R':
    case 'r':
    case 'P':
    case 'p':
    case 'S':
    case 's':
        return true;
    default:
        return false;
    }
}
```
```

**Function retrievePlay**: Because the enumeration type cannot be read directly, this function converts the entered choice (R, r, P, p, S, or s) and returns the appropriate object type. This function thus has one parameter, of type char. It is a value-returning function, and it returns a value of type objectType. In pseudocode, the algorithm of this function is:

```
```text
if selection is 'R' or 'r'
    return ROCK;

if selection is 'P' or 'p'
    return PAPER;

if selection is 'S' or 's'
    return SCISSORS;
```
```