# 8.6 (Displaying Strings in Uppercase and Lowercase)

Write a program that inputs a line of text into char array s[100]. Display the line in uppercase letters and in lowercase letters.

# 8.7 (Converting Strings to Integers for Calculations)

Write a program that inputs four strings representing integers, converts the strings to integers, sums the values and prints the total of the four values.

# 8.8 (Converting Strings to Floating Point for Calculations)

Write a program that inputs four strings representing floating-point values, converts the strings to double values, sums the values and prints the total of the four values.

# 8.9 (Comparing Strings)

Write a program that uses function strcmp to compare two strings input by the user. The program should state whether the first string is less than, equal to or greater than the second string.

# 8.10 (Comparing Portions of Strings)

Write a program that uses function strncmp to compare two strings input by the user. The program should input the number of characters to be compared, then display whether those characters from the first string are less than, equal to or greater than the second string.

# 8.11 (Random Sentences)

Use random-number generation to create sentences. Your program should use four arrays of pointers to char called article, noun, verb and preposition. Create a sentence by selecting a word at random from each array in the following order: article, noun, verb, preposition, article and noun. The arrays should be filled as follows: The article array should contain the articles "the", "a", "one", "some" and "any"; the noun array should contain the nouns "boy", "girl", "dog", "town" and "car"; the verb array should contain the verbs "drove", "jumped", "ran", "walked" and "skipped"; the preposition array should contain the prepositions "to", "from", "on", "under" and "over". As each word is picked, concatenate it to the previous words in an array large enough to hold the entire sentence. Separate the words by spaces. The final sentence should start with a capital letter and end with a period. Generate 20 such sentences. Modify your program to produce a short story consisting of several of these sentences. (How about the possibility of a random term-paper writer?)

# 8.12 (Limericks)

A limerick is a humorous five-line verse in which the first and second lines rhyme with the fifth, and the third line rhymes with the fourth. Using techniques similar to those developed in Exercise 8.11, write a program that produces random limericks. Polishing this program to produce good limericks is a challenging problem, but the result will be worth the effort!

# 8.13 (Pig Latin)

Write a program that encodes English-language phrases into pig Latin. Pig Latin is a form of coded language often used for amusement. Many variations exist in the methods used to form pig-Latin phrases. For simplicity, use the following algorithm:

To form a pig-Latin phrase from an English-language phrase, tokenize the phrase into words with function strtok. To translate each English word into a pig-Latin