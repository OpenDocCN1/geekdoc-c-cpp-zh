
## 12.5. RANDOMLY PERMUTING A VECTOR

```cpp
/*
 * Returns a pseudorandom number in the range begin...end - 1,
 * inclusive. Returns 0 if begin >= end.
 */
int random(int begin, int end) {
    if (begin >= end)
        return 0;
    else {
        int range = end - begin;
        return begin + rand() % range;
    }
}
/*
 * Randomly permute a vector of integers.
 * a is the vector to permute, and n is its length.
 */
void permute(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // Select the pseudorandom location from the current
        // location to the end of the collection
        swap(a[i], a[random(i, n)]);
    }
}
// Tests the permute function that randomly permutes the
// contents of a vector
int main() {
    // Initialize random generator seed
    srand(static_cast<int>(time(0)));
    // Make the vector {1,2,3,4,5,6,7,8}
    vector<int> vec { 1, 2, 3, 4, 5, 6, 7, 8 };

    // Print vector before
    print(vec);
    cout << endl;

    permute(vec);

    // Print vector after
    print(vec);
    cout << endl;
}
```

One run of Listing 12.8 (randompermute.cpp) produces

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|
| 2 | 7 | 1 | 6 | 4 | 8 | 3 | 5 |

Notice that the permute function in Listing 12.8 (randomperm.cpp) uses a simple un-nested loop and no recursion. The permute function varies the i variable from 0 to the index of the next to last element in the vector. Within the loop, the function obtains by rand a pseudorandom index greater or equal to i. It exchanges the elements at position i and the random position. At this all elements at index i are smaller and will not change; the function's execution continues. The loop increments index i, and the process continues until all i values have been considered.

To be correct, the permute function is able to generate any valid permutation of the vector. It is important that our permute function is able to produce all possible permutations with equal probability; said another way, we do not want our permute function to generate some permutations more often than others. The permute function in Listing 12.8 (randomperm.cpp) is fine, but consider a slight variation of the algorithm.

```cpp
// Randomly permute a vector?
void faulty_permute(vector<int>& a) {
  int n = a.size();
  for (int i = 0; i < n; i++) {
    // Select a pseudorandom position in the vector
    swap(a[i], a[rand(0, n)]);
  }
}
```

Do you see the difference between faulty_permute and permute? The faulty_permute function chooses its random index from all valid indices, whereas permute can exchange any element within a vector at any position during any loop iteration. While this approach may appear to be as good as permute, it in fact creates an uneven distribution of permutations. Listing 12.9 (comparepermutations.cpp) exercises each permutation 1,000,000 times on the vector (1, 2, 3) and totals each permutation. There are exactly six permutations of this three-element vector.

Listing 12.9: comparepermutations.cpp
```cpp
#include <iostream>
#include <vector>
#include <ctime>
#include <cstdlib>

using namespace std;

/*
* prints the contents of an int vector
* a is the vector to print; a is not modified
* is the number of elements in the vector
*/
void print(const vector<int>& a) {
  int n = a.size();
  cout << " ";
  if (n > 0) {
    cout << a[0]; // Print the first element
    for (int i = 1; i < n; i++) {
      cout << ', ' << a[i]; // Print the rest
    }
  }
  cout << endl;
}

/*
* Returns a pseudorandom number in the range begin..end - 1,
* Returns 0 if begin >= end.
*/
int random(int begin, int end) {
    if (begin >= end)
        return 0;
    else {
        int range = end - begin;
        return begin + rand() % range;
    }
}

/*
* Randomly permute a vector of integers.
* a is the vector to permute, and n is its length.
*/
void permute(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // Select a pseudorandom location from the current
        // location to the end of the collection
        swap(a[i], a[random(i, n)]);
    }
}

/*
 * Randomly permute a vector?
 */
void faulty_permute(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n; i++) {
        // Select a pseudorandom position somewhere in the collection
        swap(a[i], a[random(0, n)]);
    }
}

/*
 Classify a vector as one of the six permutations */
int classify(const vector<int>& a) {
    switch (100*a[0] + 10*a[1] + a[2]) {
        case 123: return 0;
        case 132: return 1;
        case 213: return 2;
        case 231: return 3;
        case 312: return 4;
        case 321: return 5;
    }
    return -1;
}

/* Report the accumulated statistics */
void report(const vector<int>& a) {
    cout << "1,2,3: " << a[0] << endl;
    cout << "1,3,2: " << a[1] << endl;
    cout << "2,1,3: " << a[2] << endl;
    cout << "2,3,1: " << a[3] << endl;
    cout << "3,1,2: " << a[4] << endl;
    cout << "3,2,1: " << a[5] << endl;
}

/*
 // Fill the vector with zeros.
 // a is the vector, and n is its length.
 */
void clear(vector<int>& a) {
  int n = a.size();
  for (int i = 0; i < n; i++)
    a[i] = 0;
}

int main() {
    // Initialize random generator seed
    srand(static_cast<int>(time(0)));

    // permutation tally keeps track of each permutation pattern
    // permutation_tally[0] counts (1,2,3)
    // permutation_tally[1] counts (1,3,2)
    // permutation_tally[2] counts (2,1,3)
    // permutation_tally[3] counts (2,3,1)
    // permutation_tally[4] counts (3,1,2)
    // permutation_tally[5] counts (3,2,1)
    vector<int> permutation_tally(0, 0, 0, 0, 0, 0);

    // original always holds the vector (1,2,3)
    const vector<int> original (1, 2, 3);

    // working holds a copy of original gets permuted and tallied
    vector<int> working;

    // Run each permutation one million times
    const int RUNS = 1000000;

    cout << "---- Random permutation #1 ----" << endl;
    clear(permutation_tally);
    for (int i = 0; i < RUNS; i++) { // Run 1,000,000 times
        // Make a copy of the original vector
        working = original;
        // Permute the vector with the first algorithm
        permute(working);
        // Count this permutation
        permutation_tally[classify(working)]++;
    }
    report(permutation_tally);   // Report results

    cout << "---- Random permutation #2 ----" << endl;
    clear(permutation_tally);
    for (int i = 0; i < RUNS; i++) { // Run 1,000,000 times
        // Make a copy of the original vector
        working = original;
        // Permute the vector with the second algorithm
        faulty_permute(working);
        // Count this permutation
        permutation_tally[classify(working)]++;
    }
    report(permutation_tally); // Report results
}
```

In Listing 12.9 (comparepermutations.cpp)'s output, output #1 corresponds to our permute function, and output #2 is the faulty_permute function. The output of Listing 12.9 (comparepermutations) reveals the faulty permutation function favors some permutations over others:

```
Random permute #1
1,2,3: 166608
1,3,2: 166820
2,1,3: 166350
2,3,1: 166702
3,1,2: 166489
3,2,1: 167031
Random permute #2
1,2,3: 168517
1,3,2: 184756
2,1,3: 185246
2,3,1: 185225
3,1,2: 148476
3,2,1: 147980
```

In one million runs, the permute function provides an even distribution of the six permutations ({1, 2, 3}, {2, 1, 3}, and {2, 3, 1}) more often than the permutations ({1, 2, 3}, {3, 1, 2}, and {3, 2, 1}).

To see why faulty_permute misbehaves, we need to examine all the permutations that it can produce during one call. Figure 12.5 shows a hierarchical structure that maps out how faulty_permute transforms the contents of its vector parameter for each for loop. The top of the tree shows

![](img/e326304bd50fbc4f7d5a64c1487eb635_346_0.png)

Figure 12.5: A tree mapping out the ways in which faulty_permute can transform the vector 1, 2, 3 at each iteration of its loop

original vector, {1, 2, 3}.
