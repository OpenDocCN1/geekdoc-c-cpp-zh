```
```cpp
cout << "\t<q[i]";
OBST();
print_tab();
print(0, n);
}

void OBST()
{
for(i = 0; i < n; i++)
{
r[i][i] = c[i][i] = 0; w[i][i] = q[i];
w[i][i + 1] = p[i + 1] + q[i + 1] + w[i][i];
c[i][i + 1] = w[i][i + 1];
r[i][i + 1] = i + 1;
}
c[n][n] = 0.0; r[n][n] = 0.0; w[n][n] = q[n];
for(i = 2; i <= n; i++)
{
for(j = 0; j <= n - i; j++)
{
w[j][j + i] = w[j][j + i - 1] + p[j + i] + q[j
+ i];
c[j][j + i] = 999;
for(k = j + 1; k < j + i; k++)
if(c[j][j + i] > c[j][k - 1] + c[k][j + i])
{
c[j][j + i] = c[j][k - 1] + c[k][j + i];
r[j][j + i] = k;
}
c[j][j+i]+=w[j][j+i];
}
}
}

void print(int l, int rr)
{
if(l >= rr) return;
if(r[l][r[l][rr]] - 1] == 0)
cout << "\nleft child of "<leaf[r[l][rr]].name
```
```