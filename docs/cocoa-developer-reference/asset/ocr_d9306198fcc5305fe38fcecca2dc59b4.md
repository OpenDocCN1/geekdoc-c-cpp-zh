+   - An `Icon.png` file. The icon file is the widget’s icon in Dashboard’s dock. It has a square aspect ratio and should be 85 x 85 pixels. Content should be limited to an area of 74 x 74 pixels. The I in “Icon” must be capitalized.
+   - An `info.plist` file with bundle and version information, including the widget’s name, identifier, and dimensions. This file also names the `.html` and `.js` files in the widget. Dashboard reads these references when the widget loads.
+   - A `version.plist` file with version numbering information, for Dashboard’s internal use only.

Optionally, widgets can be localized with separate `<language_name>.lproj` folders, each of which includes an `InfoPlist.strings` file with UTF-8 (Unicode Transformation Format-8) strings for each supported language. Many widgets include an extra `/Images` folder that holds graphics files.

A key feature of widgets is that the components are unprotected. Code, HTML, and graphics can be opened in any editor, copied, and changed by anyone with a basic understanding of widget technology, as shown in Figure 4.4. Mac users typically lack the skills to disable widgets, but as a developer you must assume that other developers will be able to read and copy your code.

![](bbox=[0.103, 0.478, 0.171, 0.534])

> > **CAUTION**
> >
> > Although the JavaScript files in a widget can be read by anyone, most widgets aren’t formally open sourced and are rarely developed collaboratively with an open license. You should consider all code private and proprietary unless the developer includes a license explicitly stating otherwise. If you release a widget that includes a direct copy of code by another developer without his permission, the other developer may well find out—and there might be consequences.

Many popular widgets provide front-ends for Web services such as Twitter, bit.ly, and Facebook. Although you do not have legal rights to reuse code from other widgets directly, widget scripts can be an excellent way to discover how other developers use public application programming interfaces (APIs). Even if you don’t plan to develop widgets, this is one of the most useful features of widget technology. Attempting to master an API without good sample code can be difficult. Widgets can provide you with this code.

![](bbox=[0.103, 0.715, 0.171, 0.769])

> > **NOTE**
> >
> > Although widgets are written in JavaScript and not Objective-C, these languages are similar enough to be easy to translate in either direction — even if you’re not proficient in both.

# Assembling widgets manually

You can assemble a minimal widget by hand using a text editor to create the HTML, CSS, and JavaScript, an image editor to create the graphics, and the OS X plist editor to assemble the plist files. This is a practical option for very simple widgets, and it offers the advantage of the smallest possible bundle sizes. If your widget includes the essential elements and is zipped into a folder and renamed with the `.wdgt` extension, it can be installed in Dashboard.