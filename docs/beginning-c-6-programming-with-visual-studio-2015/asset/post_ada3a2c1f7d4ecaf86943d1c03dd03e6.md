
Obviously, this iterator isn't a particularly useful one, but it does show how this works in action and how simple the implementation can be. Looking at the code, you might wonder how the code knows to return string type items. In fact, it doesn't; it returns object type values. As you know, object is the base class for all types, so you can return anything from the yield statements.

However, the compiler is intelligent enough that you can interpret the returned values as whatever type you want in the context of the foreach loop. Here, the code asks for string type values, so those are the values you get to work with. You should change one of the yield lines so that it returns, say, an integer, you would get a bad cast exception in the foreach loop.

One more thing about iterators. It is possible to interrupt the return of information to the foreach loop by using the following statement:

```
yield break;
```

When this statement is encountered in an iterator, the iterator processing terminates immediately, as does the foreach loop using it.

Now it's time for a more complicated — and useful! — example. In this Try It Out, you'll implement an iterator that obtains prime numbers.

## TRY IT OUT Implementing an Iterator: Ch11Ex03

- 1. Create a new console application called Ch11Ex03 and save it in the directory C:\BegVCSharp\Chapter11.
- 2. Add a new class called Primes and modify the code in Primes.cs as follows:

```
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace Ch11Ex03
{
public class Primes
{
private long min;
private long max;
public Primes() : this(2, 100) {}
public Primes(long minimum, long maximum)
{
if (minimum < 2)
min = 2;
else
min = minimum;
max = maximum;
}
public IEnumerator GetEnumerator()
{
for (long possiblePrime = min; possiblePrime <= max; possiblePrime++)
```

can't be less than 2. This makes sense, because 2 is the lowest prime number. The interesting code is all in the GetEnumerator() method. The method signature fulfills the rules for an iterator block in that it returns an IEnumerable type:

```
public IEnumerable GetEnumerator()
{
```

To extract prime numbers between limits, you need to test each number in turn, so you start with a for loop:

```
for (long possiblePrime = min; possiblePrime <= max; possiblePrime++)
{
```

Because you don't know whether a number is prime, you first assume that it is and then check to see if it isn't. That means checking whether any number between 2 and the square root of the number to be tested is a factor. If this is true, then the number isn't prime, so you move on to the next one. If the number is indeed prime, then you pass it to the foreach loop using yield:

```
bool isPrime = true;
for (long possibleFactor = 2; possibleFactor <= (long)Math.Floor(Math.Sqrt(possiblePrime)); possibleFactor++)
{
    long remainderAfterDivision = possiblePrime % possibleFactor;
    if (remainderAfterDivision == 0)
    {
        isPrime = false;
        break;
    }
}
if (isPrime)
{
    yield return possiblePrime;
}
}
```

An interesting fact reveals itself through this code if you set the minimum and maximum limits to very big numbers. When you execute the application, the results appear one at a time, with pauses in between, rather than all at once. This is evidence that the iterator code returns results one at a time, despite the fact that there is no obvious place where the code terminates between yield calls. Behind the scenes, calling yield does interrupt the code, which resumes when another value is requested — that is, when the foreach loop using the iterator begins a new cycle.

## Iterators and Collections

Earlier you were promised an explanation of how iterators can be used to iterate over the objects stored in a dictionary-type collection without having to deal with DictionaryItem objects. In the downloadable code for this chapter, you will find the code for the next project in the DictionaryAnimals folder. Recall the collection class Animals:

```
public class Animals : DictionaryBase
{
    public void Add(string newID, Animal newAnimal)
```

```
{
    Dictionary.Add(newID, newAnimal);
}
public void Remove(string animalID)
{
    Dictionary.Remove(animalID);
}
public Animal this[string animalID]
{
    get { return (Animal)Dictionary[animalID]; }
    set { Dictionary[animalID] = value; }
}
```

You can add this simple iterator to the code to get the desired behavior:

```
public new IEnumerator GetEnumerator()
{
    foreach (object animal in Dictionary.Values)
        yield return (Animal)animal;
}
```

Now you can use the following code to iterate through the Animal objects in the collection:

```
foreach (Animal myAnimal in animalCollection)
{
    WriteLine($"New [{myAnimal.ToString()}] object added to " +
        $" custom collection, Name = {myAnimal.Name}");
}
```

## Deep Copying

Chapter 9 described how you can perform shallow copying with the System.Object .MemberwiseClone() protected method, by using a method like the GetCopy() one shown here:

```
public class Cloner
{
    public int Val;
    public Cloner(int newVal)
    {
        Val = newVal;
    }
    public object GetCopy() => MemberwiseClone();
}
```

Suppose you have fields that are reference types, rather than value types (for example, objects):

```
public class Content
{
    public int Val;
}
public class Cloner
{
    public Content MyContent = new Content();
```

```
public Cloner(int newVal)
{
    MyContent.Val = newVal;
}
public object GetCopy() => MemberwiseClone();
}
```

In this case, the shallow copy obtained through GetCopy() has a field that refers to the same object as the original object. The following code, which uses this Cloner class, illustrates the consequences of shallow copying reference types:

```
Cloner mySource = new Cloner(5);
Cloner myTarget = (Cloner)mySource.GetCopy();
WriteLine($"myTarget.MyContent.Val = {myTarget.MyContent.Val}");
mySource.MyContent.Val = 2;
WriteLine($"myTarget.MyContent.Val = {myTarget.MyContent.Val}");
```

The fourth line, which assigns a value to mySource.MyContent.Val, the Val public field of the MyContent public field of the original object, also changes the value of myTarget.MyContent.Val. That's because mySource.MyContent refers to the same object instance as myTarget.MyContent. The output of the preceding code is as follows:

```
myTarget.MyContent.Val = 5
myTarget.MyContent.Val = 2
```

To get around this, you need to perform a deep copy. You could just modify the GetCopy() method used previously to do this, but it is preferable to use the standard .NET Framework way of doing things: implement the ICloneable interface, which has the single method Clone(). This method takes no parameters and returns an object type result, giving it a signature identical to the GetCopy() method used earlier.

To modify the preceding classes, try using the following deep copy code:

```
public class Content
{
    public int Val;
}
public class Cloner : ICloneable
{
    public Content MyContent = new Content();
    public Cloner(int newVal)
    {
        MyContent.Val = newVal;
    }
    public object Clone()
    {
        Cloner clonedCloner = new Cloner(MyContent.Val);
        return clonedCloner;
    }
}
```

```
public object Clone()
{
    Cards newCards = new Cards();
    foreach (Card sourceCard in List)
    {
        newCards.Add((Card)sourceCard.Clone());
    }
    return newCards;
}
```

Finally, implement ICloneable on the Deck class. Note a slight problem here: The Deck class in Ch11CardLib has no way to modify the cards it contains, short of shuffling them. There is no way, for example, to modify a Deck instance to have a given card order. To get around this, define a new private constructor for the Deck class that allows a specific Cards collection to be passed in when the Deck object is instantiated. Here's the code to implement cloning in this class:

```
public class Deck : ICloneable
{
    public object Clone()
    {
        Deck newDeck = new Deck(cards.Clone() as Cards);
        return newDeck;
    }
    private Deck(Cards newCards)
    {
        cards = newCards;
    }
}
```

Again, you can test this with some simple client code. As before, place this code within the Main() method of a client project for testing (you can find this code in Ch11CardClient\Program.cs in the chapter's online download):

```
Deck deck1 = new Deck();
Deck deck2 = (Deck)deck1.Clone();
WriteLine($"The first card in the original deck is: {deck1.GetCard(0)}");
WriteLine($"The first card in the cloned deck is: {deck2.GetCard(0)}");
deck1.Shuffle();
WriteLine("Original deck shuffled.");
WriteLine($"The first card in the original deck is: {deck1.GetCard(0)}");
WriteLine($"The first card in the cloned deck is: {deck2.GetCard(0)}");
ReadKey();
```

The output will be similar to what is shown in Figure 11-5.

![](img/cf72ea860016d2d680fc085fc06f265a_301_0.png)

FIGURE 11-5
