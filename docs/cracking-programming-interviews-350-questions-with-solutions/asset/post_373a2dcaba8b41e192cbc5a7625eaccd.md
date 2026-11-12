
```cpp
if (max_ending_here < 0)
{
    max_ending_here = 0;
    starti = start;
    ++starti;
}

if (max_so_far < max_ending_here)
{
    max_so_far = max_ending_here;
    sum_start = starti;
    sum_end = start;
}
++starti;
}
return std::make_tuple(max_so_far,
                       sum_start,
                       sum_end);
}
```

## Usage

In practice, a bitmap image has all non-negative pixel values. When the average is subtracted from each pixel, we can apply the maximum subarray algorithm to find the brightest area within the image.

## Program 4.7: Using Kadane’s Algorithm : Finding Indices

```cpp
#include <iostream>
#include <forward_list>
#include "kadane1d_indices.hpp"

template<typename ForwardIterator>
void printContents(ForwardIterator start,
                   ForwardIterator end)
{
    std::cout << "{";
    while (start != end)
    {
        std::cout << *start++ << " ";
    }
    std::cout << *start << "}" << std::endl;
}

int main()
{
    std::tuple<int, int*, int*> sum_start_end;
    std::array<int, 8> a
    {-2, -3, 4, -1, -2, 1, 5, -3};

    sum_start_end =
        kadane1d(a.begin(), a.end());

    auto max_sum = std::get<0>(sum_start_end);

    auto start_index =
        std::distance(std::begin(a),
                      std::get<1>(sum_start_end));

    auto end_index =
        std::distance(std::begin(a),
                      std::get<2>(sum_start_end));

    std::cout << "<sum: " << max_sum << ", "
              << "start_index: " << start_index << ", "
              << "end_index: " << end_index << ">"
              << "\nMax subarray is: ";

    printContents(std::get<1>(sum_start_end),
                  std::get<2>(sum_start_end));

    std::vector<int> v
    {-1, 4, -2, 5, -5, 2, -20, 6};

    typedef std::vector<int>::iterator vitr;
    std::tuple<int, vitr, vitr>
        sum_start_end_v;
    sum_start_end_v =
        kadane1d(v.begin(), v.end());

    max_sum = std::get<0>(sum_start_end_v);

    start_index =
        std::distance(v.begin(),
                      std::get<1>(sum_start_end_v));

    end_index = std::distance(v.begin(),
                              std::get<2>(sum_start_end_v));

    std::cout << "<sum: " << max_sum << ", "
              << "start_index: " << start_index << ", "
              << "end_index: " << end_index << ">"
              << "\nMax subarray is: ";

    printContents(std::get<1>(sum_start_end_v),
                  std::get<2>(sum_start_end_v));

    std::forward_list<int> l
    {-2, 1, -3, 4, -1, 2, 1, -5, 4};

    typedef std::forward_list<int>::iterator
        litr;
    std::tuple<int, litr, litr> sum_start_end_l;
    sum_start_end_l =
        kadane1d(l.begin(), l.end());
```

have the sum of this sub-array as:

$$a[l] + a[l + 1] + \ldots + a[k - 1] + a[k]$$

$$=$$

$$prefix[l] - prefix[l - 1] +$$
$$prefix[l + 1] - prefix[l] +$$
$$\ldots$$

$$prefix[k - 1] - prefix[k - 2] +$$
$$prefix[k] - prefix[k - 1]$$

$$=$$

$$prefix[k] - prefix[l - 1]$$

Hence the sum of a[l..k] to be equal to zero, we should have

$$prefix[k] = prefix[l - 1]$$

Hence the sum closest to zero can be found by locating the two closest elements in prefixa.

Let us formalize the above algorithm as follows:

- 1. Compute prefix array with index of original array as well, so it is a collection of pair(value, index). $O(n)$

- 2. Sort the above prefix array by value. $O(n\log n)$

- 3. Compute pair-wise diff by value. Prepare absolute values to get a measure of how far/close these are to zero. $O(n)$

- 4. The closest pair is that with minimum value found above. $O(n)$

- 5. Report the indices found above in the original array. This is the subarray with sum being closest to zero. (2 comparisons needed).

Please note that the first and last entries of the prefix array are sentinel points (hence special cases) because these cannot be represented effectively by any other two prefix sums. Suppose the closest pair indices reported above is (l, k), then the subarray with sum closest to zero will be decided by the minimum of (closest pair-wise diff val, first entry of prefix, last entry of prefix), i.e. the desired subarray would be

- a[l..k] if closest pair-wise diff val is minimum

- a[0] if first entry of prefix is minimum

- a[0..n − 1] if last entry of prefix is minimum

Hence overall time complexity is $O(n + n\log n)$. Let us start walking through an implementation approach in C++ to understand it better.

## Program 4.8: Finding sum closest to zero

```cpp
#include <utility>
#include <algorithm>
#include <tuple>
#include <iostream>

typedef std::pair<int, size_t> ValueIndexPair;

std::vector<int>
findSubArraySumZero(std::vector<int> & a)
{
    typedef std::tuple<int, size_t, size_t>
        ValStartEndIndices;

    size_t len = a.size();
    std::vector<ValueIndexPair> prefixa(len);
    prefixa[0] = ValueIndexPair(a[0], 0);

    for(size_t i = 1; i < len; ++i)
        prefixa[i] =
            ValueIndexPair(
                prefixa[i - 1].first + a[i], i);

    std::cout <<
        "Printing_Prefix_Array_with_Value_and"
        "_Original_Index"
        << std::endl;

    for(ValueIndexPair vip : prefixa)
        std::cout << vip.first << " : "
                  << vip.second << " ";
    std::cout << std::endl;

    int start_prefix = prefixa[0].first;
    int end_prefix = prefixa[len - 1].first;

    std::sort(prefixa.begin(), prefixa.end(),
        [](ValueIndexPair f, ValueIndexPair s)
        {
            return f.first < s.first;
        }
    );

    std::cout
        << "Printing_Value_Sorted_Prefix_Array"
        << std::endl;

    for(ValueIndexPair vip : prefixa)
        std::cout << vip.first << " : "
                  << vip.second << " ";
    std::cout << std::endl;

    std::vector<ValStartEndIndices>
        pairwiseDiff_vec(len - 1);
    for(size_t i = 0; i < len - 1; ++i)
    {
        pairwiseDiff_vec[i] =
            std::make_tuple(
                prefixa[i + 1].first - prefixa[i].first,
                prefixa[i].second,
                prefixa[i + 1].second);
    }

    std::cout <<
        "Printing_Pairwise_Value_Differences_with_"
        "original_indices"
        << std::endl;

    for (ValStartEndIndices vsei :
            pairwiseDiff_vec)
        std::cout << "("
            << std::get<0>(vsei) << ","
            << std::get<1>(vsei) << ","
            << std::get<2>(vsei) << ")_";
    std::cout << std::endl;

    std::vector<ValStartEndIndices>::iterator itr =
        std::min_element(
            pairwiseDiff_vec.begin(),
            pairwiseDiff_vec.end(),
            [](ValStartEndIndices f,
               ValStartEndIndices s)
            {
                return std::abs(std::get<0>(f))
                     < std::abs(std::get<0>(s));
            }
        );

    ValStartEndIndices closest_indices = *itr;

    std::vector<int> vcandidates(3);

    vcandidates[0] =
        std::abs(std::get<0>(closest_indices));
    vcandidates[1] =
        std::abs(start_prefix); // a[0]
    vcandidates[2] =
        std::abs(end_prefix); // a[0..n - 1]

    int close_zero = *std::min_element(
        vcandidates.begin(), vcandidates.end());

    std::vector<int> vsumzero;

    size_t start_index, end_index = 0;

    if(close_zero == vcandidates[1])
    {
        vsumzero.push_back(a[0]);
    }
    else if (close_zero == vcandidates[2])
    {
        vsumzero = a;
    }
    else // close_zero == vcandidates[0]
    {
        std::pair<size_t, size_t> se =
            std::minmax(std::get<1>(
                closest_indices),
                std::get<2>(closest_indices));

        vsumzero.assign(a.begin() +
                        se.first + 1,
                        a.begin() + se.second + 1);
    }
    return vsumzero;
}

int main()
{
    std::vector<int> v
    { 8, -3, 2, 1, -4, 10, -5 };

    std::vector<int> vclosest_sum_zero =
        findSubArraySumZero(v);

    std::cout << "Subarray with sum closest"
              " to zero is" << std::endl;
    for (int e : vclosest_sum_zero)
        std::cout << e << " ";
    std::cout << std::endl;
    std::cout << std::endl;

    v = { -3, 2, 4, -6, -8, 10, 11 };
    vclosest_sum_zero = findSubArraySumZero(v);

    std::cout << "Subarray with sum closest to"
              " zero is" << std::endl;
    for (int e : vclosest_sum_zero)
        std::cout << e << " ";
    std::cout << std::endl;
    std::cout << std::endl;

    v = { 10, -2, -7 };
    vclosest_sum_zero = findSubArraySumZero(v);

    std::cout << "Subarray with sum closest to"
              " zero is" << std::endl;
    for (int e : vclosest_sum_zero)
        std::cout << e << " ";
    std::cout << std::endl;
    std::cout << std::endl;
}
```
