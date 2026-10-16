ints, they would do this – PracticeList<int> list = new PracticeList<int>(); and it would become an array of ints.

Let’s carry on building this class.

We will also need a constructor that sets the array to have 0 items to start with:

```
public PracticeList()
{
	items = new T[0];
}
```

This is easy enough; a new array has been created with the generic type and it has 0 items in it. Ok, it is quite worthless at this stage, but it is somewhere to start. As new items get added, we will make our array longer to accommodate them.

We also want a method that will return a specified item from our list. In this case, we want the generic type returned:

```
public T GetItem(int index)
{
	return items[index];
}
```

Again, straightforward enough; the generic type is returned. If this was used by someone else and turned into a PracticeList of ints, the return type would be ints. Once your list is created, the IntelliSense feature in Visual Studio will indicate that the method is returning the int type.

Let’s add another method; this one will add some items to the list. As far as generics go, this is as easy as everything else we have done but the code used to add items is more complex:

```
public void Add(T newItem)
{
}
```