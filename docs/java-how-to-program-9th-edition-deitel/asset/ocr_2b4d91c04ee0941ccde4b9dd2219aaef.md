capabilities go far beyond those presented in this chapter. They include the Java Media Framework (JMF) API (for adding audio and video media to an application), Java Sound API (for playing, recording and modifying audio), Java 3D API (for creating and modifying 3D graphics), Java Advanced Imaging API (for image-processing capabilities, such as cropping and scaling), Java Speech API (for inputting speech from the user and converting it to text, or outputting text to the user as speech), Java 2D API (for creating and modifying 2D graphics, covered in Chapter 15) and Java Image I/O API (for reading images from and outputting images to files). Section 24.8 provides web links for these APIs.]

# 24.2 Loading, Displaying and Scaling Images

We begin our discussion with images. We'll use several different images in this chapter. You can create your own images with software such as Adobe® Photoshop®, Corel® Paint Shop Pro®, Microsoft® Paint and G.I.M.P. (gimp.org).

The applet of Fig. 24.1 uses Java Web Start and the JNLP FileOpenService (package javax.jnlp) to allow the user to select an image, then displays that image and allows the user to scale it. After the user selects an image, the applet gets the bytes from the file, then passes them to the ImageIcon (package javax.swing) constructor to create the image that will be displayed. Class ImageIcon's constructors can receive arguments of several different formats, including a byte array containing the bytes of an image, an Image (package java.awt) already loaded in memory, or a String or a URL representing the image's location. Java supports various image formats, including Graphics Interchange Format (GIF), Joint Photographic Experts Group (JPEG) and Portable Network Graphics (PNG). File names for these types typically end with .gif, .jpg (or .jpeg) and .png, respectively.

```
1  // Fig. 24.1: LoadImageAndScale.java
2  // Loading, displaying and scaling an image in an applet
3  import java.awt.BorderLayout;
4  import java.awt.Graphics;
5  import java.awt.event.ActionEvent;
6  import java.awt.event.ActionListener;
7  import javax.jnlp.FileContents;
8  import javax.jnlp.FileOpenService;
9  import javax.jnlp.ServiceManager;
10 import javax.swing.ImageIcon;
11 import javax.swing.JApplet;
12 import javax.swing.JButton;
13 import javax.swing.JFrame;
14 import javax.swing.JLabel;
15 import javax.swing.JOptionPane;
16 import javax.swing.JPanel;
17 import javax.swing.JTextField;
18 
19 public class LoadImageAndScale extends JApplet
20 {
21     private ImageIcon image; // references image to display
22     private JPanel scaleJPanel; // JPanel containing the scale-selector
```