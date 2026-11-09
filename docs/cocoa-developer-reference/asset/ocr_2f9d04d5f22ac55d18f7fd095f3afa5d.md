> **TIP**
> 
> The example sets the animation radius to a fixed to-value of 1000. For a more sophisticated effect, try setting the to-value to a number related to the view’s bounds. This guarantees that when the view is resized on a large monitor, the animation won’t stop suddenly before it reaches the edges of the view.

One final nicety is the use of a delegate. The sample code for this example on the Web site for this book (www.wiley.com/go/ocafref) has minimal implementations of the animationDidStart: and animationDidEnd: finished: methods that log a message to the console. In a more complex application, you can use them to trigger associated features, including other animations, as each animation starts and ends. With expanded code, it’s possible to animate many filters simultaneously, creating extremely rich visual effects.

> **NOTE**
> 
> You can use similar code to animate any animatable property. Conventional properties have much simpler keypaths. Typically you use the property name — there’s no need to create a custom filter or name it. However, you can use this more complex code to experiment with animating other Core Image filters.

# Using OpenGL

OpenGL is designed for stand-alone 3D scene rendering. It’s a separate animation technology and isn’t directly connected to Core Animation.

> **NOTE**
> 
> Behind the scenes, Core Animation creates its effects with OpenGL calls, but there’s no API (Application Programming Interface) for the connection between the two. You can use Core Animation or OpenGL, but you can’t work with the interface between them.

OpenGL is powerful, but complex and challenging, and has a very steep learning curve. A full introduction is outside the scope of this book, but the rest of this chapter is an introduction to Cocoa’s NSOpenGLView class, which provides a simple wrapper for OpenGL code that runs in an OpenGL context.

NSOpenGLView is a hybrid view class with most of the features of NSView and three unique methods. The reshape method is called when the view is resized. drawRect: is called to render a scene into the view. Both methods support OpenGL code as well as standard Cocoa objects and features. The remaining method is openGLContext, which runs on the NSOpenGLContext class and returns a context for the drawing code.

Optionally, you can optimize an application by creating another body of code that is used to set up the key features of an OpenGL scene. Typically, you implement this with a custom method with a suitable name, such as setUp. setUp is run once, when the application loads. It sets the background color of a scene, creates and initializes lights, and so on. This method isn’t obligatory. You can — and sometimes have to — re-run the same setup code for each refresh; but it’s efficient to split run-once code from run-often code.