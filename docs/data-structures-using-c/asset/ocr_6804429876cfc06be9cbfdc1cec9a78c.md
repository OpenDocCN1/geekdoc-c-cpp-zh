```
```cpp
<< "<t><leaf[r[1][r[1][rr] - 1]].name;
if (r[r[1][rr]][rr] == 0)
cout << "\nright child of"<< leaf[r[1][rr]].name
<< "<t><leaf[r[1][rr]][rr]].name;
print(1, r[1][rr] - 1);
print(r[1][rr], rr);
}

void print_tab()
{
cout << "\noutput:\n";
cout << "----------------------------------------";
cout << "\n";
for(i = 0; i < n; i++)
cout << "w" << i << i << "=" << w[i][i] << "\n";
for(i = 0; i < n; i++)
cout << "w" << i << i << "=" << c[i][i] << "\n";
for(i = 0; i < n; i++)
cout << "w" << i << i << "=" << r[i][i] << "\n";
cout << "----------------------------------------\n";
k = 1;
while(k <= n)
{
for(i = 0, j = i + k; i < n, j <= n; i++, j++)
cout << "w" << i << j << "=" << w[i][j] << "\n";
for(i = 0, j = i + k; i < n, j <= n; i++, j++)
cout << "c" << i << j << "=" << c[i][j] << "\n";
for(i = 0, j = i + k; i < n, j <= n; i++, j++)
cout << "R" << i << j << "=" << r[i][j] << "\n";
cout << "----------------------------------------\n";
k++;
}
cout << "\nOBST:c[0][n]<w[0][n]<leaf[r[0][n]]
.name";
cout << "\nOBST:c[0][%d] = %0.2f w[0][%d] = %0.2f
r[0][%d] = %s, n, c[0][n], n, w[0][n], n, leaf[r[0]
[n]].name");
}
```
```