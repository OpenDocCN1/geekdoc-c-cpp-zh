```
}
#endregion IListable
// ...
}
```

In this listing, notice the addition of the CellColors property getter. As you can see, it includes an implementation even though it is the member of an interface. The feature is called a default interface member member because it provides a default implementation of the method so that any class that implements the interface will already have a default implementation—so that code will continue to compile without any changes even though the interface has additional members. The Contact class, for example, has no implementation for the CellColors property getter, so it relies on the default implementation provided by the IListable interface.

Not surprisingly, you can override a default implementation of the method in the implementing class to provide a different behavior that makes more sense to the class. This behavior is all consistent with the purpose of enabling polymorphism as outlined at the beginning of the chapter.

However, the default interface member feature includes additional features. The primary purpose of these features is to support refactoring of default interface members (though some would debate this interpretation). To use them for any other purpose likely indicates a flaw in the code structure, because it implies the interface is used for more than polymorphism. Table 8.1 lists the additional language constructs along with some of their important limitations.