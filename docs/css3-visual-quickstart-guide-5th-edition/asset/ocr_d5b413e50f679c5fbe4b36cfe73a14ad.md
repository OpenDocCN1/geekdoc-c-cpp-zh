# Currentcolor keyword

In addition to the color keyword list, you can use the currentcolor keyword. Using currentcolor to set any color value will use the element's current color value. For example, to create an aqua border color:

color: aqua;
border-color: currentcolor;

If you assign currentcolor specifically to the color property, it will inherit its parent element's color value just like using color: inherit.

# Transparent keyword

Another important keyword is transparent, which is the equivalent of a 0 alpha, that is, it's completely transparent. This keyword allows anything behind deat element to show through.

# RGB hex values

Hexadecimal values can range from 0–9 and a–f Values of hexadecimal values representing the levels of red, green, and blue (in that order) in the desired color. The color value couples range from 00 (no color) to FF (full color). However, if the couples contain the same hex value, only three values are needed to define the color. For example, these two sets of values represent the same pure blue:

```
#000ff
#00f
```

# RGB decimal values

Often, simply referred to as the RGB values, RGB uses decimal values from 0 (no color) to 255 (full color) to represent the levels of red, green, and blue (in that order) present in the desired color.

![](bbox=[0.555, 0.068, 0.905, 0.442])

> RGB hex values are represented by three couple values, or by three single values ranging from 0–9 or A–F that indicate the levels of red, green, and blue that combine to create the color.

> RGB decimal color values range from 0–255 to indicate the levels of red, green, and blue that combine to create the color.