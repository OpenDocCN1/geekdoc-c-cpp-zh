grew out of Smalltalk. Today, the most significant software design methodologies and programming languages are object oriented. Although the origin of some of the ideas of object-oriented languages came from SIMULA 67, they reached maturation in Smalltalk. It is clear that Smalltalk's impact on the computing world is extensive and will be long-lived.

The following is an example of a Smalltalk class definition:

```
"Smalltalk Example Program"
"The following is a class definition, instantiations of which
can draw equilateral polygons of any number of sides"
class name                       Polygon
superclass                       Object
instance variable names          ourPen
numSides
sideLength
"Class methods"
    "Create an instance"
    new
        ^super new getPen

    "Get a pen for drawing polygons"
    getPen
        ourPen <- Pen new defaultNib: 2

    "Instance methods"
    "Draw a polygon"
    draw
        numSides timesRepeat: [ourPen go: sideLength;
                                  turn: 360 // numSides]

    "Set length of sides"
    length: len
    sideLength <- len

    "Set number of sides"
    sides: num
        numSides <- num
```

# 2.16 Combining Imperative and Object-Oriented Features: C++

The origins of C were discussed in Section 2.12; the origins of Simula 67 were discussed in Section 2.10; the origins of Smalltalk were discussed in Section 2.15. C++ builds language facilities, borrowed from Simula 67, on top of C to support much of what Smalltalk pioneered. C++ has evolved from C through a sequence of modifications to improve its imperative features and to add constructs to support object-oriented programming.