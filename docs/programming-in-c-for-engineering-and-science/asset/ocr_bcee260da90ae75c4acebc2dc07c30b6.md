where m is the average score and σ is the standard deviation (see Problem 1). Suppose that a file contains, on each line, a student’s last name and exam store. Write a program to read this information, calculate the average and standard deviation of the scores, and produce another file containing each student’s name, exam score, and the letter grade corresponding to that score.

3. Information about computer terminals in a computer network is maintained in a file. The terminals are numbered 1 through 100, and information about the nth terminal is stored in the nth line of the file. This information consists of a terminal type (string), the building in which it is located (string), the transmission rate (integer), an access code (character), and the date of last service (month, day, year) with each of these items separated by one or more spaces. Write a program to read terminal numbers from the keyboard and directly access the line in the file for each terminal by moving the read position directly to that line. The program should retrieve and display the information about that terminal.

# DESCRIPTIONS OF DATA FILES

The following describe the contents of data files used in exercises in the text. Listings of them are available on the book’s website given in the Preface.

Inventory.txt: Each line contains the following items, separated by one or more spaces:

Item number: an integer

Number currently in stock: an integer (in the range 0 through 999)

Unit price: a real value

Minimum inventory level: an integer (in the range 0 through 999)

Item name: a character string

These items are sorted so that item numbers are in increasing order.

InventoryUpdate.txt: Each line contains the following items, separated by one or more spaces:

An order number: string (three letters followed by four digits)

Item number: same as those in Inventory.txt

Transaction code: a single character (S = sold, R = returned)

Number of items sold or returned: an integer

File is sorted so that item numbers are in increasing order. Some items in Inventory.txt may not have update records; others may have more than one.