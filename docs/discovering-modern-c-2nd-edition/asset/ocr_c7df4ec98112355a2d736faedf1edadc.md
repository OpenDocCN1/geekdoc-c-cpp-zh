=> c++11/vector_template.cpp

In the following, we want to specialize our vector example from Listing 3–1 for bool. Our goal is to save memory by packing 8 bool values into one byte. Let us start with the class definition:

```
template <>
class vector<bool>
{
    // ...
};
```

Although our specialized class is not type-parametric anymore, we still need the template keyword and the empty triangle brackets. The name vector was declared to be a class template before, and we need this seemingly surplus template notation to show that the following definition is a specialization of the Primary Template. Thus, defining or declaring a template specialization before the primary template is an error. In a specialization, we must provide within the angle brackets a type for each template parameter. These values may be parameters themselves (or expressions thereof). For instance, if we specialize for one out of three parameters, the two others are still declared as template parameters:

Click here to view code image

```
template <template T1, template T3>
class some_container<T1, int, T3>
{
    // ...
};
```

Back to our boolean vector class: our primary template defines a constructor for an empty vector and one containing n elements. For the sake of consistency, we should define the same.

With the non-empty vector, we have to round up the data size when the number of bits is not divisible by 8:

Click here to view code image

```
template <>
class vector<bool>
{
public:
    explicit vector(int size)
```