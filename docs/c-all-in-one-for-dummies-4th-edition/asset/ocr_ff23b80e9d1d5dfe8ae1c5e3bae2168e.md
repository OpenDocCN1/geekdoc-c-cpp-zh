This final test shows that the RegEx_search() function finds the three-digit value in the string. Obviously, the RegEx_search() function is great when you need to locate information but not good when you need to secure it. When you need a precise pattern match, use RegEx_match() instead.

# Breaking Strings into Tokens Using Tokenizer

Humans view strings as a sentence or at least a phrase. Mixtures of words create meaning that we can see in a moment.

![](bbox=[0.175, 0.355, 0.239, 0.422])

Computers, on the other hand, understand nothing. A computer can perform pattern matching and do math, but it can’t understand Kipling (read more about this fascinating author at https://www.poetryfoundation.org/poets/rudyard-kipling). It’s because of this lack of understanding that you must tokenize text for the computer. A computer can perform comparisons on individual tokens, usually single words or symbols, and create output based on those comparisons.

The compiler you use relies on a tokenizer, an application component that breaks text into tokens, to turn the text you type into machine code the computer can execute. However, the tokenizer appears in all sorts of applications. For example, when you perform a spelling check on a document, the word processing application breaks the text into individual words using a tokenizer, and then compares those words to words in its internal dictionary.

The Tokens example, shown in Listing 5-2, shows a method for creating tokens from strings. This basic technique works with any phrase, string, or series of strings. You’ll normally process the tokens after you finish creating them.

# LISTING 5-2: Creating Tokens from Strings

```
```cpp
#include <iostream>
#include "boost/tokenizer.hpp"

using namespace std;
using namespace boost;

int main() {
  string MyString = "This is a test string!";
  tokenizer<> Tokens(MyString);
```

```

(continued)