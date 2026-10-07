# Converting between the Implementing Class and Its Interfaces

Truck class would result in confusion as to which operation the method performs. Instead, it is preferable to implement the member explicitly so that the Dump() method can be called only from a data type of ITrace where the meaning is clearer. Using an explicit implementation if a member's purpose is unclear on the implementing class.

+   - Does a class with the same signature already exist? Explicit interface member implementation does not add a named element to the type's declaration space. Therefore, if there is already a potentially conflicting member of a type, a second one can be provided with the same name or signature as long as it is an explicit interface member.

Much of the decision-making regarding implicit explicit interface member implementation comes down to intuition. However, these questions provide suggestions about issues to consider when making your choice. Since changing an implementation from implicit to explicit results in a version-breaking change, it is better to err on the side of defining interfaces explicitly, allowing them to be changed to implicit interfaces later. Furthermore, since the decision between implicit and explicit does not have to be consistent across all interface members, defining methods as explicit and others is fully supported.

# Converting between the Implementing Class and Its Interfaces

Just as with a derived type and a base class, a conversion from an implementing type to its implemented interface is an implicit conversion. No cast operator is required because an instance of the implementing type will always provide the members in the interface; therefore, the object can always be converted successfully to the interface type.

Although the conversion will always be successful from the implementing type to the implemented interface, many different types could implement a particular interface. Consequently, you can never be certain that a “downward” cast from an interface to one of its implementing types will be successful. Therefore, converting from an interface to one of its implementing types requires an explicit cast.