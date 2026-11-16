# CHAPTER 1

![](bbox=[0.62, 0.13, 0.91, 0.39])

# HELLO WORLD

The first step in most programming books is creating a Hello World application that performs a simple function to make sure everything is working. The simplest computer game application is a window with a black background and a tight while loop that clears the screen and redraws the black background as fast as possible; however, as simple as this is, it isn't very exciting. Adding a frame rate calculator will measure the application performance and verify that the window is redrawing. Since most examples in this book measure the frame rate, a frame rate calculator is a great place to begin.

# USING THE FRAMERATE CLASS

The FrameRate class is located in the javagames.util package. All the utility code developed in this book goes into the utility package, which you can later turn into a utility library. This class is used to measure the frames per second (FPS) of the applications developed in this book. The FPS is stored as a string in the format “FPS 100”. This value is calculated every second.

The initialize() method needs to be called before the frame rate measurements begin. This method initializes the frame rate string to 0, and the last time to the current time in milliseconds.

The System.currentTimeMillis() call returns the number of milliseconds since midnight, January 1, 1970. Depending on the operating system, the accuracy of the time measured can vary. Some versions of Windows, for example, guarantee only 10 milliseconds of accuracy.