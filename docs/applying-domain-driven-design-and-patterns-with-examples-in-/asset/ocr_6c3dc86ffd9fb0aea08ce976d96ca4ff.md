referred to as the *Presentation Model* (PM).

The Presentation Model objects are a part of the PL and should have a structure and behavior
matching the requirements of the PL (in effect, matching the needs of the UI). In our example, the
PM Person class would have a FullName property rather than FirstName and LastName properties
found in the Domain Model Person class.

Why not just put the GetFullName() method in the Domain Model Person class? We could, if it had
a use in some business logic operation, but if the only use of the GetFullName() method is in the
PL, the method should go in the PM and not in the Domain Model.

Keeping your Domain Model free of non-business aspects, such as presentation and persistence, is
every bit as important as it was to keep the Business Logic Layer of yesteryear free of Presentation
logic and Data Access logic, and for just the same reason: Keeping the Domain Model free from any
non-business aspects is key to keeping the "heart" of your application understandable and
maintainable.

So for this example, assume that GetFullName() is only used in presentation and is thus a good
candidate for a method that should go on a PM rather than on the Domain Model.

The question becomes how we can connect the PM classes to the Domain Model classes, and thus
we arrive at the choice: *Mapping* or *Wrapping*?

# Wrapping the Domain Model with the Presentation Model

Wrapping is often the easier solution, requiring no additional framework for state management in
the PM. The idea here is that you pass the DM Employee object to the constructor method of the PM
Employee object. The PM Employee then keeps an internal reference to the DM object and delegates
all calls to the DM properties. See the following code listing.

```
```csharp
//Presentation Model wrapper object
namespace MyCompany.MyApplication.Presentation
{
    public class EmployeeWrapper
    {
        private Employee employee;

        public EmployeeWrapper (Employee employee)
        {
            this.employee = employee;
        }

        public int Id
        {
            get { return this.employee.Id; }
            set { this.employee.Id == value; }
        }

        public string FullName
        {
            get
```
```