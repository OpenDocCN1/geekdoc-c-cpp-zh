# Class Templates 845

This approach for sizing an array has one advantage over the constructor approach used in Stack. The constructor approach uses heap memory managed by new and delete, whereas the expression argument approach uses the memory stack maintained for automatic variables. This provides faster execution time, particularly if you have a lot of small arrays.

The main drawback to the expression argument approach is that each array size generates its own template. That is, the following declarations generate two separate classes:

+   - ArrayTP<double, 12> eggwhites;
- ArrayTP<double, 13> donuts;

The following declarations generate one class declaration, and the size information is passed to the constructor for that class:

```
Stack<int> eggs(12)
Stack<int> dunkers(13);
```

Another difference is that the constructor approach is more versatile because the array size is stored as a class member rather than being hard-coded into the definition. This makes it possible, for example, to define assignment from one size to an array of another size or to build a class that allows resizable arrays.

# Template Versatility

You can apply the same techniques to template classes as you do to regular classes. Template classes can serve as base classes, and they can be component classes. They can themselves be type arguments to other templates. For example, you can implement a stack template by using an array template. Or you can have an array template that is used to construct an array whose elements are based on a stack template. That is, you can have code along the following lines:

```
template <typename T>    // or <class T>
class Array
{
    private:
        T entry;
        ...
};
```

```
template <typename Type>
class GrowArray : public Array<Type>{...}; // inheritance
```

```
template <typename Tp>
class Stack
{
    Array<Tp> ar;      // use an Array<> as a component
    ...
```