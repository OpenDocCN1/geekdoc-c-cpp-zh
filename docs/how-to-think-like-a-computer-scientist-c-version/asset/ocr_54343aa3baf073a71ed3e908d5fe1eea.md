# 15.10. GLOSSARY

```
// break the line up into substrings
int len1 = quoteIndex[1] - quoteIndex[0] - 1;
string city1 = line.substr(quoteIndex[0]+1, len1);
int len2 = quoteIndex[3] - quoteIndex[2] - 1;
string city2 = line.substr(quoteIndex[2]+1, len2);
int len3 = line.length() - quoteIndex[2] - 1;
string distString = line.substr(quoteIndex[3]+1, len3);
int distance = convertToInt(distString);

// add the new datum to the distances matrix
distances.add(city1, city2, distance);
```

I will leave it as an exercise to you to implement the member functions of DistMatrix.

# 15.10 Glossary

+   **ordered set**: A data structure in which every element appears only once and every element has an index that identifies it.

+   **stream**: A data structure that represents a “flow” or sequence of data items from one place to another. In C++ streams are used for input and output.

+   **accumulator**: A variable used inside a loop to accumulate a result, often getting something added or concatenated during each iteration.