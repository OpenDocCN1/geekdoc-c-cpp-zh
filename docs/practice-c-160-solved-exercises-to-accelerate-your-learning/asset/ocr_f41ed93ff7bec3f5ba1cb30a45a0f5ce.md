```
std::stringstream compressed;
char currentChar = input[0];
int count = 1;

for (int i = 1; i < input.length(); i++) {
  if (input[i] == currentChar) {
    count++;
  } else {
    compressed << currentChar << count;
    currentChar = input[i];
    count = 1;
  }
}
```

// Append the last character and its count
compressed << currentChar << count;

```
std::string result = compressed.str();
if (result.length() < input.length()) {
  std::cout << "Compressed string: " << result << std::endl;
} else {
```