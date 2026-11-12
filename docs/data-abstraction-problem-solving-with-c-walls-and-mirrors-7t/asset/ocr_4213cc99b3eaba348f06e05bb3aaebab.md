the recipe contains measurements such as 2 1/2 cups, 1 tablespoon, and 1/4 teaspoon. That is, the quantities are given as mixed numbers—integers and fractions—in units of cups, tablespoons, and teaspoons.

This problem suggests another ADT—measurement—with the following operations:

```
// Returns this measure.
+getMeasure(): Measurement
// Sets this measure to another one.
+setMeasure(m: Measurement)
// Returns this measure multiplied by a fractional scale factor, which has no units.
+scaleMeasure(scaleFactor: float): Measurement
// Returns this measure converted from its old units to new units.
+convertMeasure(oldUnits: MeasurementUnit,
newUnits: MeasurementUnit): Measurement
```

Suppose that you want the ADT measurement to perform exact fractional arithmetic. Because our planned implementation language C++ does not have a data type for fractions, and floating-point arithmetic is not exact, another ADT called fraction is in order. Its operations could include addition, subtraction, multiplication, and division of fractions. For example, you could specify addition as

```
// Returns the sum, reduced to lowest terms, of this fraction and the given fraction.
+add(other: Fraction): Fraction
```

Moreover, you could include operations to convert a mixed number to a fraction and vice versa when feasible. When you finally implement the ADT measurement, you can use the ADT fraction. That is, you can use one ADT to implement another ADT.

# 1.5 The ADT Bag

Imagine a paper bag, a reusable cloth bag, or even a plastic bag. People use bags when they shop, pack a lunch, or eat potato chips. A bag contains things; it is a container of a collection of objects. We could consider the bag to be an abstract data type.

A bag is a container

Let's specify and use the ADT bag. Knowing just its interface, you can use a bag in a program. You do not need to know how the entries in the bag are represented or how the bag operations are implemented. These specifics are hidden behind the bag's wall of abstraction, and your program will not depend on these specifics. As you will see, this important program characteristic is what data abstraction is all about.

What distinguishes a bag from other ADTs? A bag doesn't do much more than contain its items. It doesn't order them in a particular way, nor does it prevent duplicate items. While describing the behaviors for the ADT bag that we'll design in this chapter, let's keep in mind that we are specifying an abstraction inspired by an actual physical bag. For example, a paper bag holds things of various dimensions and shapes in no particular order and without regard for duplicates. Our abstract bag will hold unordered and possibly duplicate objects, but let's insist that these objects have the same or related types.

Note: A bag is a container of a finite number of objects having the same data type and in no particular order. A bag can contain duplicate items.