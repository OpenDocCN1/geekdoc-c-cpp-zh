```
cout << "\nYou trade your sword for a battle axe.";
inventory[0] = "battle axe";
cout << "\nYour items:\n";
for (int i = 0; i < numItems; ++i)
{
    cout << inventory[i] << endl;
}

cout << "\nThe item name '" << inventory[0] << "' has ";
cout << inventory[0].size() << " letters in it.\n";

cout << "\nYou find a healing potion.";
if (numItems < MAX_ITEMS)
{
    inventory[numItems++] = "healing potion";
}
else
{
    cout << "You have too many items and can't carry another.";
}
cout << "\nYour items:\n";
for (int i = 0; i < numItems; ++i)
{
    cout << inventory[i] << endl;
}

return 0;
}
```

# Creating Arrays

It’s often a good idea to define a constant for the number of elements in an array. That’s what I did with MAX_ITEMS, which represents the maximum number of items the hero can carry:

```
const int MAX_ITEMS = 10;
```

You declare an array much the same way you would declare any variable you’ve seen so far: You provide a type followed by a name. In addition, your compiler must know the size of the array so it can reserve the necessary memory space. You can provide that information following the array name, surrounded by square brackets. Here’s how I declare the array for the hero’s inventory:

```
string inventory[MAX_ITEMS];
```