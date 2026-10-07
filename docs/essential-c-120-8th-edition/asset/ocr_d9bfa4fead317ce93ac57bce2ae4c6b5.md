# Overriding the Base Class

TABLE 7.1: Why the New Modifier? (continued)

| Activity | Code |
|---|---|
| Programmer B derives from Person and defines Contact with the additional property Name, In addition, he defines the Program class whose Main() method instantiates Contact, and then prints out the name. | `public class Contact : Person {
public string Name {
get
return FirstName + " " + LastName;
set
string[] names = value.Split('/');
// Error handling not shown
FirstName = names[0];
LastName = names[1];
}` |

Because Person.Name is not virtual, Programmer A expects Display() to use the Person implementation, even if a Person-derived data type, Contact, is passed in. However, Programmer B expects Contact.Name to be used in all cases where the variable type is a Contact. (Programmer B has no code where Person.Name was used, since no Person.Name property existed (initially).) To allow the addition of Person.Name without breaking either programmer's expected behavior, you cannot assume virtual was intended. Furthermore, because C# requires an override member to explicitly use the override modifier, some other semantic must be assumed instead of allowing the addition of a member in the base class to cause the derived class to no longer compile.

This semantic is the new modifier, which hides a redeclared member of the derived class from the base class. Instead of calling the most derived member, a member of the base class calls the most derived member in the inheritance chain prior to the member with the new modifier. If the inheritance contains only two classes, a member in the base class will behave as though no method was declared on the derived class (if the derived implementation overrides the base class member). Although the compiler will report the warning in either Output 7.2 or Output 7.3, if neither override nor new is specified, new will be assumed, thereby maintaining the desired version safety.