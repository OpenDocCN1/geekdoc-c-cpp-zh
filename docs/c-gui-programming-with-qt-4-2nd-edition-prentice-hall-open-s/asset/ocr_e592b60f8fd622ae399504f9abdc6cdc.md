We will review the runScript() function in several parts, since it contains several subtle details.

```
bool runScript(const QString &fileName, const QStringList &args)
{
    QFile file(fileName);
    if (!file.open(QIODevice::ReadOnly)) {
        std::cerr << "Error: Cannot read file " << qPrintable(fileName)
                  << ": " << qPrintable(file.errorString())
                  << std::endl;
    }
    return false;
}

QTextStream in(&file);
in.setCodec("UTF-8");
QString script = in.readAll();
file.close();
```

We start by reading the script into a QString.
QScriptEngine interpreter;

PumpSpreadsheet spreadsheet;
QScriptValue qsSpreadsheet = interpreter.newObject(&spreadsheet);
interpreter.globalObject().setProperty("spreadsheet", qsSpread);

Once we have the script in a QString, we create a QScriptEngine and a PumpSpreadsheet instance. We then create a QScriptValue to refer to the PumpSpreadsheet instance, and set this as a global property of the interpreter, making it accessible inside scripts as the spreadsheet global variable. All the PumpSpreadsheet's slots and properties are available through the spreadsheet variable to any script that cares to use them.

```
QScriptValue qsArgs = QScriptValueFromSequence(&interpreter, args);
interpreter.globalObject().setProperty("args", qsArgs);
```

(The empty) args list of type QStringList is passed to the runScript() function contains the command-line arguments the user wants to pass to the script. To make these arguments accessible to scripts, we must, as always, create a QScriptValue to represent them. To convert a sequential