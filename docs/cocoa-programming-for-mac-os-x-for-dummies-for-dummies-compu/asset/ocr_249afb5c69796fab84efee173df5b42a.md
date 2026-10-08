As you may have guessed, this technique works for many other colors too (blueColor, redColor, and so on). Table 12-1 lists common colors that you can use.

| **Table 12-1 Preset Color Components** |
| :--- | :--- |
| **Preset Component** | **Color It Produces** |
| blackColor | Black |
| blueColor | Bright blue |
| brownColor | Brown |
| clearColor | Clear/transparent |
| cyanColor | Light blue |
| darkGrayColor | Dark gray (for the Canadians, dark grey) |
| grayColor | Medium gray |
| greenColor | Bright green |
| lightGrayColor | Light gray (you were expecting something else?) |
| magentaColor | Pinkish purple color... or is it a purple-ish pink color |
| orangeColor | Orange |
| purpleColor | Purple |
| redColor | Bright red |
| whiteColor | White |
| yellowColor | Bright and sunny yellow |


# Using device-dependent color spaces

Eventually, you'll want some colors that the convenience methods don't cover. In that case, you have to resort to some of the more sophisticated color methods in the AppKit. The AppKit has three kinds of color spaces that you can use to create colors:

+   - **Device dependent (or device):** When you use *device colors*, you can't be sure that you'll always see the same color across devices. You're probably most familiar with this kind of color because most home computer monitors and printers display it. Stand any two computer monitors next to each other, and you'll soon discover that they don't produce colors equally. Sure, it's good enough to view Web pages, play games, and even create graphics. It also works for many kinds of home-printing chores. It's not so good, however, for professional printing, color correction, and similar color tasks.