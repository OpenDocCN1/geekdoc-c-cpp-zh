modify the internal state of your objects. Immutable types work better in hash-based collections. The value returned by Object.GetHashCode() must be an instance invariant (see Item 7); that's always true for immutable types.

In practice, it is very difficult to make every type immutable. You would need to clone objects to modify any program state. That's why this recommendation is for both atomic and immutable value types. Decompose your types to the structures that naturally form a single entity. An Address type does. An address is a single thing, composed of multiple related fields. A change in one field likely means changes to other fields. A customer type is not an atomic type. A customer type will likely contain many pieces of information: an address, a name, and one or more phone numbers. Any of these independent pieces of information might change. A customer might change phone numbers without moving. A customer might move, yet still keep the same phone number. A customer might change his or her name without moving or changing phone numbers. A customer object is not atomic; it is built from many different immutable types using composition: an address, a name, or a collection of phone number/type pairs. Atomic types are single entities: You would naturally replace the entire contents of an atomic type. The exception would be to change one of its component fields.

Here is a typical implementation of an address that is mutable:

```
// Mutable Address structure.
public struct Address
{
    private string state;
    private int zipCode;

    // Rely on the default system-generated
    // constructor.

    public string Line1
    {
        get;
        set;
    }
    public string Line2
    {
```