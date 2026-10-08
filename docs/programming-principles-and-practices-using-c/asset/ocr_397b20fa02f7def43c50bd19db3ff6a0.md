On the other hand, if you use a pointer as a function argument, the function has to beware that someone might call it with a null pointer, that is, with a `nullptr`. For example:

```
```
incr_p(nullptr); // crash: incr_p() will try to dereference the null pointer
int* p = nullptr;
incr_p(p);			// crash: incr_p() will try to dereference the null pointer
```
```

This is obviously nasty. The person who writes `incr_p()` can protect against this:

```
```
void incr_p(int* p)
{
    if (p==nullptr) error("null pointer argument to incr_p()");
    ++*p;			// dereference the pointer and increment the object pointed to
}
```
```

But now `incr_p()` suddenly doesn’t look as simple and attractive as before. Chapter 5 discusses how to cope with bad arguments. In contrast, users of a reference (such as `incr_r()`) are entitled to assume that a reference refers to an object.

If “passing nothing” (passing no object) is acceptable from the point of view of the semantics of the function, we must use a pointer argument. Note: That’s not the case for an increment operation – hence the need for throwing an exception for `p==nullptr`.

So, the real answer is: “The choice depends on the nature of the function”:

+   *   For tiny objects prefer pass-by-value.
*   For functions where “no object” (represented by `nullptr`) is a valid argument use a pointer parameter (and remember to test for `nullptr`).
*   Otherwise, use a reference parameter.

See also §8.5.6.

# ### 17.9.2 Pointers, references, and inheritance

In §14.3, we saw how a derived class, such as `Circle`, could be used where an object of its public base class `Shape` was required. We can express that idea in terms of pointers or references: a `Circle*` can be implicitly converted to a `Shape*` because `Shape` is a public base of `Circle`. For example:

```
```
void rotate(Shape* s, int n);		// rotate *s n degrees

Shape* p = new Circle(Point{100,100},40);
Circle c {Point{200,200},50};
```
```