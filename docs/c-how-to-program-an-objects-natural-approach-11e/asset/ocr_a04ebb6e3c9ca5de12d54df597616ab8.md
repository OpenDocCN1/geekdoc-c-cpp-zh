The **constraint expression** is a compile-time logical expression that determines whether a template argument satisfies a particular set of requirements—in this case, an integer or floating-point type. Constraint expressions commonly include predefined concepts, type traits and, as you’ll see in Section 15.6.5, **requires expressions** that enable you to specify other requirements. The **Numeric** concept’s template header has one type parameter representing the type to test.

Concepts with multiple template parameters also can specify relationships between types.<sup>44</sup> For example, if a template has two type parameters, you can use the predefined concept **std::same_as** to ensure two type arguments have the same type, as in:

```
```cpp
template<typename T, typename U>
    requires std::same_as<T, U>
// rest of template definition
```
```

In Section 15.12, we’ll introduce variadic templates that can have any number (of type or non-type) template arguments. There, we’ll use **std::same_as** in a variadic function template that requires all its arguments to have the same type.

# ### 15.6.2 Using a Concept

Once you define a concept, you can use it to constrain a template parameter in one of four ways. We show the first three here and the fourth in Section 15.6.5.

# #### requires Clause Following the template Header

Any concept can be placed in a **requires** clause following the template header, as we did in Fig. 15.5. Here’s our multiply function template using the custom concept `Numeric<T>`:

```
```cpp
template<typename T>
    requires Numeric<T>
T multiply(T first, T second) {return first * second;}
```
```

# #### requires Clause Following a Function Template’s Signature

You also can place the **requires** clause after a function template’s signature and before the function template’s body, as in:

```
```cpp
template<typename T>
T multiply(T first, T second) requires Numeric<T> {
    return first * second;
}
```
```

A trailing **requires** clause must be used in two scenarios:<sup>45</sup>

+   - A member function defined in a class template’s body does not have a template header, so you must use a trailing requires clause.
+   - To use a function template’s parameter names in a constraint, you must use a trailing requires clause so the parameter names are in scope before the compiler evaluates the requires clause.

44. Bjarne Stroustrup, “Concepts: The Future of Generic Programming—3.1 Specifying Template Interfaces,” January 31, 2017. Accessed April 18, 2023, https://wg21.link/p0557r0.

45. “What Is the Difference Between the Three Ways of Applying Constraints to a Template?” Accessed April 18, 2023. https://stackoverflow.com/a/61875483. [Note: The original stackoverflow.com question mentioned three ways of applying constraints to a template, but there are four, and each is mentioned in the cited answer.]