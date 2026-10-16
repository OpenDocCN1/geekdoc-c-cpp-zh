So, what is it? Simply allow the name hiding to take place. Name your local variable or parameter and your instance variable exactly the same and use a specific keyword to refer back to your instance variables. That keyword is ‘this’ and is what we discuss next.

# The this Keyword

Whenever you are in a class, there is one easy way to access everything in the class – the methods and the instance variables. The ‘this’ keyword is used to reference whatever object you are in at the time. So, to carry on with the example we started, in your Player class, whenever you want you can use this.name to access the instance variable called name. The same goes for methods; by using this.MethodName(), you could call any other method belonging to the class.

Most of the time you won’t need to do this; C# will automatically assume that you are already referring to what is in the class if there isn’t anything in the block scope of method scope by the name you are referring to.

Putting it all together, if you have name hiding in operation, using the ‘this’ keyword will let you get to the instance variable that has class scope regardless of whether there is a parameter or variable with method scope that would be hiding that instance variable.

Back to the code that we added:

```
public Player(string name)
{
    this.name = name;
}
```

```
public Player(string name, int startingLives)
{
    this.name = name;
```