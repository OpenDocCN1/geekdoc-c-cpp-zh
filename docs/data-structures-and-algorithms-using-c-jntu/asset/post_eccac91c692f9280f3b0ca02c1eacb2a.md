
## Pattern Matching and Tries

Pattern matching and Tries are introduced along with terminology. The chapter discusses about Brute Force Algorithm, Boyer–Moore Algorithm and Knuth–Morris–Pratt Algorithm in detail along with examples and their applications. Categories of Tries namely standard tries, compressed tries and suffix tries and operations on them are explained clearly with applications.

### 15.1 INTRODUCTION

In the day-to-day life of a computer user string matching has greater importance. During text editing, the user processes the text, organizes the text into sections and paragraphs and reorganizes the text very frequently. The text is searched to find a substring or pattern and replace it with some other text. Efficiency of the search algorithm is very important when searching for larger text unlike in the case of a dictionary. The algorithm does not depend only on the alphabetical order of words. For instance, in molecular biology the importance of string searching algorithms is increasing day-by-day. Its usage is in locating some pattern in the string, comparing the sequences with usual subsequences and extracting information from DNA. With the assumption that a perfect match cannot be expected, some sort of processing should be done very often. Stringology handles this type of problems and its major area of interest is pattern matching.

A tree-based data structure that supports keys with varying sizes is known as a Trie. In search operation tries uses some parts of the key. Trie belongs to the category of multi-way trees.

### 15.2 TERMINOLOGY

A pattern is a set of elements or recurring events. Elements can be a template or model which can be used to generate things or parts of a thing. A pattern is a uniquely identifiable event.

A word in the given text document is a pattern, and the pattern (word) is framed by means of putting alphabets in an order.

A sentence can be called as a pattern, and the pattern (sentence) is framed by means of putting words in an order.

An image of a human face from a photo can be called as a pattern, and the pattern (face of a human) is framed by means of putting pixels in an order.

So, the pattern is an ordered set of events like alphabets, words, pixels, etc. in the natural world.

**Pattern matching:** Pattern matching is a problem of checking for the presence of the given pattern in the given set of paragraphs. Suppose, to search for a pattern (word ‘the’) in the given document by looking at all the words in the document. It can be concluded that the pattern ‘the’ is present in the document or not. To state that the pattern ‘the’ is found or not, the words which starts with an alphabet ‘t’ followed with ‘h’ and followed with ‘e’ must be observed. If such a structure is found in the document, then it can be said that the pattern ‘the’ exists in the document.

**Pattern recognition:** Pattern recognition is the detected pattern over the set of paragraphs. If the pattern which is being searched for is found in the given document, then the pattern is recognized or else pattern is not recognized. If a human photo is given and asked to locate ‘head’ of the human from the photo, as the pattern ‘head’ is known and how the head will be, it is possible to locate that shape from the photo. If head is found in the photo, then the pattern head is recognized from the photo else the pattern is not recognized from the photo.

### 15.3 PATTERN MATCHING ALGORITHMS

Pattern matching algorithms are the procedures for matching or finding the given pattern on a set of patterns. Pattern matching algorithms are of two types:

- Fixed pattern matching algorithms
- Regular expression pattern matching algorithms

### 15.3.1 Fixed Pattern Matching Algorithms

If the given pattern for searching is constant until the search is complete, then the given search pattern is called a fixed pattern, and the algorithms used for pattern matching are called fixed pattern matching algorithms.

Example: Search for the number “21” over the set of patterns (12, 21, 23, 45, 56, 546, 58). The pattern that is to be searched is 21 and is fixed.

### 15.3.2 Regular Expression Pattern Matching

Consider a problem of searching for the number which starts with the digit “1” or “2” over the set of patterns (12, 21, 23, 45, 56, 546, 58). In this problem the search pattern varies, the recognized patterns in the set are 12, 21 and 23. In this problem the first character of the substring can be 1 or 2, which means that the first pattern is varying. In the fixed pattern search, the pattern characters will not vary in the entire search.

The regular expressions can be written with some special symbols. Every symbol in the regular expression will have a special meaning. A few important regular expression symbols are as follows:

| Symbol | Description |
| :--- | :--- |
| \d | Matches with a single digit |
| \w | Matches with a single character |
| \W | Matches with a single non-word character |
| \s | Matches with a single space character |
| \S | Matches with a single non-space character |
| r* | Regular expression occurrence for zero or more number of times |
| r+ | Regular expression occurrence for one or more number of times |

For example, to search for the pattern 'a word followed with a space and followed with a number', then the regular expression becomes “w+\s\d+”.

Here, the regular expression \w matches a word character, because the regular expression is with + symbol. So, \w+ matches with one or more number characters. Then \s matches with a space character, and the \d+ matches with one or more number of digits.

### 15.4 FIXED PATTERN MATCHING ALGORITHMS

Various algorithms that are used to match a given pattern with the available patterns are discussed. Here, the pattern that is to be matched is stable all through the search process.

### 15.4.1 Brute Force Pattern Matching Algorithm

Brute force pattern matching algorithm is a good and simple algorithm for pattern matching. This algorithm finds all the possible substrings over the given large string, and checks for the given pattern on all the possible substrings.

If the pattern is with length 5, then the first substring from the text will be from the first character to the 5th character. The first substring will be cross checked with the pattern. If the substring and the pattern match, then the brute force algorithm returns with TRUE. If the substring and the pattern do not match, then the second substring will be from second character of the text to the 6th character of the text. The second substring will be cross checked with the pattern, if matches return TRUE or else the same process will be continued until the start index of the substring reaches n-length(P).

```
Algorithm 15.1: BruteForceMatch(Text, Pattern)
//n = length of Text and m = length of Pattern
Step 1: for i=0 to n-m do /*For each character of text, loop continues*/
Step 2: for j=0 to m do
/*For each character of pattern, loop continues, used to frame text sub
string with the length of the pattern*/
/*If any character of text substring is not equal to the character
sequence of pattern, Second for loop exits and first for loop continues
with the next possible text substring*/
Step 3: if (Pattern[j] != Text[i+j]) break;
done
Step 4: if (j==m) then return TRUE
/*If any text substring pattern characters fully matches with the pattern,
Function returns true as matched*/
done
Step 5: Return FALSE
/*If all the text substring pattern characters fully match with the
pattern, Function returns false as not-matched*/
```

Here, n is length of the text string (T) and m is length of the pattern string (P). In the first step, the algorithm estimates the possible number substrings with the length of pattern string over the text string, i.e. (n-m). The second step or loop identifies all the possible strings. If all the characters of the pattern string match with the substring characters, then the algorithm returns TRUE and exits else continues to check the next substring and is cross checked against the pattern string. This process continues for all the substrings. If the given pattern matches with any of the substrings the algorithm exits by returning TRUE, i.e. pattern match message.
