| Position | Item |
|---|---|
| 2 | The size of this file in bytes |
| 10 | Offset to the start of the image data |
| 18 | The width of the image in pixels |
| 22 | The height of the image in pixels |

The image is stored as a sequence of pixel rows, starting with the pixels of the bottom-most row of the image. Each pixel row contains a sequence of blue/green/red triplets. The end of the row is padded with additional bytes so that the number of bytes in the row is divisible by 4. (See Figure 5.) For example, if a row consisted of merely three pixels, one cyan, one red, and one medium gray one, the row would be encoded as

```
255 255 0 0 255 128 128 128 x y z
```

where x y z are padding bytes to bring the row length up to 12, a multiple of 4. It is these little twists that make working with real-life file formats such a joyful experience.

![](bbox=[0.12, 0.63, 0.92, 0.78])

# Figure 5 The BMP File Format for 24-bit True Color Images

The sample program at the end of this section reads every pixel of a BMP file and replaces it with its negative, turning white to black, cyan to red, and so on. The result is a negative image of the kind that old-fashioned film cameras used to produce (see Figure 6).

![](bbox=[0.32, 0.77, 0.92, 0.93])

Figure 6
An Image and Its Negative
© Cay Horstmann.