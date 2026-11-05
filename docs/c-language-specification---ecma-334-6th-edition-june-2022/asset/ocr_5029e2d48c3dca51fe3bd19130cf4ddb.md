An `abstract` property declaration specifies that the accessors of the property are virtual, but does not provide an actual implementation of the accessors. Instead, non-abstract derived classes are required to provide their own implementation for the accessors by overriding the property. Because an accessor for an abstract property declaration provides no actual implementation, its *accessor body* simply consists of a semicolon. An abstract property shall not have a `private` accessor.

A property declaration that includes both the `abstract` and `override` modifiers specifies that the property is abstract and overrides a base property. The accessors of such a property are also abstract. Abstract property declarations are only permitted in abstract classes (§14.2.2.2). The accessors of an inherited virtual property can be overridden in a derived class by including a property declaration that specifies an `override` directive. This is known as an *overriding property declaration*. An overriding property declaration does not declare a new property. Instead, it simply specializes the implementations of the accessors of an existing virtual property.

The `override` declaration and the overridden base property are required to have the same declared accessibility. In other words, an `override` declaration may not change the accessibility of the base property. However, if the overridden base property is protected internal and it is declared in a different assembly than the assembly containing the override declaration then the override declaration's declared accessibility shall be protected. If the inherited property has only a single accessor (i.e., if the inherited property is read-only or write-only), the overriding property shall include only that accessor. If the inherited property includes both accessors (i.e., if the inherited property is read-write), the overriding property can include either a single accessor or both accessors. There shall be an identity conversion between the type of the overriding property and the inherited property.

An overriding property declaration may include the `sealed` modifier. Use of this modifier prevents a derived class from further overriding the property. The accessors of a sealed property are also sealed.

Except for differences in declaration and invocation syntax, `virtual`, `sealed`, `override`, and `abstract` accessors behave exactly like `virtual`, `sealed`, `override` and `abstract` methods. Specifically, the rules described in §14.6.4, §14.6.5, §14.6.6, and §14.6.7 apply as if accessors were methods of a corresponding form:

+   - A `get` accessor corresponds to a parameterless method with a return value of the property type and the same modifiers as the containing property.
+   - A `set` accessor corresponds to a method with a single value parameter of the property type, a void return type, and the same modifiers as the containing property.

*Example:* In the following code

```
~~~csharp
abstract class A
{
    int y;

    public virtual int X
    {
        get => 0;
    }

    public virtual int Y
    {
        get => y;
        set => y = value;
    }
}
~~~
```