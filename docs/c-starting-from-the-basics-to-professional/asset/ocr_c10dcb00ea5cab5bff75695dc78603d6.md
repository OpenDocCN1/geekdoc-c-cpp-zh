the values of inherited members to be set (that is, for now all Cartons will have dimensions 1×1×1). But we'll
return to that later. Let's first see how these class definitions work in an example:

```
```cpp
// Ex18_01.cpp
// Defining and using a derived class
import <iostream>;
import box;
import carton;

int main()
{
  // Create a Box object and two Carton objects
  Box box {40.0, 30.0, 20.0};
  Carton carton;
  Carton chocolateCarton {"Solid bleached board"};  // Good old SBB
  // Check them out - sizes first of all
  std::cout << "box occupies " << sizeof box << " bytes" << std::endl;
  std::cout << "carton occupies " << sizeof carton << " bytes" << std::endl;
  std::cout << "candyCarton occupies " << sizeof chocolateCarton << " bytes" << std::endl;

  // Now volumes...
  std::cout << "box volume is " << box.volume() << std::endl;
  std::cout << "carton volume is " << carton.volume() << std::endl;
  std::cout << "chocolateCarton volume is " << chocolateCarton.volume() << std::endl;

  std::cout << "chocolateCarton length is " << chocolateCarton.getLength() << std::endl;

  // Uncomment any of the following for an error...
  // box.m_length = 10.0;
  // chocolateCarton.m_length = 10.0;
}
```
```

We get the following output:

```
```text
box occupies 24 bytes
carton occupies 56 bytes
chocolateCarton occupies 56 bytes
box volume is 24000
carton volume is 1
chocolateCarton volume is 1
chocolateCarton length is 1
```
```

The main() function creates a Box object and two Carton objects and outputs the number of bytes
occupied by each object. The output shows what you would expect—that a Carton object is larger than a
Box object. A Box object has three member variables of type double, each of these occupies 8 bytes on nearly
every machine, so that's 24 bytes in all. Both of the Carton objects are the same size: 56 bytes. The additional
memory occupied by each Carton object is down to the member variable m_material, so it's the size of a
string object that contains the description of the material. The output of the volumes for the Carton objects
shows that the volume() function is indeed inherited in the Carton class and that the dimensions have the