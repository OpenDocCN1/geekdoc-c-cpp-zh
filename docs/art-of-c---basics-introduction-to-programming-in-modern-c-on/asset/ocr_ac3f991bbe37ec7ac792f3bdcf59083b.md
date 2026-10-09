```
private string name;
public string Name {
    get => name;
    set => name = value;
}

```

Here value is a special predefined variable to denote the value from the assignment expression in the setters.

In this example, name is a "field". Although it is legal to have a public field, the fields are almost always private. We typically use properties if the field data need to be exposed in some way.

You can access a property using the dot notation. For example, The following gets the Name (from an object called person) and assigns it to a variable name:

```
var name = person.Name;

```

You can assign a new name to the person object using the setter:

```
person.Name = "new name";

```

In this example, the string literal "new name" will be passed in to the setter definition as the special value, value.

Unless there is a special requirement for the getters and/or setters for data, using auto properties works just fine and it often leads to a more compact and more readable code.

Of course, the properties do not entirely eliminate the need for the "fields". Some data may be truly private to a class, or specific to a particular implementation, and they may not need an exposure through properties. (Although private auto-