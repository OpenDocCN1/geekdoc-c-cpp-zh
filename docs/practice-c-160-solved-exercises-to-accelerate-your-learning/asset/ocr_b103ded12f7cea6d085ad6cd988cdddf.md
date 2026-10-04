```
#include <regex>
#include <string>

int main() {
    std::string input;
    std::cout << "Enter the text: ";
    std::getline(std::cin, input);

    std::regex pattern(R"#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3}))");

    std::smatch matches;
    std::string::const_iterator searchStart(input.begin());
    while (std::regex_search(searchStart, input.end(), matches, pattern)) {
        std::cout << "Found hex color. " << matches[0] << '\\n';
        searchStart = matches.suffix().first;
    }

    return 0;
```