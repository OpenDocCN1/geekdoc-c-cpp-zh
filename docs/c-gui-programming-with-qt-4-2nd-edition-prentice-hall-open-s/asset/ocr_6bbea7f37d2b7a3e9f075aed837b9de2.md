```
bitmap.setBit((height - i - 1) * width) + j,
    word & 0x80000000);
}
return bitmap;
}
```

The readmap() function is used to read a cursor's AND and XOR masks. These masks have two unusual features. First, they store the rows from bottom to top, instead of the more common top-to-bottom approach. Second, the endianness of the data appears to be reversed from that they used everywhere else in .cur files. In view of this, we must invert the y-coordinate in the setBit() call, and we read in the mask values one byte at a time, bit-shifting and masking to extract their correct values.

To build the plugin, we must use a .pro file that is very similar to the one we used for the Bronze style plugin earlier (p. 493):

```
TEMPLATE      = lib
CONFIG        += pluginhandler.h \
HEADERS       = cursorplugin.h
SOURCES       = cursorhandler.cpp \
               cursorplugin.cpp
DESTDIR       = $$[QT_INSTALL_PLUGINS]/imageformats
```

This completes the Windows cursor plugin. Plugins for other image formats would follow the same pattern, although some implement more of the QImageIOHandler API, in particular the functions used for writing images. Plugins of other kinds follow the pattern of having a plugin wrapper that exports one or several handlers that provide the underlying functionality.