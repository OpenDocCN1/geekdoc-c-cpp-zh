Finally, data from the cube object's buffer needs to be copied to the newly allocated buffer. This is accomplished on lines [57–58] with the `std::memcpy` function (Section A.2.6). It copies bytes between two memory buffers, with the destination—which pointer is termed by the call `fDataBuf.get()`, and the source—pointed to by cube.`fDataBuf.get()`. To get the correct number of bytes, we need to multiply the amount of data expressed by the `elems` variable from line [49] by the number of bytes allocated for each data item, i.e. `sizeof(value_type)`.

| Term | Explanation |
|---|---|
| Assignment operator | An overloaded assignment operator, with one input parameter `const X&` and returning `X&`. `X& X::operator=(const X& x) { ... }` Its role is to copy the state of an existing object to the previously created object, and then return this object. |
| this | Each object of a class can access a specific pointer named `this`, which simply points at this particular object. It is passed as an implicit argument to each member function of a class; sometimes it is used in specific constructions, such as to return this object from the assignment operator. |

```
```cpp
// Assignment operator
TheCube& operator = ( const TheCube & cube )
{
    // We cannot copy if the same object
    if( this != & cube )
    {
        fDim = cube.fDim;                 // first copy the dimensions

        const auto elems = fDim[0] * fDim[1] * fDim[2];

        // Whatever was held by fDataBuf will be first deleted
        // The new block will be allocated and assigned to fDataBuf
        fDataBuf = std::make_unique<value_type[]>(elems);

        // Finally, deep copy data to the "this" buffer
        //                       source      bytes
        memcpy( fDataBuf.get(), cube.fDataBuf.get(),
                elems * sizeof( value_type ) );
    }
    return *this;
}
```
```