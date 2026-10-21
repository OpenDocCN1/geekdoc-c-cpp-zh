
has the following output:
    sum of squared:          146
    product of differences:  -200
    sum of combined digits: 31 12 73 54 45 16 67 38

## 23.2.3 std::inclusive_scan() and std::exclusive_scan()

```
OutputIterator
inclusive_scan (ExecutionPolicy&& pol,  // optional
                InputIterator inBeg, InputIterator inEnd,
                OutputIterator outBeg,
                BinaryOp op,            // optional
                T initVal)              // optional

OutputIterator
exclusive_scan (ExecutionPolicy&& pol,  // optional
                InputIterator inBeg, InputIterator inEnd,
                OutputIterator outBeg,
                T initVal,              // mandatory
                BinaryOp op)            // optional
```

- All forms compute the partial results of combining each element in the source range [beg,end) with all previous elements and write them to the destination range starting with outBeg.
- The difference between inclusive_scan() and exclusive_scan() is that exclusive_scan() starts with the initial value and excludes the last input element from the result. Note that the order of the trailing function parameters differs and that for exclusive_scan(), the initial value is mandatory.
- Thus, for the values
    a1 a2 a3 ... aN
  inclusive_scan() computes
    initVal op a1, initVal op a1 op a2, initVal op a1 op a2 op a3, ... aN
  while exclusive_scan() computes
    initVal, initVal op a1, initVal op a1 op a2, ... op aN-1
  This means that for inclusive_scan(), initVal serves as an offset for each output value, while for exclusive_scan(), it serves as the first output value (although it is not written if the input range is empty).
- All forms return the position after the last written value in the destination range (the first element that is not overwritten).
- If no op is passed, std::plus is used, so that the sum of all elements is computed.
- If no initVal is passed (inclusive_scan() only), no initial value is added. Thus, the first output value is just the first input value.
- If the range is empty (beg==end), all forms write no elements.
- The caller must ensure that the range starting with *outBeg* contains enough elements to overwrite (in fact, at least as many elements as in the source range), or that insert iterators are used.
- *op* must not modify the passed arguments.
- Complexity: linear (*numElems* calls of operator *op*).
- The algorithms are provided as the parallel version of std::partial_sum() called for associative operations. If the first optional execution policy is passed:
  - There is no guaranteed order for using the operator *op1*, which means that *op1* must be commutative and associative.
  - It is up to the caller to ensure that parallel calls of the operations do not result in a data race.
  - The iterators must be forward iterators.

For example, the following program:

*lib/scan.cpp*

```
#include <numeric>
#include <iostream>
#include <iterator>
#include <array>

int main()
{
    std::array coll{3, 1, 7, 0, 4, 1, 6, 3};

    std::cout << " inclusive_scan():   ";
    std::inclusive_scan(coll.begin(), coll.end(),
                        std::ostream_iterator<int>(std::cout, " "));

    std::cout << "\n exclusive_scan(): ";
    std::exclusive_scan(coll.begin(), coll.end(),
                        std::ostream_iterator<int>(std::cout, " "),
                        0);  // mandatory

    std::cout << "\n exclusive_scan(): ";
    std::exclusive_scan(coll.begin(), coll.end(),
                        std::ostream_iterator<int>(std::cout, " "),
                        100);  // mandatory

    std::cout << "\n inclusive_scan():   ";
    std::inclusive_scan(coll.begin(), coll.end(),
                        std::ostream_iterator<int>(std::cout, " "),
                        std::plus{}, 100);

    std::cout << "\n exclusive_scan(): ";
    std::exclusive_scan(coll.begin(), coll.end(),
                        std::ostream_iterator<int>(std::cout, " "),
```

```
100, std::plus{});  // note: different order
}
```

has the following output:

```
inclusive_scan():   3 4 11 11 15 16 22 25
exclusive_scan():  0 3 4 11 11 15 16 22
exclusive_scan():  100 103 104 111 111 115 116 122
inclusive_scan():      103 104 111 111 115 116 122 125
exclusive_scan():  100 103 104 111 111 115 116 122
```

Note that both algorithms always output the same number of elements that the input range has. However, with inclusive_scan(), we start with the value of the first element and end with the sum/combination of all elements (plus any passed initial value used as offset), while with exclusive_scan(), we start with the initial value and end with the sum/combination of all but the last element.

## 23.2.4 std::transform_inclusive_scan() and std::transform_exclusive_scan()

```
OutputIterator
transform_inclusive_scan (ExecutionPolicy&& pol,  // optional
                          InputIterator inBeg, InputIterator inEnd,
                          OutputIterator outBeg,
                          BinaryOp op2,            // mandatory
                          UnaryOp op1,             // mandatory
                          T initVal)               // optional

OutputIterator
transform_exclusive_scan (ExecutionPolicy&& pol,  // optional
                          InputIterator inBeg, InputIterator inEnd,
                          OutputIterator outBeg,
                          T initVal,               // mandatory
                          BinaryOp op2,            // mandatory
                          UnaryOp op1)             // mandatory
```

- All forms compute the partial results of combining the transformed value of each element in the source range [beg,end) with all previous transformed values and write them to the destination range starting with outBeg.
- The difference between transform_inclusive_scan() and transform_exclusive_scan() is that transform_exclusive_scan() starts with the initial value and excludes the last input element from the result. Note that the order of the trailing function parameters differs and that for exclusive_scan(), the initial value is mandatory.
- Thus, for the values
  a1 a2 a3 ... aN

transform_inclusive_scan() computes
    initVal op2 op1(a1), initVal op2 op1(a1) op2 op1(a2), ... op2 op1(aN)
while transform_exclusive_scan() computes
    initVal, initVal op2 op1(a1), initVal op2 op1(a1) op2 op1(a2), ... op2 op1(aN-1)
This means that for inclusive_scan(), initVal serves as an offset for each output value, while for exclusive_scan(), it serves as the first element (although it is not written if the input range is empty).

- All forms return the position after the last written value in the destination range (the first element that is not overwritten).
- If no initVal is passed (transform_inclusive_scan() only), no initial value is added. Thus, the first output value is just the first transformed input value.
- If the range is empty (beg==end), all forms write no elements.
- The caller must ensure that the range starting with outBeg contains enough elements to overwrite (in fact, at least as many elements as in the source range), or that insert iterators are used.
- op1 and op2 must not modify the passed arguments.
- Complexity: linear (numElems calls of operator op1 and op2).
- If the first optional execution policy is passed:
  - There is no guaranteed order for using the operator op2, which means that op2 must be commutative and associative.
  - It is up to the caller to ensure that parallel calls of the operations do not result in a data race.
  - The iterators must be forward iterators.

For example, the following program:

lib/transformscan.cpp

```
#include <numeric>
#include <algorithm>
#include <iostream>
#include <iterator>
#include <array>

int main()
{
    std::array coll{3, 1, 7, 0, 4, 1, 6, 3};

    auto twice = [] (int v) { return v*2; };

    std::cout << " source:               ";
    std::copy(coll.begin(), coll.end(),
              std::ostream_iterator<int>(std::cout, " "));

    std::cout << "\n transform_inclusive_scan():   ";
    std::transform_inclusive_scan(coll.begin(), coll.end(),
                                  std::ostream_iterator<int>(std::cout, " "),
```
