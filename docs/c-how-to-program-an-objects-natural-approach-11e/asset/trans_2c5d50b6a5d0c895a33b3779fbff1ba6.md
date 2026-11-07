
- 对于 `plaintext` 中的每个字符，第 52–89 行要么加密该字母并将其添加到 `ciphertext`，要么在该字符不是字母时直接将其传递到 `ciphertext`。
- 第 55 行判断原字符是否为小写，以便在生成密文时保持该大小写。
- 第 59–60 行将当前字符转换为大写。如果它已经是大写或不是字母，`std::toupper` 会返回原字符。函数 `std::toupper` 的结果是字符的 `int` 表示，因此我们将其转换为 `const char` 并放入 `currentChar`。
- 如果 `currentChar` 是字母（第 64 行），则第 68–84 行对其进行加密。
- 第 68 行将密钥中 `keyIndex` 处的字母转换为大写，然后减去 `'A'`，生成 0–26 的值，表示要选择的维吉尼亚方阵行。
- 第 72 行将 `keyIndex` 递增到密钥中的下一个位置；如果已到达密钥末尾，则将其重置为 0。
- 第 76 行通过从 `currentChar` 中减去 `'A'` 来计算列索引，生成 0–26 的值，表示要选择的维吉尼亚方阵列。
- 第 79 行对 `currentChar` 执行维吉尼亚密码加密算法，并将其对应的密文存入 `substituteChar`。
- 第 83–84 行随后使用 `currentChar` 的原始大小写将 `substituteChar` 追加到 `ciphertext`。
- 如果 `currentChar` 不是字母，第 87 行直接将其追加到 `ciphertext`。

## 使用维吉尼亚密码解密

解密过程将密文还原为原始明文。它与我们上面描述的过程类似，并且需要使用与加密文本时相同的密钥。与加密算法一样，解密算法也会循环使用密钥中的字母。因此，我们同样重复密钥，直到其长度与密文匹配：

| **密文：** | T | q | h | w | x | n | z | r | v | b | m | z | d | u | j | c | j | l |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **重复密钥文本：** | X | M | W | U | J | B | V | Y | H | X | Z | X | M | W | U | J | B | V |

我们开始解密时，使用重复密钥文本中的第一个字母（`'X'`）在维吉尼亚方阵中选择一行。接下来，在该行中找到密文中的第一个字母（`'T'`）。最后，用该列顶部的明文字母（`'W'`）替换密文字母，如下面的维吉尼亚方阵中高亮所示：

|   | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| A | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z |
| B | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A |
| C | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B |
| D | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C |
| E | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D |
| F | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E |
| G | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F |
| H | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G |
| I | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H |
| J | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I |
| K | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J |
| L | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K |
| M | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L |
| N | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M |
| O | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N |
| P | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O |
| Q | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P |
| R | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q |
| S | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R |
| T | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S |
| U | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T |
| V | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U |
| W | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V |
| X | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W |
| Y | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X |
| Z | Z | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y |

对密钥和密文中的每一对字母重复此过程：

| **密文：** | T | q | h | w | x | n | z | r | v | b | m | z | d | u | j | c | j | l |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **重复密钥文本：** | X | M | W | U | J | B | V | Y | H | X | Z | X | M | W | U | J | B | V |  |
| **明文：** | W | e | l | c | o | m | e | t | o | e | n | c | r | y | p | t | i | o | n |

### 成员函数 decrypt

函数 decrypt（第 96–150 行）接收要解密的密文和密钥，并返回包含原始明文的字符串：

```cpp
// decrypt receives the ciphertext and secret key, reverses
// Vigenère cipher process and returns the unencrypted plaintext
std::string decrypt(
    std::string_view ciphertext, std::string_view secret) {

    checkKey(secret); // ensure secret key contains only letters

    std::string plaintext{}; // stores unencrypted text
    size_t keyIndex{0}; // current letter index in secret key

    for (size_t i{}; i < ciphertext.size(); ++i) {
        // determine whether character at i is lowercase so we can
        // place a corresponding lowercase letter in plaintext
        const bool lower{std::islower(ciphertext.at(i)) ? true : false};

        // convert currentChar to uppercase; for uppercase
        // letters and non-letters the character remains the same
        const char currentChar{gsl::narrow_cast<const char>(
            std::toupper(ciphertext.at(i)))};

        // if current is a letter decrypt it
        if ('A' <= currentChar && currentChar <= 'Z') {
            // to get the row index in the Vigenere square, select the
            // character at keyIndex in the secret key, convert it to
            // uppercase and subtract 'A' from it
            const int row{std::toupper(secret.at(keyIndex)) - 'A'};

            // increment the keyIndex, ensuring that it is
            // reset to 0 if keyIndex reaches secret.size()
            keyIndex = (keyIndex + 1) % secret.size();

            // column in the Vigenère square
            int column{};

            // find currentChar's column in Vigenère square's current row
            for (int i{}; i < m_square.at(row).size(); ++i) {
                if (m_square.at(row).at(i) == currentChar) {
                    column = i;
                    break;
                }
            }

            // determine original character
            const char originalChar{
                gsl::narrow_cast<const char>('A' + column)};

            // add originalChar to plaintext in the correct case
            plaintext +=
                (lower ? std::tolower(originalChar) : originalChar);
        }
        else {
            plaintext += currentChar; // add non-letter to plaintext
        }
    }

    return plaintext; // return the unencrypted text
}
```

