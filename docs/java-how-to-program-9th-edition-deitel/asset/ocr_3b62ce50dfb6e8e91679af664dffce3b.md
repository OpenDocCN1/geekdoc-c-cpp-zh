| Method or constant | Description |
|---|---|
| *Graphics methods for manipulating Fonts* |  |
| `public Font getFont()` | Returns a Font object reference representing the current font. |
| `public void setFont( Font f )` | Sets the current font to the font, style and size specified by the Font object reference f. |

Fig. 15.10 | Font-related methods and constants. (Part 2 of 2.)

Class Font’s constructor takes three arguments—the font name, font style and font size. The font name is any font currently supported by the system on which the program is running, such as standard Java fonts Monospaced, SansSerif and Serif. The font style is Font.PLAIN, Font.ITALIC or Font.BOLD (each is a static field of class Font). Font styles can be used in combination (e.g., Font.ITALIC + Font.BOLD). The font size is measured in points. A point is 1/72 of an inch. Graphics method setFont sets the current drawing font—the font in which text will be displayed—to its Font argument.

> **Portability Tip 15.2**
> *The number of fonts varies across systems. Java provides five font names—Serif, Monospaced, SansSerif, Dialog and DialogInput—that can be used on all Java platforms. The Java runtime environment (JRE) on each platform maps these logical font names to actual fonts installed on the platform. The actual fonts used may vary by platform.*

The application of Figs. 15.11–15.12 displays text in four different fonts, with each font in a different size. Figure 15.11 uses the Font constructor to initialize Font objects (in lines 16, 20, 24 and 29) that are each passed to Graphics method setFont to change the drawing font. Each call to the Font constructor passes a font name (Serif, Monospaced or SansSerif) as a string, a font style (Font.PLAIN, Font.ITALIC or Font.BOLD) and a font size. Once Graphics method setFont is invoked, all text displayed following the call will appear in the new font until the font is changed. Each font’s information is displayed in lines 17, 21, 25 and 30–31 using method drawString. The coordinates passed to drawString corresponds to the lower-left corner of the baseline of the font. Line 28 changes the drawing color to red, so the next string displayed appears in red. Lines 30–31 display information about the final Font object. Method getFont of class Graphics returns a Font object representing the current font. Method getName returns the current font name as a string. Method getSize returns the font size in points.

> **Software Engineering Observation 15.2**
> *To change the font, you must create a new Font object. Font objects are immutable—class Font has no set methods to change the characteristics of the current font.*

Figure 15.12 contains the main method, which creates a JFrame to display a FontJPanel. We add a FontJPanel object to this JFrame (line 15), which displays the graphics created in Fig. 15.11.