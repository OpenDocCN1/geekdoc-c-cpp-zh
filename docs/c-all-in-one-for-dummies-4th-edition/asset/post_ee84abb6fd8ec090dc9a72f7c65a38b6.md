
Even if you could somehow use the `ifstream` class to go past the spaces, it wouldn’t know when it has reached the end of the first string because it doesn’t view a period as anything special. You must write your application to follow this protocol: A string ends with a period. That protocol is fine, because ending with a period is the case with these two strings. However, you may need to process just sequences of words, like this:

```text
"poodle steak eat puddle"
"dinner Smiths yummy"
```

And then, when you write these two strings to a file, you end up with this text inside the file:

```text
poodle steak eat puddle dinner Smiths yummy
```

Or worse, you may get this text, which contains no space between the two strings:

```text
poodle steak eat puddledinner Smiths yummy
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_740_0.png)

When working with data that doesn’t form sentences, you may not be limited to strings. You could be processing numbers, vectors, special classes, and so on. So, even though you see words strung together here, you need to think outside the box. Here’s what you need to do to solve the problem of reading complex data in various forms:

- 1. Create a protocol. Here are some choices for your protocols:
  - You can write each string on a separate line, and when you read the file, you will know that each line is a separate string.
  - You can delimit each data element with a particular character. Then you would split your strings based on those delimiters.
- 2. Develop code to implement the same protocol for both reading and writing.

## Writing and reading string-type data

When working with strings that form sentences or that you can separate into groups, your best bet is to work with them as strings separated by newline characters. The WriteReadString example, shown in Listings 3-7 (main.cpp), 3-8 (WriteString.cpp), and 3-9 (ReadString.cpp), writes and reads data (not just sentences) as elements separated by newline characters and read back in the same way. This represents the easiest method for writing complex data to disk.

![](img/128ab511de4e7360e167e3b15cdd5dd0_740_1.png)

### LISTING 3-7: Coordinating the Writing and Reading of Complex Data

```cpp
#include <iostream>

using namespace std;

void ClearFile(string Filename);
int WriteData(string Filename, string Text);
int ReadData(string Filename);

int main() {
    string const file = "../strings.txt";

    ClearFile(file);
    cout << "Data file cleared." << endl;

    int Result = WriteData(file, "Some data to write.");
    Result = WriteData(file, "Some more data to write.");
    Result = WriteData(file, "Third time's a charm.");
    if (Result == 0)
        cout << "Data written successfully!\n" << endl;

    if (ReadData(file) == 0)
        cout << "\nData read successfully!" << endl;

    return 0;
}
```

### LISTING 3-8: Clearing the Data File and Writing Complex Data to It

```cpp
#include <iostream>
#include <fstream>

using namespace std;

void ClearFile(string Filename) {
    ofstream DataFile;
    DataFile.open(Filename, ios_base::trunc);
    DataFile.close();
}

int WriteData(string Filename, string Text) {
    ofstream DataFile(Filename, ios_base::app);
    if (DataFile.is_open()) {
        DataFile << Text << endl;
    } else {
        cerr << "Unable to open file." << endl;
        return -1;
    }

    DataFile.close();
    return 0;
}
```

### LISTING 3-9: Reading the Complex Data

```cpp
#include <iostream>
#include <fstream>
#include <string.h>

using namespace std;

int ReadData(string Filename) {
    ifstream DataFile(Filename);
    if (!DataFile) {
        cerr << "File couldn't be opened!" << endl;
        cerr << "Error Code: " << strerror(errno) << endl;
        return -1;
    }

    string Data = "";
    while (getline(DataFile, Data)) {
        cout << Data << endl;
    }

    DataFile.close();
    return 0;
}
```

Many of the techniques you see in these code listings also appear in the previous examples of this chapter. However, instead of treating the data as separate elements, this example works with strings. This difference in data complexity requires a few changes.

Reading with Input Streams

Because the WriteData() function writes data and closes the file each time, appending the new data to the end of the file (using ios_base::app), you need a method of clearing the data file as needed. The ClearFile() function performs this task by opening the file, truncating it using ios_base::trunc, and closing it without writing anything to it.

The ReadData() function can’t depend on an EOF check as was used in previous examples to determine the end of file. This example uses a while loop that checks the return value from the getline() function. When getline() reaches the EOF, the eof bit is set (meaning that getline() returns false) and the while loop ends. Compare this approach to the do...while loop used in Listing 3-6.

### Writing and reading structured data

Structured data can appear in quite a few forms, but most of these structured forms require use of delimiters. A common type of delimited data file is the Comma Separated Value (CSV). It has a number of protocols to consider, but for the purpose of the example, the data file uses commas between fields and newline characters between rows. The WriteReadStructure example, shown in Listing 3-10, provides you with a simple view of how to work with this type of data.

### LISTING 3-10: Writing and Reading Structured Data

```cpp
#include <iostream>
#include <fstream>
#include <sstream>

using namespace std;

struct Box {
    string Name;
    int Height;
    int Width;
    int Depth;
    double Weight;

    friend ostream& operator << (ostream& Out, Box Data);
};

ostream& operator << (ostream& Out, Box Data) {
    Out << Data.Name << ",";
    Out << Data.Height << ",";
    Out << Data.Width << ",";
    Out << Data.Depth << ",";
    Out << Data.Weight << "\n";
}
```

### LISTING 3-10: (continued)

```cpp
cout << "Height: " << InData.Height << endl;
cout << "Width:  " << InData.Width << endl;
cout << "Depth:  " << InData.Depth << endl;
cout << "Weight: " << InData.Weight << endl;

return 0;
```

This example begins by creating a Box structure that contains a number of data types (making it harder to work with). It then defines an << operator function to allow easy output of the data to a file. You may see other methods of creating output for structured data, but this is the simplest approach in most cases. The main() code begins by opening the file and using the << operator to output the data to it.

Getting the data read back into a new Box structure, InData, is a little more difficult. This example makes use of a stringstream, ISS, to allow for easy conversion from string form to numeric form.

![](img/128ab511de4e7360e167e3b15cdd5dd0_745_0.png)

The magic in the approach used in this example is that it relies on getline() to use a delimited approach to reading the file. Each read stops at either a comma or a newline. Consequently, each read represents a single field within the data file, whether that field is part of a new row or not.

When the field is a Name, you can input the data directly into the InData structure. However, for other fields, the InString input data is actually placed within ISS. Spaces between entries make it possible for ISS to keep each of the data values separate. Field keeps track of the current field number so that the switch processes each field properly.

After the processing is complete (there is only one record, in this case), the code uses another form of streaming to send the numeric values from ISS to each of the InData numeric fields in the correct type. Now that InData contains the original information, the code produces this output:

```text
Name: Sam's Box
Height: 4
Width: 5
Depth: 6
Weight: 7.8
```
