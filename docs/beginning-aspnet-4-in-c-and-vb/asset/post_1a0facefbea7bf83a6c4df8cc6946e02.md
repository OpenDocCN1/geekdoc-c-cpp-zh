
```
{
    int compare = this.LastName.CompareTo(other.LastName);
    if (compare == 0)
        return this.FirstName.CompareTo(other.FirstName);
    return compare;
}
```

## Creating Lists

You can create list objects by invoking the default constructor. With the generic class List<T>, you must specify the type for the values of the list with the declaration. The code shows how to declare a List<T> with int and a list with Racer elements. ArrayList is a non-generic list that accepts any Object type for its elements.

Using the default constructor creates an empty list. As soon as elements are added to the list, the capacity of the list is extended to allow four elements. If the fifth element is added, the list is resized to allow eight elements. If eight elements are not enough, the list is resized again to contain 16 elements. With every resize the capacity of the list is doubled.

```
var intList = new List<int>();
var racers = new List<Racer>();
```

If the capacity of the list changes, the complete collection is reallocated to a new memory block. With the implementation of List<T>, an array of type T is used. With reallocation, a new array is created, and Array.Copy() copies the elements from the old array to the new array. To save time, if you know the number of elements in advance, that will be in the list; you can define the capacity with the constructor. Here a collection with a capacity of 10 elements is created. If the capacity is not large enough for the elements added, the capacity is resized to 20 and 40 elements — doubled again.

```
List<int> intList = new List<int>(10);
```

You can get and set the capacity of a collection by using the Capacity property:

```
intList.Capacity = 20;
```

The capacity is not the same as the number of elements in the collection. The number of elements in the collection can be read with the Count property. Of course, the capacity is always larger or equal to the number of items. As long as no element was added to the list, the count is 0.

```
Console.WriteLine(intList.Count);
```

If you are finished adding elements to the list and don't want to add any more elements, you can get rid of the unused capacity by invoking the TrimExcess() method. However, because the relocation takes time, TrimExcess() does nothing if the item count is more than 90 percent of capacity.

```
intList.TrimExcess();
```

## Collection Initializers

You can also assign values to collections using collection initializers. The syntax of collection initializers is similar to array initializers, which were explained in Chapter 6. With a collection initializer, values are assigned to the collection within curly brackets at the initialization of the collection:

```
var intList = new List<int>() {1, 2};
var stringList = new List<string>() {"one", "two"};
```

## Inserting Elements

You can insert elements at a specified position with the Insert() method:

```
racers.Insert(3, new Racer(6, "Phil", "Hill", "USA", 3));
```

The method InsertRange() offers the capability to insert a number of elements, similarly to the AddRange() method shown earlier.

If the index set is larger than the number of elements in the collection, an exception of type ArgumentOutOfRangeException is thrown.

## Accessing Elements

All classes that implement the IList and IList<T> interface offer an indexer, so you can access the elements by using an indexer and passing the item number. The first item can be accessed with an index value 0. By specifying racers[3], you will access the fourth element of the list:

```
Racer r1 = racers[3];
```

Getting the number of elements with the Count property, you can do a for loop to iterate through every item in the collection, and use the indexer to access every item:

```
for (int i = 0; i < racers.Count; i++)
{
    Console.WriteLine(racers[i]);
}
```

> Indexed access to collection classes is available with ArrayList, StringCollection, and List<T>.

Because List<T> implements the interface IEnumerable, you can iterate through the items in the collection using the foreach statement as well:

```
foreach (Racer r in racers)
{
    Console.WriteLine(r);
}
```

> How the foreach statement is resolved by the compiler to make use of the IEnumerable and IEnumerator interfaces is explained in Chapter 6.

Instead of using the foreach statement, the List<T> class also offers a ForEach() method that is declared with an Action<T> parameter:

```
public void ForEach(Action<T> action);
```

The implementation of ForEach() is shown next. ForEach() iterates through every item of the collection and invokes the method that is passed as parameter for every item.

```
public class List<T>: IList<T>
{
    private T[] items;
    //...
    public void ForEach(Action<T> action)
```

```
public class FindCountry
{
    public FindCountry(string country)
    {
        this.country = country;
    }
    private string country;
    public bool FindCountryPredicate(Racer racer)
    {
        if (racer == null) throw new ArgumentNullException("racer");
        return racer.Country == country;
    }
}
```

With the FindIndex() method, you can create a new instance of the FindCountry() class, pass a country string to the constructor, and pass the address of the Find method. After FindIndex() completes successfully, index2 contains the index of the first item where the Country property of the racer is set to Finland.

```
int index2 = racers.FindIndex(new FindCountry("Finland").FindCountryPredicate);
```

Instead of creating a class with a handler method, you can use a Lambda expression here as well. The result is exactly the same as before. Now the Lambda expression defines the implementation to search for an item where the Country property is set to Finland.

```
int index3 = racers.FindIndex(r => r.Country == "Finland");
```

Similar to the IndexOf() method, with the FindIndex() method, you can also specify the index where the search should start and the count of items that should be iterated through. To do a search for an index beginning from the last element in the collection, you can use the FindLastIndex() method.

The method FindIndex() returns the index of the found item. Instead of getting the index, you can also get directly to the item in the collection. The Find() method requires a parameter of type Predicate<T>, much as the FindIndex() method. The Find() method here is searching for the first racer in the list that has the FirstName property set to Niki. Of course, you can also do a FindLast() to find the last item that fulfills the predicate.

```
Racer racer = racers.Find(r => r.FirstName == "Niki");
```

To get not only one, but all items that fulfill the requirements of a predicate, you can use the FindAll() method. The FindAll() method uses the same Predicate<T> delegate as the Find() and FindIndex() methods. The FindAll() method does not stop when the first item is found but instead iterates through every item in the collection and returns all items where the predicate returns true.

```
List<Racer> bigWinners = racers.FindAll(r => r.Wins > 20);
```

With the FindAll() method invoked here, all racer items are returned where the property Wins is set to more than 20. All racers who won more than 20 races are referenced from the bigWinners list.

Iterating through the variable bigWinners with a foreach statement gives the following result:

```
foreach (Racer r in bigWinners)
{
    Console.WriteLine("{0}:A", r);
}
```

Michael Schumacher, Germany Wins: 91
Niki Lauda, Austria Wins: 25
Alain Prost, France Wins: 51

The result is not sorted, but this is done next.

## Sorting

The List<T> class allows sorting its elements by using the Sort() method. Sort() uses the quick sort algorithm where all elements are compared until the complete list is sorted.

You can use several overloads of the Sort() method. The arguments that can be passed are a generic delegate Comparison<T>, the generic interface IComparer<T>, and a range together with the generic interface IComparer<T>:

```
public void List<T>.Sort();
public void List<T>.Sort(Comparison<T>);
public void List<T>.Sort(IComparer<T>);
public void List<T>.Sort(Int32, Int32, IComparer<T>);
```

Using the Sort() method without arguments is possible only if the elements in the collection implement the interface IComparable.

The class Racer implements the interface IComparable<T> to sort racers by the last name:

```
racers.Sort();
racers.ForEach(Console.WriteLine);
```

If you need to do a sort other than the default supported by the item types, you need to use other techniques, for example passing an object that implements the IComparer<T> interface.

The class RacerComparer implements the interface IComparer<Racer> for Racer types. This class allows you to sort either by the first name, last name, country, or number of wins. The kind of sort that should be done is defined with the inner enumeration type CompareType. The CompareType is set with the constructor of the class RacerComparer. The interface IComparer<Racer> defines the method Compare that is required for sorting. In the implementation of this method, the CompareTo() method of the String and int types is used.

```
public class RacerComparer: IComparer<Racer>
{
    public enum CompareType
    {
        FirstName,
        LastName,
        Country,
        Wins
    }

    private CompareType compareType;
    public RacerComparer(CompareType compareType)
    {
        this.compareType = compareType;
    }

    public int Compare(Racer x, Racer y)
    {
        if (x == null) throw new ArgumentNullException("x");
        if (y == null) throw new ArgumentNullException("y");

        int result;
        switch (compareType)
        {
            case CompareType.FirstName:
                return x.FirstName.CompareTo(y.FirstName);
            case CompareType.LastName:
                return x.LastName.CompareTo(y.LastName);
            case CompareType.Country:
                if ((result = x.Country.CompareTo(y.Country)) == 0)
                    return x.LastName.CompareTo(y.LastName);
```
