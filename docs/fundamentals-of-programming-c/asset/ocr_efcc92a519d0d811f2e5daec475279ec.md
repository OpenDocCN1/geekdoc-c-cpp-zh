# 17.3. USES OF INHERITANCE

);

We want to assign the constructor's first parameter, t, to the inherited member text, but text is private in the base class. This means the FancyText constructor cannot initialize it directly. Since the constructor of its base class knows what to do with this parameter, the first expression in the constructor initialization list (the part between : and the {):

... ...

# Text (t)

explicitly calls the base class constructor, passing t. This base class initialization expression must be the first thing in the initialization list because C++ requires that the parts of an object inherited from its base class initialized before any new parts (added by the derived class) are initialized. The next three expressions in the initialization list:

```
... left_bracket(left), right_bracket(right), connector(conn) ...
```

initialize left_bracket, and connector fields as usual. The body of the constructor is empty as no other initialization is necessary.

The FixedText class is somewhat different from the FancyText class. It adds fields and does not override the get method. Its constructor accepts no parameters classes are permitted to determine the contents of the wrapped string—the text is always the FIXED. It inherits the text field and get method (as it does) from Text class.

Given the Text and FancyText classes defined in Listing 17.2 (fancytext.cpp), the following client code is legal:

```
Text t1("ABC");
FancyText t2("XYZ", "[", ":");
cout << t1.get() << " " " << t2.get() << endl;
t1 = t2;
cout << t1.get() << " " " << t2.get() << endl;
```

Since t2's declared type is FancyText, by virtue of inheritance, t2 is a Text object as well. The following code fragments

![](bbox=[0.118, 0.654, 0.783, 0.714])

Notice the assignment

```
t1 = t2;
```

copied into object t1 only the fields that FancyText has in common with Text objects; that, the text field. Since t1 is a plain Text object, it does the left_bracket, right_bracket, and connector fields capable of storing additional data contained in a FancyText object. This process of losing derived data when assigning to a base class is known as object slicing. The parts that will not fit into the base class instance are "sliced" off. Figure 17.1 illustrates object slicing. Note that assignment in the other direction:

```
t2 = t1; // Illegal
```