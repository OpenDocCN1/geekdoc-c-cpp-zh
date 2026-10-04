```
std::cout << "Enter the text: ";
std::getline(std::cin, input);
std::regex pattern(R("bhttps?://[^\s<>"]+|www\.[^\s<>"]+"));

std::smatch matches;
std::string::const_iterator searchStart(input.begin());
while (std::regex_search(searchStart, input.end(), matches, pattern)) {\std::cout << "Found URL: " << matches[0] << '\n';
searchStart = matches.suffix().first;
}
return 0;
```

# 153. Extract all hex color codes from a text (e.g., #AABBCC or #ABC).

#include <iostream>