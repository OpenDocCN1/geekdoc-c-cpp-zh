# # The Parts of a CSS Rule

```
selector { property: value; }
```

All rules, regardless of their locations or types, having the structural elements:

+   - Selectors are the alphanumeric characters that identify a rule. A selector can be an HTML tag selector, a class selector, an ID selector, a universal selector (described in Chapter 3) or a combination of those basic selectors to create context-based styles (discussed in Chapter 4).

+   - Properties identify what is being defined. Several dozen properties are available; each is responsible for an aspect of the page content's behavior and appearance.

+   - Values are assigned to a property to define its nature. A value can be a keyword such as "red", a number, or a percentage. The type of value used depends solely on the property to which it is assigned.

After the selector A, properties and their values, which together are referred to as a declaration. A single CSS rule can have multiple declarations separated by a semicolon ().

# ## Browser CSS extensions

In addition to the specified CSS properties set by the W3C, a browser developer will occasionally introduce browser-specific properties. This is often done for one of two reasons:

+   - A spec is still under development by the W3C but the browser developer wants to start using the style now.

+   - The browser developer wants to try a new idea but doesn't want to wait for the W3C to accept it and begin work on it, which can take years.

The basic syntax of a CSS rule. This starts with a selector (HTML, Class, or ID). Then add a property, a value for that property, and a semicolon, which together are called a definition. You can add as many definitions as you need long as they are separated by a semicolon.