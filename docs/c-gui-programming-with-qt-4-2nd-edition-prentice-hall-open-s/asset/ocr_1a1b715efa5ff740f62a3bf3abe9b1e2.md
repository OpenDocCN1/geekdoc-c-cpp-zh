```
spreadsheet.applyFilter(filter);
if (!spreadsheet.saveData(args[i], PumpSpreadsheet.Pump2000)
    throw Error("Error saving Pump 2000 data");

print("Removed erroneous transactions from " + args[i]);
```

This script relies on two global variables: args spreadsheet returns the command-line arguments supplied after the -script option. spreadsheet variable is a reference to a PumpSpreadsheet object that we can use to perform various operations (file format conversion, unit conversion, filtering, etc.). The script also calls slots on the PumpSpreadsheet object, instantiates and initializes PumpFilter objects, and uses the PumpSpreadsheet::FileFormat

We begin with a simple sanity check, and for each file name listed on the command line we clear the spreadsheet object and attempt to load in the file's data. We assume that the files are all in Pump 2000 (.p20) format. For each successfully loaded file, we create a new PumpFilter. We set the status property and then call PumpSpreadsheet's applyFilter() function (which is accessible because we made it a slot). Finally, we save the updated spreadsheet data back to the original file, and output a message to the user.

The other three scripts have a similar structure: they are included with the book's source code.

To support scripts such as the onlyok.js script, we need to perform the following steps in the Gas Pump application:

+   1. Detect -script command-line option.

+   2. Load the specified script file.

+   3. Expose PumpSpreadsheet instance to the interpreter.

+   4. Expose the command-line arguments to the interpreter.

+   5. Expose the FileFormat and Column enums to the interpreter.

+   Wrap the PumpFilter class so that its member variables can be accessed from the script.