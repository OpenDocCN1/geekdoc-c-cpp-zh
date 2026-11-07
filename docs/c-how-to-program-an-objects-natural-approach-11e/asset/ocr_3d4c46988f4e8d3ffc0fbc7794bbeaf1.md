```
```cpp
Cipher cipher;

// encrypt plainText using secretKey
std::string cipherText(cipher.encrypt(plainText, secretKey));
std::cout << "\nEncrypted:\n    " << cipherText << "\n";

// decrypt cipherText
std::cout << "\nDecrypted:\n    "
          << cipher.decrypt(cipherText, secretKey) << "\n";
}
```
```

```
```text
Enter the text to encrypt:
Welcome to encryption

Enter the secret key:
XMIJWBVHX

Encrypted:
    Tqhwx nzv bmzdujcjj1

Decrypted:
    Welcome to encryption
```
```

**Fig. 9.36**  Encrypting and decrypting text with a Vigenère cipher. (Part 2 of 2.)

# Class Cipher

Figure 9.37 defines the Cipher class, which we separated into parts for discussion purposes. The first part (lines 1–14) shows the headers our Vigenère implementation requires and the beginning of the class definition.

```
```cpp
// Fig. 9.37: cipher.h
// Vigenère cipher implementation.
#pragma once
#include <algorithm>
#include <array>
#include <iostream>
#include <string>
#include <string_view>
#include <cctype>
#include <stdexcept>
#include <gsl/gsl>

class Cipher {
public:
```
```

**Fig. 9.37**  Vigenère cipher implementation