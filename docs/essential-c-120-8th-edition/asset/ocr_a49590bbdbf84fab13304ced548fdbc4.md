# 472 Chapter 8: Interfaces

TABLE 8.1: Default Interface Refactoring Features (continued)

| C# 8.0-Introduced Interface Construct | Sample Code |
|--- |--- |
| private protected Access Modifier Accessing a protected member is only possible from the containing interface or interfaces that derive from the implementing interface. Even classes implementing the interface cannot access a protected member, as demonstrated by the PersonTitle property in Person. | ```csharp
class Program{
    static void Main()
{
        IPerson person = null;
        // Non-deriving classes cannot access
        // private protected member.
        Console.WriteLine(person?.GetName());
    }

    public interface IPerson
{
        string FirstName { get; }
        string LastName { get; }
        string Name => GetName();
        private protected string GetName() => $"{FirstName} {LastName}";
    }

    public interface IEmployee
{
        int EmployeeId => Employee.GetHashCode();
    }

    public class Person : IPerson
{
        public Person(string firstName, string lastName)
        {
            FirstName = firstName ?? throw new ArgumentNullException(nameof(firstName));
            LastName = lastName ?? throw new ArgumentNullException(nameof(lastName));
        }

        public string FirstName { get; }
        public string LastName { get; }
        // private protected interface members
        // are not accessible in derived classes.
        public public int PersonTitle => GetName().ToUpper();
    }
``` |