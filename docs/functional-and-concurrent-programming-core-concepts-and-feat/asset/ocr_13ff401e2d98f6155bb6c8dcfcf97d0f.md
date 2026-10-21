```
def isActive[A](ap: ActivePassive[A], elem: A): Boolean = activeSet(ap).contains(elem)

def isPassive[A](ap: ActivePassive[A], elem: A): Boolean = !isActive(ap, elem)

def allActive[A](ap: ActivePassive[A]): Set[A] = activeSet(ap)

def allPassive[A](ap: ActivePassive[A]): Set[A] = elements(ap) diff activeSet(ap)

def isAllActive[A](ap: ActivePassive[A]): Boolean =
    elements(ap).size == activeSet(ap).size

def isAllPassive[A](ap: ActivePassive[A]): Boolean = activeSet(ap).isEmpty

def activate[A](ap: ActivePassive[A], elem: A): ActivePassive[A] =
    (elements(ap), activeSet(ap) + elem)

def deactivate[A](ap: ActivePassive[A], elem: A): ActivePassive[A] =
    (elements(ap), activeSet(ap) - elem)

def activateAll[A](ap: ActivePassive[A]): ActivePassive[A] =
    (elements(ap), elements(ap))

def deactivateAll[A](ap: ActivePassive[A]): ActivePassive[A] =
    (elements(ap), Set.empty)
```

Listing 4.3: Functional active–passive sets.

The querying functions are similar to the corresponding methods used in the object-oriented implementations. They differ by the use of an explicit argument ap instead of implicitly using this:

```
// in Listings 4.1 and 4.2
def isAllActive: Boolean = activeSet.size == elements.size

// in Listing 4.3
def isAllActive[A](ap: ActivePassive[A]): Boolean =
    activeSet(ap).size == elements(ap).size
```

Because active–passive sets are now immutable, the operations that activate or deactivate elements change more substantially. They now need to create a new value: a new active–passive pair that differs from the previous one by having some elements activated or deactivated. Notice that the signatures are different from before: Instead of Unit, they now have ActivePassive[A] as their return type. For instance, to activate a single element elem in function activate, you create a new active set, activeSet(ap) + elem, and use it to make a new active–passive pair. Two private functions are added to access pair elements so as to avoid writing all the code in terms of ap(0) and ap(1), which would be error-prone. Finally, the class constructor from the object-oriented variants is replaced with a createActivePassive function.