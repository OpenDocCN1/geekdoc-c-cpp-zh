# Chapter 9: Introducing Structs and Records

Recall our analogy that suggested variables of value types are like pieces of paper with the value written on them. When you box a value, you make a photocopy of the paper and put the copy in a box. When you unbox the value, you make a photocopy of the paper in the box. Making an edit to this second copy does not change the copy that is in the box.

In Example 3, a similar problem occurs, but in reverse. Instead of calling MoveTo() directly, the value is cast to IAngle. The conversion to an interface boxes the value, so the runtime copies the data in angle to the heap and provides a reference to that box. Next, the method call modifies the value in the referenced box. The value stored in variable angle remains unmodified.

In the last case, the cast to IAngle is a reference conversion, not a boxing conversion. The value has already been boxed by object in this case, so no copy of the value occurs on this conversion. The call to MoveTo() updates the value stored in the box, and the code behaves as desired.

As you can see from this example, mutable value types are quite confusing because it is often unclear when you are mutating a copy of the value rather than the storage location you actually intend to change. By avoiding mutable value types in the first place, you can eliminate this sort of confusion.

> Guidelines
AVOID mutable value types.

# ADVANCED TOPIC avoided during Method Calls

How Boxing Can Be Avoided during Method Calls
Anytime a method is called on a value type, the value type receiving the call (represented by this in the body of the method) must be a variable, not a value, because the method might be trying to mutate the receiver. Clearly, it must be mutating the receiver's storage location, rather than mutating a copy of the receiver's value and then discarding it. Examples 2 and 4 of Listing 9.11 illustrate how this fact affects the performance of a method invocation on a boxed value type.