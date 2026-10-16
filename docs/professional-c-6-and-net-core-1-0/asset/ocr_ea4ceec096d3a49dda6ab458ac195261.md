setting the proper `ScriptEngine`, creating the `ScriptSource`, and creating the `ScriptScope`.

The `ScriptRuntime` object is the starting point, or base, for hosting. It contains the global state of the hosting environment. The `ScriptRuntime` is created using the `CreateFromConfiguration` static method. This is what the configuration file looks like (code file `DLRHostSample/app.config`):

```
<configuration>
    <configSections>
        <section name="microsoft.scripting"
            type="Microsoft.Scripting.Hosting.Configuration.Section, Microsoft.Scripting />
        </configSections>

        <microsoft.scripting>
            <languages>
                <language names="IronPython;Python;py" extensions=".py"
                    displayName="IronPython 2.7.5"
                    type="IronPython.Runtime.PythonContext, IronPython />
            </languages>
        </microsoft.scripting>
</configuration>
```

The code defines a section for `microsoft.scripting` and sets a couple of properties for the IronPython language engine.

Next, you get a reference to the `ScriptEngine` from the `ScriptRuntime`. In the example, you specify that you want the Python engine, but the `ScriptRuntime` would have been able to determine this on its own because of the `py` extension on the script.

The `ScriptEngine` does the work of executing the script code. There are several methods for executing scripts from files or from snippets of code. The `ScriptEngine` also gives you the `ScriptSource` and `ScriptScope`.

The `ScriptSource` object is what gives you access to the script. It represents the source code of the script. With it you can manipulate the source of the script, load it from a disk, parse it line by line, and even compile the script into a `CompiledCode` object. This is handy if the same script is executed multiple times.

The `ScriptScope` object is essentially a namespace. To pass a value into or out of a script, you bind a variable to the `ScriptScope`. In the following example, you call the `SetVariable` method to pass the `prodCount` and the `amt` variables into the Python script. These variables are the values from the `totalItems` and the `totalAmt` text boxes, respectively. The calculated discount is retrieved from the script by using the `GetVariable` method. In this example, the `retAmt` variable has the value you’re looking for.

The `CalcTax` button illustrates how to call a method on a Python object. The script `CalcTax.py` is a very simple method that takes an input value, adds 20 percent tax, and returns the new value. Here’s what the code