# 12.8.16.4 Collection initializers

A collection initializer specifies the elements of a collection.

```
collection_initializer
  : '{' element_initializer_list '}'
  | '{' element_initializer_list ',' '}'
  ;

element_initializer_list
  : element_initializer (',' element_initializer)*
  ;

element_initializer
  : non_assignment_expression
  | '{' expression_list '}'
  ;

expression_list
  : expression
  | expression_list ',' expression
  ;
```

A collection initializer consists of a sequence of element initializers, enclosed by { and } tokens and separated by commas. Each element initializer specifies an element to be added to the collection object being initialized, and consists of a list of expressions enclosed by { and } tokens and separated by commas. A single-expression element initializer can be written without braces, but cannot then be an assignment expression, to avoid ambiguity with member initializers. The non_assignment_expression production is defined in §12.22.

Example: The following is an example of an object creation expression that includes a collection initializer:

```
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

end example

The collection object to which a collection initializer is applied shall be of a type that implements System.Collections.IEnumerable or a compile-time error occurs. For each specified element in order from left to right, normal member lookup is applied to find a member named Add. If the result of the member lookup is not a method group, a compile-time error occurs. Otherwise, overload resolution is applied with the expression list of the element initializer as the argument list, and the collection initializer invokes the resulting method. Thus, the collection initializer shall contain an applicable instance or extension method with the name Add for each element initializer.

Example: The following shows a class that represents a contact with a name and a list of phone numbers, and the creation and initialization of a List<Contact>:

```
public class Contact
{
    public string Name { get; set; }
    public List<string> PhoneNumbers { get; } = new List<string>();
}

class A
{
    static void M()
```