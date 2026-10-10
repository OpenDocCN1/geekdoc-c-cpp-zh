
```cpp
    std::cin >> n;

    int arr[n];

    std::cout << "Enter " << n << " numbers:" << std::endl;

    for (int i = 0; i < n; i++) {

        std::cin >> arr[i];

    }

    int smallest = findSmallest(arr, n);

    std::cout << "Smallest value: " << smallest << std::endl;

    return 0;

}
```

# 144. 编写一个递归函数来判断单词是否为回文。

```cpp
#include <iostream>
#include <string>
bool isPalindrome(const std::string& word, int start, int end) {
  // 基础情况：如果 start 大于或等于 end，返回 true（该单词是回文）
  if (start >= end) return true;
  // 如果当前索引处的字符不匹配，返回 false
  if (word[start] != word[end]) return false;
  // 移动到下一组字符
  return isPalindrome(word, start + 1, end - 1);
}
int main() {
    std::string word;
    std::cout << "Enter a word: ";
    std::cin >> word;
    if (isPalindrome(word, 0, word.length() - 1)) {
        std::cout << word << " is a palindrome." << std::endl;
    } else {
        std::cout << word << " is not a palindrome." << std::endl;
    }
    return 0;
}
```

# 145. 实现一个递归函数来计算数组的和。

```cpp
#include <iostream>
int sumArray(int arr[], int size) {
    // 基础情况：如果 size 为 0，返回 0
    if (size == 0) return 0;
    // 递归地计算剩余元素的和并加上当前元素
    return arr[size - 1] + sumArray(arr, size - 1);
}
int main() {
  int n;
  std::cout << "Enter the number of elements: ";
  std::cin >> n;
  int *arr = new int[n];
  std::cout << "Enter the elements:" << std::endl;
  for (int i = 0; i < n; i++) {
    std::cin >> arr[i];
  }
  std::cout << "Sum of the array: " << sumArray(arr, n) << std::endl;
  delete[] arr; // 不要忘记释放分配的内存
  return 0;
}
```

# 正则表达式

## 46. 编写一个正则表达式来验证电子邮件地址，确保它包含 @ 和 .

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
    std::string email;
    std::cout << "Enter email: ";
    std::cin >> email;
    // 检查包含 @ 和 .
    std::regex pattern(R"(^[^@]+@[^@]+\.[^@]+$)");
    if (std::regex_match(email, pattern)) {
        std::cout << "Valid email!" << std::endl;
    } else {
        std::cout << "Invalid email!" << std::endl;
    }
    return 0;
}
```

## 47. 从字符串中提取格式为 YYYY-MM-DD 或 DD/MM/YYYY 的所有日期。

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
    std::string input;
    std::cout << "Enter text: ";
    std::getline(std::cin, input);
    // 正则表达式用于匹配两种日期的格式
    std::regex pattern(R"((\d{4}-\d{2}-\d{2})|(\d{2}/\d{2}/\d{4}))");
    std::smatch matches;
    while (std::regex_search(input, matches, pattern)) {
        std::cout << "Found date: " << matches[0] << std::endl;
        input = matches.suffix().str();
    }
    return 0;
}
```

## 48. 检查给定字符串是否为有效的信用卡号（通常为 16 位，有时由 - 或空格隔开）。

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
    std::string input;
    std::cout << "Enter credit card: ";
    std::getline(std::cin, input);
    // 信用卡号格式的正则表达式
    std::regex pattern(R"(\d{4}-\d{4}-\d{4}-\d{4}|\d{4} \d{4} \d{4} \d{4}|\d{16})");
    if (std::regex_match(input, pattern)) {
        std::cout << "Valid credit card!" << std::endl;
    } else {
        std::cout << "Invalid credit card!" << std::endl;
    }
    return 0;
}
```

## 49. 验证密码，确保它们至少包含一个大写字母、一个小写字母、一个数字和一个特殊字符，并且长度至少为 8 位。

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
    std::string input;
    std::cout << "Enter password: ";
    std::getline(std::cin, input);
    // 密码验证的正则表达式
    std::regex pattern(R"((?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[\W_]).{8,})");
    if (std::regex_match(input, pattern)) {
        std::cout << "Valid password!" << std::endl;
    } else {
        std::cout << "Invalid password!" << std::endl;
    }
    return 0;
}
```

## 150. 将文本中的多个空格替换为单格。

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
  std::string input;
  std::cout << "Enter the text: ";
  std::getline(std::cin, input);
  std::regex pattern(R"(\s+)");
  std::string replacement(" ");
  std::string result = std::regex_replace(input, pattern, replacement);
  std::cout << "Processed text: " << result << std::endl;
  return 0;
}
```

```cpp
std::smatch matches;
std::string::const_iterator searchStart(input.cbegin());
while (std::regex_search(searchStart, input.cend(), matches, pattern)) {
    std::cout << "Found currency value: " << matches[0] << '\n';
    searchStart = matches.suffix().first;
}
return 0;
```

# 152. 编写一个正则表达式从文本中提取所有的 URL。

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
    std::string input;
    std::cout << "Enter the text: ";
    std::getline(std::cin, input);
    std::regex pattern(R"(bhttps?://[^\s<>"]+|www\.[^\s<>"]+)");
    std::smatch matches;
    std::string::const_iterator searchStart(input.begin());
    while (std::regex_search(searchStart, input.end(), matches, pattern)) {
        std::cout << "Found URL: " << matches[0] << '\n';
        searchStart = matches.suffix().first;
    }
    return 0;
}
```

# 153. 从文本中提取所有的十六进制颜色代码（例如，#AABBCC 或 #ABC）。

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
    std::string input;
    std::cout << "Enter the text: ";
    std::getline(std::cin, input);
    std::regex pattern(R"(#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3}))");
    std::smatch matches;
    std::string::const_iterator searchStart(input.begin());
    while (std::regex_search(searchStart, input.end(), matches, pattern)) {
        std::cout << "Found hex color. " << matches[0] << '\n';
        searchStart = matches.suffix().first;
    }
    return 0;
}
```

# 154. 从文本中提取所有有效的 IPv4 地址。

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
    std::string input;
    std::cout << "Enter the text: ";
    std::getline(std::cin, input);
    std::regex pattern(R"(\b(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\b)");
    std::smatch matches;
    std::string::const_iterator searchStart(input.cbegin(), input.cend());
    while (std::regex_search(searchStart, input.cend(), matches, pattern)) {
        std::cout << "Found IPv4 address: " << matches[0] << '\n';
        searchStart = matches.suffix().first;
    }
    return 0;
}
```

# 155. 使用捕获组重新排列日期格式（将 YYYY-MM-DD 转换为 DD-MM-YYYY）。

```cpp
#include <iostream>
#include <regex>
#include <string>
int main() {
    std::string input;
    std::cout << "Enter the date in format YYYY-MM-DD:";
    std::getline(std::cin, input);
    std::regex pattern(R"((\d{4})-(\d{2})-(\d{2}))");
    std::string replacement("$3-$2-$1");
    std::string newFormat = std::regex_replace(input, pattern, replacement);
    std::cout << "Reformatted date: " << newFormat << '\n';
    return 0;
}
```

# 排序算法

## 156. 实现冒泡排序算法

```cpp
#include <iostream>
void bubbleSort(int arr[], int n) {
  for (int i = 0; i < n-1; i++) { // 遍历每个元素
    for (int j = 0; j < n-i-1; j++) { // 遍历未排序部分
      if (arr[j] > arr[j+1]) { // 比较相邻元素
        // 交换 arr[j] 和 arr[j+1]
        int temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;
      }
    }
  }
}
int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);
    std::cout << "Original array: \n";
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << "\n";
    bubbleSort(arr, n);
    std::cout << "Sorted array: \n";
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << "\n";
    return 0;
}
```

## 157. 实现选择排序算法

```cpp
#include <iostream>
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        int min_idx = i; // 在未排序数组中寻找最小值
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        // 将找到的元素与第一个元素交换
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}
int main() {
```
