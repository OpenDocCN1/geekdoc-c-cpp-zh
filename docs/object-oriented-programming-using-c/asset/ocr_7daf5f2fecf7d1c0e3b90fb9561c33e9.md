Object Oriented Programming using C#

We enforce the fact that Publication is non-instantiable by declaring it 'abstract':

```
public abstract class Publication
{
  // etc.
```

# 3.9 Overriding Methods

A subclass inherits the methods of itssuperclass and must therefore always provide at least that of methods, and often more. However, the implementation of a method can be changed in a subclass.

This is overriding the method.

To do this we write a new version in the subclass which replaces the inherited one.

The new method should essentially perform the same functionality that it is replacing however by changing the functionality we can improve the method and make its function more appropriate to a specific subclass.

For example, imagine a special category of magazine which has a disc attached to each copy – we can call this DiscMag and we would create a subclass of Magazine to deal with DiscMags. When a new issue of a DiscMag arrives not only do we want to update the current stock but we to check that the discs are correctly attached. Therefore we want some additional functionality in the RecNewIssue() method to remind us to do this. We achieve this by redefining RecNewIssue() in the DiscMag subclass.

Note when a new issue of Magazine arrives, as these don't have a disc we want to invoke the original RecNewIssue() method defined in the Magazine class.

![](bbox=[0.305, 0.606, 0.432, 0.796])

+   - The definition of RecNewIssue() in DiscMag overrides the inherited one.
- Magazine is not affected – it retains its original definition of RecNewIssue()
- By showing RecNewIssue() in DiscMag we are stating that the inherited method is being overridden (ie. replaced) as we do not show inherited methods in subclasses.

Download free ebooks at bookboom.com