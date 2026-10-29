| ACCESS SPECIFIER IN BASE CLASS | TYPE OF INHERITANCE (SPECIFIER AFTER CLASS NAME IN DERIVED CLASS DEFINITION) |  |  |
|---|---|---|---|
|  | `public` | `protected` | `private` |
| `public` | Public | Protected | Private (Can only be used by name in definitions of member functions and friends) |
| `protected` | Protected | Protected | Private (Can only be used by name in definitions of member functions and friends) |
| `private` | Cannot be accessed by name in the derived class | Cannot be accessed by name in the derived class | Cannot be accessed by name in the derived class |

Entries show how inherited members are treated in the derived class.

> Note that protected and private inheritance are not inheritance in the sense we described for public inheritance. With protected or private inheritance, the base class is only a tool to be used in the derived class.

# Multiple Inheritance

It is possible for a derived class to have more than one base class. The syntax is very simple: All the base classes are listed, separated by commas. However, the possibilities for ambiguity are numerous. What if two base classes have a function with the same name and parameter types? Which is inherited? What if two base classes have a member variable with the same name? All these questions can be answered, but these and other problems make multiple inheritance a very dangerous business. Some authorities consider multiple inheritance so risky that it should not be used at all. That may or may not be too extreme a position, but it is true that you should not seriously attempt multiple inheritance until you are a very experienced C++ programmer. At that point, you will realize that you can almost always avoid multiple inheritance by using some less dangerous technique. We will not discuss multiple inheritance in this book but leave it for more advanced references.