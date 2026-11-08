```
```cpp
export class Box
{
public:
  Box(double length, double width, double height)
    : m_length {length}, m_width {width}, m_height {height}
  {
    std::cout << "Box constructor called for a Box of volume " << volume() << std::endl;
  }
  virtual ~Box()
  {
    std::cout << "Box destructor called for a Box of volume " << volume() << std::endl;
  }

  // Function to calculate volume of a Box
  virtual double volume() const { return m_length * m_width * m_height; }

  void showVolume() const
  {
    std::cout << "The volume from inside Box::showVolume() is "
              << volume() << std::endl;
  }

private:
  double m_length, m_width, m_height;
};
```
```

We also need a derived class, one that overrides `Box::volume()`;

```
```cpp
export module boxes::tough_pack;
import <iostream>;
import :box;

export class ToughPack : public Box
{
public:
  ToughPack(double length, double width, double height)
    : Box{length, width, height}
  {
    std::cout << "ToughPack constructor called for a Box of volume "
              << volume() << std::endl;
  }
  virtual ~ToughPack()
  {
    std::cout << "ToughPack destructor called for a Box of volume "
              << volume() << std::endl;
  }

  // Function to calculate volume of a ToughPack allowing 15% for packing
  double volume() const override { return 0.85 * Box::volume(); }
};
```
```