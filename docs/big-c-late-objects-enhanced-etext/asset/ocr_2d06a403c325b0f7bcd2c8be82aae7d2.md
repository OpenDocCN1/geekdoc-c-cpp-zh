Write a program that reads an input file and displays the letter frequencies in that file. Such a tool will help a code breaker. If the most frequent letters in an encrypted file are H and K, then there is an excellent chance that they are the encryptions of E and T. Show the result in a table such as the one above, and make sure the columns line up.

# P8.9 Vigenère cipher.

In order to defeat a simple letter frequency analysis, the Vigenère cipher encodes a letter into one of several cipher letters, depending on its position in the input document. Choose a keyword, for example TIGER. Then encode the first letter of the input text like this:

![](bbox=[0.28, 0.38, 0.9, 0.48])

The encoded alphabet is just the regular alphabet shifted to start at T, the first letter of the keyword TIGER. The second letter is encrypted according to the following map.

![](bbox=[0.28, 0.58, 0.9, 0.68])

The third, fourth, and fifth letters in the input text are encrypted using the alphabet sequences beginning with characters G, E, and R, and so on. Because the key is only five letters long, the sixth letter of the input text is encrypted in the same way as the first.

Write a program that encrypts or decrypts an input text according to this cipher.

# P8.10 Playfair cipher.

Another way of thwarting a simple letter frequency analysis of an encrypted text is to encrypt pairs of letters together. A simple scheme to do this is the Playfair cipher. You pick a keyword and remove duplicate letters from it. Then you fill the keyword, and the remaining letters of the alphabet, into a 5 × 5 square. (Since there are only 25 squares, I and J are considered the same letter.) Here is such an arrangement with the keyword PLAYFAIR.

![](bbox=[0.45, 0.7, 0.75, 0.85])

To encrypt a letter pair, say AM, look at the rectangle with corners A and M:

![](bbox=[0.45, 0.93, 0.75, 0.0010500000000000002])

The encoding of this pair is formed by looking at the other two corners of the rectangle, in this case, FH. If both letters happen to be in the same row or column, such as 60, simply swap the two letters. Decryption is done in the same way.

Write a program that encrypts or decrypts an input text according to this cipher.