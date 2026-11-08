
```cpp
import <iostream>;

export class Box
{
public:
  Box() : Box{1.0, 1.0, 1.0} {}
  Box(double l, double w, double h) : m_length {l}, m_width {w}, m_height {h} {}

  // Function to show the volume of an object
  void showVolume() const
  { std::cout << "Box usable volume is " << volume() << std::endl; }

  // Function to calculate the volume of a Box object
  double volume() const { return m_length * m_width * m_height; }

protected:
  // Should be private in production-quality code (add getters to access)
  double m_length, m_width, m_height;
};
```

We can display the usable volume of a Box object by calling the showVolume() function for the object. The member variables are specified as protected, so they can be accessed by the member functions of any derived class.

Next, we'll define a ToughPack class with Box as a base. A ToughPack object incorporates packing material to protect its contents, so its capacity is only 85% of a basic Box object. Therefore, a different volume() function is needed in the derived class to account for this.

```cpp
// ToughPack.cpp: partition interface file for the tough_pack partition
export module boxes:tough_pack;

import :box;  // Import the box partition for use of Box as base class

export class ToughPack : public Box
{
public:
  // Inherit the Box(length, width, height) constructor
  using Box::Box;

  // Function to calculate volume of a ToughPack allowing 15% for packing
  double volume() const { return 0.85 * m_length * m_width * m_height; }
};
```

Conceivably, you could have additional members in the derived ToughPack class. But for the moment, we'll keep it simple, concentrating on how the inherited functions work. The idea here is that you can get the inherited function showVolume() to call the derived class version of volume() when you call it for an object of the ToughPack class.

Thus far we have always defined each class in its own module. In this chapter we wanted to show you some other options, though. For Ex15_01 we therefore defined the two classes—Box and ToughPack—in one and the same module, boxes. And because a single file containing too many massive classes would be truly unwieldy (just kidding: it's of course just to illustrate this interesting possibility), we split this module into two partitions—boxes:box and boxes:tough_pack.

To use Box as a base class of ToughPack we therefore first had to import the boxes:box partition into the boxes:tough_pack partition. The module import declaration that took care of this looks as follows:

```cpp
import :box;    // Import the box partition for use of Box as base class
```

Because you can only import partitions of the same module, there is no need to specify the boxes module name in this declaration. In fact, you are not even allowed to write `import boxes:box;` within the same module, nor in any other source file. Modules can only be imported in their entirety, and module partitions can only be imported within other files of the same module.

Now that we have these two module partitions—each consisting of a single partition interface file—we still need to create the module’s primary interface file. The one file that glues the module together. As explained in Chapter 11, every module needs precisely one primary interface file (a file starting with `export module name;`). For the boxes module this file simply re-exports the module’s two partitions:

```cpp
// Boxes.cppm: primary module interface file
export module boxes;

export import :box;          // Export all partitions
export import :tough_pack;
```

With this primary module interface file in place, we’re now ready to see whether invoking the inherited showVolume() function works as one might hope:

```cpp
// Ex15_01.cpp
// Behavior of inherited functions in a derived class
import boxes;

int main()
{
    Box box {20.0, 30.0, 40.0};          // Create a box
    ToughPack hardcase {20.0, 30.0, 40.0}; // Create a tough pack - same size

    box.showVolume();                     // Display volume of base box (calls volume() for box)
    hardcase.showVolume();                // Display volume of derived box (call volume() for hardcase)
}
```

Unfortunately, when we run the program we get this rather disappointing output:

```text
Box usable volume is 24000
Box usable volume is 24000
```

The derived class object, hardcase, is supposed to have a capacity that is 15% less than that of the base class object (to account for the packing material, remember?), so the program is obviously not working as intended.

Let’s try to establish what’s going wrong. The second call to showVolume() in main() is for an object of the derived class, ToughPack, but evidently this is not being taken into account. The trouble is that when the volume() function is called by the showVolume() function of Box, the compiler sets it once and for all as the version of volume() defined in the base class. No matter how you call showVolume(), it will never call the ToughPack version of the volume() function. It will always call the Box version of volume().

When function calls are fixed in this way before the program is executed, it is called *static resolution* of the function call, or *static binding*. The term *early binding* is commonly used as well. In this example the Box::volume() function is bound to the call inside Box::showVolume() when the program is compiled and linked. Every time showVolume() is called, it uses this statically bound Box::volume() function.

But what if, instead of through showVolume(), you were to call the volume() function for the ToughPack object directly? As a further experiment, let's add statements in main() to call the volume() function of a ToughPack object directly, as well as through a pointer to the base class:

```cpp
std::cout << "hardcase volume is " << hardcase.volume() << std::endl;
Box* box {&hardcase};
std::cout << "hardcase volume through a Box* pointer is "
          << box->volume() << std::endl;
```

Place these statements at the end of main(). Now when you run the program, you'll get this output:

```text
Box usable volume is 24000
Box usable volume is 24000
hardcase volume is 20400
hardcase volume through a Box* pointer is 24000
```

This is quite informative. You can see that a call to volume() for the derived class object, hardcase, calls the derived class volume() function, which is what you want. The call through the base class pointer box, however, is resolved to the base class version of volume(), even though box contains the address of hardcase. In other words, both calls are resolved statically. The compiler implements these calls as follows:

```cpp
std::cout << "hardcase volume is " << hardcase.ToughPack::volume() << std::endl;
Box* box {&hardcase};
std::cout << "hardcase volume through a Box* pointer is "
          << box->Box::volume() << std::endl;
```

A static function call through a pointer is determined solely by the pointer type and not by the object to which it points. In other words, it is determined by the *static type* of the pointer rather than the *dynamic type* of the object. The pointer box has a static type pointer-to-Box, so any static call using box calls a member function of Box.

> **Note**  
> Any call to a function through a base class pointer that is resolved statically calls a base class function. This applies not only to pointers such as box in our latest example, but also to the (implicit) *this* pointer in member functions of the base class (such as, for instance, within the Box::showVolume() function earlier).

What we want is that our program resolves which volume() function to call at runtime, not at compile time. What we want is for this to be based on the dynamic type of the pointed-to object, and not on the static type of the pointer. So, if showVolume() is called for a derived class object, the derived class volume() function should be called, not the base class version. Always, even if volume() is called through a base class pointer. This sort of operation is referred to as *dynamic binding* or *late binding*. To make this work, we have to tell the compiler that the volume() function in Box and any overrides in the classes derived from Box are special, and that calls to them are to be resolved dynamically. We can obtain this effect by specifying that volume() in the base class is a *virtual function*, which will result in a virtual function call for volume().
