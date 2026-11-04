Because the reading may happen so fast for a small file, you can insert Sleep() statements to simulate reading a large file. Figure 11-3 shows the output.

![](bbox=[0.22, 0.18, 0.78, 0.45])

Figure 11-3

# MemoryStream

Sometimes you need to manipulate data in memory without resorting to saving it in a file. A good example is the PictureBox control in a Windows Form. For instance, you have a picture displayed in the PictureBox control and want to send the picture to a remote server, say a Web Service. The PictureBox control has a Save() method that enables you to save the image to a Stream object.

Instead of saving the image to a FileStream object and then reloading the data from the file into a byte array, a much better way would be to use a MemoryStream object, which uses the memory as a backing store (which is more efficient compared to performing file I/O; file I/O is relatively slower).

The following code shows how the image in the PictureBox control is saved into a MemoryStream object:

```
//---create a MemoryStream object---
MemoryStream ms1 = new MemoryStream();

//---save the image into a MemoryStream object---
pictureBox1.Image.Save(ms1, System.Drawing.Imaging.ImageFormat.Jpeg);
```

To extract the image stored in the MemoryStream object and save it to a byte array, use the Read() method of the MemoryStream object:

```
//---read the data in ms1 and write to buffer---
ms1.Position = 0;
byte[] buffer = new byte[ms1.Length];
int bytesRead = ms1.Read(buffer, 0, (int)ms1.Length);
```