- verbose option tells lupdate to provide more feedback than usual. Here's the expected output:

```
Updating 'spreadsheet_de.ts...
Found 98 source texts (98 new and 0 already existing)
Updating 'spreadsheet_fr.ts...
Found 98 source texts (98 new and 0 already existing)
```

Every string that appears within a tr() call in the application's source code is stored in the .ts files, along with an empty translation. Strings that appear in the application's .ui files are also included.

The translate tool assumes by default that the arguments to tr() are Latin-1 strings. If this isn't the case, we must add a CODEFORTR entry to the .pro file. For example:

```
CODEFORTR = EUC-JP
```

This must be in addition to calling QTextCodec::setCodecForTr() from the application's main() function.

Translations then need to be added to the spreadsheet_de.ts and spreadsheet_fr.ts files using Qt Linguist. (Figure 18.2 shows Qt Linguist in action.)

# Figure 18.2. Qt Linguist in action

[View full size image]