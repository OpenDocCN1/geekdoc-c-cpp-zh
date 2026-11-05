We can now create contracts for the interface via the contract class **IShapeShiftableContract**, exactly like we did earlier for abstract classes.

# ## Abstract classes versus interface

To conclude the examples of abstract classes and interfaces, it all boils down to where you want your implementation. If you want to share implementation among all derived classes, you will be creating an abstract class. If you need your implementation specific to a single class or several classes, but not all classes, use an interface.

Code Contracts easily cater to both.

# ## Method purity

A book on Code Contracts would not be complete without mentioning purity. When referring to Code Contracts, what exactly does method purity mean? Well, Code Contracts have an attribute called **[Pure]** that you can decorate methods with. This is basically an expression of the quality of the method, and that the method can’t change the state of any objects seen by callers. In other words, pure methods are only allowed to change objects created after the method has been entered.

Code Contracts require all methods called inside a contract to be pure. The reasons for this are simply:

+   - To avoid side effects in methods used in preconditions and postconditions.
+   - To make the task of the static checker easier because it can assume object states will be the same after the method is called.
+   - To improve design by specifically clarifying your intent that the method will not alter the state of objects after the method call has ended.

To illustrate the effect that a non-pure method has on the static checker, consider the following code listing.

```
```csharp
public class DemoPurity
{
    /// <summary>
    /// Property for cutting factor
    /// </summary>
    public int CutFactor { get; private set; }

    /// <summary>
    /// Public Constructor
    /// </summary>
    /// <param name="cutFactor"></param>
    public DemoPurity(int cutFactor)
    {
        CutFactor = cutFactor;
```
```