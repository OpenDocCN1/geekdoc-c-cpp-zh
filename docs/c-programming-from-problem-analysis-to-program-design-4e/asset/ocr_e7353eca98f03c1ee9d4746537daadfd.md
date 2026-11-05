entered is a new file, objects are instantiated of the FileStream and BinaryWriter classes. Notice that the second argument to the FileStream constructor is an enumeration. The FileMode enumerated type specifies how the operating system should open the file. As shown in Figure 13–10, the field value member named CreateNew indicates that the operating system should create a new file. IntelliSense notes that the System.IO.IOException is thrown if the file already exists. Another option for an enumerated value for FileMode is Create. Create differs from CreateNew in that it will replace an existing file with a new one, if one already exists, instead of throwing an exception.

![](bbox=[0.185, 0.267, 0.912, 0.372])

**FIGURE 13-10** Enumerated FileMode

The BinaryWriter object is based on the FileStream object or wrapped around the FileStream object. The FileStream object is sent in as an argument to the BinaryWriter constructor.

In Example 13–8, first a string argument is written to the file. This is followed by several integers and a decimal value. Finally, for the file to be created properly, both files must be closed. Figure 13–11 shows the console output produced. In the foreground of the figure, you see the newly created file.

![](bbox=[0.185, 0.581, 0.912, 0.895])

**FIGURE 13-11** BinaryInputTestFile.bin file created