# 15.4 Manipulating Fonts

This section introduces methods and constants for manipulating fonts. Most font methods and font constants are part of class Font. Some methods of class Font and class Graphics are summarized in Fig. 15.10.

Fig. 15.9 | HSB and RGB tabs of the JColorChooser dialog. (Part 2 of 2.)

Fig. 15.10 | Font-related methods and constants. (Part 1 of 2.)

| Method or constant | Description |
|---|---|
| Font constants, constructors and methods | |
| public final static int PLAIN | A constant representing a plain font style. |
| public final static int BOLD | A constant representing a bold font style. |
| public final static int ITALIC | A constant representing an italic font style. |
| public Font( String name, int style, int size ) | Creates a Font object with the specified font name, style and size. |
| public int getStyle() | Returns an int indicating the current font style. |
| public int getSize() | Returns an int indicating the current font size. |
| public String getName() | Returns the current font name as a string. |
| public String getFamily() | Returns the font's family name as a string. |
| public boolean isPlain() | Returns true if the font is plain, else false. |
| public boolean isBold() | Returns true if the font is bold, else false. |
| public boolean isItalic() | Returns true if the font is italic, else false. |

![](bbox=[0.285, 0.115, 0.71, 0.44])