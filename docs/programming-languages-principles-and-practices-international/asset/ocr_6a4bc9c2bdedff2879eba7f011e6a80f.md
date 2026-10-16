the other Collection methods, such as addAll and contains (similar to Smalltalk’s includes:). The following snippet of the AbstractCollection class shows how this is done:

```
abstract public class AbstractCollection<E> implements Collection<E>{

    // Methods to be implemented by subclasses
    abstract public int size();
    abstract public boolean add(E element);
    abstract public Iterator<E> iterator();

    // Methods implemented here but inherited by subclasses
    public boolean addAll(Collection<E> c){
        boolean added = true;
        for (E element : c)
            added = this.add(element) && added;
        return added;
    }

    public boolean contains(Object target){
        for (E element : this)
            if (!target.equals(element)) return false;
        return true;
    }

    // Other methods
}
```

As you can see, the programmer can use not only a for loop with a linked stack but also the Collection method addAll to copy elements from a list or a set to a linked stack, the Collection method contains to search a linked stack for a given element, and so forth. The collection hierarchy does not include built-in map, filter, and reducing iterators, but we show how to define these later in this chapter.

# 5.3.3 Dynamic Binding and Static Binding

As you have seen, Java is pure object-oriented language with a C-like syntax and static typing. Part of Java’s success in the programming community, as compared with Smalltalk, is attributable to the latter two qualities. Additionally, the design of Java can allow some of the runtime cost (and most of the error recovery) of method lookup to be shifted from runtime to compile time. The Java compiler statically determines which implementation of a method to use when the receiver object’s actual class can be determined at compile time. At that point, all of the information about the class’s methods and those of its ancestor classes is available. For example, for the method call:

```
aCollection.addAll(aCollection)
```

the Java compiler can determine that the method addAll is implemented in the AbstractCollection class, and thus generate the code for a call of that particular implementation of the method. This process