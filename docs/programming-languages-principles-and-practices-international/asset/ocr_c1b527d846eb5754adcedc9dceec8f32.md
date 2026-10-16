The functions to the right of the equal signs are all built-in definitions that are hidden inside the standard library modules.

Haskell determines the type of the square function by looking for the symbol * in a class definition (because the body of square depends on the availability of *) and applying the appropriate qualification. Then, the square function can be applied to any value whose type is an instance of the Num class.

There is, however, more structure to type classes than this simple description suggests. In the case of Int, for example, the Num class does not describe all of the functions that need to be available, such as equality tests and order functions like <. Nor does the Int instance include the functions div and mod. The Num class above does not even require any division operation. Additional type classes do require these functions. The class Eq requires the equality operator ==, the class Ord requires the less-than operator <, and the class Integral requires the div and mod operations. To provide full capability, Int should be defined to be an instance of all of these type classes. To accomplish this, many of the type classes themselves are defined to be part of other type classes, so that any instances are forced to be instances of these other classes as well. This dependency of type classes on other type classes is called type class inheritance. Type inheritance relies upon a hierarchy of type classes. Two type classes at the base of this hierarchy are the Eq and Show classes. The class Show is used to establish the existence of a show function, which is used to display values of member types. All predefined Haskell types are instances of the Show class. The class Eq establishes the ability of two values of a member type to be compared using the == operator. Most types are instances of Eq. However, function types are not, because the equality of functions cannot be defined in a way that would provide useful information.

Here is a complete definition of the Eq class from the Haskell standard library:

```
class Eq a where
  (==), (/=) :: a -> a -> Bool
  x == y  = not (x/=y)
  x /= y  = not (x==y)
```

This class definition shows an additional feature: the use of default definitions for the required functions. Such default definitions are typically based on other required functions. In the preceding code, the default definition of /= (not equal) depends on the definition of == being available, and the default definition of == depends on the definition of /= being available. This apparent circularity means that, for a type to be declared an instance of Eq, only one of the two required functions needs to be defined, with the other implicitly defined by default. For example, Int is defined to be an instance of Eq as follows:

```
instance Eq Int where (==) = primEqInt
```

To establish the inheritance requirements for each type class, Haskell uses a notation similar to type qualification. For example, the definition of the Num class in the Haskell standard library begins as follows:

```
class (Eq a, Show a) => Num a where ...
```