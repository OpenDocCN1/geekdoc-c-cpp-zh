There are some important characteristics of Generic types that make them special to the conventional nongeneric type as follows:

+   - Type Safety.
+   - Performance.
+   - Binary Code reuse.

# Type Safety

One of the most important features of Generics is Type Safety. In the case of the nongeneric ArrayList class, if objects are used, any type can be attach to the collections that can sometimes result in a great problem. The following example point out that adding a, string integer, and object to the collection of an ArrayList type:

```
ArrayList obj = new ArrayList();
obj.Add(50);
obj.Add("Dog");
obj.Add(new TestClass());
```

Now, if the collection is going through the foreach statement using integer elements, the compiler accepts the code, but because all the elements in the collection are not an integer, a runtime exception occurs:

```
foreach(int i in obj)
{
    Console.WriteLine(i);
}
```