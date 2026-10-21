
## 3.9 Updating Collections of Mutable/Immutable Objects

As noted earlier, a non-reassignable variable can refer to an immutable object or a mutable object. In the same way, an immutable structure, like a functional list or a persistent set, can contain mutable or immutable objects. This has an impact on how you update a state that uses those structures.

Consider the following scenario as an illustration. Data is represented as immutable lists of Load objects. Each Load object has a weight, which can be reduced by one. A mutable variant of Load implements two methods:

```
trait Load:
  def weight: Int    // current weight
  def reduce(): Unit // reduce load weight by one
```

Listing 3.6: Example of a mutable type; contrast with Listing 3.7.

An application needs to perform an operation that reduces the weight of all the loads in a list by one. You can implement it as follows:

```
def reduceAll(loads: List[Load]): List[Load] =
  for load <- loads do load.reduce()
  loads
```

Even though the list is immutable, its contents are being modified. However, the same list, containing the same objects, is returned.

Alternatively, you could implement loads as an immutable type:

```
trait Load:
  def weight: Int    // current weight
  def reduced: Load // a reduced load, with a weight reduced by one
```

Listing 3.7: Example of an immutable type; contrast with Listing 3.6.

The weight method is unchanged from before. However, since loads are now immutable, the reduce action is replaced with a reduced function without side effects, which produces a new load with a reduced weight. You can no longer implement the function reduceAll by modifying the loads. Instead, new load objects must be created and then

![](img/74309e2bdd93f68d2e94338a3d73517f_75_0.png)

This page intentionally left blank

## Chapter 4

## Case Study: Active–Passive Sets

To help cement the ideas explored in Chapters 1 to 3, this first case study develops several variants of a small program. The functionality to be implemented is a structure that keeps track of the states of a collection of objects. Each element from the collection can be in an active or passive state. States can be queried, and changed from passive to active, or from active to passive. The state of the entire collection can also be queried and modified by global operations that activate or deactivate all the elements. The service is implemented in a classic object-oriented style, a purely functional style, and a hybrid style that uses functional objects.

### 4.1 Object-Oriented Design

Consider first a standard, object-oriented implementation—nothing functional here. An ActivePassive class is parameterized by the type of active/passive elements. It is implemented in terms of a mutable set, activeSet, used to represent the subset of elements that are active—elements outside the set are passive. Initially, all the elements are passive, and this set is empty.

```
class ActivePassive[A](elements: Set[A]):
  private val activeSet = mutable.Set.empty[A]

  def isActive(elem: A): Boolean = activeSet.contains(elem)

  def isPassive(elem: A): Boolean = !isActive(elem)

  def allActive: Set[A] = activeSet.toSet

  def allPassive: Set[A] = elements diff activeSet

  def isAllActive: Boolean = activeSet.size == elements.size

  def isAllPassive: Boolean = activeSet.isEmpty

  def activate(elem: A): Unit = activeSet += elem

  def deactivate(elem: A): Unit = activeSet -= elem
```

```
def activateAll(): Unit = activeSet ++= elements

def deactivateAll(): Unit = activeSet.clear()
```

Listing 4.1: Object-oriented active-passive sets, using underlying mutable sets.

This class uses two fields: elements, an immutable set (initialized in the constructor), and activeSet, a mutable set, initially empty. Methods isActive and isPassive are implemented in terms of lookups in activeSet: An element is active if it is found, and inactive if it is not found.¹ A user can retrieve the set of all currently active elements by calling method allActive. This method makes a copy of the mutable activeSet using method toSet, which returns an immutable set.² To produce a set of all inactive elements, you need to calculate the set difference between elements and activeSet, which is done with method diff in Scala. Method isAllActive must return true exactly when all the elements are active—in other words, when elements == activeSet. Since activeSet is always a subset of elements, this is equivalent to the faster test activeSet.size == elements.size. Implementing isAllPassive is simpler: Just test if allActive is empty. To activate an element, you add it to the (mutable) set activeSet. To deactivate an element, you remove it from the set. To activate all the elements, you add the entire elements set to activeSet. To deactivate all the elements, you simply clear the activeSet.

Instances of class ActivePassive are mutable: They change when elements are activated or deactivated. The implementation in Listing 4.1 relies on a mutable set, but you could implement a mutable ActivePassive class using immutable sets instead. Listing 4.2 shows this version.

```
private var activeSet = Set.empty[A]

def allActive: Set[A] = activeSet

def activate(elem: A): Unit = activeSet += elem

def deactivate(elem: A): Unit = activeSet -= elem

def activateAll(): Unit = activeSet = elements

def deactivateAll(): Unit = activeSet = Set.empty
...
```

Listing 4.2: Object-oriented active-passive sets, using underlying immutable sets.

¹ As always, argument checking is omitted. It is assumed that isActive, isPassive, activate, etc., are always called on members of the elements set.

² In Java, you could avoid the copy by returning an immutable wrapper on the mutable set—Collections.unmodifiableSet(activeSet)—but Scala has no such mechanism in its standard library.

### 4.2 Functional Values

Method allActive is simpler than before: You can just return a reference on field activeSet instead of having to copy the set. This works because activeSet is an immutable set, and returning a reference to it is harmless. The code for methods activate and deactivate looks unchanged but is actually compiled differently. Instead of calling methods ++ and -- on a mutable set, you are now creating a new immutable set and reassigning a mutable field. (The similarity in this syntax was discussed in Section 3.6.) Methods activateAll and deactivateAll are implemented without any set operation. They simply (and efficiently) reset field activeSet with the value elements, or with an empty set. The other methods (isActive, isPassive, allActive, and isAllPassive) are unchanged.

In summary, there are two ways you can define activeSet to implement a mutable active–passive set:

```
```scala
private val activeSet = mutable.Set.empty[A] // in Listing 4.1
private var activeSet = Set.empty[A] // in Listing 4.2
```
```

In one case, you activate/deactivate elements by modifying a mutable set. In the other case, you do it by building a new immutable set and reassigning a mutable field.

### 4.2 Functional Values

Let us now put on our functional programmer hat and rewrite the active–passive example entirely in terms of pure functions and immutable values. We need some type to represent ActivePassive values. A typical functional approach is to use pairs.

```
```scala
opaque type ActivePassive[A] = (Set[A], Set[A])
```
```

The first set in a pair represents the entire collection; the second set is the subset of active elements. Both sets are immutable. All the remaining code is written as functions:

```
```scala
private def elements[A](ap: ActivePassive[A]): Set[A] = ap(0)
private def activeSet[A](ap: ActivePassive[A]): Set[A] = ap(1)

def createActivePassive[A](elements: Set[A]): ActivePassive[A] = (elements, Set.empty)
```

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
