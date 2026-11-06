

```cpp
    // output split step
    cout << "split:    ";
    displayElements(items, low, high);
    cout << "          ";
    displayElements(items, low, middle1);
    cout << "          ";
    displayElements(items, middle2, high);
    cout << endl;

    // split array in half; sort each half (recursive calls)
    mergeSort(items, low, middle1); // first half of array
    mergeSort(items, middle2, high); // second half of array

    // merge two sorted arrays after split calls return
    merge(items, low, middle1, middle2, high);
}

// merge two sorted subarrays into one sorted subarray
template <typename T, size_t size>
void merge(array<T, size>& items,
        size_t left, size_t middle1, size_t middle2, size_t right) {
    size_t leftIndex{left}; // index into left subarray
    size_t rightIndex{middle2}; // index into right subarray
    size_t combinedIndex{left}; // index into temporary working array
    array<T, size> combined; // working array

    // output two subarrays before merging
    cout << "merge:    ";
    displayElements(items, left, middle1);
    cout << "          ";
    displayElements(items, middle2, right);
    cout << endl;

    // merge arrays until reaching end of either
    while (leftIndex <= middle1 && rightIndex <= right) {
        // place smaller of two current elements into result
        // and move to next space in array
        if (items[leftIndex] <= items[rightIndex]) {
            combined[combinedIndex++] = items[leftIndex++];
        }
        else {
            combined[combinedIndex++] = items[rightIndex++];
        }
    }

    if (leftIndex == middle1 + 1) { // if at end of left array
        while (rightIndex <= right) { // copy in rest of right array
            combined[combinedIndex++] = items[rightIndex++];
        }
    }
    else { // at end of right array
        while (leftIndex <= middle1) { // copy in rest of left array
            combined[combinedIndex++] = items[leftIndex++];
        }
    }

    // copy values back into original array
    for (size_t i = left; i <= right; ++i) {
        items[i] = combined[i];
    }

    // output merged array
    cout << "        ";
    displayElements(items, left, right);
    cout << endl;
}

int main() {
    // use the default random-number generation engine to produce
    // uniformly distributed pseudorandom int values from 10 to 99
    default_random_engine engine{
        static_cast<unsigned int>(time(nullptr))};
    uniform_int_distribution<int> randomInt{10, 99};

    const size_t arraySize{10}; // size of array
    array<int, arraySize> data; // create array

    // fill data with random values
    for (int &item : data) {
        item = randomInt(engine);
    }

    // display data's values before mergeSort
    cout << "Unsorted array:" << endl;
    displayElements(data, 0, data.size() - 1);
    cout << endl;

    mergeSort(data, 0, data.size() - 1); // sort the array data

    // display data's values after mergeSort
    cout << "Sorted array:" << endl;
    displayElements(data, 0, data.size() - 1);
}
```

```text
Unsorted array:
  30 47 22 67 79 18 60 78 26 54

split:    30 47 22 67 79 18 60 78 26 54
          30 47 22 67 79
                              18 60 78 26 54

split:    30 47 22 67 79
          30 47 22
                    67 79

split:    30 47 22
          30 47
                22

split:    30 47
          30
             47

merge:    30
             47
          30 47

merge:    30 47
                22
          22 30 47

split:                 67 79
                      67
                         79

merge:                 67
                         79
                      67 79

merge:    22 30 47
                         67 79
          22 30 47 67 79

split:                        18 60 78 26 54
                             18 60 78
                                  26 54

split:                        18 60 78
                             18 60
                                  78

split:              18 60
                     18
                          60

merge:              18
                          60
                     18 60

merge:              18 60
                              78
                     18 60 78

split:                    26 54
                           26
                                54

merge:                    26
                                54
                           26 54

merge:              18 60 78
                           26 54
                     18 26 54 60 78

merge:       22 30 47 67 79
                     18 26 54 60 78
               18 22 26 30 47 54 60 67 78 79

Sorted array:
  18 22 26 30 47 54 60 67 78 79
```

图 20.6 使用归并排序将数组按升序排列。

## 函数 `mergeSort`

递归函数 `mergeSort`（第 25–48 行）接收待排序的 `array` 以及待排序元素范围的 `low` 和 `high` 索引作为参数。第 28 行测试基本情况。如果 `high` 索引减去 `low` 索引为 `0`（即包含一个元素的子 `array`），函数将直接返回。如果两个索引之差大于或等于 `1`，函数会将 `array` 分成两部分——第 29–30 行确定分割点。接下来，第 42 行递归调用函数 `mergeSort`，处理 `array` 的前半部分；第 43 行递归调用函数 `mergeSort`，处理 `array` 的后半部分。当这两个函数调用返回时，每一半都已完成排序。第 46 行调用函数 `merge`（第 51–98 行），将两个已排序的部分合并成一个更大的已排序 `array`。

## *函数* `merge`

函数 `merge` 中的第 67–76 行循环执行，直到程序到达某个子 `array` 的末尾。第 70 行测试两个子 `array` 开头的元素，判断哪个更小。如果左侧子 `array` 中的元素更小，或者两个元素相等，第 71 行会将该元素放入合并后的 `array` 中。如果右侧子 `array` 中的元素更小，第 74 行会将该元素放入合并后的 `array` 中。`while` 循环完成后，一个完整的子 `array` 已经位于合并后的 `array` 中，但另一个子 `array` 仍包含数据。第 78 行测试左侧子 `array` 是否已经到达末尾。如果是，第 79–81 行会将右侧子 `array` 中的元素填入合并后的 `array`。如果左侧子 `array` 尚未到达末尾，那么右侧子 `array` 必定已经到达末尾，第 84–86 行会将左侧子 `array` 中的元素填入合并后的 `array`。最后，第 90–92 行将合并后的 `array` 复制到原始 `array` 中。

## *归并排序的效率*

归并排序是一种比插入排序或选择排序高效得多的算法——不过，看到**图 20.6**中繁忙的输出时，这一点可能很难令人相信。考虑对函数 `mergeSort` 的第一次（非递归）调用（第 120 行）。该调用会导致两次对函数 `mergeSort` 的递归调用，所处理的子数组大小均约为原始 `array` 大小的一半，并且还会调用一次函数 `merge`。调用 `merge` 最多需要进行 *n* − 1 次比较，才能填充原始 `array`，因此其复杂度为 *O(n)*。（请记住，每个 `array` 元素都是通过比较两个子数组中的各一个元素来确定的。）对函数 `mergeSort` 的两次调用会进一步导致四次对函数 `mergeSort` 的递归调用——每次处理的子数组大小约为原始 `array` 的四分之一——并调用两次函数 `merge`。这两次对函数 `merge` 的调用各自最多需要 *n*/2 − 1 次比较，因此比较次数总计为 *O(n)*。这一过程会持续进行：每次调用 `mergeSort` 都会生成两次额外的 `mergeSort` 调用和一次 `merge` 调用，直到算法将 `array` 分割成只包含一个元素的子数组。在每一层中，合并子数组都需要进行 *O(n)* 次比较。每一层都会将 `array` 的大小减半，因此将 `array` 的大小加倍需要增加一层；将 `array` 的大小扩大四倍则需要增加两层。这种模式呈对数增长，最终得到 log₂ *n* 层。因此，总体效率为 **O(n log n)**。

