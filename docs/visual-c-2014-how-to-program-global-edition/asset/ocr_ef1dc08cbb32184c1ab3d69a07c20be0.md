# 17.6 Serialization

e) Displaying accounts with zero balances

![](bbox=[0.375, 0.127, 0.843, 0.272])

**Fig. 17.7** Credit-inquiry program. (Part 5 of 5.)

When the user clicks the Open File button, the program calls the event handler openButton_Click (lines 23–60). Line 29 creates an OpenFileDialog, and line 31 calls its ShowDialog method to display the Open dialog, in which the user selects the file to open. Lines 47–48 create a FileStream with read-only access and assign it to reference. Line 51 creates a StreamReader that we use to read text from the FileStream.

When the user clicks Credit Balances, Debit Balances or Zero Balances, the program invokes getBalances_Click (lines 64–116). Line 67 sends the parameter, which is an object reference to the control that generated it, a Button object. Line 170 extracts the button's text, which the program uses to determine which type of accounts to display. Line 76 uses FileStream method Seek to reset the file-pointer back to the beginning of the file. FileStream method Seek allows you to reset the file-pointer by choosing the number of bytes to be offset from the file’s beginning, or current position. The value offset is chosen using constants from SeekOrigin enumeration. Our stream is out 0 bytes from the file’s beginning SeekOrigin.Begin. Line 102 uses method ShouldDisplay1 (lines 119–135) to determine whether each record in the file, the while loop obtains each record by repeatedly calling StreamReader ReadLine (line 85) and splitting it into tokens (line 94) that are used to initialize record object (lines 97–99). Line 88 determines whether the file-pointer has reached the end of the file, in which ReadLine returns null. If so, the program returns from method getBalances_Click (line 90).

# 17.6 Serialization

Section 17.3 demonstrated how to write the individual fields of a Record object to a text file, and Section 17.4 demonstrated how to read fields from a file and place their values in a Record object in memory. In the examples Record was used to aggregate the information for one record. When the instance variables for Record were output to a disk file as text, certain information was lost, such as the type of each value. For instance, if the value "3" is read from a text file, there’s no way to tell if the value was an int, a string or a decimal. We have only data, not type information, on disk. If the program