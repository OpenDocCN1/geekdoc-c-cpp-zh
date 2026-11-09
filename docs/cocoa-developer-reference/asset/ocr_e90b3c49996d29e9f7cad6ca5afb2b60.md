# Figure 15.12

Replacing static text

![](bbox=[0.253, 0.199, 0.779, 0.536])

To create a file, right-click Resources and choose Add➔New File. Select Mac OS X Resource and Strings File, as shown in Figure 15.14.

The file is saved as **Localizable.strings**, as shown in Figure 15.15. The filepath should be **English.lproj** for an English file, **French.lproj** for a French file, and so on. This creates a **Localizable.strings** item in Xcode with separate files for each language.

Before you edit a file with non-English text, convert it to the UTF-8 encoding. Right-click it, select Get Info, and select the encoding from drop-down menu, as shown in Figure 15.16. Select the Convert option at the alert.

You can edit each file in Xcode. Strings are stored in key-text pairs.

```
"key" = "Localized text";
```