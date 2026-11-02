
## Branding Your App 101: The Splash Screen and Other Visuals

With activation, we first need to take a step back even *before* the app host gets loaded, to the very moment a user taps your tile on the Start screen or when your app is launched some other way (except for pre-launching). At that moment, before any app-specific code is loaded or run, Windows displays your app's splash screen image against your chosen background color, both of which you specify in your manifest.

The splash screen shows for at least 0.75 seconds (so that it's never just a flash even if the app loads quickly) and accomplishes two things. First, it guarantees that something shows up when an app is activated, even if no app code loads successfully. Second, it gives users an interesting branded experience for the app—that is, your image—which is better than a generic hourglass. (So don't, as one popular app I know does, put a generic hourglass in your splash screen image!) Indeed, your splash screen and your app tile are the two most important ways to uniquely brand your app. Make sure you and your graphic artist(s) give full attention to these. (For further guidance, see [Guidelines and checklist for splash screens](#).)

The default splash screen occupies the whole view where the app is being launched (in whatever view state), so it's a much more directly engaging experience for your users. During this time, an instance of the app host gets launched to load, parse, and render your HTML/CSS, and load, parse, and execute your JavaScript, firing events along the way, as we'll see in the next section. When the app's first page is ready, the system removes the splash screen.¹⁷

Additional settings and graphics in the manifest also affect your branding and overall presence in the system, as shown in the tables on the next page. Be especially aware that the Visual Studio and Blend templates provide some default and thoroughly unattractive placeholder graphics. Take a solemn vow right now that you truly, truly, cross-your-heart will not upload an app to the Windows Store with these default graphics still in place! (The Windows Store will reject your app if you forget, delaying certification.)

In the second table, you can see that it lists multiple sizes for various images specified in the manifest to accommodate varying pixel densities: 100%, 140%, and 180% scale factors, and even a few at 80% (don't neglect the latter; they are typically used for most desktop monitors and can be used when you turn on Show More Tiles on the Start screen's settings pane). Although you can just provide a single 100% scale image for each of these, it's almost guaranteed that stretching that graphics for higher pixel densities will look bad. Why not make your app look its best? Take the time to create each individual graphic consciously.

¹⁷ This system-provided splash screen is composed of only your splash screen image and your background color and does not allow any customization. Through an extended splash screen (see Appendix B) you can control the entire display.

| Manifest Editor Tab | Text Item or Setting | Use |
| --- | --- | --- |
| Application | Display Name | Appears in the "all apps" view on the Start screen, search results, the Settings charm, and in the Store. |
| Visual Assets | Tile > Short name | Optional; if provided, is used for the name on the tile in place of the Display Name, as Display Name may be too long for a square tile. |
| Visual Assets | Tile > Show name | Specifies which tiles should show the app name (the small 70x70 tile will never show the name). If none of the items are checked, the name never appears. |
| Visual Assets | Tile > Default size | Indicates whether to show the square or wide tile on the Start screen after installation. |
| Visual Assets | Tile > Foreground text | Color of name text shown on the tile if applicable (see Show name). Options are Light and Dark. There must be a 1.5 contrast ratio between this and the background color. Refer to The Paciello Group's Contrast Analyser for more. |
| Visual Assets | Tile > Background color | Color used for transparent areas of any tile images, the default background for secondary tiles, notification backgrounds, buttons in app dialogs, borders when the app is a provider for file picker and contact picker contracts, headers in settings panes, and the app's page in the Store. Also provides the splash screen background color unless that is set separately. |
| Visual Assets | Splash Screen > Background color | Color that will fill the majority of the splash screen; if not set, the App UI Background color is used. |

| Visual Assets Tab Image | Use | Image Sizes 80% | Image Sizes 100% | Image Sizes 140% | Image Sizes 180% |
| --- | --- | --- | --- | --- | --- |
| Square 70x70 logo | A small square tile image for the Start screen. If provided, the user has the option to display this after installation; it cannot be specified as the default. (Note also that live tiles are not supported on this size.) | 56x56 | 70x70 | 98x98 | 126x126 |
| Square 150x150 logo | Square tile image for the Start screen. | 120x120 | 150x150 | 210x210 | 270x270 |
| Wide 310x150 logo | Optional wide tile image. If provided, this is shown as the default unless overridden by the Default option below. The user can use the square tile if desired. | 248x120 | 310x150 | 434x210 | 558x270 |
| Square 310x310 logo | Optional double-size/large square tile image. If provided, the user has the option to display this after installation; it cannot be specified as the default. | 248x248 | 310x310 | 434x434 | 558x558 |
| Square 30x30 logo | Tile used in zoomed-out and "all apps" views of the Start screen, and in the Search and Share panes if the app supports those contracts as targets. Also used on the app tile if you elect to show a logo instead of the app name in the lower left corner of the tile. Note that there are also four "Target size" icons that are specifically used in the desktop file explorer when file type associations exist for the app. We'll cover this in Chapter 15, 'Contracts.' | 24x24 | 30x30 | 42x42 | 54x54 |
| Store logo | Tile/logo image used for the app on its product description page in the Windows Store. This image appears only in the Windows Store and is not used by the app or system at runtime. | n/a | 50x50 | 70x70 | 90x90 |
| Badge logo | Shown next to a badge notification to identify the app on the lock screen (uncommon, as this requires additional capabilities to be declared; see Chapter 16). | n/a | 24x24 | 33x33 | 43x43 |
| Splash screen | When the app is launched, this image is shown in the center of the screen against the Splash Screen > Background color (or Tile > Background color if the other isn't specified). The image can utilize transparency if desired. | n/a | 620x300 | 868x420 | 1116x540 |

The Visual Assets tab in the editor shows you which scale images you have in your package, as shown in Figure 3-1. To see all visual elements at once, select All Image Assets in the left-hand list.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_95_0.png)

FIGURE 3-1 Visual Studio's Visual Assets tab of the manifest editor. It automatically detects whether a scaled asset exists for the base filename (such as images\tile.png).

In the table, note that 80% scale tile graphics are used in specific cases like low DPI modes (generally when the DPI is less than 130 and the resolution is less than 2560 x 1440) and should be provided with other scaled images. When you upload your app to the Windows Store, you'll also need to provide some additional graphics. See the App images topic in the docs under "Promotional images" for full details.

The combination of small, square, wide, and large square tiles allows the user to arrange the Start screen however they like. For example:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_96_0.png)

Of course, it's not required that your app supports anything other than the 150x150 square tile; all others are optional. In that case Windows will scale your 150x150 tile down to the 70x70 small size to give users at least that option.

When saving scaled image files, append -scale-80, -scale-100, -scale-140, and -scale-180 to the filenames, before the file extension, as in splashscreen.scale-140.png (and be sure to remove any file that doesn't have a suffix). This allows you, both in the manifest and elsewhere in the app, to refer to an image with just the base name, such as splashscreen.png, and Windows will automatically load the appropriate variant for the current scale. Otherwise it looks for one without the suffix. No code needed! This is demonstrated in the HereMyAm3a example, where I've added all the various branded graphics (with some additional text in each graphic to show the scale). With all of these graphics, you'll see the different scales show up in the manifest editor, as shown in Figure 3-1 above.

To test these different graphics, use the set resolution/scaling button in the Visual Studio simulator—refer to Figure 2-5 in Chapter 2—or the Device tab in Blend, to choose different pixel densities on a 10.6" screen (1366 x 768 = 100%, 1920 x 1080 = 140%, and 2560 x 1440 = 180%), or the 7" or 7.5" screens (both use 140%). You'll also see the 80% scale used on the other display choices, including the 23" and 27" settings. In all cases, the setting affects which images are used on the Start screen and the splash screen, but note that you might need to exit and restart the simulator to see the new scaling take effect.

One thing you might also notice is that full-color photographic images don't scale down very well to the smallest sizes (store logo and small logo). This is one reason why Windows Store apps often use simple logos, which also keeps them smaller when compressed. This is an excellent consideration to keep your package size smaller when you make more versions for different contrasts and languages. We'll see more on this in Chapter 20, "Apps for Everyone, Part 2."
