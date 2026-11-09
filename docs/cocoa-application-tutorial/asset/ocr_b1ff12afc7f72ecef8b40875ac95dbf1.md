# CHAPTER 8

# Expanding on the Basics

If you had buttons of a different style, they would also respond in characteristic ways to mouse clicks.

Now click in one of the text fields. See how the insertion point blinks in place. Type some text and select it. Use the commands in the Edit menu to copy it and paste it in the other text field.

Do you recall the `nextKeyView` connections you made between the Currency Converter text fields? Insert the cursor in a text field, press the Tab key and watch the cursor jump from field to field.

# Menu Commands

Interface Builder gives every new application a default menu that includes the application, File, Edit, Window, and Help menus. Some of these menus, such as Edit, contain ready-made sets of commands. For example, with the Services submenu (whose items are added by other applications at runtime) you can communicate with other Mac OS X applications. You can manage your application’s windows with the Window menu.

Currency Converter needs only a few commands: the Quit and Hide commands and the Edit menu’s Copy, Cut, and Paste commands. You can delete the unwanted commands if you wish. However, you could also add new ones and get “free” behavior. An application designed in Interface Builder can acquire extra functionality with the simple addition of a menu or menu command, without the need for compilation. For example:

+   - The Font submenu adds behavior for applying fonts to text in text view objects, like the one in the text view object in the Text palette. Your application gets the Font window and a font manager “for free.” Text elements in your application can use this functionality right out of the box. See *Font Panel* for more information.
+   - The Text submenu allows you to align text anywhere text is editable and to display a ruler in the `NSText` object for tabbing, indentation, and alignment.
+   - Thanks to the PDF graphics core of Mac OS X, many objects that display text or images can print their contents as PDF documents.

# Document Management

Many applications create and manage repeatable, semi-autonomous objects called documents. Documents contain discrete sets of information and support the entry and maintenance of that information. A word-processing document is a typical example. The application coordinates with the user and communicates with its documents to create, open, save, close, and otherwise manage them. You could also save your Currency Converters as documents, with a little extra code.

See *Document-Based Applications Overview* in Cocoa Design Guidelines Documentation for more information.

# File Management

An application can use the Open dialog, which is created and managed by the Application Kit framework, to help the user locate files in the file system and open them. It can also use the Save dialog to save information in files. Cocoa also provides classes for managing files in the file system (creating, comparing, copying, moving, and so forth) and for managing user defaults.