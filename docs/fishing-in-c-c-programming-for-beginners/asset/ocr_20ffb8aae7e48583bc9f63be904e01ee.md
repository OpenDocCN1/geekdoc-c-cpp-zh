```
while(!fin.eof())
{
    ch=fin.get();
    fout<<ch;
    cout<<<(count++*100)/file_length<<"% completed"<'\r';
}
cout<<"File copied";
fout.close();
fin.close();
}
```

Output

Enter the file name to copy from
example.txt
Enter the file name to copy to
b.txt
100% completed
File copied

In the above program, we take the file name as input from user. To obtain the length of the file at first we placed the handle to the end of file using the code snippet
fin.seekg(0,ios::end); then we stored the offset of the last character using the code snippet
int file_length=fin.tellg();. At last we returned the handle to the beginning of file using snippet fin.seekg(0,ios::beg);

# Binary files

Using the methods written above, we can read and write most of the files like text files, dat files and most of other but not all. When we were learning formfeed there we saw that we can write in a doc or doc file. Can we also read them?

Consider the following program: