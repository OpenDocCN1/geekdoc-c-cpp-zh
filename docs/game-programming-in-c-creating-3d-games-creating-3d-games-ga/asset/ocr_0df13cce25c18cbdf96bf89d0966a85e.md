# Listing A.1.

# Listing A.1 Circle Class with const Member Function

Click here to view code image

```
class Circle
{
public:
    float GetRadius() const { return mRadius }

    // Other functions omitted

    // ...

private:
    Point mCenter;
    float mRadius;
};
```

To summarize, the best practices when it comes to references, const, and classes are as follows:

+   - Pass non-basic types by reference, const reference, or pointers, to avoid making copies.
+   - Pass by const reference when a function does not need to modify a reference parameter.
+   - Mark member functions that don't modify data as const.