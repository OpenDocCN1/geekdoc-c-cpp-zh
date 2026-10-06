# Chapter 10: Audio and Visual Effects 297

setAttribute(), and finally, appendChild() to append the new element
to the DOM.

Next, the variable index is initialized to 0; this will be used later to index the next image
in a slide show. The first image is then assigned the contents of the first element in the
images array, which will be the location of a photo or other image:

```
var index = 0
O('SS_IMG1').src = images[0]
O(id).SS_Flag = true
```

The SS_Flag property is also set to true to indicate that a slide is in progress.
After that, the second image has its opacity set to 0 to make it invisible, and the first
image is faded in over a period of msecs milliseconds:

```
Opacity('SS_IMG2', 0)
FadeIn('SS_IMG1', msecs, 0)
```

Finally, in the setup section of the code, the setTimeout() function is called to set up
in interrupt to call the DoSlideshow() subsection after a period of msecs + wait
milliseconds. This accounts for the time it will take the image to fade in, plus the time
required for the wait:

```
setTimeout(DoSlideshow, msecs + wait)
```

# The DoSlideshow() Subfunction

The job of this function is to transition between two images and then initiate an
interrupt to call itself when the next transition is due (unless it is cancelled).

The first thing this function does load the first image with the current value in the
images array, as indexed by index. The first time it calls this, nothing happens since the
same has already been loaded. However, on all future transitions it has the effect of
taking the picture that is being displayed in the second image and duplicating it in the first,
so that they are showing the same picture:

```
O('SS_IMG1').src = images[index]
```

Since both images are the same picture, it is safe to set the first one to be fully
visible and the second one to invisible, like:

```
Opacity('SS_IMG1', 100)
Opacity('SS_IMG2', 0)
```

Having made this swap, the index variable is incremented to point to the next picture
in the slide show, and it becomes larger than the number of images in the images array, it
is reset to 0 (using the % operator) to start again at the beginning, as follows:

```
index = ++index % len
```

Next, it's time to load the next picture listed in the images array into the second
image, because the first image is the currently being displayed, and the second has been
made invisible to do:

```
O('SS_IMG2').src = images[index]
```