To get the desired alpha blending result for transparency, you set the source factor to the alpha of the pixel you're drawing (the source alpha) and the destination factor to one minus source alpha:

```
outputColor = srcAlpha · sourceColor + (1-srcAlpha) · destinationColor
```

```
outputColor = srcAlpha
· sourceColor + (1 - srcAlpha)
· destinationColor
```

For example, suppose you have 8 bits per color, and the color buffer at some pixel is red. In this case, this is the destination color:

```
destinationColor = (255, 0, 0)
```

```
destinationColor = ( 255, 0, 0 )
```

Next, say that you want to draw a pixel that's blue; this is the source color:

```
sourceColor = (0, 0, 255)
```

```
sourceColor = ( 0, 0, 255 )
```

Now suppose the source alpha is zero, meaning the pixel is completely transparent. In this case, our equation evaluates to the following:

```
outputColor = 0 · (0, 0, 255) + (1-0) · (255, 0, 0)
outputColor = (255, 0, 0)
outputColor = 0 · ( 0, 0, 255 )
+ (1 - 0) · ( 255, 0, 0 )
outputColor = ( 255, 0, 0 )
```