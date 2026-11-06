the input document. Choose a keyword, for example TIGER. Then encode the first letter of the input text like this:

<table>
<tr><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>H</td><td>I</td><td>J</td><td>K</td><td>L</td><td>M</td><td>N</td><td>O</td><td>P</td><td>Q</td><td>R</td><td>S</td><td>T</td><td>U</td><td>V</td><td>W</td><td>X</td><td>Y</td><td>Z</td></tr>
<tr><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td></tr>
<tr><td>T</td><td>U</td><td>V</td><td>W</td><td>X</td><td>Y</td><td>Z</td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>H</td><td>I</td><td>J</td><td>K</td><td>L</td><td>M</td><td>N</td><td>O</td><td>P</td><td>Q</td><td>R</td><td>S</td></tr>
</table>

The encoded alphabet is just the regular alphabet shifted to start at T, the first letter of the keyword TIGER. The second letter is encrypted according to the following map.

<table>
<tr><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>H</td><td>I</td><td>J</td><td>K</td><td>L</td><td>M</td><td>N</td><td>O</td><td>P</td><td>Q</td><td>R</td><td>S</td><td>T</td><td>U</td><td>V</td><td>W</td><td>X</td><td>Y</td><td>Z</td></tr>
<tr><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td><td>↓</td></tr>
<tr><td>I</td><td>J</td><td>K</td><td>L</td><td>M</td><td>N</td><td>O</td><td>P</td><td>Q</td><td>R</td><td>S</td><td>T</td><td>U</td><td>V</td><td>W</td><td>X</td><td>Y</td><td>Z</td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>H</td></tr>
</table>

The third, fourth, and fifth letters in the input text are encrypted using the alphabet sequences beginning with characters G, E, and R, and so on. Because the key is only five letters long, the sixth letter of the input text is encrypted in the same way as the first. Write a program that encrypts or decrypts an input text according to this cipher.

**P8.20** *Playfair cipher.* Another way of thwarting a simple letter frequency analysis of an encrypted text is to encrypt pairs of letters together. A simple scheme to do this is the Playfair cipher. You pick a keyword and remove duplicate letters from it. Then you fill the keyword, and the remaining letters of the alphabet, into a 5 × 5 square. (Since there are only 25 squares, I and J are considered the same letter.)

Here is such an arrangement with the keyword PLAYFAIR.

<table>
<tr><td>P</td><td>L</td><td>A</td><td>Y</td><td>F</td></tr>
<tr><td>I</td><td>R</td><td>B</td><td>C</td><td>D</td></tr>
<tr><td>E</td><td>G</td><td>H</td><td>K</td><td>M</td></tr>
<tr><td>N</td><td>O</td><td>Q</td><td>S</td><td>T</td></tr>
<tr><td>U</td><td>V</td><td>W</td><td>X</td><td>Z</td></tr>
</table>

To encrypt a letter pair, say AM, look at the rectangle with corners A and M:

<table>
<tr><td>P</td><td>L</td><td>A</td><td>Y</td><td>F</td></tr>
<tr><td>I</td><td>R</td><td>B</td><td>C</td><td>D</td></tr>
<tr><td>E</td><td>G</td><td>H</td><td>K</td><td>M</td></tr>
<tr><td>N</td><td>O</td><td>Q</td><td>S</td><td>T</td></tr>
<tr><td>U</td><td>V</td><td>W</td><td>X</td><td>Z</td></tr>
</table>

The encoding of this pair is formed by looking at the other two corners of the rectangle, in this case, FI. If both letters happen to be in the same row or column, such as GO, simply swap the two letters. Decryption is done in the same way. Write a program that encrypts or decrypts an input text according to this cipher.

**P8.21** Write a program that edits an image file and reduces the blue and green values by 30 percent, giving it a "sunset" effect.

![](bbox=[0.427, 0.855, 0.781, 0.918])