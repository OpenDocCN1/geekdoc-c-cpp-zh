# CHAPTER 13 Strings

+   9. If the word variable contains the string "Bells", which of the following statements will change the contents of the variable to "Bell"?

+   a. word.erase(word.length() - 1, 1);

+   b. word.replace(word.length() - 1, 1, "");

+   c. word = word.substr(0, word.length() - 1);

+   d. all of the above

+   10. Which of the following statements changes the contents of the word variable from "men" to "mean",

+   a. word.addTo(2, "a");

+   b. word.insert(2, "a");

+   c. word.insert(3, "a");

+   d. none of the above

+   11. If the msg variable contains the string "Happy holidays", what will the cout << msg.find("day", 0); statement display on the screen?

+   a. -1

+   b. 0

+   c. 10

+   d. 11

+   12. If the msg variable contains the string "Happy holidays", what will the location = msg.find("Day", 0); statement assign to the location variable?

+   a. -1

+   b. 0

+   c. 10

+   d. 11

+   13. Which of the following assigns the location of the comma in the amount variable to an int variable named loc?

+   a. loc = amount.contains(",");

+   b. loc = amount.substr(",");

+   c. loc = amount.find(",", 0);

+   d. none of the above

+   14. Which of the following statements searches for the string "CA" in a string variable named state and assigns the result to an int variable named result? The search should begin with the character located in subscript 5 in the state variable. The state variable's contents are uppercase.