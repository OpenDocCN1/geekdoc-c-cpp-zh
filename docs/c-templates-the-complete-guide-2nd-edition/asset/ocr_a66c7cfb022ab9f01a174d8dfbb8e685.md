class Integer { ... };
Integer const operator+ (Integer const&, Integer const&); Adding two Array<Integer> values will result in an array of Integer const, which is most likely not what we intended. In fact, what we want is to transform the result type by removing references and qualifiers, as discussed in the previous section: Click here to view code image
template<typename T1, typename T2>
Array<RemoveCV<RemoveReference<PlusResult<T1, T2>>>>
operator+ (Array<T1> const&, Array<T2> const&); Such nesting of traits is common in template libraries and is often used in the context of metaprogramming. Metaprogramming will be covered in detail in Chapter 23. (The convenience alias templates are particularly helpful with multilevel nesting like this. Without them, we’d have to add a typename and a ::Type suffix at every level.) At this point, the array addition operator properly computes the result type when adding two arrays of (possibly different) element types. However, our formulation of PlusResultT places an undesirable restriction on the element types T1 and T2: Because the expression T1() + T2() attempts to value-initialize values of types T1 and T2, both of these types must have an accessible, nondeleted, default constructor (or be nonclass types). The Array class itself might not otherwise require value-initialization of its element type, so this is an additional, unnecessary restriction.

# declval

Fortunately, it is fairly easy to produce values for the + expression without requiring a constructor, by using a function that produces values of a given type T. For this, the C++ standard provides std::declval<>, as introduced in Section 11.2.3 on page 166. It is defined in <utility> simply as follows:
Click here to view code image

```
namespace std {
template<typename T>
add_rvalue_reference_t<T> declval() noexcept;
}
```

The expression declval<T>() produces a value of type T without requiring a default constructor (or any other operation).

This function template is intentionally left undefined because it’s only meant to be used within decltype, sizeof, or some other context where no definition is ever needed. It has two other interesting attributes: • For referenceable types, the return type is always an rvalue reference to the type, which allows declval to work even with types that could not normally be returned from a function, such as abstract class types (classes with pure virtual