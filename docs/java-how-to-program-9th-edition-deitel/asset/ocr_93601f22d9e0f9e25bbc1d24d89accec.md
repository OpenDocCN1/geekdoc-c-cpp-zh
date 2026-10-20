# Self-Review Exercises

24.1 Fill in the blanks in each of the following statements:
a) Graphics method ______ displays an image on an applet.
b) Java provides two mechanisms for playing sounds in an applet—the Applet’s play method and the play method of the ______ interface.
c) A(n) ______ is an image that has hot areas that the user can click to accomplish a task such as loading a web page.
d) Method ______ of class ImageIcon displays the ImageIcon’s image.
e) Java supports several image formats, including ______, ______ and ______.
f) The JNLP ______ class’s static lookup method obtains a reference to the FileOpenService.

24.2 Determine whether each of the following statements is true or false. If false, explain why.
a) A sound is marked for garbage collection after it plays via the play method of class Applet.
b) Class ImageIcon provides constructors that allow an ImageIcon object to be initialized only with an image from the local computer.
c) Method play of class AudioClip continuously loops an audio clip.
d) The Java Image I/O API is used for adding 3D graphics to a Java application.
e) Applet method getDocumentBase returns, as an object of class URL, the location on the Internet of the HTML file that invoked the applet.
f) FileOpenService methods openFileDialog and openMultiFileDialog return a FileContents object and an array of FileContents objects, respectively.

# Answers to Self-Review Exercises

24.1 a) drawImage. b) AudioClip. c) image map. d) paintIcon. e) Graphics Interchange Format (GIF), Joint Photographic Experts Group (JPEG), Portable Network Graphics (PNG). f) ServiceManager.

24.2 a) True. b) False. ImageIcon can load images from the Internet as well. c) False. Method play of class AudioClip plays an audio clip once. Method loop of class AudioClip continuously loops an audio clip. d) False. The Java 3D API is used for creating and modifying 3D graphics. The Java Image I/O API is used for reading from and outputting images to files. e) True. f) True.

# Exercises

24.3 ("Browser-Friendly" Animation) Describe how to make an animation "browser friendly."

24.4 (Audio Clips) Describe the Java methods for playing and manipulating audio clips.

24.5 (Image Maps) Explain how image maps are used. List several examples of their use.

24.6 (Randomly Erasing an Image) Suppose an image is displayed in a rectangular screen area. One way to erase the image is simply to set every pixel to the same color immediately, but the visual effect is dull. Write a Java program that displays an image, then erases it by using random-number generation to select individual pixels to erase. After most of the image is erased, erase all the remaining pixels at once. You can draw individual pixels as a line that starts and ends at the same coordinates. You might try several variants of this problem. For example, you might display lines randomly or display shapes randomly to erase regions of the screen.

24.7 (Text Flasher) Create a Java program that repeatedly flashes text on the screen. Do this by alternating the text with a plain background-color image. Allow the user to control the "blink speed" and the background color or pattern. You'll need to use methods getDelay and setDelay of class