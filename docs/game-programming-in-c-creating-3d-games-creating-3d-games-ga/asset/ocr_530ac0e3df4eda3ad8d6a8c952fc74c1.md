# LOCALIZATION

**Localization** is the process of converting a game from one region or **locale** to a different one. The most common items to localize include any voice-over dialogue as well as any text shown onscreen. For example, a game developer working in English may want to localize to Chinese if releasing the game in China. The biggest expense of localization is in the content: Someone must translate all the text and dialogue, and in the case of dialogue, different actors must speak the lines in different languages.

However, part of the responsibility of localization falls on the programmer. In the case of the UI, the game needs some system to easily show text from different locales onscreen. This means you can’t hard-code strings such as “Do you want to quit?” throughout the code. Instead, you minimally need a map to convert between a key like "QuitText" and the actual text shown onscreen.

# Working with Unicode

One issue with localizing text is that each ASCII character only has 7 bits of information (though it’s stored internally as 1 byte). Only 7 bits of information means there is a total of 128 characters. Of these characters, 52 are letters (upper- and lowercase English), and the rest of the characters are numbers and other symbols. ASCII does not contain any glyphs from other languages.