```
Duplicate code

#include <iostream>
#include <fstream>
#include <string>

int primary() {
    std::ifstream inputFile("input.txt");//Open the document

    if (inputFile.is_open()) {//Check assuming that the record is open
        std::string line;

        while (std::getline(inputFile, line)) {//Read each line from the document
            std::cout << line << std::endl;//Print the line
        }
        inputFile.close();//Close the record
    } else {
```