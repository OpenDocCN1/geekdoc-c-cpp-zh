Wait a minute; we're not done yet. I do not want to create the false impression that the class design is a quick easy task, just decide about the operations you want to support, choose the private, protected and public members and you are done. Even this is a difficult decision. For example, wouldn't be safer and easier in order to control the class to have no public members at all and to have set()/get() public functions to access the class data? Much worse, think about creators. When providing a class to the outside world (e.g., string) you must ensure that the protection of the class, as well as protected in the case of a derived class, is functional and won't change or over. Any changes the developer of the class makes to the design should be related to the implementation code, not the public interface. Imagine that the programmers who already use the class be forced to change their code often because of a new version of the class that the public functions changed or some public members were removed.

Also, when designing a class, besides its operations, you have to decide on many of its features, such as what would be the valid values of its (e.g., in a Time class, the valid range for the hour member is 0-24), if the class would overload operators, if it'd be used as a base class, if it would contain virtual functions, if you use the default functions or others you specify, if it'd allow conversion from/to another, and many more "ifs". Who said the design is an easy job?

# Structures/Unions and Classes

The concept of structure and how to use variables is very similar to the class and objects. Indeed, the difference is that the members of a class are private by default, while the members of a structure are public by default. A similar difference, as we will see in Chapter 19, is that a derived class inherits a base class with private access, while a derived structure has public access. Since there is no fundamental difference between them, someone might ask, couldn't we have one type, struct and class, and just change the default access if needed? Why not? Reasonable to wonder, I'm not sure about the answer. I imagine that in the beginning, the struct type was pre-existing in C and because object-oriented features were new programming concepts that had not yet spread, Stroustrup would like to introduce a new type in C++ with focus on object-oriented operations. Then, it was decided that the struct type would also support object-oriented operations.

The common practice is to use a class when both variables and functions are needed to represent an entity, while the structure is used when only variables are required. Also, if the members are public only, the structure is usually chosen, while if there are private members all, the class is chosen.

Regarding unions, we know from Chapter 13, only one of its members has a valid value. As with structure, the members of a union are public by default. A union supports the properties of the class, but not all. For example, a union may contain public, private, and protected sections. It can also contain member functions including constructors and destructors. However, a union cannot be used as a base class, nor can it inherit another class. Therefore, it cannot contain virtual functions.

# const Member Functions

In our first example C.17.1, the show() function can change the values of the object that it calls. For

```
void Student::show()
{
    grd = 2;
    }
```