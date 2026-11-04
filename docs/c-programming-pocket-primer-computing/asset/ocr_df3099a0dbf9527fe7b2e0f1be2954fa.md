loop checks if the current character has already detected; if so, the position of that character in the counts array is incremented. If not, then the current character is appended to the chars array and its corresponding value in the counts array is set to 1.

The final block of code in Listing 6.20 iterates through the chars array and prints each element, along with its count (which is stored in the counts array). The output from compiling and launching the code in Listing 6.20 is here:

Full string: This is a string with some short words that wraps around and let's see how well the code in this code sample actually works!

```
```
char T count 1 at array position: 0
char h count 7 at array position: 1
char i count 6 at array position: 2
char s count 12 at array position: 3
char   count 23 at array position: 4
char a count 8 at array position: 5
char t count 9 at array position: 6
char r count 6 at array position: 7
char n count 4 at array position: 8
char g count 1 at array position: 9
char w count 6 at array position: 10
char o count 8 at array position: 11
char m count 2 at array position: 12
char e count 9 at array position: 13
char d count 5 at array position: 14
char p count 2 at array position: 15
char u count 2 at array position: 16
char l count 6 at array position: 17
char ' count 1 at array position: 18
char c count 3 at array position: 19
char y count 1 at array position: 20
char k count 1 at array position: 21
char ! count 1 at array position: 22
```
```