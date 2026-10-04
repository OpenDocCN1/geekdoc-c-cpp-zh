```
std::getline(std::cin, sentence);

// Replace every space with newline
for (int i = 0; i < sentence.length(); i++) {
    if (sentence[i] == ' ') {
        sentence[i] = '\n';
    }
}

// Display the modified sentence
std::cout << "Modified sentence:\n" << sentence << std::endl;

    return 0;
}
```

# 110. Write a program that receives a name and checks that it starts with the letter "A".

```
#include <iostream>
#include <string>
```