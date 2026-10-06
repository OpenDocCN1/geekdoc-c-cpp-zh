
-   Fantasy—Decorative fonts that don't fit into any of the preceding categories are referred to as fantasy fonts. These fonts usually are extremely ornamental but are still letters, so exclude dingbats or picture fonts, illustrations, or icons.

Like cursive fonts, fantasy fonts are best reserved for decoration. You should use fantasy fonts sparingly and choose them carefully to reinforce the look and feel of your Web site, since each fantasy font invariably has a strong personality.

![](img/9cd61ac1d4015ed5688d0c411434a660_145_0.png)

- Examples of Dingbats. These are drawn from the dingbat font, Webdings.

# Dingbats

Although it does not have an official CSS designation, there is another important category of fonts to consider. Dingbats, also called symbol or picture fonts, do not represent numbers or letters, but are instead a collection of icons or pictograms each corresponding to a letter on the keyboard. The most common example of this font type is Webdings, which is installed on most computers. Webdings is a collection of common symbols. Although these glyphs can be used in place of a graphic version, there is no guarantee that the font will be installed. However, if you use dingbats as described later in this chapter, you can be relatively sure that you will get what you want, replacing some graphic icons with.

# HTML entities

A more reliable alternative to dingbats are HTML character entities. These are a collection of specialized glyphs that, instead of being represented by a single letter, are represented by code that begins with an ampersand (&) and ends with a semicolon (;). For example, the ampersand is represented in the code:

```
&amp;
```

For many characters (such as the ampersand), this is the only way to display them consistently across browsers and operating systems.

# What Are Webfonts?

Webfonts are a recent development in Web design that allow you to include fonts in your designs by linking to a font file on your server. Although this seems simple (and it is), this ability has been long coming and will revolutionize typography.

# Setting a Font Stack

The font-family property lets you determine the visual effect of your message by choosing the font for displaying your text. The typeface you use to display your text can make a powerful difference in how readers perceive your message. Whether you use a serif, sans-serif, monospace, or fantasy typeface can speak volumes before your visitor reads the first line of text. Examples of different typefaces. What do we do? To define the font family for an element:

- 1. Add the font-family property to your CSS rule. Type the font-family, followed by a colon. In this example, font-family is applied to the body tag, which will set the font for the entire page (Code 5.2).
- 2. Define the name of the primary font you want to use, followed by a comma. This name is not sensitive. Fonts that contain a space in their names must be enclosed in quotation marks, either single or double ("Times Roman" will work).
- 3. Define a list of alternative fonts, called fallback fonts, separated by commas. You can include as many as you want. These fonts will be used (in the order specified) if the previous font in the list is not available on the visitor's computer. See "Why Include Fallback Fonts" in this chapter for more details.
- 4. Define the generic font family. After the last fallback font, type the name of the generic font family for the particular style of font you're using. Table 5.2 lists generic values for families. Although including this value is optional, doing so is a good idea.

font-family: Helvetica, Arial,

# TABLE 5.2 Font-Family Values

| Value | Compatibility |
| --- | --- |
| <family-name> | IE3, IE7, CSS1+ |
| serif | IE3, IE7, CSS1+ |
| sans-serif | IE4/5/6, IE7, CSS1+ |
| cursive | IE4, IE7, CSS1+ |
| fantasy | IE4, IE7, CSS1+ |
| monospace | IE4, IE7, CSS1+ |

# Alice's Adventures in Wonderland

By Lewis Carroll

Chapter 1. Down the Rabbit-Hole Alice was getting very tired of sitting by the bank, and of nothing to do she wondered whether the book she was reading was any worth reading—what was the use of a book without pictures or conversations?—As Alice began... there was nothing so remarkable in the world that Alice had never twice seen before, as to mock a White Rabbit with a waistcoat and a watch in its pocket. But she thought nothing of this; yet she was very curious to see what the Rabbit was going to with such a watch, and when it hurried off down the hole, Alice, without a moment's hesitation, blankly went after it—and was in time to see how deep such a rabbit hole went.

> The body copy is displayed in Helvetica, Arial, or depending on which is available on the visitor's computer. However, headers are displayed in Georgia, Times, or Times Roman, depending on availability.

Code 5.2 font-properties.css—Two typefaces are applied to the page; the first affects the appearance of all text on the page; the second affects only others and the .baseline class.

```
*** CSS - Chapter 5 - font-properties.css ***

body {
  font-family: Helvetica, Arial, sans-serif;
}

font-family: Georgia, Times, "Times New Roman", serif;
```

# Font or Font Family?

Keep in mind the difference between a font and a font family. A font family is a series of fonts with similar appearance—such as Times—where a font refers to a specific version—such as Times normal, Times bold, Times italic, and so on.

# Why Include Fallback Fonts and Generic Font Families?

When you provide a list of fonts, the browser tries to use the first font on list. If it isn't available, the browser continues through the list until it finds a font that is installed on the visitor's computer. If no match is found, the browser displays the text in the visitor's default font. The advantage of using a generic font is that the browser tries to use the text, even if specific fonts are not available.
