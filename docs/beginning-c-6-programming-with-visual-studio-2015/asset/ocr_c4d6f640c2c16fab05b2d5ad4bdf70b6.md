```
assigned[destCard] = true;
newDeck[destCard] = cards[i];
}
newDeck.CopyTo(cards, 0);
}
}
```

The last line of this method uses the CopyTo() method of the System.Array class (used whenever you create an array) to copy each of the cards in newDeck back into cards. This means you are using the same set of Card objects in the same cards object, rather than creating any new instances. If you had instead used cards = newDeck, then you would be replacing the object instance referred to by cards with another. This could cause problems if code elsewhere were retaining a reference to the original cards instance — which wouldn’t be shuffled!

That completes the class library code.

# A Client Application for the Class Library

To keep things simple, you can add a client console application to the solution containing the class library. To do so, simply right-click on the solution in Solution Explorer and select Add ▸ New Project. The new project is called Ch10CardClient.

To use the class library you have created from this new console application project, add a reference to your Ch10CardLib class library project. You can do that through the Projects tab of the Reference Manager dialog box, as shown in Figure 10-12.

![](bbox=[0.1, 0.71, 0.88, 0.81])

FIGURE 10-12

Select the project and click OK to add the reference.

Because this new project is the second one you've created, you also need to specify that it is the startup project for the solution, meaning the one that is executed when you click Run. To do so, simply right-click on the project name in the Solution Explorer window and select the Set as StartUp Project menu option.