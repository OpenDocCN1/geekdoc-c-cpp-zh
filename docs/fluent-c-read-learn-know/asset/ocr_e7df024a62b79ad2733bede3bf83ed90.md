# FIELDS AND PROPERTIES

I bet you'd tell just about anybody the name of your bank, but even your close friends probably don't know exactly how much you have in your checking account, and if you let more than one or two people have access to the account itself, you're far more trusting than I am. (Or you live in a commune.)

When you transfer this principle to programming, it's called Information Hiding, and we'll look at it again in Chapter 12. Access modifiers are a big part of information hiding—best practice dictates that everything is on a need to know basis—but in the context of a class definition, it's also implemented by the combination of a private field, called a backing field, and a public property that allows you to control how information is seen or changed. The basic pattern looks like this:

```
private <type> m_name
```

```
public <type> Name
{
    get {...}
    set {...}
}
```

The actual data is stored in the private field. Nobody gets to touch it, or even see it, outside the class definition.

The data is made available outside the class as a public property. The get clause lets you do thing like format it for display, while the set clause lets you check the data before you update the field.

Both the get and set clauses (called ACCESSORS) are optional. We'll talk about the implications of that in a few pages.