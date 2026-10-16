```
double sum = 0.0;
char middleInitial = 'C';
```

for example, we could write

```
double sum(0.0);
char middleInitial('C');
```

The syntax using `=` is simply provided as a convenient shorthand to this approach.²

# 14.3.2.6 Accessor Methods

Now that we have constructors, we turn to implementing other operations of class Temperature, starting with some of the simplest ones. An **accessor method** retrieves the value of a data member of the class but may not modify it.³ For example, sending the message

```
temp1.getDegrees()
```

to Temperature object temp1 will retrieve the number of degrees in temp1, and the message

```
temp1.getScale()
```

will retrieve its scale.

Specifications for these function members are straightforward:

+   - **Return:** myDegrees
+     for getDegrees() and
+   - **Return:** myScale
+     for getScale().

Example 14.5 shows their definitions. Because they are simple, we inline them and store their definitions in the class header file Temperature.h, and because they read but do not modify the data members, they are designated as const methods.

```
**Example 14.5  Temperature Accessors**

// -------- Degrees extractor ------------------------------
inline double Temperature::getDegrees() const
{
    return myDegrees;
}

// -------- Scale extractor -------------------------------
```