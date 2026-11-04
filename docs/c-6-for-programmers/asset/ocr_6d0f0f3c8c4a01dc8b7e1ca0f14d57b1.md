```
```csharp
63     }
64     blueToolStripMenuItem.Checked = true;
65 }
66
67 // update Menu state and color display red
68 private void redToolStripMenuItem_Click(
69     object sender, EventArgs e)
70 {
71     // reset checkmarks for Color ToolStripMenuItems
72     ClearColor();
73
74     // set color to Red
75     displayLabel.ForeColor = Color.Red;
76     redToolStripMenuItem.Checked = true;
77 }
78
79 // update Menu state and color display green
80 private void greenToolStripMenuItem_Click(
81     object sender, EventArgs e)
82 {
83     // reset checkmarks for Color ToolStripMenuItems
84     ClearColor();
85
86     // set color to Green
87     displayLabel.ForeColor = Color.Green;
88     greenToolStripMenuItem.Checked = true;
89 }
90
91 // reset checkmarks for Font ToolStripMenuItems
92 private void ClearFont()
93 {
94     // clear all checkmarks
95     timesToolStripMenuItem.Checked = false;
96     courierToolStripMenuItem.Checked = false;
97     comicToolStripMenuItem.Checked = false;
98 }
99
100 // update Menu state and set Font to Times New Roman
101 private void timesToolStripMenuItem_Click(
102     object sender, EventArgs e)
103 {
104     // reset checkmarks for Font ToolStripMenuItems
105     ClearFont();
106
107     // set Times New Roman font
108     timesToolStripMenuItem.Checked = true;
109     displayLabel.Font = new Font("Times New Roman", 14,
110         displayLabel.Font.Style);
111 }
```
```

Fig. 15.7 | Using menus to change text font and color. (Part 3 of 5.)