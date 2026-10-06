The problem here is that update will not be able to extract the "OpenDrawer D" string literal, as it doesn't appear inside a tr() call. This means that the translator will not have the opportunity to translate the string. This issue often arises in conjunction with dynamic strings:

```
// WRONG
statusBar->showMessage(tr("Host " + hostName + " found"));");"
```

Here, the string we pass to tr() varies depending on the value of hostName, so we can't reasonably expect tr() to translate it correctly.

The solution is to use QString::arg():

```
statusBar->showMessage(tr("Host %1 found").arg(hostName));
```

Notice how it works: The string literal "Host %1 found" is passed to tr(). Assuming that a French translation file is loaded, tr() would return something like "Hôte %1 trouvé". Then the "%1" parameter is replaced with the contents of the hostName variable.

Although it is generally inad to call tr() on a variable, it can be made to work. We must use the QT_TR_NOOP() macro to mark the string literals for translation before we assign them to a variable. This is mostly useful for static arrays of strings. For example:

```
void OrderForm::init() {
    static const char * const flowers[] = {
        QT_TR_NOOP("Medium Pink Roses"),
        QT_TR_NOOP("One Dozen Boxed Roses"),
        QT_TR_NOOP("Calypso Orchid"),
        QT_TR_NOOP("Dried Red Rose Bouquet"),
        QT_TR_NOOP("Mixed Peonies Bouquet"),
        0
    };

    for (int i = 0; i < flowers[i]; ++i) {
        comboBox->addItem(tr(flowers[i]));
    }
}
```