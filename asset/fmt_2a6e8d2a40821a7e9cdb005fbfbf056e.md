
## 157. 实现选择排序算法

```cpp
int arr[] = {64, 25, 12, 22, 11};

int n = sizeof(arr) / sizeof(arr[0]);

std::cout << "Original array: \n";

for (int i = 0; i < n; i++) {
    std::cout << arr[i] << " ";
}

std::cout << "\n";

selectionSort(arr, n);

std::cout << "Sorted array: \n";

for (int i = 0; i < n; i++) {
    std::cout << arr[i] << " ";
}

std::cout << "\n";

return 0;
}
```

## 158. 实现插入排序算法

```cpp
#include <iostream>

void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        // 将 arr[0..i-1] 中大于 key 的元素移动到当前位置
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    std::cout << "Original array: \n";
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << "\n";
    insertionSort(arr, n);
    std::cout << "Sorted array: \n";
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << "\n";
    return 0;
}
```

## 159. 实现归并排序算法

```cpp
#include <iostream>

void merge(int arr[], int l, int m, int r) {
  int n1 = m - l + 1;
  int n2 = r - m;
  // 创建临时数组
  int L[n1], R[n2];
  // 将数据拷贝到临时数组 L[] 和 R[]
  for (int i = 0; i < n1; i++) {
    L[i] = arr[l + i];
  }
  for (int j = 0; j < n2; j++) {
    R[j] = arr[m + 1 + j];
  }
  int i = 0;
  int j = 0;
  int k = l;
  // 将临时数组合并回 arr[l..r]
  while (i < n1 && j < n2) {
    if (L[i] <= R[j]) {
      arr[k] = L[i];
      i++;
    } else {
      arr[k] = R[j];
      j++;
    }
    k++;
  }
  // 如果 L[] 还有剩余元素，将其拷贝
  while (i < n1) {
    arr[k] = L[i];
    i++;
    k++;
  }
  // 如果 R[] 还有剩余元素，将其拷贝
  while (j < n2) {
    arr[k] = R[j];
    j++;
    k++;
  }
}

void mergeSort(int arr[], int l, int r) {
  if (l >= r) {
    return; // 递归返回
  }
  int m = l + (r - l) / 2;
  mergeSort(arr, l, m);
  mergeSort(arr, m + 1, r);
  merge(arr, l, m, r);
}

int main() {
  int arr[] = {12, 11, 13, 5, 6, 7};
  int n = sizeof(arr) / sizeof(arr[0]);
  std::cout << "Original array: \n";
  for (int i = 0; i < n; i++) {
    std::cout << arr[i] << " ";
  }
  std::cout << "\n";
  mergeSort(arr, 0, n - 1);
  std::cout << "Sorted array: \n";
  for (int i = 0; i < n; i++) {
    std::cout << arr[i] << " ";
  }
  std::cout << "\n";
  return 0;
}
```

## 160. 实现快速排序算法

```cpp
#include <iostream>

// 交换两个元素
void swap(int* a, int* b) {
    int t = *a;
    *a = *b;
    *b = t;
}

// 使用最后一个元素作为基值的划分函数
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        // pi 是划分索引
        int pi = partition(arr, low, high);
        // 分别排序划分前后的元素
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    std::cout << "Given array: \n";
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << "\n";
    quickSort(arr, 0, n - 1);
    std::cout << "Sorted array: \n";
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << "\n";
    return 0;
}
```
