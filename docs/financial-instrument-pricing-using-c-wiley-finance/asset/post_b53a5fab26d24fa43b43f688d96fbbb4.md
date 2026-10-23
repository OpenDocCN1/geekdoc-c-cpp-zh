
// predicate is true
std::vector<int>::iterator posF
    = std::find_if(std::begin(v), std::end(v),
                   [&searchValue] (double d)
                   {return d > searchValue - 2; });
if (posF != std::end(v))
{
    std::cout << "First value *found* > "
              << searchValue - 2 << " is: " << *posF << std::endl;
}
else
{
    std::cout << "Value not found\n";
}

The output is:

```
**** Block III, Finding ****
vector: 1,2,3,4,5,5,-6,
Value found: 4
First value *found* > 2 is: 3
```

When using the algorithms in this category we distinguish between offset and position; an offset is zero-based and a position has initial index one. For example, the first element of a container has offset zero and position one.

## 17.3.4 Searching for Subranges

Whereas the algorithms in Section 17.3.3 search for a single value (usually the first-found element) in a range, the algorithms in this section search for the occurrence of a subrange within a range:

```
void Search()
{
    std::cout << "\n**** Block IV, Searching ****\n";
    // 3. Find all occurrences of a subrange in a range.
    // Output is the start position.
    std::vector<int> myRange
        = { 0, 1, 2, 3, 4, 5, 6, 6, 1, 2, 2, 9, 9, 9, 8, 7, 1, 2, 3 };
    std::vector<int> mySubRange = { 1, 2, 3 };
    print(myRange, "range to be searched in");
    print(mySubRange, "subrange to be searched for");

    auto pos = myRange.begin();

    // Search first subrange
    pos = std::search(myRange.begin(), myRange.end(),
                      mySubRange.begin(), mySubRange.end());
```

```
// Loop while subrange found
while (pos != myRange.end())
{
        // Distance between the iterators (plus 1):
        // position := distance + 1
        std::cout << "Subcollection search found at offset: "
                  << std::distance(std::begin(myRange), pos) << std::endl;

        pos = std::search(++pos, myRange.end(), mySubRange.begin(),
                          mySubRange.end());
}

// Search first n matching *consecutive* elements with value
// *compared* to myValue. Overloaded version with binary predicate.
std::vector<int> myRangeA
    = { 0, 2, 2, 2, 2, 9, 9, 8, 7, 6, 6, 6, 6, 6, 1, 3, 3, 3, 3, 3 };
print(myRangeA, "range to be searched for consecutive elements");

int count = 4; // Number of consecutive elements
int myValue = 6; // The value with 'consecutive replication'
auto pos22 = std::search_n(std::begin(myRangeA), std::end(myRangeA),
                           count, myValue);

if (pos22 != std::end(myRangeA))
{
        std::cout << count << " Consecutive elems(position==offset + 1): "
                  << std::distance(std::begin(myRangeA), pos22) + 1
                  << std::endl;
}
else
{
        std::cout << "Consecutive elements not found\n";
}

// Find count *consecutive* elements with value > myValue
// Tricky: think about this a bit
std::vector<int> myRangeB
    = { 0, 2, 2, 2, 9, 1, 8, 7, 0, 6, 0, 6, 6, 1, 3, 3, 3, 3, 3 };
print(myRangeB, "range to be searched");
count = 3;
myValue = 2;
auto posB = std::search_n(std::begin(myRangeB), std::end(myRangeB),
                          count, myValue, std::greater<int>());

if (posB != std::end(myRangeB))
{
        std::cout << count << " Consecutive elems(position): >> "
                  << myValue << ": "
                  << std::distance(std::begin(myRangeB), posB) + 1
                  << std::endl;
}
```

```
else
{
    std::cout << "Consecutive elements not found\n";
}
```

The output from this code is:

```
**** Block IV, Searching ****
range to be searched in: 0,1,2,3,4,5,6,6,1,2,2,9,9,9,8,7,1,2,3,
subrange to be searched for: 1,2,3,
Subcollection search found at offset: 1
Subcollection search found at offset: 16
range to be searched for consecutive elements:
0,2,2,2,2,2,9,9,8,7,6,6,6,6,1,3,3,3,3,3,
4 Consecutive elements (position == offset + 1): 11
range to be searched: 0,2,2,2,9,9,1,8,7,0,6,0,6,1,3,3,3,3,
3 Consecutive elements {position}: >> 2: 15
```

## 17.3.5 Advanced Find Algorithms

The algorithms in this category are concerned with finding the first and subsequent occurrences of a subrange in a range as well as algorithms that find elements based on values of their *adjacent elements*:

```
void AdvancedFind()
{
    std::cout << "\n**** Block V, Advanced Find ****\n";
    std::vector<int> myRange
        = { 0, 1, 2, 3, 4, 5, 6, 6, 1, 2, 2, 9, 9, 9, 8, 7, 1, 2, 3 };
    std::vector<int> mySubRange = { 1, 2, 3 };

    print(myRange, "range to be searched");
    print(mySubRange, "subrange to be searched for");

    // Find position of the first element of the first
    // subrange matching the input range.
    auto pos = std::find_first_of(std::begin(myRange), std::end(myRange),
                                  std::begin(mySubRange), std::end(mySubRange));
    std::cout << "First subrange found at position: "
              << distance(std::begin(myRange), pos) + 1 << std::endl;

    // First position of last subcollection in a collection
    pos = std::find_end(std::begin(myRange), std::end(myRange),
                        std::begin(mySubRange),
                        std::end(mySubRange));
    std::cout << "Last subrange found at position: "
              << std::distance(std::begin(myRange), pos) + 1;
}
```

```
std::pair<std::vector<int>::iterator, std::vector<int>::iterator>
    values;
values = std::mismatch(std::begin(myRangeD), std::end(myRangeD),
                        std::begin(myRangeE));

if (values.first == std::end(myRangeD))
{
    std::cout << "No mismatch found in D<E\n";
}
else
{
    std::cout << "First mismatch D,E VALUES: " << *values.first
              << "," << *values.second << std::endl;
}

// Return 1st two corresponding elements of ranges that return
false values = std::mismatch(std::begin(myRangeD), std::end(myRangeD),
                            std::begin(myRangeE), std::less_equal<int>());

if (values.first == std::end(myRangeD))
{
    std::cout << "No mismatch D,E found\n";
}
else
{
    std::cout << "First mismatch (with FO) D,E VALUES: "
              << *values.first << "," << *values.second << std::endl;
}

// Lexicographical comparisons. We use ASCII collating sequence.
std::vector<char> myRangeF; myRangeF = { 'a', 'b', 'c' };// 61, 62, 63
std::vector<char> myRangeG; myRangeG = { 'A', 'B', 'C' };// 41, 42, 43
print(myRangeF, "range F");
print(myRangeG, "range G");
boolalpha(std::cout);
std::cout << "Equality F,G: "
          << std::lexicographical_compare(std::begin(myRangeF),
          std::end(myRangeF), std::begin(myRangeG),
          std::end(myRangeG)) << std::endl;
std::cout << "Comparison using function object: "
          << std::lexicographical_compare(std::begin(myRangeF),
          std::end(myRangeF),std::begin(myRangeG),
          std::end(myRangeG),
          [] (double d1, double d2) -> bool
          { return (d1 > d2); }) << std::endl;
```

The output is:

```
**** Block VI, Ranges and their algorithms ****
range B: 1,3,2,4,5,6,7,
```

```
range C: 1,4,3,
Ranges B, C equal: false
range D: 1,3,2,4,3,27,0,
range E: 2,4,7,5,8,43,3,
Ranges D,E satisfy less relation: true
range D: 1,2,3,4,5,6,
range E: 1,4,9,16,25,36,
Ranges D, E satisfy squared relation: true
range D: 1,2,3,4,5,6,
range E: 1,2,3,8,16,3,
First mismatch D,E VALUES: 4,8
First mismatch (with function object) D,E VALUES: 6,3
range F: a,b,c,
range G: A,B,C,
Equality F,G: false
Comparison using function object: true
```

## 17.4 MODIFYING ALGORITHMS

These algorithms change the values of elements in a container. They may modify the elements of a range directly or they may modify them as they are being copied into another range.

The algorithm categories are:

- Perform an operation on each element of the range.
- Copy a range.
- Merge two ranges; swap two ranges.
- Replace each element value (or *n* elements) with a given value.
- Replace each element value (or *n* elements) with the result of an operation.
- Replace elements with a special value by another value.
- Remove elements from a range.

We now discuss these algorithms in detail.

### 17.4.1 Copying and Moving Elements

Copying and moving the elements of one container to another container is a common occurrence. For this reason we examine how STL supports these operations. In general, it is preferable to use them rather than creating your home-grown versions. We notice that the operations have copy and move variants. The main algorithms are:

- Copy all elements from source to destination.
- Copy only those elements from source to destination that satisfy a certain criterion.
- Copy the first *n* elements from source to destination.
- Copy source to destination, starting at the end of destination (copy backwards).
- Move all elements from source to destination.
- Move source to destination, starting at the end of destination.
