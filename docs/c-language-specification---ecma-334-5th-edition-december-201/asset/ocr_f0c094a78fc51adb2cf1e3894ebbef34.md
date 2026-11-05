# Example:

```
/// <summary>A generic_list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
public class MyList<T> {
    """
}
```

# D.3.18 <typeparamref>

This tag is used to indicate that a word is a type parameter. The documentation file can be processed to format this type parameter in some distinct way.

# Syntax:

```
<typeparamref name="name"/>
```

where

*name*

The name of the type parameter.

# Example:

```
/// <summary>This method fetches data and returns a list of <typeparamref name="T" />.</summary>
/// <param name="string">query to execute</param>
public List<T> FetchData<T>(string query) {
    """
}
```

# D.3.19 <value>

This tag allows a property to be described.

# Syntax:

```
<value>property description</value>
```

where

*property description*

A description for the property.

# D.4 Processing the documentation file

# D.4.1 General

The following information is intended for C# implementations targeting the CLI.

The documentation generator generates an ID string for each element in the source code that is tagged with a documentation comment. This ID string uniquely identifies a source element. A documentation viewer can use an ID string to identify the corresponding item to which the documentation applies.

The documentation file is not a hierarchical representation of the source code; rather, it is a flat list with a generated ID string for each element.

# D.4.2 ID string format

The documentation generator observes the following rules when it generates the ID strings: