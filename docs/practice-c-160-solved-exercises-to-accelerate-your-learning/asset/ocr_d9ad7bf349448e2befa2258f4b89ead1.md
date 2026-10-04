```
std::string word;
std::cout << "Enter a word: ";
std::cin >> word;
```

```
if (isPalindrome(word, 0, word.length() - 1)) {
    std::cout << word << " is a palindrome." << std::endl;
} else {
    std::cout << word << " is not a palindrome." << std::endl;
}
```

```
return 0;
}
```

# 145. Implement a recursive function to calculate the sum of elements of an array.

```
#include <iostream>
```

```
int sumArray(int arr[], int size) {
    // Base case: if the size is zero, return 0
    if (size == 0) return 0;
```