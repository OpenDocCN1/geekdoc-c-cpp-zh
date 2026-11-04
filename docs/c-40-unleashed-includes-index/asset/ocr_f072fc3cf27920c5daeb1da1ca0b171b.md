![](bbox=[0.05, 0.12, 0.45, 0.2])

# FIGURE 6.17 Constructor overloads? Brain overload!

If scanning a bunch of overloads yields no suitable overload, this can be quite a frustrating experience. Object initializer expressions can help alleviate this. To illustrate this, let's first create the simplest type possible:

```
class Person
{
    public Person(string name)
    {
        Name = name;
    }

    public string Name { get; set; }
    public int Age { get; set; }
}
```

IntelliSense will show exactly one overload for this Person type, which for some reason doesn't provide an overload that also accepts an age. But still we want to initialize both the Name and Age (automatically implemented, as discussed in Chapter 11, “Fields, Properties, and Indexers”) properties. Before the C# 3.0 release, you had to write two statements to do this:

```
Person me = new Person("Bart");
me.Age = 26;
```

For creation of a new instance, this is a bit verbose, but it gets even worse if you just want to pass a Person object to a method because you need an intermediate variable:

```
Person he = new Person("John");
he.Age = 62;
LogEntry(he /* why can't I create the Person object inline? */, DateTime.Now);
```

Object initializer expressions combine calling a constructor with assignment to fields or properties, like this (also using type inference for the variable using C# 3.0 var):

```
var me = new Person("Bart") { Age = 26 };
```

and

```
LogEntry(new Person("John") { Age = 62 }, DateTime.Now);
```