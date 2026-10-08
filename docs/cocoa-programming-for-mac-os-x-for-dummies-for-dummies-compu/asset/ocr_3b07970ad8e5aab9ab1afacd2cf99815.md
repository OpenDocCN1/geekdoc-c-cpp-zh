# Chapter 12

# Graphics

+   In This Chapter

- Defining colors
- Creating a custom view
- Drawing rectangles and ovals
- Painting irregular shapes
- Creating text
- Displaying images

From the beautiful fonts in a word processor to the shiny Finder interface, the Mac OS has always prided itself on fantastic looking graphics. Mac OS X is no different. With its sophisticated Quartz graphics engine, Mac OS X can produce stunning graphics. Cocoa gives you direct access to these powerful features of Mac OS X.

This chapter covers the basics of working with graphics in Cocoa. You create a custom view for displaying your graphics and draw on it with a variety of colors, shapes, and images. You even write code to change the opacity of your graphics, giving them the coveted see-through look.

# Cocoa and the Art of Graphics

Before jumping head first into graphics, you need to familiarize yourself with a few important Cocoa data types: NSPoint, NSRect, NSSize, and NSColor. You need them to do any type of graphics programming in Cocoa, so they make a good starting point.

# Points

Just like in geometry, Cocoa uses points to designate positions on a square grid. To work with points in Cocoa, you use an NSPoint structure. NSPoint