
![](img/020c376b6cc4874983a4344f51a256de_443_0.png)

*Figure 12-9. Information needed in a Truckload object to manage the list*

Consider how retrieving Box objects from a Truckload object could work. This inevitably involves stepping through the list so the starting point is the first object in the list. You could define a getFirstBox() member function in the Truckload class to retrieve the pointer to the first Box object and record the address of the Package object that contained it in m_current. You can then implement a getNextBox() member function that will retrieve the pointer to the Box object from the next Package object in the list and then update m_current to reflect that. Another essential capability is the ability to add a Box to the list and remove a Box from the list, so you'll need member functions to do that; addBox() and removeBox() would be suitable names for these. A member function to list all the Box objects in the list will also be handy.

Here's the file defining the Truckload class based on these ideas:

```cpp
// Truckload.cpp - Module interface of the truckload module
export module truckload;

export import :shared_box;
import :package;
import <vector>;

export class Truckload
{
public:
  Truckload() = default;           // Default constructor - empty truckload

  Truckload(SharedBox box)         // Constructor - one Box
  { m_head = m_tail = new Package{box}; }
  Truckload(const std::vector<SharedBox>& boxes);  // Constructor - vector of Boxes
  Truckload(const Truckload& src); // Copy constructor

  ~Truckload() { delete m_head; }  // Destructor: clean up the list

  SharedBox getFirstBox();         // Get the first Box
  SharedBox getNextBox();          // Get the next Box
  void addBox(SharedBox box);      // Add a new SharedBox
  bool removeBox(SharedBox box);   // Remove a Box from the Truckload
  void listBoxes() const;          // Output the Boxes

private:
    Package* m_head {};                  // First in the list
    Package* m_tail {};                  // Last in the list
    Package* m_current {};               // Last retrieved from the list
};
```

The member variables are private because they don’t need to be accessible outside the class. The getFirstBox() and getNextBox() members provide the mechanism for retrieving Box objects. Each of these needs to modify the m_current pointer, so they cannot be const. The addBox() and removeBox() functions also change the list so they cannot be const either.

There are four constructors. The default constructor defines an object containing an empty list. You can also create an object from a single pointer to a Box object, from a vector of pointers, or as a copy of another Truckload. The destructor of the class makes sure the linked list it encapsulates is properly cleaned up. As described earlier, deleting the first Package will trigger all other Packages in the list to be deleted as well.

The definitions of the constructor that accepts a vector of pointers to Box objects, the copy constructor, and the other member functions of the class will be placed in a Truckload.cpp module implementation file. We discuss the definitions of these functions in the upcoming subsections.

### Traversing the Boxes Contained in a Truckload

Before we look at how the linked list is constructed, we’ll look at the member functions that traverse the list. We start with the const member function called listBoxes() that outputs the contents of the Truckload object, which could be implemented like this:

```cpp
void Truckload::listBoxes() const
{
    const size_t boxesPerLine{ 4 };
    size_t count {};
    Package* currentPackage{m_head};
    while (currentPackage)
    {
        std::cout << ' ';
        currentPackage->getBox()->listBox();
        if (!(++count % boxesPerLine)) std::cout << std::endl;
        currentPackage = currentPackage->getNext();
    }
    if (count % boxesPerLine) std::cout << std::endl;
}
```

The loop steps through the Package objects in the linked list, starting with m_head, until a nullptr is reached. For each Package, it outputs the Box object that it contains by calling listBox() on the corresponding SharedBox. Box objects are output four on a line. The last statement of the function outputs a new line when the number of Box objects output is fewer than four.

If you want, you could also write this while loop as a for loop:

```cpp
void Truckload::listBoxes() const
{
    const size_t boxesPerLine{ 4 };
    size_t count {};
    for (Package* package{m_head}; package; package = package->getNext())
    {
        std::cout << ' ';
        package->getBox()->listBox();
        if (!(++count % boxesPerLine)) std::cout << std::endl;
    }
    if (count % boxesPerLine) std::cout << std::endl;
}
```

Both loops are completely equivalent, so you're free to use either pattern to traverse linked lists.

Arguably, the for loop is somewhat nicer because there is a clearer distinction between the initialization and advancement code of the package pointer (nicely grouped in front of the body, between the round brackets of the for (...) statement) and the core logic of the listing algorithm (the loop's body, which now is no longer cluttered by any list traversal code).

To allow our analysis of the Truckload class to traverse the SharedBoxes stored in a Truckload in a similar fashion, the class offers the getFirstBox() and getNextBox() member functions. Before we discuss their implementation, it’s better to give you an idea how these functions are intended to be used. The pattern used to traverse the Boxes in a Truckload by external code will look similar to that of the listBoxes() member function (of course, an equivalent while loop could be used as well):

```cpp
Truckload truckload{ ... };

for (SharedBox box{truckload.getFirstBox()}; box; box = truckload.getNextBox())
{
    ...
}
```

The getFirstBox() and getNextBox() functions operate using the m_current member variable of Truckload, a pointer that must at all times point to the Package whose Box was last returned by either function. Such an assertion is known as a class invariant—a property of the member variables of a class that must hold at all times. Before returning, all member functions should therefore make sure that all class invariants hold again. Conversely, they can trust that the invariants hold at the start of their execution. Other invariants for the Truckload class include that m_head points to the first Package in the list and that m_tail points to the last one (see also Figure 12-9). With these invariants in mind, implementing getFirstBox() and getNextBox() is actually not that hard.

```cpp
SharedBox Truckload::getFirstBox()
{
    // Return a head's box (or nullptr if the list is empty)
    m_current = m_head;
    return m_current ? m_current->getBox() : nullptr;
}
```

```cpp
SharedBox Truckload::getNextBox()
{
    if (!m_current)                         // If there's no current...
        return getFirstBox();               // ... return the 1st Box

    m_current = m_current->getNext();       // Move to the next package

    return m_current ? m_current->getBox() : nullptr;  // Return its box (or nullptr...)
}
```

The getFirstBox() function is a piece of cake—just two statements. We know that the address of the first Package object in the list is stored in m_head. Calling the getBox() function for this Package object obtains the address of its Box object, which is the desired result for getFirstBox(). Only if the list is empty will m_head be nullptr. For an empty Truckload, getFirstBox() should return a nulled SharedBox as well. Before returning, getFirstBox() also stores the address of the first Package object in m_current. This is done because the class invariants state that m_current must always refer to the last Package whose Box was retrieved.

If, at the start of getNextBox(), the m_current pointer is nullptr, then the first Box in the list (if any) is obtained and returned by calling getFirstBox(). Otherwise, the getNextBox() function accesses the Package object that follows the one whose Box was returned last by calling m_current->getNext(). If this Package* is nullptr, the end of the list has been reached, and nullptr is returned. Otherwise, the Box of the current Package is returned. Of course, getNextBox() also correctly updates m_current to respect its class invariant.

### Adding and Removing Boxes

We'll start with the easiest of the remaining members: the vector<>-based constructor definition. This creates a list of Package objects from a vector of smart pointers to Box objects:

```cpp
Truckload::Truckload(const std::vector<SharedBox>& boxes)
{
    for (const auto& box : boxes)
    {
        addBox(box);
    }
}
```

The parameter is a reference to avoid copying the argument more than necessary. The vector elements are of type SharedBox, which is an alias for std::shared_ptr<Box>. The loop iterates through the vector elements, passing each one to the addBox() member of the Truckload class, which will create and add a Package object on each call.

The copy constructor simply iterates over all packages in the source Truckload and calls addBox() for each box to add it to the newly constructed Truckload:

```cpp
Truckload::Truckload(const Truckload& src)
{
    for (Package* package(src.m_head); package; package = package->getNext())
    {
        addBox(package->getBox());
    }
}
```

Both of these constructors are made easy because all the heavy lifting is delegated to addBox(). The definition of this member will be as follows:

```cpp
void Truckload::addBox(SharedBox box)
{
    auto package( new Package{box} );  // Create a new Package

    if (m_tail)                        // Check list is not empty
        m_tail->setNext(package);      // Append the new object to the tail
```
