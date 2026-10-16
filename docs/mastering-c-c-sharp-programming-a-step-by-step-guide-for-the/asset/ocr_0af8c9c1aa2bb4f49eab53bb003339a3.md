For example, we can create a phone book using the Dictionary. The names of the people will be strings and their phone numbers will be ints. These may not be the best thing to use for the numbers but, for now, I just want to give you a simple example of how it works with two types.

We could create a Contact or a Person class that will store the names and all other information and a class called PhoneNumber to store the phone number details including area and country codes. However, we’re not going to do that because I want to keep it simple.

Like the List class, Dictionary is also generic, but instead of one, it has two generic types – the key used for looking up, and the value that we look up. Rather than putting one type between our angled brackets, we put both, one for each generic piece:

```
Dictionary<string, int> phoneBook = new Dictionary<string, int>();
```

Now we can make use of the indexing operator to get a value or set a value in our Dictionary:

```
phoneBook["Bunter, Billy"] = 1526587;
```

```
phoneBook["Twain, Mark"] = 1625874;
```

```
int billsNumber = phoneBook["Bunter, Billy"]; // We're good friends...
```

As with our List class, we have several methods that can be used so take a bit of time and explore the Dictionary class, and see what can be done with it.

# Quick Primer

+   - C# Generics are much the same as they are in Java and as C++ templates.

+   - Generics are used for creating type-safe classes without having to specify one specific type.

+   - When an instance is created of a generic class, you must indicate the type or types that you want to use for a specific