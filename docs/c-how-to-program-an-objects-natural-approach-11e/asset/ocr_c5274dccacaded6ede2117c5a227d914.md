The function operates as follows:

+   - Line 99 calls utility function `checkKey` (defined lines 160–170) to ensure that the secret key contains only letters.
+   - Line 101 defines the string `plaintext`, which will store the unencrypted text.
+   - Line 102 defines the `size_t keyIndex`, which will keep track of the current character in the secret key. That character is used to select a Vigenère square row.
+   - For each character in `plaintext`, lines 104–147 either decrypt the letter and add it to `plaintext` or, if the character is not a letter, simply add it to `plaintext`.
+   - Line 107 determines whether the original character was lowercase, so we can maintain that case as we create the plaintext.
+   - Lines 111–112 convert the current character to uppercase. If it is already uppercase or is not a letter, `std::toupper` returns the original character. We convert `std::toupper`’s result (an `int`) to a `char` and place it in `currentChar`.
+   - If `currentChar` is a letter (line 115), then lines 119–142 decrypt it.
+   - Line 119 converts the secret’s letter at `keyIndex` to uppercase, then subtracts 'A' to produce a value from 0–26 representing the Vigenère square row to select.
+   - Line 123 increments the `keyIndex` to the next position in secret, setting it back to 0 if we’ve reached the end of secret.
+   - Lines 126–138 perform the Vigenère cipher decryption algorithm for one character. We determine the Vigenère square column index by iterating through the current row to locate the index (i) of the character that matches `currentChar`. Then, lines 137–138 add that column to 'A' to determine `originalChar`.
+   - Lines 141–142 then append `originalChar` to `plaintext` using `currentChar`’s original case.
+   - If `currentChar` was not a letter, line 145 simply appends it to `plaintext`.

# private Data and Utility Function checkKey

Line 153 defines the static constant `m_size`, representing the number of rows and columns in the Vigenère square. Line 156 defines the two-dimensional array of chars `m_square`, which the constructor (lines 16–39) populates with the Vigenère square. The static utility function `checkKey` (lines 160–170) receives a secret-key string and ensures that it contains only letters; otherwise, the function throws an `invalid_argument` exception because the key cannot be used with our Vigenère cipher implementation.