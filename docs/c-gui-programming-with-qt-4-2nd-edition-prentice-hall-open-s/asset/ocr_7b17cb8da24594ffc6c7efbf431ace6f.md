```
args << "monochrome";
args << sourceFile << targetFile;

process.start("convert", args);
}
```

When the user clicks the Convert button, we copy the source file's name and change the extension to match the target file format. We use the platform-specific directory separator ('/' or '\', as available via QDir::separator()) instead of hardcoding slashes because the file name will be visible to the user.

We disable the Convert button to avoid the user accidentally launching multiple conversions, and we clear the text editor that we use to show status information.

To initiate run external process, we call QProcess::start() with the name of the program we want to run (convert) and any arguments it. In this case, we pass the -enhance and -monochrome flags if the user checked the appropriate options, followed by the source and target file names. The convert program infers the required conversion from the file extensions.

```
void ConvertDialog::updateConsoleText()\{
    QByteArray newData = process.readAllStandardError();
    QString text = outputTextEdit->toPlainText()
    + QString::fromLocal8Bit(newData);
    outputTextEdit->setPlainText(text);
}
```

Whenever the external process writes to cerr, the updateConsoleText slot is called. We read the error text and add it to the QTextEdit's existing text.

```
void ConvertDialog::processFinished(int exitCode,
QProcess::ExitStatus exitStatus)
{
    if (exitStatus == QProcess::CrashExit) {
        outputTextEdit->append(tr("Conversion crashed"));
    } else if (exitCode != 0) {
        outputTextEdit->append(tr("Conversion failed"));
    } else {
        outputTextEdit->append(tr("File %1 created").arg(targetFile));
    }
    buttonBox->button(QDialogButtonBox::Ok)->setEnabled(true);
}
```