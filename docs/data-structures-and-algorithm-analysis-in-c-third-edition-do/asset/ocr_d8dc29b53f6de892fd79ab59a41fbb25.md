Another approach is to implement the matrix as an orthogonal list. Consider the following sparse matrix:

| 10 23 0 0 0 19 |
| 45 5 0 93 0 0 |
| 0 0 0 0 0 0 |
| 0 0 0 0 0 0 |
| 40 0 0 0 0 0 |
| 0 0 0 0 0 0 |
| 0 0 0 0 0 0 |
| 0 32 0 12 0 7 |

The corresponding orthogonal array is shown in Figure 12.7. Here we have a list of row headers, each of which contains a pointer to a list of matrix records. A second list of column headers also contains pointers to matrix records. Each non-zero matrix element stores pointers to its non-zero neighbors in the row, both following and preceding it. Each non-zero element also stores pointers to its non-zero neighbors following and preceding it in the column. Thus, each non-zero element stores its value, its position within the matrix, and four pointers. Note that the first non-zero element in a given row could be in any column; likewise, the neighboring non-zero element in any row or column could be at any (higher) row or column in the array. Thus, each non-zero element must also store its row and column position.

To find if a particular position in the matrix contains a non-zero element, we looking for the element at Row 7 and Column 1, we can traverse the list either for Row 7 or for Column 1. When traversing a row or column list, if we come to an element with the correct position, its value is non-zero. If we encounter an element with a higher position, then the element we are looking is not in the sparse matrix. In this case, the element's value is zero. For example, when traversing the list for Row 7 in the matrix of Figure 12.7, we first reach the element at Row 7 and Column 1. If this is what we are looking for, then the search stops. If we are looking for the element at Row 7 and Column 2, then the search proceeds along Row 7 list to reach the element at Column 3. At point we know that no element at Row 7 and 2 is stored in the sparse matrix.

Insertion and deletion can be performed by working in a similar way to insert delete elements within the appropriate row and column lists.

Each non-zero element stored in the sparse matrix representation takes much space than an element stored in a simple $n \times n$ matrix. When is the sparse matrix more efficient than the standard representation? To calculate this, we need to determine how much space the standard matrix requires, and how much