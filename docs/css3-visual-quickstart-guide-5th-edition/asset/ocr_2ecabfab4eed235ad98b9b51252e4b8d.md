browsers using the W3C standard (Firefox, Safari, Opera) would set the content area to 100 pixels wide but have a total width of 130 pixels A:

100 + 5 + 5 + 10 + 10 = 130

On the other hand, Internet Explorer 5.5 and earlier would set the total width of the element (from border to border) as 100 pixels, shrinking the width of the content to 70 pixels B:

100 - 5 - 5 - 10 - 10 = 70

This is a problem, and it only gets worse. Versions 6 and later of Internet Explorer fix this problem by following the W3C standards. However, if you are using the transitional document type definition (DTD) for your page—which is still very common—or a DTD that the browsers do not recognize—such as HTML5-IE6 and IE7 revert to the "quirky" version of the box model. Unfortunately, more often than not, your site will probably trigger IE's quirks mode.

So what's a good Web designer to do? You have few options:

+   - Do not use a border and/or padding with any element that has a set dimension. If you do, don't expect pixel-perfect layouts. Generally, this solution isn't practical, but for simple pages it might do the trick.

+   - Code for the strict DTD so that the browser uses the standards-compliant box model. Generally, this approach is not practical the slightest error can return the browser to quirks mode and destroy the whole design.

+   - Use one of the IE techniques (most likely the conditional comments) to code separate "equalizing" widths and/ heights for Internet Explorer.

> The Caterpillar and Alice looked at each other for some time in silence: at last the Caterpillar took the hookah out of its mouth, and addressed her in a languid, sleepy voice.

The box using the CSS box model. The content area is 100 pixels with padding and border added for a total width of 130 pixels.

![](bbox=[0.595, 0.415, 0.895, 0.67])

Internet Explorer box model has its own way of dealing with the width, making the total width 100 pixels and shrinking the content area to 70 pixels.

Interestingly, a new CSS3 property (box-sizing) that's still under development will allow you to choose which of these box models you want to use.

334 Chapter 13