
Remember that it would be perfectly possible to have robsAccount in multiple arraylists, just like your name can appear on multiple lists in the real world. It might be that the bank has many lists of customers. It will have a list of all the customers, along with a list of 'special' customers and perhaps another list of those who owe it the most money. So, an item 'in' an arraylist is never actually in it, the list actually contains a reference to that item. When an item is removed from an arraylist, it is not necessarily destroyed; it is just no longer on that list.

## Accessing Items in an ArrayList

Items in arraylists can be accessed in just the same way as array elements, but with a tricky twist. It would be very nice if we could just get hold of the account from the arraylist and use it.

```
Account a = store[0];
a.PayInFunds(50);
```

Unfortunately this won't work. If you write this code you will get a compilation error. The reason for this is that an arraylist holds a list of object references. If you think about it, this is the only thing that it could hold. The designers of the ArrayList class had no idea precisely what type of object a programmer will want to use it with and so they had to use the object reference.

You will no doubt remember from the discussion of object hierarchies that an object reference can refer to an instance of any class (since they are all derived from object) and so that is the only kind of reference that the arraylist works with.

This is not actually a huge problem, because a program can use a cast to change the type of the item the arraylist returns:

```
Account a = (Account) store[0];
a.PayInFunds(50);
```

This would get the element at the start of the arraylist, cast it into an Account class and then pay fifty pounds into it.

A slightly larger problem is that an arraylist is not typesafe. This means that I can't be sure that an arraylist you give me has nothing other than accounts in it:

```
KitchenSink k = new KitchenSink();
store.Add(k);
```

This puts a reference to a KitchenSink instance into our bank storage. This will cause problems (and an exception) if we ever try to use it as an Account. To get a properly typesafe Account storage we have to take a look at generics in detail a bit later.

## Removing Items from an ArrayList

It is not really possible to remove things from an array, but the arraylist class provides a really useful Remove behaviour. This is given a reference to the thing to be removed:

```
store.Remove(robsAccount);
```

This removes the first occurrence of the reference robsAccount from the store arraylist. If the store contained more than one reference to robsAccount then each of them could be removed individually. Note that if the reference given is not actually in the arraylist (i.e. if I ran the code above when store did not contain robsAccount) this does not cause an error. If you remove an item the size of the arraylist is decreased.

## Finding the size of an ArrayList

You can use the property Count to find out how many items there are in the list:

```
if (store.Count == 0)
{
    Console.WriteLine("The bank is empty");
}
```

## Checking to see if an ArrayList contains an item

The final trick I'm going to mention (but there are lots more things an arraylist can do for you) is the Contains method. This is simply a quick way of finding out whether or not an arraylist contains a particular reference.

```
if (store.Contains(robAccount))
{
    Console.WriteLine("Rob is in the bank");
}
```

The Contains method is given a reference to an object and returns true if the arraylist contains that reference. You could of course write this behaviour yourself, but having it built into the class makes it much easier.

## ArrayLists and Arrays

ArrayLists and arrays look a lot the same. They both let you store a large number of items and you can use subscripts (the values in square brackets) to get hold of elements from either. They also throw exceptions if you try to access elements that are not in the array. If you wish you can use arraylists in place of arrays and have the benefits of storage that will grow and shrink as you need it, the only problem that you have is that an arraylist will always hold references to objects, not any particular class. However, this can be fixed when you move over to the List class.

## 5.1.2 The List class

The List class gives you everything that an arraylist gives you, with the advantage that it is also typesafe. It is newer than the ArrayList class, being based on the generic features provided by a more recent version of the C# language. To understand how it works you have to understand a bit of generics.

## Generics and Behaviours

If you think about it, the fundamental behaviours of arrays are always the same. Whether you have an int, string, float or Account array the job that it does is exactly the same. It holds a bunch of things in one place, and provides you with some means to work with them. The abilities an array gives you with an array of integers are exactly the same as those you have with an array of Account. And because each array is declared as holding values of a particular type, C# can make sure that an array always holds the appropriate type of values. The way that the system works, there is just no way that you can take an Account reference and place it in an array of integers. This is all to the good, but the ArrayList breaks things a bit.

The ArrayList was added afterwards, and because it is not quite as much a part of the language as an array is, it has to use a compromise to allow it to hold references to any kind of item in a program. It does this by using references to objects, but this can lead to programs which are dangerous, in that there is nothing to stop references of any type being added to an arraylist.

This sounds a bit confusing, how about an example.

If you wanted to share out marbles amongst you and your friends you could come up with a way of doing that. Something like: “Divide the number of marbles by the number of friends and then distribute the remainder randomly.” You now have a system that lets you share marbles. However, you could also use it to share out sweets, cakes or even cars. What the system works on is not particularly important. You could take your universal sharing algorithm and use it to share most anything. The sharing algorithm could have been invented without worrying about the type of the thing being shared; it can be a general sharing behaviour that is then applied to the things we want to share. In this respect, generics can be regarded as another form of abstraction.

## Generics and the List

In the case of generics, the behaviour you want is that of a list. What the list stores is not important when making the list, just as long as you have a way of telling it what to store. The C# features that provide generics add a few new notations to allow you to express this. The List class lives in the System.Collections.Generic namespace and works like this:

```
List<Account> accountList = new List<Account>();
```

The above statement creates a list called accountList which can hold references to Accounts. The type between the < and > characters is how we tell the list the kind of things it can store. We could create a List that can hold integers in a similar way:

```
List<int> scores = new List<int>();
```

Because we have told the compiler the type of things the list can hold it can perform type validation and make sure that nothing bad happens when the list is used:

```
KitchenSink k = new KitchenSink();
accountList.Add(k);
```

The above statements would cause a compilation error, since the accountList variable is declared as holding a list of Account references, and will not accept the kitchen sink.

Since the compiler knows that accountList holds Account references, this means that you can write code like this:

```
accountList[0].PayInFunds(50);
```

There is no need to cast the item in the list as the type has already been established.

You can do everything with a List (Add, Count, Remove) that you can with an ArrayList, which makes them the perfect way to store a large number of items of a particular type.

## 5.1.3 The Dictionary class

Just as ArrayList has a more powerful, generically enhanced, cousin called List, so the Hashtable has a more powerful cousin called Dictionary. This allows the key to your hashtable, and the items it stores, to be made typesafe. For example, we might want to use the name of an account holder as a way of locating a particular account. In other words, we have a string as the key and an Account reference as the value. We can create a dictionary to hold these key/value pairs as follows:

```
Dictionary<string,Account> accountDictionary = new Dictionary<string,Account>();
```

We can now add items into our dictionary:

```
accountDictionary.Add("Rob", robAccount);
```

This looks just like the way the Hashtable was used (and it is). However, using a Dictionary has the advantage that we can only add Account values which are located by means of a string. In other words statements like this would be rejected.
