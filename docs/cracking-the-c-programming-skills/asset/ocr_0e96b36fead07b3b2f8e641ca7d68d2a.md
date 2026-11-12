25. Find the output of the following piece of code. (L3)

```
OutFileStreamObj.
open("FewLines.txt");
OutFileStreamObj.
write("C++Programming", 15);
FilePointerCurrentPosition =
OutFileStreamObj.tellp();
OutFileStreamObj.seekp(FilePointerCurrentPosition -15);
OutFileStreamObj.write("c",
1);
```

+   - (a) C Programming
+   - (b) C+C Programming
+   - (c) Programming C
+   - (d) None of the above

Answer: (a) we are writing the words “C++ Programming” to the file, after writing, the file pointer would be in the EOF position. We are then moving the pointer to the beginning of the file and replace C++ by C.

26. Say true or false. C++ supports reading a video file. (L1)

+   - (a) True
+   - (b) False

Answer: (a) True. Note: we can include opencv header file for achieving this.

27. Which of the following I/O modes fails when we try to open a file which is not existing? (L1)

+   - (a) ios::nocreate
+   - (b) ios::noreplace
+   - (c) ios::ate
+   - (d) ios::app

Answer: (b) ios::noreplace checks for the existence of the file. If it doesn't exist, then the call to open fails.

28. Identify the piece of code used to get number of lines in a file. (L4)

```
(a) while(!fileInputStreamObj.eof())
{
    fileInputStreamObj>>strWord;
    count++;
}
Cout<<count;
```

```
(b) while(!fileInputStreamObj.eof())
{
    fileInputStreamObj.getline(strWord,255);
    count++;
}
Cout<<count;
```

```
(c) while(!fileInputStreamObj.eof())
{
    fileInputStreamObj.get(charVariable);
    count++;
}
Cout<<count;
```

+   - (d) None of the above

Answer: (b) getLine() function reads line by line. After we call getLine(), we are incrementing the count.

29. Which of the following flags are used to calculate the offset from the current file pointer position. (L1)

+   - (a) ios::ate
+   - (b) ios::beg
+   - (c) ios::app
+   - (d) ios::cur

Answer: (d) ios::cur

30. Identify the output of the following program. (L2)
Assume the file "InputFile.txt" has the following text: “Learning C++ Programming on 4th may 2016”

```
int digitCount=0;
ifstream ifStreamObject("InputFile.txt",ios::in);
while(!ifStreamObject.eof())
{
    if(isdigit(ifStreamObject.get(charVariable)))digitCount++;
}
Cout<<digitCount;
```

+   - (a) 40
+   - (b) 5
+   - (c) 7
+   - (d) 6

Answer: (b) 5. The above piece of code checks the number of digits in the file InputFile. txt. in the file, there are 5 digits - 4, 2, 0, 1, 6