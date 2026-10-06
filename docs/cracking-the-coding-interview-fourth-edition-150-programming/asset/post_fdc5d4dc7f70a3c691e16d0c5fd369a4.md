
# Solutions to Chapter 1 | Arrays and Strings

##5. String with non-contiguous duplicate, e.g.: abababa
Algorithm—With Additional Memory of Constant Size

```java
public static void removeDuplicatesEff(char[] str) {
    if (str == null) return;
    int len = str.length;
    if (len < 2) return;
    boolean[] hit = new boolean[256];
    for (int i = 0; i < 256; ++i) {
        hit[i] = false;
    }
    hit[str[0]] = true;
    int tail = 1;
    for (int i = 1; i < len; ++i) {
        if (!hit[str[i]]) {
            str[tail] = str[i];
            ++tail;
            hit[str[i]] = true;
        }
    }
    str[tail] = 0;
}
```

## Test Cases:

- 1. String does not contain any duplicates, e.g.: abcd
- 2. String contains all duplicates, e.g.: aaaa
- 3. Null string
- 4. Empty string
- 5. String with all continuous duplicates, e.g.: aaabbb
- 6. String with non-contiguous duplicates, e.g.: abababa

# Solutions to Chapter 1 | Arrays and Strings

## 1.4 Write a method to decide if two strings are anagrams or not.

### SOLUTION

There are two easy ways to solve this problem:

Solution #1:Sort the strings

```java
boolean anagram(String s, String t) {
    return sort(s) == sort(t);
}
```

Solution #2:Check if the two strings have identical counts for each unique char.

```java
public static boolean anagram(String s, String t) {
    if (s.length() != t.length()) return false;
    int[] letters = new int[256];
    int num_unique_chars = 0;
    int num_completed_t = 0;
    char[] s_array = s.toCharArray(); // count number of each char in s.
    for (char c : s_array) {
        if (letters[c] == 0) ++num_unique_chars;
        ++letters[c];
    }
    for (int i = 0; i < t.length(); i++) {
        int c = (int) t.charAt(i);
        if (letters[c] == 0) { // Found more of char c in t than s.
            return false;
        }
        --letters[c];
        if (letters[c] == 0) {
            ++num_completed_t;
            if (num_completed_t == num_unique_chars) {
                // it's a match if t has been processed completely
                return i == t.length() - 1;
            }
        }
    }
    return false;
}
```

# Solutions to Chapter 1 | Arrays and Strings

## 1.5 Write a method to replace all spaces in a string with '%20'.

### SOLUTION

The algorithm is as follows:

- 1. Count the number of spaces during the first scan of the string.
- 2. Parse the string again from the end and for each character:
   - If a space is encountered, store "%20"
   - Else, store the character as it is in the newly shifted location.

```java
public static void ReplaceFun(char[] str, int length) {
    int spaceCount = 0, newLength, i = 0;
    for (i = 0; i < length; i++) {
        if (str[i] == ' ') {
            spaceCount++;
        }
    }
    newLength = length + spaceCount * 2;
    str[newLength - 1] = '\0';
    for (i = length - 1; i >= 0; i--) {
        if (str[i] == ' ') {
            str[newLength - 1] = '0';
            str[newLength - 2] = '2';
            str[newLength - 3] = '%';
            newLength = newLength - 3;
        } else {
            str[newLength - 1] = str[i];
            newLength = newLength - 1;
        }
    }
}
```

![](img/50974dc108b2978cf2cacf9397df9934_106_0.png)

# Solutions to Chapter 1 | Arrays and Strings

## 1.6 Given an image represented by an NxN matrix, where each pixel in the image is 4 bytes, write a method to rotate the image by 90 degrees. Can you do this in place?

### SOLUTION

The rotation can be performed in layers, where you perform a cyclic swap on the edges on each layer. We rotate the first layer (outermost edges). We rotate the edges by doing a four-way swap first on the corners, then on the element clockwise from the edges, then on the element three steps away.

Once the exterior elements are rotated, we then rotate the interior region's edges.

```java
public static void rotate(int[][] matrix, int n) {
    for (int layer = 0; layer < n / 2; ++layer) {
        int first = layer;
        int last = n - 1 - layer;
        for (int i = first; i < last; ++i) {
            int offset = i - first;
            int top = matrix[first][i]; // save top
            // left -> top
            matrix[first][i] = matrix[last - offset][first];
            // right -> bottom
            matrix[last - offset][first] = matrix[last][last];
            // ... (logic continues for full rotation)
        }
    }
}
```

# Solutions to Chapter 1 | Arrays and Strings

## 1.7 Write an algorithm such that if an element in an Nx matrix is 0, its entire row and column is set to 0.

### SOLUTION

At first glance, this problem seems easy: just iterate through the matrix and every time we see a 0, set that row and column to 0. There’s one problem with that though: we will recognize those 0s later on in our iteration and set the entire matrix will be set to 0.

One way around this is to keep a second matrix which flags the 0 locations. We would then do a second pass through the matrix to set zeros. This would take O(MN) space.

Do we really need O(MN) space? No. Since we're going to set the entire row and column to zero, we only need to know which cell, for example, has a zero.

The code below implements this. We keep track in two arrays all the rows and columns with zeros.

```java
public static void setZeros(int[][] matrix) {
  int[] row = new int[matrix.length];
  int[] column = new int[matrix[0].length];
  // Store the row and column index with 0
  for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[0].length; j++) {
      if (matrix[i][j] == 0) {
        row[i] = 1;
        column[j] = 1;
      }
    }
  }
  // Set matrix[i][j] to 0 if either row i or column j has 1
  for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[0].length; j++) {
      if (row[i] == 1 || column[j] == 1) {
        matrix[i][j] = 0;
      }
    }
  }
}
```

# Solutions to Chapter 1 | Arrays and Strings

## 1.8 Assume you have a method isSubstring which checks if one word is substring of another. Given two strings, s1 and s2, write code to check if s2 is a rotation of s1 using only one call to isSubstring (i.e., "waterbottle" is a rotation of "bottlewat").

### SOLUTION

Just do the following checks

- 1. Check if length(s1) == length(s2). If not, return false.
- 2. Else, concatenate s1 with itself and see whether s2 is substring of the result.
  input: s1 = apple, s2 = pleap => apple is a substring of pleapple
  input: s1 = apple, s2 = pale => apple is not a substring of paleapple

```java
public static boolean isRotation(String s1, String s2) {
    int len = s1.length();
    /* check that s1 and s2 are equal length and not empty */
    if (len == s2.length() && len > 0) {
        /* concatenate s1 and s1 within buffer */
        String s1s1 = s1 + s1;
        return isSubstring(s1s1, s2);
    }
    return false;
}
```

# Solutions to Chapter 2 | Linked Lists

## 2.1 Write code to remove duplicates from an unsorted linked list.

### FOLLOW UP
How would you solve this problem if a temporary buffer is not allowed?

### SOLUTION

If we use a buffer, we can keep track of elements in a hashtable and remove any dups:

```java
public static void deleteDups(ListNode n) {
    Hashtable table = new Hashtable();
    ListNode previous = null;
    while (n != null) {
        if (table.containsKey(n.data)) previous.next = n.next;
        else {
            table.put(n.data, true);
            previous = n;
        }
        n = n.next;
    }
}
```

Without a buffer, we can iterate with two pointers: "current" does a normal iteration, while "runner" iterates through all prior nodes to check for dups. Runner will only see one dup per node, because if there were multiple duplicates they would have been removed already.

```java
public static void deleteDups2(ListNode head) {
    if (head == null) return;
    ListNode previous = head;
    ListNode current = head.next;
    while (current != null) {
        ListNode runner = head;
        while (runner != current) { // Check for earlier dups
            if (runner.data == current.data) {
                ListNode tmp = current.next; // remove current
                current.next = tmp;
                previous = tmp;
                current = tmp; // update current to next node
                break; // all other dups have already been removed
            }
            runner = runner.next;
        }
        if (runner == current) { // current not updated - update now
            previous = current;
            current = current.next;
        }
    }
}
```
```
