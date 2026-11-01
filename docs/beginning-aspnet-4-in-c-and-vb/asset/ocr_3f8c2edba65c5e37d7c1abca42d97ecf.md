```
this.BackColor =
    Color.FromArgb(redComponent, greenComponent, blueComponent);
this.DesktopLocation = new Point(X, Y);

listBoxMessages.Items.Add("Background color: " + BackColor.Name);
listBoxMessages.Items.Add("Desktop location: " + 
    DesktopLocation.ToString());
listBoxMessages.Items.Add("Size: " + new Size(Width, Height).ToString());
listBoxMessages.Items.Add("Window State: " + WindowState.ToString());

storStream.Close();
storFile.Close();
}
}
return true;
```

Using the GetFileNames() method, the SelfPlacingWindow.xml document is pulled from the isolated storage and then placed into a stream and parsed using the XmlTextReader object:

```
IsolatedStorageFile storFile = IsolatedStorageFile.GetUserStoreForDomain();
string[] userFiles = storFile.GetFileNames("SelfPlacingWindow.xml");

foreach (string userFile in userFiles)
{
    if(userFile == "SelfPlacingWindow.xml")
    {
        listBoxMessages.Items.Add("Successfully opened file " + 
            userFile.ToString());

        StreamReader storStream =
            new StreamReader(new IsolatedStorageFileStream("SelfPlacingWindow.xml",
            FileMode.Open, storFile));
```

After the XML document is contained within the IsolatedStorageFileStream object, it is parsed using the XmlTextReader object:

```
System.Xml.XmlTextReader reader = new
    System.Xml.XmlTextReader(storStream);
```

After, it is pulled from the stream via the XmlTextReader. The element values are then pushed back into the application. You will then find — just as was accomplished in the SelfPlacingWindow sample that used the registry to record and retrieve application state values — that using isolated storage is just as effective as working with the registry. The application remembers the color, size, and position just as before.

# SUMMARY

In this chapter, you examined how to use the .NET base classes to access the file system and registry from your C# code. You have seen that in both cases the base classes expose simple, but powerful, object models that make it very simple to perform almost any kind of action in these areas. For the file system, these actions are copying files; moving, creating, and deleting files and folders; and reading and writing both binary and text files. For the registry, these are creating, modifying, or reading keys.

This chapter also reviewed isolated storage and how to use this from your applications to store them in the application state.

This chapter assumed that you were running your code from an account that has sufficient access rights to do whatever the code needs to do. Obviously, the question of security is an important one, and it is discussed in Chapter 21.