```
int getOpen(ostream& fileOut)
{
    string name;

    cout << "\nEnter a file name: ";
    getline(cin, name);

    fileOut.open(name.c_str());                   // open the file

    if (fileOut.fail())                        // check for successful
    {
        cout << "Cannot open the file" << endl;
        exit(1);
    }
    else
        return 1;
}
```

```
void inOut(ostream& fileOut)
{
    const int NUMPLIES = 5;                    // number of lines
    int count;
    string line;

    cout << "\nPlease enter five lines of text:" << endl;
    for (count = 0; count < NUMPLIES; ++count)
    {
        getline(cin, line);
        fileOut << line << endl;
    }

cout << "\nThe file has been successfully written.";

    return;
}
```

Program 8.9 allows the user to enter a filename from the standard input device and then opens the ofstream connection to the external file. If an existing data file's name is entered, the file is destroyed when it's opened for output. A useful trick for preventing this mishap is to open the entered file using an input file stream. If the file exists, the fail() method indicates a successful open (that is, the open doesn't fail), which indicates the file is available for input. This technique can be used to alert the user that the entered name exists in the system and to request confirmation that the data in the file can be destroyed and the file opened for output. Before the file is reopend for output, the input file stream should be closed. Implementing this trick is left for you to try in Exercise 4.