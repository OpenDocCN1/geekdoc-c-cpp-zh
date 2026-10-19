**Treat even simple items as ADTs** You don’t have to have a formidably data type to justify using an abstract data type. One of the ADTs in the example list is a light that supports only two operations—turning it on and turning it off. You might think that it would be a waste to isolate simple “on” and “off” operations in routines of their own, but even simple operations can benefit from the use of ADTs. Putting the light and its operations into an ADT makes the code more self-documenting and easier to change, confines the potential consequences of changes to the `TurnLightOn()` and `TurnLightOff()` routines, and reduces the number of data items you have to pass around.

**Refer to an ADT independently of the medium it’s stored on** Suppose you have an insurance-rates table that’s so big that it’s always stored on disk. You might be tempted to refer to it as a “rate file” and create access routines such as `RateFile.Read()`. When you refer to it as a file, however, you’re exposing more information about the data than you need to. If you ever change the program so that the table is in memory instead of on disk, the code that refers to it as a file will be incorrect, misleading, and confusing. Try to make the names of classes and access routines independent of how the data is stored, and refer to the abstract data type, like the insurance-rates table, instead. That would give your class and access routine names like `rateTable.Read()` or simply `rates.Read()`.

# Handling Multiple Instances of Data with ADTs in Non-Object-Oriented Environments

Object-oriented languages provide automatic support for handling multiple instances of an ADT. If you’ve worked exclusively in object-oriented environments and you’ve never had to handle the implementation details of multiple instances yourself, count your blessings! (You can also move on to the next section, “ADTs and Classes.”)

If you’re working in a non-object-oriented environment such as C, you will have to build support for multiple instances manually. In general, that means including services for the ADT to create and delete instances and designing the ADT’s other services so that they can work with multiple instances.

The font ADT originally offered these services:

```
currentFont.SetSize( sizeInPoints )
currentFont.SetBoldOn()
currentFont.SetBoldOff()
currentFont.SetItalicOn()
currentFont.SetItalicOff()
currentFont.SetTypeFace( faceName )
```