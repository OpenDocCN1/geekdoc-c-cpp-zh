# // Program 12_7

+   1 // A more complete function: counting words in a string, alternative
2 #include<iostream>
3 #include<string>
4 #include<sstream>
5 using namespace std;
6

```
int wordCount(string str_to_count) {
    // count number of spaces
    int count = 0;
    for (i i = 0; i < str_to_count.size(); i++) {
        if (str_to_count[i] == ' ') {
            count++;
        }
    }
    // Number of words is one more than number of spaces
    return count + 1;
}

int main() {
    string s = "This is a string that has eight words";
    cout << "There are " << wordCount(s) << " words in the string." << endl;
}
```

That isn't the only way you could implement that function. Another option would be to count the spaces between words. If you can assume that there's just one space in in each word, then the number of words in the string will be just more than the number of spaces in the string.

To implement this function, you'll first declare a count variable (18) and a variable i (11).

Then, you'll loop through all the characters of the string, one by one, letting i take on one less than the string length (h).

You'll check each character to see if it is a space (13). If so, you'll increment count (14).

Finally, you'd return count+1 (18), remembering that there will be one less space than the number of words.

In terms of the main function that calls the word_count function, it is exactly the same as before (23).