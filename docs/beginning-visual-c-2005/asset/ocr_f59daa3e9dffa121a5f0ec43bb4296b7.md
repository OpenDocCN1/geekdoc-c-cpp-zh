# # Class Inheritance and Virtual Functions

```
```cpp
// Calling the base class constructor
CCandyBox(double lv, double wv, double hv, char* str = "Candy"):
CBox(lv, wv, hv)
{
    ...
}
```
```

This is perfectly consistent with what you are doing here because you are essentially initializing a CBox sub-object of the derived class object. In the first case, you are explicitly calling the default constructor for the double members m_Length, m_Width and m_Height in the initialization list. In the second instance, you are calling the constructor for CBox. This causes the specific CBox constructor you have chosen to be called before the CCandyBox constructor is executed.

If you build and run this example, it produces the output shown as follows:

```
CBox constructor called
CBox constructor called
CBox constructor1 called
CBox constructor called
CBox constructor2 called
myBox occupies 24 bytes
myCandyBox occupies 32 bytes
myMintBox occupies 32 bytes
myMintBox volume is 6
```

| Screen output | Object being constructed |
|---------------|-------------------------|
| CBox constructor called | MyBox |
| CBox constructor called | MyCandyBox |
| CBox constructor1 called | MyCandyBox |
| CBox constructor called | MyMintBox |
| CBox constructor2 called | MyMintBox |

The first line of output is due to the CBox class constructor call, originating from the declaration of the CBox object, myBox. The second line of output arises from the automatic call of the base class constructor caused by the declaration of the CCandyBox object myCandyBox.

> *Notice how the base class constructor is always called before the derived class constructor.*

The following line is due to your version of the default derived class constructor being called for the myCandyBox object. This constructor is invoked because the object is not initialized. The fourth line of output arises from the explicit identification of the CBox class constructor to be called in our new constructor for CCandyBox objects. The argument values specified for the dimensions of the CCandyBox object are passed to the base class constructor. Next comes the output from the new derived class constructor itself, so constructors are again called for the base class first, followed by the derived class.