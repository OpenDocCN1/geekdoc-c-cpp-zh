# A New Version of the Student Class Example

To get private inheritance, use the keyword private instead of public when defining the class. (Actually, private is the default, so omitting an access qualifier also leads to private inheritance.) The Student class should inherit from two classes, so the declaration should list both:

```
class Student : private std::string, private std::valarray<double>
{
public:
    ...
};
```

Having more than one base class is called multiple inheritance (MI). In general, MI, particularly MI, can lead to problems that have to be resolved with additional syntax rules. We'll talk about such matters later in this chapter. But in this particular case, MI has no problems.

Note that the new class doesn't need private data.That because the inherited classes already provide all the needed data members. The containment version of this example provides two explicitly named objects as members. Private inheritance, however, provides two nameless subclasses as inherited members. This is one of the main differences in the two approaches.

# Initializing Base-Class Components

Having implicitly inherited components instead of member objects affects the coding of this example because you can no longer use name and scores to describe the objects. Instead, you have to go back to the techniques used for public inheritance. Containment uses this constructor for example, consider constructors.

```
Student(const char * str, const double * pd, int n)
    : name(str), scores(pd, n) {} // use object names for containment
```

The new version should use the member initializer list for inherited classes, which uses the class name of member to identify a constructor:

```
Student(const char * str, ArrayDB*pd, int n)
    : std::string(str), ArrayDB(pd, n) {} // use class names for inheritance
```

Here, in the preceding example, ArrayDB is a typedef of std::array<double>. Be sure to note that the member initializer list uses terms as std::string(str) instead of name(str). This is the second main difference in the two approaches

Listing 14.4 shows the new declaration. The only changes are the omission of explicit object names and the use of class names instead of member names in the inline constructors.