# Using the Tools of the Trade 539

before it is performed and lets you select or deselect any of the items that would be renamed.

+   **Extract Method:** Perhaps you've written a block of code and then thought "oh boy, I am going to need this over there." If so, Extract Method is for you. It will take a highlighted block of code, move it to a method, extract all the variables, make them parameters, and then you'll be ready to use code.

+   **Encapsulate Field:** In a similar vein as extracting a method, Encapsulate Field takes a private variable and makes it a public field. For instance, take a line of code like private string _theValue; highlight it in designer and select Encapsulate Field from the Refactor menu.

Visual Studio asks you to name the new property and create a new property by your selections:
```cs
public string TheValue
{
    get { return _theValue; }
    set { _theValue = value; }
}
```

+   **Extract Interface:** Extract Interface takes a set of method signatures and makes an interface for you. Interfaces are vital to contract driven development.

If you are working on a project that suddenly has more than one programmer (as in, they you get help?), extracting interfaces to common classes in your project decreases barriers to the new folks' entry pattern and lets you make your code easier to change in the future.

+   **Remove Parameters:** This is the safe way to get excess parameters out of methods. In honesty, use this refactoring to the last.

+   **Reorder Parameters:** Being able to change the order of parameters is significantly handier. Sometimes, you just need to switch the order of two parameters. If you do this, all the places you call that method must have the parameter order changed, or you will send the wrong stuff.

This simple tool enables you to change the parameter order and finds all places that call the method in question and switches the parameter order sent in.

![](bbox=[0.935, 0.69, 0.965, 0.85])