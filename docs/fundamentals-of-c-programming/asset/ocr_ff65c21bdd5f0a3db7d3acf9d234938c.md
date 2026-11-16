```
if (fin.good()) { // Open the file for reading
std::string word;
while (fin >> word) {
// Capitalize all the letters in the word
transform(word.begin(), word.end(),
std::begin(word), toupper);
std::begin(word), toupper);
std::begin(word), toupper);
// Add word to appropriate set based on the word's length
groups[word.length()].insert(word);
}
// Report the counts for each word
for (auto item : groups)
std::cout << item.first << ": " << item.second << '\n';
}
else
std::cout << "Cannot open file for reading\n";
}
```

The following shows a sample run of Listing 21.18 (groupwords.cpp) on our snippet from the Declaration of Independence:

```
1:(A)
2:(IN, IT, OF, TO)
3:(AND, FOR, GOD, ONE, THE)
4:(HAVE, LAWS, THAT, THEY, WHEN, WITH)
5:(AMONG, BANDS, EARTH, EQUAL, HUMAN, IMPEL, WHICH)
6:(ASSUME, CAUSES, COURSE, DECENT, EVENTS, NATURE, PEOPLE, POWERS, SHOULD)
7:(ANCIENT, BECOMES, DECLARE, ENTITLE, MANKIND, RESPECT, STATION)
8:(DISSOLVE, NATURE'S, OPINIONS, REQUIRES, SEPARATE)
9:(CONNECTED, NECESSARY, POLITICAL)
10:(SEPARATION)
```

Each integer key represents the length of all the strings in the set it oversees.

In this example the need for a map object is not as compelling as in Listing 21.17 (wordcount.cpp), because in practice the length of English words is limited. We could instead use a vector of 50 sets. Only rarely used, highly technical words exceed 50 letters. We could handle these "too-long" words in a special way, perhaps storing them in the set in the last position in the vector with other words of more than 49 letters. Our program could use special processing for this set of long words if it ever becomes nonempty. This approach under typical circumstances would result in a number of empty sets at higher indices because most English text contains words of at most about 20 letters. The advantage of a map is that it stores only what it needs. Listing 21.19 (groupwordsvector.cpp) is close transliteration of Listing 21.18 (groupwords.cpp) that uses a vector in place of a map.

# Listing 21.19: groupwordsvector.cpp

```
// Uses a vector to group words in a document by their length.
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <set>
#include <algorithm>
#include <cctype>
```