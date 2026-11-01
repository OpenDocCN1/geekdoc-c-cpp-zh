This section also describes various interfaces and delegates used with these classes.

# List<T>

Rather than derive a class from CollectionBase and implement the required methods as you did in the last chapter, it can be quicker and easier simply to use the List<T> generic collection type. An added bonus here is that many of the methods you normally have to implement, such as Add(), are implemented for you.

Creating a collection of type T objects requires the following code:

```
List<T> myCollection = new List<T>();
```

That's it. You don't have to define any classes, implement any methods, or do anything else. You can also set a starting list of items in the collection by passing a List<T> object to the constructor. List<T> also has an Item property, enabling array-like access:

```
T itemAtIndex2 = myCollection[2];
```

This class supports several other methods, but that's plenty to get you started. The following Try It Out demonstrates how to use List<T> in practice.

# TRY IT OUT Using List<T>: Ch12Ex02

+   1. Create a new console application called Ch12Ex02 and save it in the directory C:\BegVCSharp\Chapter12.
+   2. Right-click on the project name in the Solution Explorer window and select the Add <> Existing Item option.
+   3. Select the Animal.cs, Cow.cs, and Chicken.cs files from the C:\BegVCSharp\Chapter11\Ch11Ex01\Ch11Ex01 directory and click Add.
+   4. Modify the namespace declaration in the three files you added as follows:
+      namespace Ch12Ex02
+   5. Modify Program.cs as follows:
+      static void Main(string[] args)
+      {
+        List<Animal> animalCollection = new List<Animal>();
+        animalCollection.Add(new Cow("Rual"));
+        animalCollection.Add(new Chicken("Donna"));
+        foreach (Animal myAnimal in animalCollection)
+        {
+          myAnimal.Feed();
+        }
+        ReadKey();
+      }