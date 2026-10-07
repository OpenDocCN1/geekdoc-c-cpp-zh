# DATA STRUCTURES IN C++

```
int main() {
vector<vector<int> > v, v1;
int rows = 3, ncols = 2;
v.resize(rows);
for(int i = 0; i < rows; i++){
  v[i].resize(ncols);
  for(int j = 0; j < ncols; j++) {
    v[i][j] = (i + 1)*(j + 1);
  }
}

 v1.assign(v.begin() + 2, v.end());
printVec(v1, "v1");
vector<vector<int> > v2(v);
printVec(v2, "v2");

return 0;
}
```

```
void printVec(vector<vector<int>> > v
```

The main function creates a vector<vector<int>> object that is then populated with six integers in three rows and two columns. The begin() iterator is incremented by two in an application of assign which will have the consequence that only the last row of the vector v will be copied into the object v1. Next, the constructor is used to copy all of v to a new object v2. This copying is printed to standard output using a utility function printVec created for that purpose. The program produces

The number of rows in v1 is 1
The length of row 0 is 2
v1[0][0] = 3 v1[0][1] = 6
The number of rows in v2 is 3
The length of row 0 is 2
v2[0][0] = 1 v2[0][1] = 2
The length of row 1 is 2
v2[1][0] = 2 v2[1][1] = 4
The length of row 2 is 2
v2[2][0] = 3 v2[2][1] = 6

The output demonstrate that both copying procedures were successful.
The STL container deque is similar to the vector class. The difference is that new elements can be prepended well as appended in constant time. The deque containers become available through the include statement

```
#include <deque>
```