
```cpp
for (int swaps = 0; swaps < wordLen; swaps++) {
    pos1 = rand() % wordLen;
    pos2 = rand() % wordLen;
    temp = word.at(pos1);
    word.at(pos1) = word.at(pos2);
    word.at(pos2) = temp;
}
cout << word << endl;
return 0;
}
```

## 用名称替换数字字符。

```cpp
#include <iostream>
using namespace std;
int main() {
    string text;
    getline(cin, text);
    unsigned int textLen = text.length();
    string newText = "";
    for (unsigned int pos = 0; pos < textLen; pos++) {
        switch (text.at(pos)) {
            case '1': newText += "one"; break;
            case '2': newText += "two"; break;
            case '3': newText += "three"; break;
            case '4': newText += "four"; break;
            case '5': newText += "five"; break;
            // 等. 直到 9
            default: newText += text.at(pos); break;
        }
    }
    cout << newText << endl;
}
```

## 4. 将单词转换为大写并插入符号。

```cpp
#include <iostream>
#include <cctype>
using namespace std;
int main() {
    string text;
    cin >> text;
    unsigned int textLen = text.length();
    string newText = "";
    for (unsigned int pos = 0; pos < textLen; pos++) {
        newText += toupper(text.at(pos));
    }
    cout << newText << endl;
    return 0;
}
```

# 第 9 章：数组数据

### 1. 验证数组索引。

```cpp
#include <iostream>
using namespace std;
int main() {
    string cityName[3];
    cityName[0] = "London";
    cityName[1] = "Paris";
    cityName[2] = "New York";
    int choice;
    while (true) {
        cout << "Type a number 0, 1 or 2:" << endl;
        cin >> choice;
        if (choice < 0 || choice > 2)
            cout << "That number is not array index" << endl;
        else
            cout << cityName[choice] << endl;
    }
    return 0;
}
```

### 创建 10x10 的随机数字并在屏幕上显示。

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;
int main() {
    srand(time(0));
    int grid[10][10];
    int row, col;
    for (row = 0; row < 10; row++) {
        for (col = 0; col < 10; col++)
            grid[row][col] = random() % 10;
    }
    for (row = 0; row < 10; row++) {
        for (col = 0; col < 10; col++)
            cout << grid[row][col] << '\t';
    }
    cout << endl;
    return 0;
}
```

### 3. 计算并存储斐波那契数列的前 20 项到数组中。

```cpp
#include <iostream>
using namespace std;
int main() {
    int fibonacci[20];
    fibonacci[0] = 1;
    fibonacci[1] = 1;
    int term;
    for (term = 2; term < 20; term++)
        fibonacci[term] = fibonacci[term-1] + fibonacci[term-2];
    for (term = 0; term < 20; term++)
        cout << fibonacci[term] << endl;
    return 0;
}
```

# 第 10 章：函数

### 1. 创建一个名为 displayColourLine 的函数，用指定的颜色显示字符串值。

```cpp
#include <iostream>
using namespace std;
void displayColourLine(string textToDisplay, char colour) {
    switch (colour) {
        case 'r': cout << "\e[31m"; break;
        case 'g': cout << "\e[32m"; break;
        case 'b': cout << "\e[34m"; break;
    }
    cout << textToDisplay << endl;
}
int main() {
    displayColourLine("Fire engine", 'r');
    displayColourLine("Rain forest", 'g');
    return 0;
}
```

### 写一个名为 trim 的函数，用于删除字符串值开头结尾的空格。

```cpp
string trimString( string originalString )
{
    int lengthOriginal = originalString.length();
    string trimmedString;
    int leftPos = 0;
    while ( leftPos < lengthOriginal && originalString.at(leftPos) == ' ') {
        leftPos++;
    }
    if ( leftPos < lengthOriginal) {
        int rightPos = lengthOriginal - 1;
        while ( rightPos > leftPos && originalString.at(rightPos) == ' ') {
            rightPos--;
        }
        trimmedString = originalString.substr(leftPos, 1 + rightPos-leftPos);
    } else {
        trimmedString = "";
    }
    return trimmedString;
}
```

### 3. 创建一个用于整数的函数，并检查用户是否输入了整数整数。

```cpp
#include <iostream>
#include <climits>
using namespace std;
int promptForInteger( string promptMessage )
{
    int typedIn;
    bool validIntSupplied = false;
    while (! validIntSupplied) {
        cout << promptMessage << endl;
        cin >> typedIn;
        if (cin.good()) {
            cout << "Thank you." << endl;
            validIntSupplied = true;
        } else {
            cout << "You did not type in a valid integer." << endl;
            cin.clear();
            cin.ignore(INT_MAX, '\n');
        }
    }
    return typedIn;
}
int main()
{
    promptForInteger("Please type in a whole number.");
    promptForInteger("Now type in another.");
    return 0;
}
```

### 创建一个函数，判断两个字符串值是否为彼此的镜像。

```cpp
bool mirrorStrings( string firstString, string secondString ) {
    int lengthFirstString = firstString.length();
    int lengthSecondString = secondString.length();
    if (lengthFirstString != lengthSecondString)
        return false;
    else {
        bool mirrorImage = true;
        int leftPos = 0;
        int lastPos = lengthSecondString - 1;
        while (leftPos < lengthFirstString) {
            if (firstString.at(leftPos) == secondString.at(lastPos - leftPos) ) {
                mirrorImage = false;
                break;
            }
            leftPos++;
        }
        return mirrorImage;
    }
}
```

# 第 11 章：数据文件

### 1. 读取文件并显示其中包含的空行和非空行的数量摘要。

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main() {
    cout << "Please type in the filename:" << endl;
    string filename;
    cin >> filename;
    ifstream myFile;
    myFile.open(filename.c_str());
    if (myFile.is_open()) {
        string lineOfText;
        int numBlankLines = 0;
        int numNonBlank = 0;
        while (myFile.good()) {
            getline(myFile, lineOfText);
            if (lineOfText.length() == 0)
                numBlankLines++;
            else
                numNonBlank++;
        }
        myFile.close();
    }
    cout << "Lines in file: " << numBlankLines + numNonBlank << endl;
    cout << "Blank lines: " << numBlankLines << endl;
    cout << "Lines that contain text: " << endl << numNonBlank << endl;
    } else {
        cout << "File not found!" << endl;
    }
    return 0;
}
```

### 2. 读取一个文本文件并确定字母表中每个字母出现的多少次。

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main() {
    cout << "Please type in the filename:" << endl;
    string fileName;
    cin >> fileName;
    fstream myFile;
    myFile.open(fileName.c_str());
    if (myFile.is_open()) {
        char charFromFile;
        int alphabetCount[26];
        int alphabetIndex = 0;
        for (int i = 0; i < 26; i++) {
            alphabetCount[i] = 0;
        }
        while (myFile.good()) {
            myFile.get(charFromFile);
            if (isalpha(charFromFile)) {
                alphabetCount[toupper(charFromFile) - 65]++;
            }
        }
        myFile.close();
        alphabetIndex = 0;
        for (alphabetIndex = 0; alphabetIndex < 26; alphabetIndex++) {
            cout << "Letter " << static_cast<char>('A' + alphabetIndex) << " appears " << alphabetCount[alphabetIndex] << endl;
        }
    } else {
        cout << "File not found!" << endl;
    }
    return 0;
}
```

### 3. 使用一系列文件名将数据副本保存到五个不同的文件中。

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main() {
    string startFileName = "data";
    ofstream myNewFile;
    for (int digit = 0; digit < 5; digit++) {
        string fileName = startFileName + to_string(digit);
        myNewFile.open(fileName.c_str());
        if (myNewFile.is_open()) {
            myNewFile << "some data" << endl;
            myNewFile.close();
        }
    }
    return 0;
}
```

### 4. 读取一个文件并确定字母表中每个字母出现的多少次。

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main() {
    cout << "Please type in the filename:" << endl;
    string fileName;
    cin >> fileName;
    fstream myFile;
```
