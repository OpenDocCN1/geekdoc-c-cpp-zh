# Input with cin 1113

The program peeks at the next character. If it is not the # character, the program reads the next character, echoes it, and peeks at the next character. This continues until the terminating character shows up.

Now let's look, promised, at an example—Listing 17.15—that uses peek() to determine whether an entire line has been read. If only part of a line fits in the input array, the program discard the rest of the line.

Listing 17.15 truncate.cpp

```
// truncate.cpp -- using get() to truncate input line, if necessary
#include <iostream>
const int SLEN = 10;
inline void eatline() { while (std::cin.get() != '\n') continue; }
int main() {
	std::cin;
	std::cout;
	std::endl;

	char name[SLEN];
	title[SLEN];
	cout << "Enter your name: ";
	cin.get(name,SLEN);
	if (cin.peek() != '\n')
		cout << "Sorry, we only have enough room for \n"
		<< name << endl;

	eatline();
	cout << "Dear " << name << \
```

Here is a sample run of the program in Listing 17.15:

Enter your name: Ella Fishniffer
Sorry, we only have enough room for Ella Fish
Dear Ella Fish, enter your title:
Executive Adjunct
We were forced to truncate your title.