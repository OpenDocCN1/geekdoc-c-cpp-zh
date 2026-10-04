```
std::cout << "Enter elements of the second matrix:\\n";
for (int i = 0; i < rows2; i++) {
  for (int j = 0; j < cols2; j++) {
    std::cin >> matrix2[i][j];
  }
}
```

```
// Check for multiplication possibility
if (cols1 != rows2) {
  std::cout << "Matrix multiplication is not possible.";
  return 0;
}
```

```
// Perform multiplication
std::vector<std::vector<double>> result(rows1, std::vector<double>(cols2, 0));
for (int i = 0; i < rows1; i++) {
  for (int j = 0; j < cols2; j++) {
    for (int k = 0; k < cols1; k++) {
      result[i][j] += matrix1[i][k] * matrix2[k][j];
    }
  }
}
```