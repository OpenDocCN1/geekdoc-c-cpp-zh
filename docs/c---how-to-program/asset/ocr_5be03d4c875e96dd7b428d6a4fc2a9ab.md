# Answers to Self-Review Exercises

+   6.1 a) arrays. b) index. c) symbolic constant. d) sorting. e) searching. f) two-dimensional.

+   6.2 a) False. An array can store only values of the same type.
+       b) False. An array index must be an integer or an integer expression.
+       c) False. C automatically initializes the remaining elements to zero.
+       d) True.
+       e) False. Individual elements of an array are passed by value. If the entire array is passed to a function, then any modifications to the elements will be reflected in the original.

+   6.3 a) #define SIZE 10
+       b) double fractions[SIZE] = { 0.0 };
+       c) fractions[4]
+       d) fractions[9] = 1.667;
+       e) fractions[6] = 3.333;
+       f) printf("%.2f %.2f\n", fractions[6], fractions[9]);
+          Output: 3.33 1.67.
+       g) for (x = 0; x < SIZE; ++x) {
+              printf("fractions[%u] = %f\n", x, fractions[x]);
+          }
+          Output:
+          fractions[0] = 0.000000
+          fractions[1] = 0.000000
+          fractions[2] = 0.000000
+          fractions[3] = 0.000000
+          fractions[4] = 0.000000
+          fractions[5] = 0.000000
+          fractions[6] = 3.333000
+          fractions[7] = 0.000000
+          fractions[8] = 0.000000
+          fractions[9] = 1.667000

+   6.4 a) int table[SIZE][SIZE];
+       b) Nine elements. printf("%d\n", SIZE * SIZE);
+       c) for (x = 0; x < SIZE; ++x) {
+              for (y = 0; y < SIZE; ++y) {
+                  table[x][y] = x + y;
+              }
+          }
+       d) for (x = 0; x < SIZE; ++x) {
+              for (y = 0; y < SIZE; ++y) {
+                  printf("table[%d][%d] = %d\n", x, y, table[x][y]);
+              }
+          }
+          Output:
+          table[0][0] = 1
+          table[0][1] = 8
+          table[0][2] = 0
+          table[1][0] = 2
+          table[1][1] = 4
+          table[1][2] = 6
+          table[2][0] = 5
+          table[2][1] = 0
+          table[2][2] = 0