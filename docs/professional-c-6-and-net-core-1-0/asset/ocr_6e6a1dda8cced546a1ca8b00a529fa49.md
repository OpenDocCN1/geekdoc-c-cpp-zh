If you are finished adding elements to the list and don’t want to add any more, you can get rid of the unneeded capacity by invoking the TrimExcess method; however, because the relocation takes time, TrimExcess has no effect if the item count is more than 90 percent of capacity:

```
intList.TrimExcess();
```

# Collection Initializers

You can also assign values to collections using collection initializers. The syntax of collection initializers is similar to array initializers, which are explained in Chapter 7. With a collection initializer, values are assigned to the collection within curly brackets at the time the collection is initialized:

```
var intList = new List<int>() {1, 2};
var stringList = new List<string>() {"one","two"};
```

> NOTE Collection initializers are not reflected within the IL code of the compiled assembly. The compiler converts the collection initializer to invoke the Add method for every item from the initializer list.

# Adding Elements

You can add elements to the list with the Add method, shown in the following example. The generic instantiated type defines the parameter type of the Add method:

```
var intList = new List<int>();
intList.Add(1);
intList.Add(2);
```

```
var stringList = new List<string>();
stringList.Add("one");
stringList.Add("two");
```

The variable racers is defined as type List<Racer>. With the new operator, a new object of the same type is created. Because the class List<T> was instantiated with the concrete class Racer, now only Racer objects can be added with the Add method. In the following sample code, five Formula-1 racers are created and added to the collection. The first three are added using the collection initializer, and the last two are added by explicitly invoking the Add method (code file ListSamples/Program.cs):

```
var graham = new Racer(7,"Graham","Hill","UK", 14);
var emerson = new Racer(13,"Emerson","Fittipaldi","Brazil", 14);
var mario = new Racer(16,"Mario","Andretti","USA", 12);
```

```
var racers = new List<Racer>(20) {graham, emerson, mario};
```

```
racers.Add(new Racer(24,"Michael","Schumacher","Germany", 91));
```