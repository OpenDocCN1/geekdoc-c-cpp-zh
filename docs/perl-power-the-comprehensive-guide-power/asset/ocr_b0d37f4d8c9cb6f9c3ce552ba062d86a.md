representative identifiers (`$DinoName`, `$FamilyName`, and `$Period`). You then employ these three identifiers as arguments to the `print()` function. As the first argument to the `print()` function, you provide a newline character. As explained previously, this is used as a cosmetic element.

The form the `print()` function assumes involves the file handle identifier (`FILE`) as its first argument. You follow this with the record field specification as given by the `pack()` function. (In this case, you do not use the `length()` function because you are not seeking to output an integer but only to create the record specification.) You use the same field values you used before to create the display value that follows the data table. After the `for` loop traverses the four records, it terminates. You then call the `close()` function to close the file stream. Then, to view the results of your work, you employ the `system()` function to invoke Notepad and display the contents of the file you have created. Figure 14.13 shows you the results.

![](bbox=[0.131, 0.405, 0.643, 0.589])

**Figure 14.12**  
You display the data before you write it and indicate the length of the record you intend to create.

Listing14_08 automatically uses a call to the `system()` function to open Notepad so you can view the file you have created, as Figure 14.13 shows. To exit Notepad, select File > Exit. This leaves the command window for Listing14_08 still open. Press Return to exit.

![](bbox=[0.167, 0.7, 0.609, 0.813])

**Figure 14.13**  
The program writes records to the data file in fixed field lengths.