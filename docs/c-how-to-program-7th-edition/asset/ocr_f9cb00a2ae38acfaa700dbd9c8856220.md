properly copies objects. If a particular user-defined type will not work with our Stack template or requires customized processing, you can define an explicit specialization of the class template for a particular type. Let’s assume we want to create an explicit specialization Stack for Employee objects. To do this, form a new class with the name Stack< Employee > as follows:

```
```cpp
template<>
class Stack< Employee >
{
    // body of class definition
};
```
```

The Stack<Employee> explicit specialization is a complete replacement for the Stack class template that is specific to type Employee—it does not use anything from the original class template and can even have different members.

# ## 14.6 Notes on Templates and Inheritance

Templates and inheritance relate in several ways:

+   - A class template can be derived from a class-template specialization.
+   - A class template can be derived from a nontemplate class.
+   - A class-template specialization can be derived from a class-template specialization.
+   - A nontemplate class can be derived from a class-template specialization.

# ## 14.7 Notes on Templates and Friends

We’ve seen that functions and entire classes can be declared as friends of nontemplate classes. With class templates, friendship can be established between a class template and a global function, a member function of another class (possibly a class-template specialization), or even an entire class (possibly a class-template specialization).

Throughout this section, we assume that we’ve defined a class template for a class named X with a single type parameter T, as in:

```
```cpp
template< typename T > class X
```
```

Under this assumption, it’s possible to make a function f1 a friend of every class-template specialization instantiated from the class template for class X. To do so, use a friendship declaration of the form

```
```cpp
friend void f1();
```
```

For example, function f1 is a friend of X< double >, X< string > and X< Employee >, etc.

It’s also possible to make a function f2 a friend of only a class-template specialization with the same type argument. To do so, use a friendship declaration of the form

```
```cpp
friend void f2( X< T > & );
```
```

For example, if T is a float, function f2( X< float > & ) is a friend of class-template specialization X< float > but not a friend of class-template specialization X< string >.

You can declare that a member function of another class is a friend of any class-template specialization generated from the class template. To do so, the friend declaration