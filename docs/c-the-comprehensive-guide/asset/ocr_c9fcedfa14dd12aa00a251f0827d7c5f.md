However, you must not clean up a heap object twice. If you copy the pointer to the object and store it in multiple places, it is very important that you designate exactly one of the pointers as the *owner* of the object and consider all others as *users*. The owner is responsible for removing it with `delete` at the appropriate time. With raw pointers, this owner is unfortunately only in the programmers' minds and hopefully in the documentation. There are several variants of smart pointers where the ownership relationships are clear with the chosen type.

A typical use case for a heap-allocated object is when the new object needs to outlive the function in which it was created. For example, in a game framework, there might be a function that you need to override when a certain button is pressed, perhaps `createPlanet(const Event &evt)`. The return value must then be a `Planet` created within the function. As a stack object, it would be removed upon exiting the function. One solution would be to return it by value, thus as a copy, using return.

```
```cpp
Planet createPlanet(const Event &evt) {  // return by value
    Planet result{"Earth"};             // stack object
    result.setLocation(evt.getPosition());
    return result;                       // return creates (potential) copy
}
```
```

**Listing 20.2** Returning by value can create a copy.

There is nothing wrong with this variant if it works in your project. You and the compiler can make this very performant code without a copy. Sometimes, however, returning by value is not possible or desired. In such a case, use `new` to create the object on the heap.

```
```cpp
// return as (smart) pointer:
unique_ptr<Planet> createPlanet(const Event &evt) {
    unique_ptr<Planet> result{(new Planet{"Venus"})};  // heap object
    result->setLocation(evt.getPosition());
    return result;  // passes the address
}
```
```

**Listing 20.3** Returning as a pointer only copies the pointer, not the object.

You return the address of the new object wrapped in a `unique_ptr` so that you cannot forget to call `delete`.

Please excuse the use of `unique_ptr`: I wanted to present the good example first so that you remember it better than the one that works with raw pointers. Because for you, from now on, every dynamic creation of an object with `new` should always be associated with a smart pointer. Now that you know how to do it correctly, I will reduce the example to the essentials and remove `unique_ptr`. But there can be no new without a corresponding delete, so you need some code around it: