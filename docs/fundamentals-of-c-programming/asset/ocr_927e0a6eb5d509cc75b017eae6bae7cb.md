```
int result = 0;
for (int elem : v)
    result += elem;
return result;
}

int main() {
  std::vector<int> list{ 2, 4, 6, 8, };
  // Print the contents of the vector
  print(list);
  // Compute and display sum
  std::cout << sum(list) << '\n';
  // Zero out all the elements of list
  for (int i = 0; i < list.size(); i++)
    list[i] = 0;
  // Reprint the contents of the vector
  print(list);
  // Compute and display sum
  std::cout << sum(list) << '\n';
}
```

Listing 11.7 (vectorfunc0.cpp) produces

```
2 4 6 8
20
0 0 0 0
0
```

The print function's definition:

```
void print(std::vector<int> v) {
```

shows that a vector formal parameter is declared just like a non-vector formal parameter. In this case, the print function uses pass by value, so during the program's execution an invocation of print will copy the data in the actual parameter (list) to the formal parameter (v). Since a vector potentially can be quite large, it generally is inefficient to pass a vector by value as shown above. Pass by value requires a function invocation to create a new vector object for the formal parameter and copy all the elements of the actual parameter into the new vector which is local to the function. A better approach uses pass by reference, with a twist:

```
void print(const std::vector<int>& v) {
  for (int elem : v)
    std::cout << elem << " ";
  std::cout << '\n';
}
```

The & symbol indicates that a caller invoking print will pass v by reference (see Section 10.9). This copies the address of the actual parameter (owned by the caller) to the formal parameter v instead of making a copy of all the data in the caller's vector. Passing the address is much more efficient because on most systems an address is the same size as a single int, whereas a vector could, for example, contain 1,000,000 ints. With pass by value a function invocation would have to copy all those 1,000,000 integers from the caller's actual parameter into the function's formal parameter.