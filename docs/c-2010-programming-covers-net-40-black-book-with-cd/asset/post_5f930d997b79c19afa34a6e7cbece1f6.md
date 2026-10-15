
## Chapter 29: File Handling in C# 2010

Now, let's create an application, named CompressingFile (available on the CD-ROM), and perform the following steps to compress files:

- 1. Add a Label control, two Button controls, a TextBox control, an OpenFileDialog control, and a SaveFileDialog control.
- 2. Change the Text property of the Label control to Path of the file to compress: and the Text property of the Button controls to Browse and Compress File, respectively, as shown in Figure 29:30:

![](img/e073a4882197be4ab61103cbe0bcb394_1453_0.png)

3. Open the Form1.cs file of the CompressingFile application and replace the existing code with the code shown in Listing 29.11:

### Listing 29.11: Showing the Code for the Form1.cs File of the CompressingFile Application

```
```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.IO;
using System.IO.Compression;

namespace CompressingFile
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    }

    private void button1_Click(object sender, EventArgs e)
    {
        if (openFileDialog1.ShowDialog() == DialogResult.OK)
        {
            textBox1.Text = openFileDialog1.FileName;
        }
    }

    private void button2_Click(object sender, EventArgs e)
    {
        if (saveFileDialog1.ShowDialog() == DialogResult.OK)
        {
            // Note: code in image transcription is incomplete at this point
        }
    }
}
```
```

```
byte[] bufferwrite;
FileStream fsSource;
FileStream fsDest;
GZipStream gzCompressed;
fsSource = new FileStream(textBox1.Text, FileMode.Open, FileAccess.Read, FileShare.Read);
bufferwrite = new byte[fsSource.Length];
fsSource.Read(bufferwrite, 0, bufferwrite.Length);
fsDest = new FileStream(saveFileDialog1.FileName, FileMode.OpenOrCreate, FileAccess.Write);
gzCompressed = new GZipStream(fsDest, CompressionMode.Compress, true);
gzCompressed.Write(bufferwrite, 0, bufferwrite.Length);
fsSource.Close();
gzCompressed.Close();
fsDest.Close();
}
}
```

4. Press the F5 key to run the application and click the Browse button. The Open dialog box appears, as shown in Figure 29.31:

![](img/e073a4882197be4ab61103cbe0bcb394_1454_0.png)

Figure 29.31: Showing the Open Dialog Box

5. Select the file that you want to compress from the Open dialog box and click the Open button (Figure 29.31). In our case, we have selected the File.txt file. The path of the selected file appears in the Path of the file to compress text box, as shown in Figure 29.32:

![](img/e073a4882197be4ab61103cbe0bcb394_1454_1.png)

Figure 29.32: Displaying the Path of the Compressed File

6. Click the Compress File button to compress the file. The Save As dialog box appears, as shown in Figure 29.33:

![](img/e073a4882197be4ab61103cbe0bcb394_1455_0.png)

Figure 29.33: Showing the Save As Dialog Box

7. Specify the name and location for the file and click the Save button (Figure 29.33).

After compressing the files, let's learn how to decompress them. For this, create an application named DecompressingFiles (also available on CD-ROM) and perform the following steps:

- 1. Add a Label control, two Button controls, a TextBox control, an OpenFileDialog control, and a SaveFileDialog control on Form1.
- 2. Change the Text property of the Label control to Select file to decompress and the Text property of the Button controls to Browse and Decompress File, respectively, as shown in Figure 29.34:

![](img/e073a4882197be4ab61103cbe0bcb394_1455_1.png)

Figure 29.34: Showing the Design View of the DecompressingFiles Application

- 3. Open the Form1.cs file of the DecompressingFiles application and replace the existing code with the code shown in Listing 29.12:

### Listing 29.12: Showing the Code for the Form1.cs File of the DecompressingFiles Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.IO;
using System.IO.Compression;

namespace DecompressingFiles
```

```
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                textBox1.Text = openFileDialog1.FileName;
            }
        }

        private void button2_Click(object sender, EventArgs e)
        {
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                byte[] bufferwrite;
                FileStream fsSource;
                FileStream fsDest;
                GZipStream gzDecompressed;
                fsSource = new FileStream(textBox1.Text, FileMode.Open, FileAccess.Read, FileShare.Read);
                gzDecompressed = new GZipStream(fsSource, CompressionMode.Decompress, true);
                bufferwrite = new byte[4];
                fsSource.Position = (int)fsSource.Length - 4;
                fsSource.Read(bufferwrite, 0, 4);
                fsSource.Position = 0;
                int bufferLength = BitConverter.ToInt32(bufferwrite, 0);
                byte[] buffer = new byte[bufferLength + 100];
                int readoffset = 0;
                int totalBytes = 0;
                while (true)
                {
                    int bytesRead = gzDecompressed.Read(buffer, readoffset, 100);
                    if (bytesRead == 0)
                        break;
                    readoffset += bytesRead;
                    totalBytes += bytesRead;
                }
                fsDest = new FileStream(saveFileDialog1.FileName, FileMode.Create);
                fsDest.Write(buffer, 0, totalBytes);
                fsSource.Close();
                gzDecompressed.Close();
                fsDest.Close();
            }
        }
    }
}
```

- 4. Press the F5 key to run the application and click the Browse button to open the Open dialog box.
- 5. Select the compressed file from the Open dialog box and click the Open button, as shown in Figure 29.35:

![](img/e073a4882197be4ab61103cbe0bcb394_1457_0.png)

Figure 29.35: Showing the Open Dialog Box

6. Now, click the Decompress File button on the Form1 form, as a result, the Save As dialog box appears, as shown in Figure 29.36:

![](img/e073a4882197be4ab61103cbe0bcb394_1457_1.png)

Figure 29.36: Showing the Save As Dialog Box

7. Specify the name for the file in the File Name combo box of the Save As dialog box, so that you can easily locate the file in the specified location in its decompressed form. In this case, we have specified DecompressedFile (Figure 29.36).

8. Click the Save button to save the file with the name DecompressedFile in the desired location. Now, let’s summarize the main topics discussed in this chapter.

## Summary

In this chapter, you have learned about the System.IO namespace and its classes. Next, you have learned how to work with directories and files. In addition, you have learned to check directory existence, create, rename, and delete the directories. You have also learned that file I/O operations involve checking the file properties; and performing other operations such as creating, reading, writing, renaming, and copying files. Finally, you have learned how to compress and decompress files.

In the next chapter, you learn to work with Extensible Markup Language (XML) and .NET.

## 30

## Working with XML and .NET

![](img/e073a4882197be4ab61103cbe0bcb394_1458_0.png)

| If you need an Immediate Solution to: | See page: |
|---|---|
| Working with Streamed XML | 1425 |
| Implementing DOM in .NET | 1432 |
| Navigating and Transforming Data | 1435 |
| Converting ADO.NET and XML Data | 1438 |
| Implementing Object Serialization with XML | 1442 |
