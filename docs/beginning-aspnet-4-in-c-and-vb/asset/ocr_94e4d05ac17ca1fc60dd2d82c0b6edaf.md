Reading from the storage is done through the ReadSettings() method. This method is presented in the following code example:

```
bool ReadSettings()
{
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
            System.Xml.XmlTextReader reader = new
                System.Xml.XmlTextReader(storStream);

            int redComponent = 0;
            int greenComponent = 0;
            int blueComponent = 0;

            int X = 0;
            int Y = 0;

            while (reader.Read())
            {
                switch (reader.Name)
                {
                    case "Red":
                        redComponent = int.Parse(reader.ReadString());
                        break;
                    case "Green":
                        greenComponent = int.Parse(reader.ReadString());
                        break;
                    case "Blue":
                        blueComponent = int.Parse(reader.ReadString());
                        break;
                    case "X":
                        X = int.Parse(reader.ReadString());
                        break;
                    case "Y":
                        Y = int.Parse(reader.ReadString());
                        break;
                    case "Width":
                        this.Width = int.Parse(reader.ReadString());
                        break;
                    case "Height":
                        this.Height = int.Parse(reader.ReadString());
                        break;
                    case "WindowState":
                        this.WindowState = (FormWindowState)FormWindowState.Parse
                            (WindowState.GetType(), reader.ReadString());
                        break;
                    default:
                        break;
                }
            }
        }
    }
}
```