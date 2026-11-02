this narrow width is about the 2.5 physical inches wide. So far so good.

With a large monitor, on the other hand, let's say a 2560x1440 monster, those 320 pixels would only be 12.5% of the width, so the layout of the whole screen looks quite different. However, given that such monitors are in the 24-inch range, those 320 pixels still end up being about 2.5 physical inches wide, meaning that the narrow view gives essentially the same visual experience as before, just now with much more vertical space to play with and much more remaining screen space for other app views.

This now brings up the question of pixel density—what happens if your app ends up on a really small screen that also has a really high resolution, like a 7" 1920x1200 (323dpi) screen? Obviously, 320 pixels on the latter display would be barely an inch wide. Anyone got a magnifying glass? And as new and even higher density displays are produced in the years ahead, it seems like the problem will just get harder to deal with.

Fortunately, this isn't anything a Store app has to worry about...almost. The main user benefit for such displays is greater sharpness, not greater density of information. Touch targets need to be the same size on any size display no matter how many pixels it occupies, because human fingers don't change with technology! To accommodate this, Windows automatically scales down the effective resolution that's reported to apps, which is to say that whatever coordinates you use within your app (in HTML, CSS, and JavaScript) are automatically scaled up to the necessary device resolution when the UI is actually rendered. This happens within the low-level HTML/CSS rendering engine in the app host so that everything is drawn directly against native device pixels for maximum sharpness.

As for the "almost" above, the one place where you do need to care about pixel density is with raster graphics, as we discussed in Chapter 3, "App Anatomy and Performance Fundamentals," for your splash screen and tiles. We'll return to this shortly in the "Graphics that Scale Well" section below.

Display sizes and pixel densities can both be tested again using the Visual Studio simulator or the Device tab in Blend. The latter, shown in Figure 8-6, indicates the applicable DPI and scaling factor. 100% scale means the device resolution is reported directly to an app. 140% and 180%, on the other hand, indicate that scaling is taking place. Doing a little match, you can see that the effective resolution that the app sees is generally near the standard 1366x768 or 1024x768 sizes:

| Display Size | Physical Resolution | Scaling | Effective Resolution |
|---|---|---|---|
| 7" | 1920x1200 | 140% (1.4) | 1371x857 (1920/1.4 by 1200/1.4) |
| 7.5" | 1440x1080 | 140% (1.4) | 1028x771 |
| 10.6" | 1920x1080 | 140% (1.4) | 1371x771 |
| 10.6" | 2560x1440 | 180% (1.8) | 1422x800 |

In all these cases, layouts designed for 1024x768 and 1366x768 are quite sufficient. Of course, you'll need to adapt to the exact pixel dimensions and to the larger 100% resolutions, but you don't have to worry about resizing touch targets and such based on pixel density—all that happens transparently.