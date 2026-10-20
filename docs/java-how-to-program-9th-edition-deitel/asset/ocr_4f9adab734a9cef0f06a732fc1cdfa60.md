# Java Multimedia API References

www.oracle.com/technetwork/java/javase/tech/media-141984.html
The online home of the Java Media APIs.

www.oracle.com/technetwork/java/index-139508.html
The Java Sound API home page. Java Sound provides capabilities for playing and recording audio.

java3d.dev.java.net/
The Java 3D API home page. This API can be used to produce three-dimensional images typical of today's video games.

java.sun.com/products/java-media/speech/
The Java Speech API enables programs to perform speech synthesis and speech recognition.

freetts.sourceforge.net/docs/index.php
FreeTTS is an implementation of the Java Speech API.

# Summary

# Section 24.2 Loading, Displaying and Scaling Images

+   - Class ImageIcon’s constructors can receive arguments of several different formats, including a byte array containing the bytes of an image, an Image (package java.awt) already loaded in memory, or a String or a URL representing the image’s location.
+   - Java supports several image formats, including Graphics Interchange Format (GIF), Joint Photographic Experts Group (JPEG) and Portable Network Graphics (PNG). The file names for these types typically end with .gif, .jpg (or .jpeg) and .png, respectively.
+   - Java Web Start programs can access the local file system via the JNLP APIs (package javax.jnlp). You can use JNLP’s FileOpenService (p. 969) to request limited access to the local file system.
+   - The JNLP ServiceManager class’s static lookup (p. 972) method obtains a reference to the FileOpenService (p. 969). Since other services are provided by JNLP, this method returns an Object reference, which you must cast to the appropriate type.
+   - FileOpenService method openFileDialog method (p. 972) displays a file-selection dialog. Java Web Start prompts the user to approve the program’s request local file-system access. If the user gives permission, the Open dialog is displayed. The openFileDialog method has two parameters—a String to suggest a directory to open and a String array of acceptable file extensions.
+   - Method openFileDialog returns a FileContents object, which for security reasons does not give the program access to the file’s exact location on disk. Instead, the program can get an InputStream and read the file’s bytes.
+   - FileContents method getLength (p. 973) returns the number of bytes in the file.
+   - Component methods getWidth and getHeight (p. 973) return the width and height of a Component.
+   - ImageIcon methods getIconWidth and getIconHeight (p. 973) return the width and height of an image, respectively.
+   - Class Graphics provides overloaded drawImage methods (p. 973), one of which displays a scaled version of an Image (p. 969). The first argument is the Image to draw. The second and third arguments represent the upper-left corner coordinates of the Image. The fourth and fifth arguments specify the Image’s scaled width and height, respectively. The last argument is a reference to an ImageObserver (p. 973)—an interface implemented by class Component.
+   - As an Image loads, its ImageObserver receives notifications and updates the image on the screen as necessary.