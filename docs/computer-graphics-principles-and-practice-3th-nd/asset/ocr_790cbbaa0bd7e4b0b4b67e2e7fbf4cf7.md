That’s it! You can run the program to see how well it works. When you click only two points, your polygon looks like a line segment. When you then subdivide, the line segment appears shorter. Explain to yourself why subdividing again doesn’t make it shorter still.

A similar process can be used to take a 3D polyhedron and “cut corners” in an attempt to smooth it out. Will it always get smoother? We’ll discuss this further in Chapter 23. In the meantime, having seen how rapidly subdivision seems to smooth out curves, you can ask yourself, “How could I analyze whether the curve approaches a limit, and whether such a limit is smooth at a particular point?” This is addressed (for a somewhat different subdivision method, but the principles are similar) in Chapter 22.

# 4.7 Discussion

We’ve given you the tools to create simple applications in WPF for experimenting with ideas from graphics, and worked through a subdivision application as an example of using those tools. The exercises in this chapter will give you the opportunity to explore the power of the 2D test bed, and to discover some interesting ideas in graphics that you’ll encounter again later in this book. We strongly advise you to complete at least a couple of these exercises so that working with this framework will be simple for you in the future.

This test bed was built for a reason. Lots of years of working in computer graphics have taught us another principle:

> ✓ **THE FIRST PIXEL PRINCIPLE:** The first pixel is the hardest.

When you write a new program in graphics, the most common first result is a completely black screen. That’s almost impossible to debug, because any of a million things could be causing the problem. Usually when you manage to get *anything* to show up on the screen, you’re finished with a great deal of your debugging. It’s therefore proven useful to start with a program that does something like what you’re trying to do, and to gradually modify it until it *does* do what you want, but make the modifications so that at every stage you can tell, by looking at it, that it’s doing what you expected. The test bed provides you with a starting point for a whole host of possible programs. We hope it will save you countless hours of debugging.

# 4.8 Exercises

+   **Exercise 4.1:** Modify the corner-cutting program to place the cutoff points one-fourth and three-fourths of the way along the line; describe the results.
+   
+   **Exercise 4.2:** Modify the corner-cutting program to be a “dualizing” program: It replaces a polygon with its dual, a polygon whose vertices are the midpoints of the original polygon, connected in the same order, so that the dual of a square is a diamond. Experiment: Does repeated dualizing tend to remove crossings of self-intersecting polygons? Can you find a polygon whose successive duals are *always* self-intersecting?