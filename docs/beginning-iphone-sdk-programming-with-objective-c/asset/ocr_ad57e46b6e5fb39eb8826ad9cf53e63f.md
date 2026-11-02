# 15

# Simple Animations

# WHAT YOU WILL LEARN IN THIS CHAPTER

+   - How to use the `NSTimer` class to create timers that will call methods at regular time intervals
+   - How to perform some simple animations using the `NSTimer` class
+   - How to perform affine transformation on the `ImageView`
+   - How to animate a series of images using the `ImageView`

Up to this point, the applications you have written have all made use of the standard views provided by the iPhone SDK. As Apple has reiterated, the iPhone and iPod Touch are more than just phones. The iPhone is also a music player and, more important for this chapter, the iPhone is also a gaming platform.

In this chapter, you can have some fun and create something visual. You learn how to perform some simple animations using a timer object and then perform some transformations on a view. Although it is beyond the scope of this book to show you how to create animations using OpenGL, this chapter does show you some interesting techniques that you can use to make your applications come alive!

# USING THE NSTIMER CLASS

One of the easiest ways to get started with animation is to use the NSTimer class. The NSTimer class creates timer objects, which allow you to call a method at regular time intervals. Using an NSTimer object, you can update an image at regular time intervals, thereby creating an impression that it is being animated.