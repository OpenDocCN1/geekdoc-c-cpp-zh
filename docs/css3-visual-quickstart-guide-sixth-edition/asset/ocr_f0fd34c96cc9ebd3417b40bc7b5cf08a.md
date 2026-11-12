# Fixing the Box Model for Older Versions of Internet Explorer (continued)

So what’s a good Web designer to do? You have a few options:

+   - Do not use a border and/or padding with any element that has a set dimension. If you do, don’t expect pixel-precise layouts. Generally, this solution isn’t practical, but for simple pages it might do the trick.
+   - Code for the strict DTD so that the browser uses the standards-compliant box model. Generally, this approach is not practical because the slightest error can return the browser to quirks mode and destroy the whole design.
+   - Use conditional CSS (explained in Chapter 14 to code separate “equalizing” widths and/or heights for older versions of Internet Explorer.

Because IE7 and earlier now make up less than five percent of the browsers currently in use worldwide, this problem increasingly becomes a moot point, but you may still run across it from time to time. Interestingly, a new CSS3 property under discussion, box-sizing, explained in Chapter 10, will allow you to choose which of these box models you want to use. This gives you control over which method gets used.