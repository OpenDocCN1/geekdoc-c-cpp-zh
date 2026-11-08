# Nested Classes

The Package class was designed to be used specifically within the Truckload class. It would make sense to ensure that Package objects can only be created by member functions of the Truckload class. Granted, because the Package class is not exported from the module, the rest of the world already cannot use it. But in general you may want to go one step further, and employ a mechanism where Package objects are private to Truckload class members and not available to the rest of the module. You can do this by using a nested class. A nested class is a class that has its definition inside another class definition. The name of the nested class is within the scope of the enclosing class and is subject to the member access specification in the enclosing class. We could put the definition of the Package class inside the definition of the Truckload class, like this:

```
```cpp
export module truckload;
import box;
import <memory>;
import <vector>;

// We no longer need the truckload:shared_box partition (or any other partition file)
export using SharedBox = std::shared_ptr<Box>;

export class Truckload
{
public:
    // Exact same public member functions as before...

private:
    class Package
    {
    public:
        SharedBox m_box;        // Pointer to the Box object contained in this Package
        Package* m_next;        // Pointer to the next Package in the list

        Package(SharedBox box) : m_box{box}, m_next{nullptr} {} // Constructor
        ~Package() { delete m_next; }                          // Destructor
    };

    Package* m_head {};      // First in the list
    Package* m_tail {};      // Last in the list
    Package* m_current {};   // Last retrieved from the list
};
```
```

The Package type is now local to the scope of the Truckload class definition. Because the definition of the Package class is in the private section of the Truckload class, Package objects cannot be created or used from outside the Truckload class. Because the Package class is entirely private to the Truckload class, there’s also no harm in making all its members public. Hence, they’re directly accessible to member functions of a Truckload object. The getBox(), getNext(), and setNext() members of the original Package class are no longer needed. All of the Package members are directly accessible from Truckload objects but inaccessible outside the class.