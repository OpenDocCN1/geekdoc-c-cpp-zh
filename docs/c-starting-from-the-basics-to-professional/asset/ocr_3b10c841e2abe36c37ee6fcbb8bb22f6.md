The first constructor is declared as `explicit` to prevent its use for implicit conversions. The second constructor is the copy constructor. Together with the copy assignment operator it allows `Array<T>` objects to be deep-copied from others, which is something you can’t do with ordinary arrays. If you wanted to inhibit this capability, you should declare these members with `= delete` to prevent the compiler from supplying the default (as shown in Chapter 13).

The subscript operator has been overloaded on `const`. The non-const version of the subscript operator applies to non-const array objects and returns a non-const reference to an array element. Thus, this version can appear on the left of an assignment. The const version is called for const objects and returns a const reference to an element; obviously this version cannot appear on the left of an assignment.

The copy members both accept a parameter of type `const Array<T>&`. This type is reference to const `Array<T>`. When a class is synthesized from the template this is a reference to the class name for that particular class. With `T` as type `double`, for example, this would then be `const Array<double>&`. More generally, the class name for a specific instance of a template is formed from the template name followed by the template arguments between angle brackets. The template name followed by the list of parameter names between angle brackets is called the *template ID*.

It’s not essential to use the full template ID within a template definition. Within the body of the Array template, Array by itself will always be taken to mean `Array<T>`. This means we can simplify the class template as follows:

```
```cpp
template <typename T>
class Array
{
public:
  explicit Array(size_t size);        // Constructor
  ~Array();                           // Destructor
  Array(const Array& array);          // Copy constructor
  Array& operator=(const Array& rhs); // Copy assignment operator

  // Other members remain the same...
};
```
```

# Defining Member Functions of a Class Template

The syntax for defining members outside of the template body is a little different from what applies to a normal class. The clue to understanding this syntax is to realize that external definitions for member functions of a class template are themselves templates. This is true even if a member function has no dependence on the type parameter `T`. So even `getSize()`, for instance—which always returns the same value of type `size_t`, irrespective of the value of `T`—would need a template definition if we hadn’t defined it inside the class template already. The parameter list for the template that defines a member function must always match that of the class template. That is, you cannot, for instance, omit template parameters that the member function template does not need (see also later).

All member function definitions that you’ll write in this section are templates that are inextricably bound to the `Array<>` class template. They are not function definitions; they’re templates to be used by the compiler when the code for one of the member functions of the class template needs to be generated.