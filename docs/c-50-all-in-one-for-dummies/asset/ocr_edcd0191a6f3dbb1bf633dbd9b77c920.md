```
ArrayList ints = new ArrayList();  // An old-fashioned list of Objects
int myInt = (int)ints[0];           // Extract the first int in the list.
```

It’s as though your ints were hidden inside Easter eggs. If you don’t cast, you create errors because, for instance, Object doesn’t support the + operation or other methods, properties, and operators that you expect on ints. You can work with these limitations, but this kind of code is error-prone, and it’s just plain tedious to do all that casting. (Besides, as I discuss in Book I, Chapter 8, working with Easter eggs adds some processing overhead because of the “boxing” phenomenon. Too much boxing slows your program.)

And, if the collection happens to contain objects of more than one type — pomegranates and basketballs, say — the problem becomes tougher. Somehow, you have to detect that the object you fish out is a pomegranate or a basketball so that you can cast it correctly.

With those limitations on the older, nongeneric collections, the newer generic ones are a gale of fresh air. You never have to cast, and you always know what you’re getting because you can put only one type into any given collection. But you still see the older collections occasionally, in code that other people write — and sometimes you may even have a legitimate reason to stick apples and oranges in the same collection.

![](bbox=[0.13, 0.58, 0.19, 0.71])

The nongeneric collections are found in the System.Collections and System.Collections.Specialized namespaces. The Specialized collections are interesting, sometimes useful, oddball collections, and mainly nongeneric. The modern, generic ones are found in System.Collections.Generic. (I explain namespaces and generics in Book II, in my discussion of object-oriented programming).