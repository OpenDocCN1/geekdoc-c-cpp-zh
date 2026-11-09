+   - HTML
+   - MS Word

The MS Word importer isn’t guaranteed to support the latest MS Word format. You can pass an optional dictionary pointer to an `initWith<type>` method to receive a list of document attributes extracted from the file.

To save a file, convert it to an `NSData` object using one of the conversion methods listed below, and then save the data object to disk. All formats support an optional dictionary of attributes that defines the attributes included in the file:

+   - `dataFromRange:` is a generic converter that supports all valid attributes and is ideal for Mac-only document saving.
+   - `docFormatFromRange:` creates an MS Word file, usually of a legacy type.
+   - `RTFFromRange:` Creates an RTF file. For sample code, see the Nanopad example later in this chapter.
+   - `RTFDFromRange:` creates a folder that contains an RTF file and associated image attachments. This is a legacy format and isn’t widely used.

# Drawing and using attributed strings

`NSAttributedString` supports direct drawing. You can draw a string at a point or inside a `RECT` with the `drawAtPoint:` and `drawInRect:` methods. When your application has more than one window, the string is drawn into the current top view.

```
```objc
//Draw a string at the bottom left
[attrString drawAtPoint: NSZeroPoint];
```
```

Potentially, you can use this feature to animate strings and create Flash-like effects.

# Drawing text on a path

There is no easy way to draw text on a path. You must draw each glyph on a path separately, applying size, rotation, and position transforms as needed.

The Documentation includes sample code for a project called CircleView that draws text on a circular path. It uses Cocoa’s text storage, text layout, and text container classes, which are typically used to implement page design tools for desktop publishing and advanced PDF creation.

This approach isn’t any simpler or more efficient than a character-by-character solution; it simply wraps the character-by-character code inside container objects that your application may not need.

# Using attributed text in controls

Many controls support a `setAttributedTitle:` method. Use this method to label buttons and other controls with attributed text; for example, to set the label text color or add a text drop shadow.