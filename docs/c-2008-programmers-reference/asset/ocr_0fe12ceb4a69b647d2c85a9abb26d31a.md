Populate the default Form1 with the controls shown in Figure 15-43 (load the pictureBox1 with a JPG image).

![](bbox=[0.22, 0.22, 0.82, 0.5])

Figure 15-43

In the code-behind of Form1, define the two helper functions as follows:

> Remember to import the System.IO namespace for these two helper functions.

```
public byte[] ImageToByteArray(Image img)
{
    MemoryStream ms = new MemoryStream();
    img.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);
    return ms.ToArray();
}

public Image ByteArrayToImage(byte[] data)
{
    MemoryStream ms = new MemoryStream(data);
    Image img = new Bitmap(ms);
    return img;
}
```

Code the Test button as follows:

```
private void btnTest_Click(object sender, EventArgs e)
{
    //---create an instance of the Helper class---
    Base64Codec.Helper codec = new Base64Codec.Helper();
    //---convert the image in pictureBox1 to base64---
```