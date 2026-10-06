is given as the second argument to the load() call. If an error occurs, we
warn the user and return.

```
QScriptValue qsDialog = interpreter.newQObject(dialog);
qsScript.setProperty("dialog", qsDialog);
```

```
QScriptValue qsTextEdit = interpreter.newQObject(jTextField);
qsScript.setProperty("jTextField", qsTextEdit);
QAction *action = new QAction(this);
action->setText(qsScript.property("text"));
action->setData(QVariant::fromValue(qsScript));
connect(action, SIGNAL(triggered()),
this, SLOT(actionTriggered()));
```

```
scriptsMenu->addAction(action);
```

```
return true;
```

```
}
```

Once we have successfully read the script and its user interface file, we are almost
ready to add the script to the Scripts menu. But first, there are a few details that we
must attend to. We want the run() function of our script to have access to the
dialog we just created. In addition, the script should be allowed to access the
QLineEdit that contains the HTML document being edited. 

We begin by adding the dialog to the interpreter as a QObject *. In response, the
interpreter returns the Object that to represent the dialog. We store this in
qsDialog. We add the qsDialog object to the qsScript object as a new property
called dialog. This means the script can access the dialog, including its
widgets, through the newly created dialog property. We use the same technique
to provide the script with access to the application's QLineEdit.

Finally, we create a new QAction to represent the script in the GUI. We set the
action's text to qsScript's text property, and the action "data" item to qsScript
itself. Lastly, we connect the action's triggered() signal to a custom
scriptActionTriggered() slot, and add the action to the Scripts menu.

```
void HtmlWindow::scriptActionTriggered()
{
QAction action = qobject_cast<QAction>(sender());
QScriptValue qsScript = action->data().value<QScriptValue>();
qsScript.property("run").call(qsScript);
}
```