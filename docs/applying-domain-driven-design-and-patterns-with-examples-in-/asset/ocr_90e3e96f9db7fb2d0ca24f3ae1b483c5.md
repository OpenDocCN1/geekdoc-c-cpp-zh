In fact, the O/O Mapper could even write directly to the private fields of the PM objects, so you wouldn't have to implement the protected properties at all indeed, the mapper probably should access the private fields directly in order to avoid triggering side effects in the property getters and setters that should only be invoked when client code accesses the properties, not when the framework wants to move data.

However, some O/O Mappers may offer advanced features (such as Lazy Loading) that depend on properties being there so that access to them can be intercepted, and so you may want to keep the properties around for that reason. The following code listing shows a PM object that relies on O/O Mapping.

```
```csharp
//Presentation Model object that relies on O/O Mapping
namespace MyCompany.MyProject.Presentation
{
    public class EmployeeView
    {
        private int id;
        private decimal salary;
        private string firstName;
        private string lastName;

        public EmployeeView() { }

        public int Id
        {
            get { return this.id; }
            set { this.id = value; }
        }

        public decimal Salary
        {
            get { return this.salary; }
            set { this.salary = value; }
        }

        protected string FirstName
        {
            get { return this.firstName; }
            set { this.firstName = value; }
        }

        protected string LastName
        {
            get { return this.lastName; }
            set { this.lastName = value; }
        }

        public string FullName
        {
            get
            {
                return this.firstName + " " +
```
```