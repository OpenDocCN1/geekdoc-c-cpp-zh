![](bbox=[0.18, 0.16, 0.83, 0.35])

*Figure 12-9. Information needed in a Truckload object to manage the list*

Consider how retrieving Box objects from a Truckload object could work. This inevitably involves stepping through the list so the starting point is the first object in the list. You could define a getFirstBox() member function in the Truckload class to retrieve the pointer to the first Box object and record the address of the Package object that contained it in m_current. You can then implement a getNextBox() member function that will retrieve the pointer to the Box object from the next Package object in the list and then update m_current to reflect that. Another essential capability is the ability to add a Box to the list and remove a Box from the list, so you'll need member functions to do that; addBox() and removeBox() would be suitable names for these. A member function to list all the Box objects in the list will also be handy.

Here's the file defining the Truckload class based on these ideas:

```
~~~cpp
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
};
~~~
```