+   4. Define the source for newer versions of Internet Explorer. Because of a bug in Internet Explorer versions earlier than IE9, you need to define the source of the EOT file again and include a little code trick after the path: ?#iefix. This prevents older versions of IE from causing problems with loading the correct format.
+   
+   `src: url('.../fonts/DVS/DejaVuSerif.eot?#iefix') format('embedded-opentype'),`

+   5. Define the source of the WOFF, TrueType or OpenType, and SVG format of the font file. Now add the location of your WOFF and TTF/OTF font files. Each browser will use the one best suited for it.
+   
+   `url('.../fonts/DVS/DejaVuSerif.woff') format('woff'),`
+   `url('.../fonts/DVS/DejaVuSerif.ttf') format('truetype');`

+   6. Optional Add weight, style, and stretch associated with this font. This will mean the font is used only if these properties are also applied with the specific value. For the exact values, see the relevant sections for each in this chapter.
+   
+   `font-weight: normal;`
+   `font-style: normal;`
+   `font-stretch: normal }`