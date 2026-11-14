Next, the code performs three comparisons of the hash values using the CompareHash method of the Cryptography Manager. It compares the hash of the first string with first string itself, to prove that they are equivalent. Then it compares the hash of the first string with the second string, to provide that they are not equivalent. Finally, it compares the hash of the second string with the third string, which varies only in letter case, to prove that these are also not equivalent.

As in earlier examples, we've removed some of the lines of code that simply write values to the console screen to make it easier to see the code that actually does the work.

```
```vb
' Define the text strings instance to encrypt.
Dim sample1Text As String = "This is some text to hash."
Dim sample2Text As String = "This is some more text to hash."
Dim sample3Text As String = "This is Some More text to hash."

' Create the hash values using the SHA512 Hash Algorithm Provider.
' The overload of the CreateHash method that takes a
' string returns the result as a string.
Dim hashed1Text As String = _
    defaultCrypto.CreateHash("SHA512CryptoServiceProvider", sample1Text)
Dim hashed2Text As String = _
    defaultCrypto.CreateHash("SHA512CryptoServiceProvider", sample2Text)
Dim hashed3Text As String = _
    defaultCrypto.CreateHash("SHA512CryptoServiceProvider", sample3Text)

' Compare the strings with some of the hashed values.
Console.WriteLine("Comparing the string '{0}' with the hash of this string:", _
    sampleText)
Console.WriteLine("- result is {0}" _
    defaultCrypto.CompareHash("SHA512CryptoServiceProvider", _
    sample1Text, hashed1Text))

Console.WriteLine("Comparing the string '{0}' with hash of the string '{1}'", _
    sample1Text, sample2Text)
Console.WriteLine("- result is {0}" _
    defaultCrypto.CompareHash("SHA512CryptoServiceProvider", _
    sample1Text, hashed1Text))

Console.WriteLine("Comparing the string '{0}' with hash of the string '{1}'", _
    sample2Text, sample3Text)
Console.WriteLine("- result is {0}" _
    defaultCrypto.CompareHash("SHA512CryptoServiceProvider", _
    sample3Text, hashed2Text))
```
```