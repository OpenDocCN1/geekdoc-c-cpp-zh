Make it possible to instantiate PumpFilter objects from the script.

# 8. Execute the script.

The relevant code is located in main.cpp, scripting.cpp, and scripting.h. Let's begin with main.cpp:

```
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    QStringList args = QApplication::arguments();
    if (args.count() >= 3 && args[1] == "-script") {
        runScript(args[2], args.mid(3));
        return 0;
    } else if (args.count() == 1) {
        Pumpwindow window;
        window.show();
        window.resize(600, 400);
        return app.exec();
    } else {
        std::cerrerr << "Usage: gaspump [-script myscript.js <arguments>" << std::endl;
        return 1;
    }
}
```

The command-line arguments are accessible through the QApplication::arguments() function, which returns a QStringList. The first item in the list is the application's name. If there are at least three arguments and the second argument is -script, we assume that the third argument is a script name. In this case, we runScript() with the script's name as its first argument and the rest of the string list as its second parameter. Once the script has been run, the application terminates immediately.

If there is just one argument, the application's name, we create and show a PumpWindow, and start off the application's event loop in the conventional way.

The application's scripting support is provided by scripting.h and scripting.cpp. These files define the runScript() function, the pumpFilterConstructor() support function, and the PumpFilterPrototype supporting class. The supporting function and class are specific to the Gas Pump application, but we will still review them since they illustrate some general points about making applications scriptable.