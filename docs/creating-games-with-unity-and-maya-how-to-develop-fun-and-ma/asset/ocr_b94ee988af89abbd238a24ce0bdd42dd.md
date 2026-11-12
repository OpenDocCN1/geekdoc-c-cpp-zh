![](bbox=[0.19, 0.1, 0.51, 0.31])

**FIGURE 4.3** Offset and the results.

# Why?

The problem with any image and trying to make it seamless is getting to the seams. The seams are the edges of the image. The Offset with the Wrap Around option activated does some important things for us. First, it offsets or slides all the pixels over (and/or down) and then wraps the pixels that it slides off the edge of the canvas around to the other side of the image. This means two important things. First, after the Offset filter has been applied, the right edge of the image matches seamlessly to the left edge of the image and the top and the bottom match as well. Second, it takes the old edges (the old seams) and puts them right in the middle of the scene where we can deal with them.

**Step 4:** Clone Stamp out the seams. The Clone Stamp is an incredibly powerful tool that allows for interactively painting the pixels from one part of an image to another. To use it, select it from the Photoshop tool bar, then hold the Alt (Option on a Mac) and click the area where the pixels are to be pulled from. Release the Alt and mouse, and then go and paint where the pixels are to be painted (in this case the seams in the middle of the image). The results are seen in Figure 4.4.

![](bbox=[0.2, 0.7, 0.51, 0.92])

**FIGURE 4.4** Clone Stamped image.