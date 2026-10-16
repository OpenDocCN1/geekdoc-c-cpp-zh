type that is used with the index. An array offers indexers with the int type, so int types are here used as well to pass the information directly to the contained array _people. The use of the set and get accessors is very similar to properties. The get accessor is invoked when a value is retrieved, the set accessor when a (Person object) is passed on the right side.

```
public Person this[int index]
{
    get { return _people[index]; }
    set { _people[index] = value; }
}
```

With indexers, you cannot only define int types as the indexing type. Any type works, as is shown here with the DateTime struct as indexing type. This indexer is used to return every person with a specified birthday. Because multiple persons can have the same birthday, not a single Person object is returned but a list of persons with the interface IEnumerable<Person>. The Where method used makes the filtering based on a lambda expression. The Where method is defined in the namespace System.Linq:

```
public IEnumerable<Person> this[DateTime birthDay]
{
    get { return _people.Where(p => p.Birthday == birthDay); }
}
```

The indexer using the DateTime type offers retrieving person objects, but doesn’t allow you to set person objects as there’s only a get accessor but no set accessor. With C# 6, a shorthand notation exists to create the same code with an expression-bodied member (the same syntax available with properties):

```
public IEnumerable<Person> this[DateTime birthDay] =>
    _people.Where(p => p.Birthday == birthDay);
```

The Main method of the sample application creates a PersonCollection object and passes four Person objects to the constructor. With the first WriteLine method, the third element is accessed using the get accessor of the indexer with the int parameter. Within the foreach loop, the indexer with the DateTime parameter is used to pass a specified date (code file CustomIndexerSample/Program.cs):

```
static void Main()
{
    var p1 = new Person("Ayrton","Senna", new DateTime(1960, 3, 21));
    var p2 = new Person("Ronnie","Peterson", new DateTime(1944, 2, 14));
    var p3 = new Person("Jochen","Rindt", new DateTime(1942, 4, 18));
    var p4 = new Person("Francois","Cevert", new DateTime(1944, 2, 25));
    var coll = new PersonCollection(p1, p2, p3, p4);

    WriteLine(coll[2]);
```