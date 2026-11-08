Now the example will no longer compile! Of course, the fact that the compiler refuses to compile the last three lines in the previous code fragment is exactly what you want. After all, you should not be able to alter the state of a const object. We said earlier already the compiler prevents direct assignments to member variables—supposing you have access—so why should it allow indirect assignments inside member functions? The Box object would not be much of an immutable constant if you were allowed to call these setters, now would it?

Unfortunately, however, the getter functions cannot be called on a const object either simply because there's the risk that they could change the object. In our example, this means that the compiler will not only refuse to compile the last three lines but also the output statement before that. Similarly, any attempt to call the volume() member function on a const myBox would result in a compilation error:

```
    std::cout << "myBox's volume is " << myBox.volume() << std::endl;  // Will not compile!
```

Even though you know that volume() doesn't alter the object, the compiler does not. At least not at that point in the compilation. All it considers when compiling this volume() expression is the function's signature. And even if it does know the function's definition from inside the class definition—as with our three getters earlier—the compiler makes no attempt to deduce whether a function modifies the object's state. All the compiler uses in this setting is the function's signature.

So, with our current definition of the Box class, const Box objects are rather useless. You cannot call any of its member functions, not even the ones that clearly do not modify any state. To solve this, you'll have to improve the definition of the Box class. You need a way to tell the compiler which member functions are allowed to be called on const objects. The solutions are so-called const member functions.

First, you need to specify all functions that don't modify an object as const in the class definition:

```
    export class Box
    {
    public:
      // Same constructors as before...

      double volume() const;  // Function to calculate the volume of a box

      // Functions to provide access to the values of member variables
      double getLength() const { return m_length; }
      double getWidth() const { return m_width; }
      double getHeight() const { return m_height; }

      // Functions to set member variable values
      void setLength(double length) { if (length > 0) m_length = length; }
      void setWidth(double width)   { if (width > 0) m_width = width; }
      void setHeight(double height) { if (height > 0) m_height = height; }

    private:
      // Same member variables as before...
    };
```

Next, you must change the out-of-class function definition accordingly:

```
    double Box::volume() const
    {
      return m_length * m_width * m_height;
    }
```