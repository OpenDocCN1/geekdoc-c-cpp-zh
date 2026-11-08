```
// Function to calculate the volume of a Box object
virtual double volume() const { return m_length * m_width * m_height; }

// ...
};
```

> > **Caution** If a member function definition is outside the class definition, you must *not* add the **virtual** keyword to the function definition; it would be an error to do so. You can only add **virtual** to declarations or definitions inside a class definition.

To make it more interesting, let's implement the volume() function in a new class called Carton a little differently. Here is the class definition:

```
// Carton.cppm
export module boxes:carton;

import :box;          // For the Box base class
import <algorithm>;   // For std::max()
import <string>;
import <string_view>;

export class Carton : public Box
{
public:
  // Constructor explicitly calling the base constructor
  Carton(double l, double w, double h, std::string_view mat = "cardboard")
    : Box(l, w, h), m_material(mat)
  {}

  // Function to calculate the volume of a Carton object
  double volume() const
  {
    const double volume {(m_length - 0.5) * (m_width - 0.5) * (m_height - 0.5)};
    return std::max(volume, 0.0);      // Or: return volume > 0.0 ? volume : 0.0;
  }

private:
  std::string m_material;
};
```

The volume() function for a Carton object assumes the thickness of the material is 0.25, so 0.5 is subtracted from each dimension to account for the sides of the carton. If a Carton object has been created with any of its dimensions less than 0.5 for some reason, then this will result in a negative value for the volume, so in such a case, the carton's volume will be set to 0.