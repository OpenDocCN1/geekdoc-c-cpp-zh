The primary module interface file for boxes is trivial as always:

```
```cpp
export module boxes;
export import :box;
export import :tough_pack;
```
```

And in this case the main program is trivial as well. All it does is create an instance of the derived class ToughPack and then show its volume:

```
```cpp
// Ex15_08.cpp
// Calling virtual functions from constructors and destructors
import boxes;

int main()
{
    ToughPack toughPack{1.0, 2.0, 3.0};
    toughPack.showVolume();     // Should show a volume equal to 85% of 1x2x3, or 5.1
}
```
```

This is the resulting output:

```
```text
Box constructor called for a Box of volume 6
ToughPack constructor called for a Box of volume 5.1
The volume from inside Box::showVolume() is 5.1
ToughPack destructor called for a Box of volume 5.1
Box destructor called for a Box of volume 6
```
```

Let’s first focus our attention on the middle line of this output, which is the product of the ToughPack::showVolume() function call. ToughPack overrides volume(), so if you call volume() on a ToughPack object, you expect the version of ToughPack to be used, even if this call originates from inside a base class function such as Box::showVolume(). The output clearly shows that this is also what happens. Box::showVolume() prints out a volume of 0.85 * 1 * 2 * 3, or 5.1, as expected.

Now let’s see what happens if you call volume() not from a regular base class member function such as showVolume() but from a base class constructor. The first line in the output shows you that volume() then returns 6. So, it’s clearly the original function of Box that gets called, not the overridden version of ToughPack! Why is that? You’ll recall from the previous chapter that when an object is constructed, all its subobjects are constructed first, including the subobjects of all its base classes. While initializing such a subobject—for instance, the Box subobject of our ToughPack—the object of the derived class will therefore at most be partially initialized. It would in general be extremely dangerous to call member functions on an object whose subobjects have not yet been fully initialized. This is why all function calls from inside a constructor, including those of virtual members, are always resolved statically.

Conversely, when destroying an object, all its subobjects are destructed in the reverse order in which they were constructed. So, by the time the destructor of the base class subobject is called, the derived class is already partially destructed. It would thus again be a bad idea to call members of this derived object. So, all function calls in destructors are thus resolved statically as well.