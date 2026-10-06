right. In those languages, the language of the application may be reversed, and this is done by calling QApplication::setLayoutDirection(Qt::RightToLeft). The translation files for Qt contain a special marker called 'LTR' that tells Qt whether the language is left-to-right or right-to-left, so we normally don't need to call setLayoutDirection() ourselves.

It may prove more convenient for users if we use our applications with Qt's resource system. Not only does this reduce the number of files distributed as part of the product, but it also avoids the risk of translation files getting lost or deleted by accident. Assuming that the .qm files are located in a translations subdirectory in the source tree, we would then have a myapp.qrc file with the following contents:

```
<RCC>
<resource>
    <file>translations/myapp_de.qm</file>
    <file>translations/myapp_fr.qm</file>
    <file>translations/myapp_zh.qm</file>
    <file>translations/qt_de.qm</file>
    <file>translations/qt_fr.qm</file>
    <file>translations/qt_zh.qm</file>
</resource>
</RCC>
```

The .pro file would contain the following entry:

```
RESOURCES += myapp.qrc
```

Finally, in main(), we must specify :/translations as the path for the translation files. The leading colon indicates that the path refers to a resource as opposed to a file in the file system.

We have now covered all that is required to make an application able to operate using translations into other languages. But language and the direction of the writing system are not the only things that vary between countries and cultures. An internationalized program must also take into account the locale and date formats, numeric formats, string collation order. Qt includes a QLocale class that provides localized numeric and date/time formats. To query other locale-specific information, we can use the standard C++ setlocale() and localeconv() functions.

Some Qt classes and functions adapt their behavior to the locale: