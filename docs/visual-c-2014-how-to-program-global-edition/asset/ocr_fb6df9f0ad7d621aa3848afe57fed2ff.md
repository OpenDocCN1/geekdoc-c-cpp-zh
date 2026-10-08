# 17.9 Classes File and Directory 769

```
15 InitializeComponent();
16    }
17    // invoked when user presses key
18    private void input TextBox_KeyDown(object sender, KeyEventArgs e)
19    {
20        // determine whether user pressed Enter key
21        if (e.KeyCode == Keys.Enter)
22        {
23                // get user-specified file or directory
24                string fileName = TextBox.Text;
25
26                // determine whether fileName is a file
27                if (File.Exists(fileName))
28                {
29                    // get file's creation date, modification date, etc.
30                    GetInformation(fileName);
31
32                    // display file contents through StreamReader
33                    try
34                    {
35                        // read and file contents
36                        using (var stream = new StreamReader(fileName))
37                        {
38                            TextBox.AppendText(stream.ToEnd());
39                        }
40                    }
41                    catch (IOException)
42                    {
43                        MessageBox.Show("Error reading from file",
44                        "File Error", MessageBoxButtons.Ok, MessageBoxIcon.Error);
45                    }
46                }
47                // determine whether fileName is a directory
48            else if (Directory.Exists(fileName))
49\50            {
51                // get directory's creation date,
52                // modification date, etc.
53                GetInformation(fileName);
54
55                // obtain directory list of specified directory
56                string[] directoryList = 
57                Directory.GetDirectories(fileName);
58
59                TextBox.AppendText("Directory contents:\n");
60
61                // output directoryList contents
62                foreach (var directory in directoryList)
63                {
64                    TextBox.AppendText($"{directory}\n");
65                }
66            }
67}
```

Fig. 17.13 | Using classes File and Directory. (Part 2 of 4.)