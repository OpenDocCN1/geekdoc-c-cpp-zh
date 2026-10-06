# Plug-In JavaScript: 100 Power Solutions

```
var index = 0
O('SS_IMG1').src = images[0]
Opacity('SS_IMG2', 0)
FadeIn('SS_IMG1', msecs, 0)
setTimeout(DoSlideshow, msecs + wait)
}

function DoSlideshow() {
  O('SS_IMG1').src = images[index]
  Opacity('SS_IMG1', 100)
  Opacity('SS_IMG2', 0)
}

index = ++index % images.length
O('SS_IMG2').src = images[index]
var next = InsVars('O('SS_IMG1').src = '#1#'
images(index + 1) % len)
FadeBetween('SS_IMG1', 'SS_IMG2', msecs, 0)

if (O(id).SS_Stop) setTimeout(DoSlideshow, msecs + wait)
elelse O(id).SS_Flag = false
```

# 79 Billboard()

This plug-in is similar to the Slideshow() plug-in in that it fades objects in a sequence. The difference is that the Billboard() plug-in allows you to put any objects in a show

A great use for this plug-in is to rotate banners or other advertisements, which can be images, divs, spans, or other objects. Figure 10-3 shows one image in a sequence displayed using this plug-in.

Figure 10-3 creates a billboard of rotating objects and/or images.

![](bbox=[0.305, 0.678, 0.845, 0.868])