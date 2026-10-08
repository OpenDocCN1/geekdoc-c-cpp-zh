# 17.9 Classes File and Directory 773

```
54      // display the number of files with current extension
55      resultsTextBox.AppendText(
56          $"{found[current]} {current} files." + 
57          Environment.NewLine);
58  )
59  
60      found.Clear(); // clear results for new search
61      {
62      }
63
64      // search directory using LINQ
65      private void SearchDirectory(string folder)
66      {
67          // find files contained in the directory
68          string[] files = Directory.GetFiles(folder);
69
70          // subdirectories in the directory
71          string[] directories = Directory.GetDirectories(folder);
72
73          // find all extensions in this directory
74          var extensions = =
75              from file in files
76              group file by Path.GetExtension(file);
77
78              foreach (var extension in extensions)
79              {
80                  if (found.ContainsKey(extension.Key))
81                      found[extension.Key] += extension.Count(); // update count
82                  else
83                  {
84                      found[extension.Key] = extension.Count(); // add count
85                  }
86              }
87  
88
90          // recursive call to search subdirectories
91              foreach (var subdirectory in directories)
92              {
93                  SearchDirectory(subdirectory);
94              }
95      }
96  
97      // allow user to delete backup files (.bak)
98      private void CleanDirectory(string folder)
99      {
100          // find files contained in the directory
101          string[] files = Directory.GetFiles(folder);
102
103          // subdirectories in the directory
104          string[] directories = Directory.GetDirectories(folder);
105      }
```

Fig. 17.14 | Using LINQ to search directories and determine file types (Part 2 of 3.)