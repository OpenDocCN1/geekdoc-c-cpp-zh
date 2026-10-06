# Automating Tasks through Scripting

Sometimes we use GUI applications to manipulate data sets in the same way each time. If the manipulation consists of invoking many menu options, or interacting with a dialog, not only does it become tedious but there is a risk that on occasions we may miss steps, transpose the order of a couple of steps—and perhaps not realize that a mistake has been made. One way to make things easier for users is to allow them to write scripts to perform sequences of actions automatically.

In this section, -script, that lets the user specify a script to execute. The application will then start up, execute the script, and terminate, with no GUI appearing at all.

The application we will use to illustrate this technique is called Gas Pump. It runs in lists of transactions recorded by a trucker gas station's pumps and presents the data in a tabular format, as shown in Figure 22.5.

# Figure 22.5. The Gas Pump application

![](bbox=[0.019, 0.415, 0.586, 0.735])

Each transaction is recorded by date and time, and by the pump, the quantity taken, the company ID and user ID of the trucker, and the transaction's status. The Gas Pump application can be used to manipulate the data in quite sophisticated ways, sorting it, filtering it, computing totals, and converting between liters and gallons.

The Gas Pump application supports transaction data in two formats: "Pump 2000", a plain text format with extension .p20, and "XML Gas Pump", an XML format with extension .gpx. The application can load and save in both formats, so it can be used to convert between them, simply by loading in one format and saving in the