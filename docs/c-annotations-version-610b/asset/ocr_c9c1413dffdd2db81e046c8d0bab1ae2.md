+   - First, A `SortVector` object is created for `MultiData` objects. It uses the copy generic algorithm to fill the `SortVector` object from information appearing at the program’s standard input stream. Having initialized the object its elements are displayed to the standard output stream:

```
SortVector<MultiData> sv;

copy(istream_iterator<MultiData>(cin),
     istream_iterator<MultiData>(),
     back_inserter(sv));
```

+   - An array of pointers to members is initialized with the addresses of two member functions. The text comparison is the most significant sort criterion:

```
bool (MultiData::*arr[])(MultiData const &rhv) const =
{
    &MultiData::textCmp,
    &MultiData::intCmp,
};
```

+   - Next, the array’s elements are sorted and displayed to the standard output stream:

```
sv.hierarchicSort(arr, 2);
```

+   - Then the two elements of the array of pointers to `MultiData`’s member functions are swapped, and the previous step is repeated:

```
swap(arr[0], arr[1]);
sv.hierarchicSort(arr, 2);
```

After compiling the program the following command can be given:

```
echo a 1 b 2 a 2 b 1 | a.out
```

This results in the following output:

```
a 1 b 2 a 2 b 1
====
a 1 a 2 b 1 b 2
====
a 1 b 1 a 2 b 2
====
```

# 21.11.3  Deriving class templates from ordinary classes

An ordinary class may be used as the base class for deriving a template class. The advantage of such an inheritance tree is that the base class’s members may all be compiled beforehand. When objects of the class template are now instantiated only the actually used members of the derived class template must be instantiated.

This approach may be used for all class templates having member functions whose implementations do not depend on template parameters. These members may be defined in a separate class which is then used as a base class of the class template derived from it.

As an illustration of this approach we’ll develop such a class template below. We’ll develop a class `Table` derived from an ordinary class `TableType`. The class `Table` displays elements of some type in a table having a configurable number of columns. The elements are either displayed horizontally (the first *k* elements occupy the first row) or vertically (the first *r* elements occupy a first column).