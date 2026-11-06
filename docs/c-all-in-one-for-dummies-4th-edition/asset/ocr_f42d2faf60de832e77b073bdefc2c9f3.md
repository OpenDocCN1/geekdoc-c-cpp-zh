# **LISTING 3-10: (continued)**

```
cout << "Height: " << InData.Height << endl;
cout << "Width:  " << InData.Width << endl;
cout << "Depth:  " << InData.Depth << endl;
cout << "Weight: " << InData.Weight << endl;

return 0;
```

This example begins by creating a Box structure that contains a number of data types (making it harder to work with). It then defines an << operator function to allow easy output of the data to a file. You may see other methods of creating output for structured data, but this is the simplest approach in most cases. The main() code begins by opening the file and using the << operator to output the data to it.

Getting the data read back into a new Box structure, InData, is a little more difficult. This example makes use of a stringstream, ISS, to allow for easy conversion from string form to numeric form.

![](bbox=[0.164, 0.474, 0.226, 0.543])

The magic in the approach used in this example is that it relies on getline() to use a delimited approach to reading the file. Each read stops at either a comma or a newline. Consequently, each read represents a single field within the data file, whether that field is part of a new row or not.

When the field is a Name, you can input the data directly into the InData structure. However, for other fields, the InString input data is actually placed within ISS. Spaces between entries make it possible for ISS to keep each of the data values separate. Field keeps track of the current field number so that the switch processes each field properly.

After the processing is complete (there is only one record, in this case), the code uses another form of streaming to send the numeric values from ISS to each of the InData numeric fields in the correct type. Now that InData contains the original information, the code produces this output:

```
Name: Sam's Box
Height: 4
Width: 5
Depth: 6
Weight: 7.8
```