this practice, when you add code such as validation code, the entire class immediately takes advantage of it.⁵

Although rare, it is possible to assign value inside the setter, as Listing 5.19 does. In this case, the call to value.Trim() removes any whitespace surrounding the new last name value.

# Guidelines

AVOID accessing the backing field of a property outside the property, even from within the containing class.

DO use "value" for the paramName argument when calling the ArgumentException() or ArgumentNullException() constructor ("value" is the implicit name of the parameter on property setters).

# ADVANCED TOPIC

# nameof Operator

If during property validation you determine that the new value assignment is invalid, it is necessary to throw an exception—generally of type ArgumentException() or ArgumentNullException(). Both of these exceptions take an argument of type string called paramName that identifies the name of the parameter that is invalid. In Listing 5.19, we pass "value" as the argument for this parameter, but C# 6.0 provides an improvement with the nameof operator. The nameof operator takes an identifier, like the value variable, and returns a string representation of that name—in this case, "value".

The advantage of using the nameof operator is that if the identifier name changes, then refactoring tools will automatically change the argument to nameof as well. If no refactoring tool is used, the code will no longer compile, forcing the developer to change the argument manually.

In the case of a property validator, the "parameter" is always value and cannot be changed, so the benefits of leveraging the nameof operator are

5. As described later in the chapter, one exception to this occurs when the field is marked as read-only, because then the value can be set only in the constructor. In C# 6.0, you can directly assign the value of a read-only property, completely eliminating the need for the read-only field.