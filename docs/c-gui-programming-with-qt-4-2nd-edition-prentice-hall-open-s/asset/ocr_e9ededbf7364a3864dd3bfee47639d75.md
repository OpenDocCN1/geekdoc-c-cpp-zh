# Customizing Qt/Embedded Linux

When installing Qt/Embedded Linux, we can specify features we want to leave out to reduce its memory footprint. Qt/Embedded Linux includes more than one hundred configurable features, each of which is associated with a preprocessor symbol. For example, `QT_NO_FILEDIALOG` excludes `QFileDialog` from the QtGui library, and `QT_NO_I18N` leaves out support for internationalization. The features are listed in `src/corelib/global/qfeatures.txt`.

Qt/Embedded Linux provides five example configurations (minimum, small, medium, large, and dist) that are stored in `src/corelib/global/qconfig-xxx.h` files. These configurations can be specified using the `configure` script's `-qconfig xxx` option, for example:

```
./configure -qconfig small
```

To create custom configurations, we can manually provide a `qconfig-xxx.h` and use it as though it were a standard configuration. Alternatively, we can use the `qconfig` graphical tool, located in Qt's `tools` subdirectory.

Qt/Embedded Linux provides the following classes for interfacing with input and output devices and for customizing the look and feel of the window system:

| Class | Base Class for |
| --- | --- |
| QScreen | Screen drivers |
| QScreenDriverPlugin | Screen driver plugins |
| QSMouseHandler | Mouse drivers |
| QMouseDriverPlugin | Mouse drivers |
| QKeyboardHandler | Keyboard drivers |
| QbdDriverPlugin | Keyboard driver plugins |
| QWSInputMethod | Input methods |
| QDecoration | Window decoration styles |
| QDecorationPlugin | Window decoration style plugins |

To obtain the list of predefined drivers, input methods, and window decoration styles, run the `configure` script with the `-help` option.

The screen can be specified using the `-display` command-line option when starting the Qt/Embedded Linux server, as seen in the previous section, or by