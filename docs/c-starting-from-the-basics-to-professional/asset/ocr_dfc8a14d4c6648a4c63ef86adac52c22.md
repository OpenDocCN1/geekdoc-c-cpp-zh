```
// Functions to provide access to the values of member variables
double getLength() { return m_length; }
double getWidth() { return m_width; }
double getHeight() { return m_height; }

private:
double m_length{1.0};
double m_width {1.0};
double m_height{1.0};
};
```

The values of the member variables are fully accessible, but they can't be changed from outside the class, so the integrity of the class is preserved without the secrecy. Functions that retrieve the values of member variables are referred to as *accessor* functions.
Using these accessor functions is simple:

```
Box myBox {3.0, 4.0, 5.0};
std::cout << "myBox dimensions are " << myBox.getLength()
          << " by " << myBox.getWidth()
          << " by " << myBox.getHeight() << std::endl;
```

You can use this approach for any class. You just write an accessor function for each member variable that you want to make available to the outside world.
There will be situations in which you *do* want to allow member variables to be changed from outside the class. If you supply a member function to do this rather than exposing the member variable directly, you have the opportunity to perform integrity checks on the value. For example, you could add functions to allow the dimensions of a Box object to be changed as well:

```
class Box
{
public:
  // Constructors
  Box() = default;
  Box(double length, double width, double height);

  double volume();    // Function to calculate the volume of a box

  // Functions to provide access to the values of member variables
  double getLength() { return m_length; }
  double getWidth() { return m_width; }
  double getHeight() { return m_height; }

  // Functions to set member variable values
  void setLength(double length) { if (length > 0) m_length = length; }
  void setWidth(double width)   { if (width > 0) m_width = width; }
  void setHeight(double height) { if (height > 0) m_height = height; }

private:
  double m_length{1.0};
  double m_width {1.0};
  double m_height{1.0};
};
```