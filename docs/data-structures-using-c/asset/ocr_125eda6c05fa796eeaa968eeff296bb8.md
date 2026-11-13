# RECAPITULATION

+   - Data can be organized in either a linear or a non-linear manner. In linear or sequential organization, all the elements can be arranged in a particular sequence and each element has a unique successor (and/or predecessor) in the sequence.
+   - Linear data organization can be realized using arrays. An array is a very common and simple means of sequential (or linear) data structuring and is supported by almost all programming languages.
+   - Sequential organization allows storing data at a fixed distance apart. If the pth element is stored at location X, then the next sequential ((i+1)th) element is stored at location X + C, where C is a constant.
+   - An array allows direct or random access to any data element of the list at a constant time,

+   that is, O(1) as sequential organization uses continuous memory locations to store its data. The data access time remains constant for accessing any element of the list, irrespective of the total length or size of the data list.
+   - For in-between insertions or deletions of elements, we need to perform data shifting to keep the organization consistent and intact, which is expensive with respect to time.
+   - When data is organized in multiple dimensions, a one-dimensional array proves to be insufficient, and we need two-dimensional, three-dimensional, or multidimensional arrays. A multidimensional array is an extension of a two-dimensional array to three, four, or more dimensions.
+   - Arrays are efficiently used for matrix, polynomial, and string operations.

# KEY TERMS

+   **Array** An array is a finite ordered collection of homogeneous data elements that provides direct access (or random access) to any of its elements.
+   **Linear and non-linear data structure** In linear (or sequential) organization, all the elements can be arranged in a particular sequence, and each element has a unique successor (and/or predecessor) in the sequence. When each element may have one or more successors (or predecessors), it is called a non-linear data structure.
+   **Memory representation of array** A computer's memory can be well thought-out as one long list of bits grouped together into bytes and/or words. Each of them can be referred to as just location to avoid machine-dependent details about whether memory is structured with a one-byte, two-byte, or an n-byte word. In addition, the addressing scheme such as byte addressable or word addressable varies.
+   **Memory representation of two-dimensional arrays** Let us consider a two-dimensional array A

+   of dimension m x n. Though the array is multi-dimensional, it is usually stored in memory as a single-dimensional array. A multidimensional array is represented in memory as a sequence of m x n consecutive memory locations. The elements of a multidimensional array can be stored in memory as a row-major representation or a column-major representation.
+   **Sequential organization** Sequential organization allows storing data at a fixed distance apart. If the pth element is stored at location X, then the next sequential ((i+1)th) element is stored at location X + C, where C is a constant.
+   **Sparse matrix** In many situations, the matrix size is very large but out of it, most of the elements are 0s (not necessarily always 0s). Only a small fraction of the matrix is actually used. A matrix of such a type is called a sparse matrix, as the matrix is filled sparsely by data and most of the positions are empty or contain non-relevant data.