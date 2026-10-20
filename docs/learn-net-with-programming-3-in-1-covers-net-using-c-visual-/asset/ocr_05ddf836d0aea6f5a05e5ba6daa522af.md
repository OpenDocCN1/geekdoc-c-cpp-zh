have their own implementation of an animal sound (the pig oinks, and the cat meows, etc.):

# Example:

```
Class Animal // Base class (parent)
{
	Public void animalsound()
	{
		Console.writeline("The animal makes a sound");
	}
}

Class Pig : Animal // Derived class (child)
{
	Public void animalsound()
	{
		Console.writeline("The pig says: wee wee");
	}
}

Class Dog : Animal // Derived class (child)
{
```