```
```cpp
// Output "word (count)", where word has a dynamic field width
std::cout << std::format("{:>{}}", word, field_width, count);
previous_initial = word[0];
}
std::cout << std::endl;
}
```
```

The fact that we used a map<> automatically ensures that all words are sorted in alphabetical order, making it easy for us to print them out alphabetically as well. In particular, showWordCounts() groups words that begin with the same letter on the same line. Beyond this, showWordCounts() does not really contain much you haven’t seen several times before in similar output functions. So, we believe we can skip any further explanations and fast-forward to seeing it all working in a complete example:

```
```cpp
// Ex20_05.cpp - Working with maps
import <iostream>;
import <format>;
import <map>;
import <string>;
import <string_view>;
import <vector>;

// Type aliases
using Words = std::vector<std::string_view>;
using WordCounts = std::map<std::string_view, size_t>;

// Function prototypes
Words extractWords(std::string_view text, std::string_view separators = " ,.!?\"\\n");
WordCounts countWords(const Words& words);
void showWordCounts(const WordCounts& wordCounts);
size_t maxWordLength(const WordCounts& wordCounts);

int main()
{
    std::string text;    // The string to count words in

    // Read a string from the keyboard
    std::cout << "Enter a string terminated by *:" << std::endl;
    getline(std::cin, text, '*');

    Words words = extractWords(text);
    if (words.empty())
    {
        std::cout << "No words in text." << std::endl;
        return 0;
    }

    WordCounts wordCounts = countWords(words);
    showWordCounts(wordCounts);
}

// The implementations of the extractWords(), countWords(), showWordCounts(),
// and maxWordLength() functions as discussed earlier.
```
```