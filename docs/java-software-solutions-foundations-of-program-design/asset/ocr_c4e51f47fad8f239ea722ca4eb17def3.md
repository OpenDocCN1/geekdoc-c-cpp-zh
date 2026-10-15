+   - The system should make a distinction between the stroke color (the outline) and the fill color (the interior) of a shape. Therefore, each shape will have a separate stroke and fill color. Lines and polylines will have only a stroke color because they cannot be filled.
+   - An option to save a drawing under a particular name should be provided (the traditional “save as” operation).
+   - Traditional keyboard shortcuts for operations such as cut, copy, and paste should be included.
+   - The system should perform checks to ensure that the user does not lose unsaved changes to a drawing.
+   - The system should present an initial “splash screen” to introduce the program when it is executed.

These issues must be integrated into the formal description of the requirements document for the project. Several discussions with the client, with additional screen sketches, may be necessary before we have an accurate and solid set of program requirements.

# PaintBox Architectural Design

After we have clarified the requirements with the client, we can begin to think about some of the elements of the high-level *architectural design* of the system. For example, many of the classes needed for the user interface can come from the Java standard class library in the Swing package.

It also seems reasonable that a separate class could be used to represent each shape type. Further, each individually drawn shape should be an instantiation of the appropriate shape class. For example, we could define an Oval class to represent an oval, a Line class to represent a line, and so on. Each class should be responsible for keeping track of the information it needs to define it, and it should provide methods to draw itself.

A drawing may be composed of many shapes, so we need a way to keep track of all of them. An ArrayList might be a good choice for this. As each new shape is drawn, we can add the object that represents it to the list. The list will also inherently define the order in which shapes are drawn. Since some shapes will be drawn on top of others, the list will also keep track of the order in which shapes are “stacked.”

The process of defining an architectural design could take a while. The key is to make the most important and fundamental decisions that will affect the entire system without skipping ahead to decisions that are better left to individual refinements of the system.