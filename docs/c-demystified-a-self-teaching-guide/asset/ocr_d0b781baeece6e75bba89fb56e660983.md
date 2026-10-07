```
while(!infile.fail())
{
    cout << data << endl;
    getline(infile, data);
    infile.close();
    return 0;
}
```

```
bool writeFile (ostream& file, char* strFile)
{
    file.open(strFile);
    if (file.fail())
        return false;
    else
        return true;
}
```

```
bool readFile (istream& file, char* strFile)
{
    infile.open(strFile);
    if (file.fail())
        return false;
    else
        return true;
}
```

For each function, the file object is passed by reference instead of by value even though neither function changes the contents of the file. The reason is that the internal state of a file object may change with an open operation even if the contents of the file may not change.

Team LiB PREVIOUS NEXT