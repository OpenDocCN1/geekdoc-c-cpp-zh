```
```cpp
int main()
{
    Line l1;
    Circle c1, c2;

    myGeom(l1);        // myGeom(GeoObj&) -> Line
    myGeom(c1);        // myGeom(GeoObj&) -> Circle

    distance(c1,c2);   // distance(GeoObj&,GeoObj&)
    distance(l1,c1);   // distance(GeoObj&,GeoObj&)

    std::vector<GeoObj> coll;  // heterogeneous collection
    coll.push_back(l1);        // insert line
    coll.push_back(c1);        // insert circle
    drawElems(coll);           // draw different kinds
}
```
```

The key polymorphic interfaces are the functions `draw()` and `center_of_gravity()`. Both are virtual member functions. Our example demonstrates their use in the functions `mydraw()` and `drawElems()`. The latter functions are expressed using the common base type `GeoObj`. A consequence of this approach is that it is generally unknown at compile time which version of `draw()` (or `center_of_gravity()`) must be called. However, at run time, the complete dynamic type of the objects for which the virtual functions are invoked is accessed to dispatch the function calls. Hence, depending on the actual type of a geometric object, the appropriate operation is performed. If `mydraw()` is called for a `Line` object, the expression `obj.draw()` calls `Line::draw()`, whereas for a `Circle` object, the function `Circle::draw()` is called. Similarly, which instance of the member functions `center_of_gravity()` is appropriate for the argument objects are called.

Perhaps the most compelling feature of this dynamic polymorphism is the ability to handle heterogeneous collections of objects, drawn in Listing 18.1. This trait then connects:

```
```cpp
elems[i]->draw()
```
```

results in invoking different member functions, depending on the dynamic type of the element being iterated over.

# 18.2 STATIC POLYMORPHISM

Templates can also be used to implement polymorphism. However, they rely only on the factoring of common behavior in base classes. Instead, the commonality is implicit in that the different “shapes” of an application must support operations using common syntax (i.e., the relevant functions must have the same names). Concrete classes are defined independently from each other (see Figure 18.2). The polymorphic power is then enabled when templates are instantiated with the concrete classes.

![](bbox=[0.08, 0.654, 0.92, 0.707])

*Figure 18.2. Polymorphism implemented via templates*

For example, the function `mydraw()` in the previous section:

Click here to view code image

```
```cpp
void mydraw (GeoObj const& obj)    // GeoObj is abstract
{
    obj.draw();
}
```
```

could conceivably be rewritten as

Click here to view code image

```
```cpp
template<typename GeoObj>
void mydraw(GeoObj const& obj)    // GeoObj is template
{
    obj.draw();
}
```
```

Comparing the two implementations of `mydraw()` we may conclude that the main difference is the specification of `GeoObj` as a template parameter instead of a common base class. There are, however, more fundamental differences under the hood. For example, using dynamic polymorphism, we had only one `mydraw()` function at run time, whereas with the template we have instantiated functions, such as `mydraw<Circle>()` and `mydraw<Line>()`.

We may attempt to remodel the complete example of the previous section using static polymorphism. First, instead of a hierarchy of geometry classes, we have several individual geometric classes: