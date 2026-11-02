Notice also that the SPARK aspects for Insert are slightly different than for the underlying version of the procedure. The flow dependency contract adds a dependency of Status on Underlying_Tree. Furthermore, the postcondition is changed to assert that the size of the tree increases if and only if the subprogram returns successfully.

It would be more natural to write the postcondition as

```
Post => (if Status = Success
    then Size = Size'Old + 1
    else Size = Size'Old);
```

However, Ada disallows use of the 'Old attribute with a prefix of a function call in a context where it might not be evaluated, such as in a branch of a conditional expression. Recall that 'Old implies the value of the prefix expression is saved when the subprogram is entered. It is undesirable to call a function when the result might not be needed. Here, Size'Old is used in both branches of the conditional expression. Nevertheless the rules of Ada forbid it in this case.

The Underlying_Tree state abstraction is intended to represent the internal tree of the underlying package. Strictly speaking, Interval_Tree.Wrapper has no internal state so declaring any Abstract_State for it is a “lie.” The SPARK tools will not notice the lie because the body of Interval_Tree.Wrapper is, as you will see, not in SPARK and thus not examined by the tools. However, if the only access to the underlying package is through the wrapper, the lie is not really a problem because the wrapper package, in effect, assumes the internal state of the wrapped package, just as wrapping paper can be said to contain the same present as the box it wraps.

In this case, however, Interval_Tree has a SPARK specification and could potentially be called directly by SPARK code willing to pass exceptions through to a higher level. For the SPARK tools to properly understand the relationship between that other code and the wrapper package, it is necessary to tell the truth about what the wrapper package is doing. This can be done by defining no Abstract_State on Interval_Tree.Wrapper and instead explicitly referencing Interval_Tree . Internal_Tree in the SPARK aspects where Underlying_Tree is mentioned previously.

The body of the wrapper package contains relatively simple subprograms that wrap the subprograms of the underlying library package. Here is the implementation of Insert in the wrapper package:

```
procedure Insert (Item : in Interval;
    Status : out Status_Type) is
begin
    Interval_Tree . Insert ( Interval_Tree . Interval (Item));
```