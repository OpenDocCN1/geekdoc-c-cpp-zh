Push and Pop are short enough that they could also be implemented in the class definition. We take them outside here to show the syntax. In the case of template classes, all definitions are contained in a header file.

```
```
private:
    using DataContainer = std::vector< value_type >;
    DataContainer    fData;
public:
    // Here we need an additional typename
    using size_type = typename DataContainer::size_type;
public:
    auto GetStackSize( void ) const { return fData.size(); }
public:
    // This function puts an element onto the stack
    // INPUT:
    // new_elem - a reference to the element to
    // be put. Actually its copy is put onto
    // the stack.
    // OUTPUT:
    // true - if operation successful,
    // false - failure, due to insufficient
    // space on the stack (e.g. too many
    // elements)
    bool Push( const value_type & new_elem );
    // This function removes an element from the stack
    // INPUT:
    // ret_elem - a reference to the object which
    // will be copied with topmost element
    // from the stack. Then the topmost element
    // is removed from the stack.
    // OUTPUT:
    // true - if operation successful,
    // false - failure, due to empty stack
    bool Pop( value_type & ret_elem );
```
```