# 636 Chapter 14 Graphical User Interfaces with Windows Forms: Part I

should allow the user to watch what or she is typing on the screen without looking at the actual keyboard. Use Buttons to represent the keys. As the user presses each key, the app highlights the corresponding Button and adds the character to a TextBox that shows what the user has typed so far. [Hint: To highlight a Button, use its BackColor property to change its background color. When the key is released, reset its original background color.]

You can test your program by typing a pangram—a phrase that contains every letter of the alphabet at least once—such as "The quick brown fox jumped over a lazy dog." You can find other pangrams on the web.

To make the program more interesting you could monitor the user's accuracy. You could have the user type specific phrases that you prestored in your program and you display on the screen above the virtual keyboard. You could keep track of how many keystrokes the user types correctly and how many are typed incorrectly. You could also keep track of which keys the user is having difficulty with and display a report showing those keys.