```
fsObj.open("demoFile.txt",ios ::in);
fsObj.get(charValue);
while(fsObj.eof( )==0)
{
fsObj.get(ch); count ++;
}
Cout<<count;
```

(d) None

**Answer**: (b)

**18.** Identify the line where we have a bug in the program meant to reverse the content of file and print it on console. (L2)

```
1. x=1;
2. file.seekg(0,ios : :end)
3. count = file.tellg();
4. while(x<=count)
5. {
6. file.seekg(x,ios : :end);
7. file.get(ch);
8. cout.put(ch);
9. x++;
10. }
```

+   (a) No error
+   (b) Seekg should have a negative value in the first parameter on line 6
+   (c) x<=count on the line 4; it should have been x>=count
+   (d) x-- should have been there on line 9 instead of x++

**Answer**: (a) The pointer is at the end and we cannot move it in the forward direction.

**19.** Choose the proper of using clear (iostate state=value) function of the file stream. (L1)

+   (a) De-allocates the memory occupied by the stream object
+   (b) Clears the content of the file
+   (c) Overwrites the current value of the error state flags with the value provided
+   (d) There is no clear() function associated with the file stream

**Answer**: (c) If the state value is 0, then it means there is no error.

**20.** Say true or false. Can we use a file stream to connect to more than a file at a time? (L1)
(a) True (b) False
**Answer**: True

**21.** Which file will be set when we execute the following piece of code? (L2)

```
std::fstream fsObj;
fsObj.open ("filednam.txt",std::fstream::in);
fsObj<< "test";
```

(a) Good bit (b) Bad bit
(c) Fail bit (d) EOF bit

**Answer**: (c) Fail bit, since we have opened the file for reading and we are performing write to the file.

**22.** Function to read the current error state. (L1)
(a) readstate() (b) getstate()
(c) rdstate() (d) None
**Answer**: (c) rdstate()

**23.** What does the following iostate value denote : 0010? (L3)
(a) Fail bit is set (b) EOF bit is set
(c) Good bit is set (d) Bad bit is set

**Answer**: (a) From left the bits are identified as follows. Good bit ➔bad bit➔fail bit ➔ EOF bit. When bad bit, fail bit is not set, good bit will be set. So 1000 indicates that there is no error in the file processing.

**24.** What is the following rdstate indicates: 8? (L1)
(a) Good bit is set (b) Bad bit is set
(c) EOF bit is set (d) None of the above

**Answer**: (a) Good bit is set. Binary equivalent of 8 is 1000 and it denotes that good bit is set.