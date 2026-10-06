```
this.dialog.frame.charCountLineEdit.text = text.length;
this.dialog.frame.wordCountLineEdit.text = this.wordCount(text);
this.dialog.frame.lineCountLineEdit.text = this.lineCount(text);
this.dialog.exec();
```

The second property we create is the run() function. The function reads the text from the dialog's QText, populates the dialog's widgets with the results of the calculations, and finishes by showing the dialog.

This function can work only if the Object variable, obj, has suitable textEdit dialog properties, which is why we need to add them at the end of the createScriptAction(). The dialog itself must have a frame object (in this case a QFrame, which type does not matter), with three widgets—charCountLineEdit, wordCountLineEdit, and lineCountLineEdit, each with a writable text. Instead of this.dialog.frame.xxxCountLineEdit, we could also write findChild("xxx CountLineEdit"), which performs a recursive search and is more robust if we choose to change the dialog's design.

```
obj.wordCount = function(text) {
  var regExp = new RegExp("\w+", "g");
  var count = 0;
  while (regExp.exec(text)) {
    count++;
  }
  return count;
}
```

```
obj.lineCount = function(text) {
  var count = 0;
  var pos = 0;
  while ((pos = text.indexOf("\n", pos)) != -1) {
    count++;
    pos++;
  }
  return count + 1;
}
```

```
return obj;
```

The wordCount() and lineCount() functions have no external dependencies and work purely in terms of the String passed in them. Note that the wordCount() function uses the ECMAScript RegExp class, not Qt's QExp class. At the end of the script file, the return statement ensures that the Object and the text