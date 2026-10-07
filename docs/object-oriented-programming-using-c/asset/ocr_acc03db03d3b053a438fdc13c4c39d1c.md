# Object Oriented Programming using C#

# Case Study

The application window will look as shown below....

![](bbox=[0.185, 0.127, 0.862, 0.323])

Note this includes buttons for increasing a client's credit and deleting a client – we realised some ago that we needed but functionality was not added to the first version of this system. We will extend our system to add this additional functionality once a basic system is working.

The ApplicationWindow_Load() method is shown below -

```
private void ApplicationWindow_Load(object sender, EventArgs e)
{
    clientBook = new ClientBook();
    messageSet = new MessageSet();
    try
    {
        FileStream inFile = new FileStream("ClientAndData", FileMode.Open, FileAccess.Read);
        BinaryFormatter bf = new BinaryFormatter();
        clientBook = (ClientBook)bf.Deserialize(inFile);
        messageSet = (MessageSet)bf.Deserialize(inFile);
        inFile.Close();
        inFile.Dispose();
    }
    catch (FileNotFoundException)
    {
    }
}
```

Download free ebooks at bookboom.com

238