# # CORE ANIMATION AND PERFORMANCE (continued)

![](bbox=[0.1, 0.19, 0.69, 0.47])

![](bbox=[0.7, 0.19, 0.94, 0.47])

**FIGURE 4.19** Highlighting offscreen-rendered views using Instruments

**FIGURE 4.20** All offscreen-rendered views are highlighted in yellow

If we cannot use shouldRasterize to solve our performance problems, we may need to revert back to custom drawing. In our case, we could create a subclass of UIView and override the drawRect: method, manually drawing our curved rectangle and gradient fills. Typically, the drawing code is only called once, when the object is first placed onscreen. It is then cached in the view's CALayer and can be scrolled, resized, or otherwise animated without requiring additional drawing. Of course, the initial drawing may be slightly slower than the Core Animation method calls, but we're converting a per-frame cost into a one-time cost. In many cases, this produces significant performance improvements.

We'll cover custom drawing in more depth in Chapter 5, “Drawing Custom Views.”