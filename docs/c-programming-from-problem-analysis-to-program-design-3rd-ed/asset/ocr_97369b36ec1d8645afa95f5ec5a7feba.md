Example 13-8 first checks to see if the filename entered by the user already exists. This is accomplished using the **static Exists()** method of the **File** class. When the name entered is a new file, objects are instantiated of the **FileStream** and **BinaryWriter** classes. Notice that the second argument to the **FileStream** constructor is an enumeration. The **FileMode** enumerated type specifies how the operating system should open the file. As shown in Figure 13-10, the field value member named **CreateNew** indicates that the operating system should create a new file. IntelliSense notes that the **System.IO.IOException** is thrown if the file already exists.

![](bbox=[0.177, 0.281, 0.901, 0.386])

**Figure 13-10** Enumerated FileMode

The **BinaryWriter object** is based on the **FileStream object** or wrapped around the **FileStream object**. The **FileStream object** is sent in as an argument to the **BinaryWriter** constructor.

In Example 13-8, first a string argument is written to the file. This is followed by several integers and a decimal value. Finally, for the file to be created properly, both files must be closed. Figure 13-11 shows the console output produced. In the foreground of the figure, you see the newly created file.