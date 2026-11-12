
## Alice's Adventures In Wonderland

By Lewis Carroll

## Chapter I Down the Rabbit-Hole

Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, 'and what is the use of a book,' thought Alice 'without pictures or conversation?' So she was considering in her own mind (as well as she could, for the hot day made her feel very sleepy and stupid), whether the pleasure of making a daisy-chain would be worth the trouble of getting up and picking the daisies, when suddenly a White Rabbit with pink eyes ran close by her. There was nothing so VERY remarkable in that; nor did Alice think it so VERY much out of the way to hear the Rabbit say to itself, 'Oh dear! Oh dear! I shall be late!' (when she thought it over afterwards, it occurred to her that she ought to have wondered at this, but at the time it all seemed quite natural); but when the Rabbit actually TOOK A WATCH OUT OF ITS WAISTCOAT-POCKET, and looked at it, and then hurried on, Alice started to her feet, for it flashed across her mind that she had never before seen a rabbit with either a waistcoat-pocket, or a watch to take out of it, and burning with curiosity, she ran across the field after it, and fortunately was just in time to see it pop down a large rabbit-hole under the hedge. In another moment down went Alice after it, never once considering how in the world she was to get out again. The rabbit-hole went straight on like a tunnel for some way, and then dipped suddenly down, so suddenly that Alice had not a moment to think about stopping herself before she found herself falling down a very deep well.

The page is now looking a bit more distinctive typographically by including fonts that are not often seen on the Web.

## To define a Web font to your font stack:

- 1. Add the font face rule to your CSS.

Begin by typing the @font-face rule, where you will define the name and location of the font file you want to use in your designs (Code 5.3).

```
@font-face {
```

- 2. Define the name of your font family.

Type the name of the font family you want to import. This can actually be anything you choose, as long as you reference it consistently in your font stack.

```
font-family: 'BodyCopy';
```

Many developers choose to use just the name of the font, but I recommend creating a name that indicates how the font is used in the design. Then, if the typeface is changed, you don't have to change the font name everywhere it is referenced.

> Remember: if you want to use a font name with two or more words separated by a space, put the whole name in quotes.

- 3. Define the source of the EOT format of the font file for older versions of Internet Explorer. Add your font file sources. Always begin with the EOT file for use in Internet Explorer, but do not add a format attribute.

```
src: url('../fonts/DVS/DejaVuSerif.eot');
```

- 4. Define the source for newer versions of Internet Explorer. Because of a bug in Internet Explorer versions earlier than IE9, you need to define the source of the EOT file again and include a little code trick after the path: ?#iefix. This prevents older versions of IE from causing problems with loading the correct format.

  `src: url('.../fonts/DVS/DejaVuSerif.eot?#iefix') format('embedded-opentype'),`

- 5. Define the source of the WOFF, TrueType or OpenType, and SVG format of the font file. Now add the location of your WOFF and TTF/OTF font files. Each browser will use the one best suited for it.

  `url('.../fonts/DVS/DejaVuSerif.woff') format('woff'),`
  `url('.../fonts/DVS/DejaVuSerif.ttf') format('truetype');`

- 6. Optional Add weight, style, and stretch associated with this font. This will mean the font is used only if these properties are also applied with the specific value. For the exact values, see the relevant sections for each in this chapter.

  `font-weight: normal;`
  `font-style: normal;`
  `font-stretch: normal }`

- 7. Add the Web font name to your font stack. To leverage a downloaded Web font and trigger its download, place the name you gave it at as the first value of the font stack.

`font-family: "BodyCopy", Constantia, Georgia, "Times New Roman", serif;`

- 8. Add @font-face for different weights, styles, and stretch. Particularly if you will be using italic or bold text, you must define the font files for each of these, as well as the normal/regular style.

- 9. Add @font-face for different typefaces. You can use multiple typefaces; in this case I'm including one for the titles.

Although the SVG format can be used as a Web font, I tend not to include it as it is known to cause problems in some older Web browsers.

For this example, I've loaded a lot of different font files. Although they are not huge—the ones I used are 20–35 KB and could be reduced in size by sub-setting the font. However, the file sizes can add up quickly, so be careful not to bloat your page size.

Once loaded, though, the font files are cached, so they will not be downloaded again for subsequent pages that use them.

For more information on Mac fonts, see developer.apple.com/textfonts/.

For more information on Windows fonts, see www.microsoft.com/typography/fonts/. For a more detailed examination of Web fonts and Web typography in general, check out my book Fluid Web Typography (www.webtypographynow.info).

The font Little Trouble Girl was created by Jess Latham (bfonts.com).

## Using Font Squirrel to Convert Font Files

Although you are now free to start downloading Web fonts for use in your designs, you still face two major hurdles:

- 1. Legal. While you might assume that you can use a purchased font as a Web font, that is rarely the case. Most fonts have usage restrictions outlined in their End User License Agreements (EULA). If the EULA does not specifically state that you can use a font for @font-face linking, you can’t do so legally. To be sure, check with the font vendor before proceeding.

- 2. Technical. How do you get all of those different font formats? Currently, even if licensed to do so, most font foundries or resellers do not provide these formats.

## What to do?

One great resource I use regularly is the Font Squirrel Web site (www.fontsquirrel.com), which provides an index of over 500 freely licensed, downloadable Web fonts. Each is complete with the font formats as well as sample CSS code

The site also provides an insanely useful tool—the @font-face Kit Generator—that can convert any OTF or TTF file into EOT, SVG, and WOFF formats (www.fontsquirrel.com/fontface/generator). It’s easy to use and fast. Just make sure that your EULA is in order before using it.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_161_0.png)

![](img/e1ed1e3c1873fa9fc855210fb83699d0_161_1.png)

Font Squirrel (www.fontsquirrel.com) offers over 500 free fonts that are ready for use in your Web site.

Use the @font-face Kit Generator (www.fontsquirrel.com/fontface/generator) to convert any licensed fonts for use on the Web.

## Web font service bureaus

Another add-on-coming option for adding specific fonts to a Web design is Web font service bureaus (WFSB). They provide licensed fonts for your use (generally at a cost) but retain the actual files on their own servers while allowing you to reference them in your code. Some enable this with a straightforward CSS link; others use their own proprietary methods, generally incorporating JavaScript.

- The advantages to using WFSBs include:
  - Fonts are licensed, so you don't have to worry about violating a EULA and getting sued.
  - Fonts are hosted on the bureaus' servers, which means you are taking up less bandwidth on your own servers.
  - Browser support is handled by the bureau, as are potential updates and upgrades.

- However, there are disadvantages as well:
  - Since the fonts are on a third-party server, you are depending on someone else's system to always be fast and reliable.
  - If you do not have a copy of the font on your own computer, you will not be able to create graphical comps to show clients.
  - Price scales vary from service to service. Some charge a one-time fee; others require a yearly subscription. If you forget to pay, your font goes bye-bye.
