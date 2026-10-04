```
std::cout << "Enter a sentence: ";
std::getline(std::cin, sentence);

// Loop through each character and count
spaces
for (char c : sentence) {
    if (c == ' ') {
        count++;
    }
}

std::cout << "Number of blank spaces: " << count <<n std::endl;

return 0;
}
```

# 115. Create a program that reads a word and displays the number of vowels present in it.

```
#include <iostream>
#include <string>
```