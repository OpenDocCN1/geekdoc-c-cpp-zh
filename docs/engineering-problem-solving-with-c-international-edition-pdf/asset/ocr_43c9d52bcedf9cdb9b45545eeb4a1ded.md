This string can then be used by the open() function as illustrated in the following code segment:

```
...
string filename;
cout << "Enter the name of the output file";
cin >> filename;
balloon.open(filename.c_str());
...
```

![](bbox=[0.15, 0.24, 0.22, 0.3])

We declared filename to be a string object, since these are easy to work with. However, the open() function requires a C-style string as an argument, so filename must call the function c_str(). The function c_str() is a member function of the string class, and it returns a C-style string that is equivalent to the calling object. We will use this combination of statements in all the sample programs that use files in this and the chapters that follow.

# ## 5.2 Reading Data Files

To read information from a data file, we must first know some details about the file. Obviously, we must know the file name so that we can open the file. We must also know the order and data type of the values stored in the file so that we can declare corresponding identifiers correctly. Finally, we need to know if there is any special information in the file to help us determine how much information is in the file. If we attempt to execute an input statement after we have read all the data in the file, the value of the input object will remain unchanged. This may cause unexpected results in our program. To avoid this situation, we need to know when we have read all the data.

Data files generally have one of three common structures. Some files have been generated such that the first line in the file contains the number of lines (also called records) with information that follow. For example, suppose that a file containing sensor data has 150 sets of time and sensor information. The data file could be constructed such that the first line contains only the value 150, and that line would then be followed by 150 lines containing the sensor data. To read the data from this file, we use a counter-controlled loop, as discussed in Chapter 4.

Another form of file structure uses a trailer signal or sentinel signal. These signals are special data values that are used to indicate or signal the last record of a file. For example, the sensor data file constructed with a sentinel signal would contain the 150 lines of information followed by a line with special values, such as –999.0 for the time and sensor value. These sentinel signals must be values that could not appear as regular data in order to avoid confusion. To read data from this type of file, we use a while loop, as discussed in Chapter 4.

The third data file structure does not contain an initial line with the number of valid data records that follow, and it does not contain a trailer or sentinel signal. For this type of data file, we use the value returned by the file stream object to help us determine when we have reached the end of the file. To read data from this type of file, we use end-of-file loop, as discussed in Chapter 4.

We now present programs for reading sensor information and printing a summary report that contains the number of sensor readings, the average value, the maximum value, and the minimum value. Each of the three common file formats discussed will be used in the following programs.