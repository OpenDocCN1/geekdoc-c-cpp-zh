# 634 Get Your ViewModel

# Test positive and negative conditions

When writing unit tests, it's important to test success as well as failure conditions. For the CanExecute method of the custom Save command, that means tests cover when the parameter is null or in addition to having a string value. These tests are shown in Listing 4-11.

# Listing 4-11: Testing the CanExecute Event Handler

```
public void Should_Not_Execute_If_Parameter_Is_Null()
{
    ICCommand command = new CustomSaveCommand("**");
    bool canExecute = command.CanExecute(null);
    Assert.IsFalse(canExecute);
}

public void Should_Not_Execute_If_Parameter_Is_Empty_String()
{
    ICCommand command = new CustomSaveCommand("**");
    bool canExecute = command.CanExecute(string.Empty);
    Assert.IsFalse(canExecute);
}

public void Should_Execute_If_Parameter_Is_Not_Empty_String()
{
    ICCommand command = new CustomSaveCommand("**");
    bool canExecute = command.CanExecute("*Test*\*");
    Assert.IsTrue(canExecute);
}
```

# Get Your ViewModel

Design patterns have been around for some time. Over time, some of the older patterns lose relevance, and new ones get created to fill needs of current development. One pattern that has gained significant traction with WPF and Silverlight is the Model-View-ViewModel pattern. Commonly referred to as "ViewModel" (although this is still much in flux, within the walls of Microsoft), this pattern is very similar to Martin Fowler's Presentation Model pattern.

![](bbox=[0.14, 0.755, 0.222, 0.808])

You can read Martin Fowler's paper on the Presentation Model pattern at http://martinfowler.com/eaaDev/PresentationModel.html.

# Who cares?

I know you're thinking. "Why can't I just sit down and start coding a WPF application using all the goodies I've learned so far? The short answer is that you can. But although that debate still rages among those who like to sit around and debate these things. Using a user interface pattern (such as ViewModel) promotes separation of concerns, cuts down on repeated code, increases testability, and reduces complexity can hurt.