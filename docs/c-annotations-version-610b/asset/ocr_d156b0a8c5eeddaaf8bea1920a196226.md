```
```cpp
{
    d_data.push_back(
        d_is polymorphic ?
            obj.clone()
        :
            new Type(obj)
    );
}
```
```

The intent is to use the `clone` member function of the class `Type` if `Type` is a polymorphic class and the standard copy constructor if `Type` is a value class.

Unfortunately, this scheme usually fails as value classes do not define `clone` member functions and polymorphic base classes should delete their copy constructors (cf. section 7.5). It doesn’t matter to the compiler that `clone` is never called for value classes and that the copy constructor is only available in value classes and not in polymorphic classes. It merely has some code to compile, and can’t do that because of missing members. It’s as simple as that.

# ### 22.2.2.1 Defining overloading members

Template meta programming comes to the rescue. Knowing that class template member functions are only instantiated when used, our plan is to design overloaded add member functions of which only one is going to be called (and thus instantiated). Our selection will be based on an additional (in addition to `Type` itself) template non-type parameter that indicates whether we’ll use `Storage` for polymorphic or non-polymorphic classes. Our class `Storage` starts like this:

```
```cpp
template <typename Type, bool isPolymorphic>
class Storage
```
```

Initially two overloaded versions of our `add` member are defined: one used with `Storage` objects storing polymorphic objects (using `true` as its template non-type argument) and one storing value class objects (using `false` as its template non-type argument).

Unfortunately we run into a small problem: functions cannot be overloaded by their argument values but only by their argument types. But the small problem may be solved. Realizing that types are defined by the combination of template names and their template arguments we may convert the values `true` and `false` into types using the knowledge from section 22.2.1.1 about how to convert integral values to types.

We’ll provide one (private) `add` member with a `IntType<true>` parameter (implementing the polymorphic class) and another (private) `add` member with a `IntType<false>` parameter (implementing the non-polymorphic class).

In addition to these two private members a third (public) member `add` is defined calling the appropriate private `add` member by providing an `IntType` argument, constructed from `Storage`’s template non-type parameter.

Here are the implementations of the three add members:

```
```cpp
// declared in Storage’s private section:

template <typename Type, bool isPolymorphic>
void Storage<Type, isPolymorphic>::add(Type const &obj, IntType<true>)
{
    d_data.push_back(obj.clone());
}

template <typename Type, bool isPolymorphic>
```
```