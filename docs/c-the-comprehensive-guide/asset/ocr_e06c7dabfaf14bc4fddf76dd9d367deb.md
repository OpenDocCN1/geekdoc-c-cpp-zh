# 12.9.3  Data with “struct”, Behavior with “class”

Apart from this technical distinction, I recommend that you still make a certain distinction between structure and class in your mind and that you also highlight this by using struct and class:

+   - Use `struct` for those types that are primarily holders of data and have only a little behavior through methods.
+   - Use `class` when you consider the actual data as an implementation detail, and it is the behavior that you want to expose.

# 12.9.4  Initialization of Types with Private Data

You have already learned that if you add at least one constructor to your data type, you can no longer value-initialize. The same applies if you pack data into the private area of your type.

```
```cpp
// https://godbolt.org/z/Pr76Y5SP4
class Rect {
    int area_;  // private data
public:
    int x_, y_;
    void set(int x, int y) { x_=x; y_=y; area_=x_*y_; }
    int calc() { return area_; }
};
```
```

**Listing 12.22** Parts of the data are private.

Because you are no longer allowed to directly access the `area_` member variable from the outside, you can no longer simply fill it with curly brackets. You cannot write Rect r{1,2}; or Rect s{6,2,3};. With area_ in the private section of the class, value initialization for Rect is impossible.

You definitely need a constructor here. Never accept that something lies around uninitialized after definition! Fortunately, the compiler sees it the same way, and therefore generates a constructor in these cases—specifically, one without parameters. This allows you to at least use Rect t{}; (and you should).

And what does this generated constructor do? Effectively, it initializes your object with zeros or, in the case of member variables of more complex types, with an appropriate equivalent. This is called zero initialization. (In fact, your object is first zero-initialized, and then the generated constructor is called, which does nothing; the effect is the same here.)

You have to get through a lot of automation first. Think of the readers of your program and provide a constructor, even if it's just the parameterless constructor. On the other hand, if the constructor only does what the compiler would generate anyway, you can