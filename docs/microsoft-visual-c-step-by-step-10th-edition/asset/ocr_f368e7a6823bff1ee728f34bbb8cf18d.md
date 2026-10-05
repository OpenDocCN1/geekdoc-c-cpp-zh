generates a warning message informing you that Horse.Talk hides the inherited method Mammal.Talk:

Click here to view code image

```
class Mammal
{
  ...
  public void Talk() // assume that all mammals can talk
  {
    ...
  }
}
```

```
class Horse : Mammal
{
  public void Talk() // horses talk in a different way from other mammals!
  {
    ...
  }
}
```

Although your code will compile and run, you should take this warning seriously. If another class derives from Horse and calls the Talk method, it might expect the method implemented in the Mammal class to be called. However, the Talk method in Horse hides the Talk method in the Mammal class, and the Horse.Talk method will be called instead.

Most of the time, such a coincidence is best a source of confusion, and you should consider renaming methods to avoid clashes. However, if you're sure that you want the two methods to have the same signature, hiding the Mammal.Talk method, you can silence the warning by using the new keyword, as follows:

Click here to view code image

```
class Mammal
{
  ...
  public void Talk()
  {
    ...
  }
}
```