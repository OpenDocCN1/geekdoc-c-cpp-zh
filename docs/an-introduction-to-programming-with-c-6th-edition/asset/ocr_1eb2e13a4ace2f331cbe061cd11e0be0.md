# CHAPTER 14 Sequential Access Files

(continued)

| Input | Processing | Output |
| --- | --- | --- |
| main function | Processing items: none | none |
| Input menu option | Algorithm:
 repeat
 display menu
 get menu option
 If (menu option is 1)
 call the saveCd function
 else
 if (menu option is 2)
 call the displayCds function
 end if
 end repeat while (menu option is not 3) | |

584

| Input | Processing | Output |
| --- | --- | --- |
| saveCds function | Processing items: none | cds.txt file (sequential access) |
| Input CD name artist name | Algorithm:
 1. open the cds.txt file for append
 2. if (the cds.txt file was opened successfully)
 enter the CD name
 repeat while (the CD name is not "-1")
 enter the artist name
 write the CD name and artist name to the cds.txt file
 get another CD name
 repeat
 close the cds.txt file | |

| Input | Processing | Output |
| --- | --- | --- |
| displayCds function | Processing items: none | CD name artist name |
| Input cds.txt file (sequential access) | Algorithm:
 1. open the cds.txt file for input
 2. if (the cds.txt file was opened successfully)
 read the CD name and artist name from the cds.txt file
 repeat while (it's not the end of the cds.txt filen display the CD name and artist name
 read the CD name and artist name from the cds.txt file
 repeat
 close the cds.txt file
 else
 display the "File could not be opened" message
 end if | |

Figure 14-1 Problem specification and IPO charts for the CD collection program