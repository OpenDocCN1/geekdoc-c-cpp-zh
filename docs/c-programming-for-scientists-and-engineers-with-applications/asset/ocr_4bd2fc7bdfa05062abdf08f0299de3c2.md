```
}
for(i = 0; i < n; i++)
{
  for(j = 0; j < m; j++)
    printf("%f ", pressure[i][j]);
  printf("%f\n", rowmax[i]);
}
```

+   4. define IMAX 10
#define JMAX 5

+   a. int main() {
  float temperature[IMAX][JMAX];
  float rowavg[IMAX], colavg[JMAX];
  funcin(temperature);
  funcavg(temperature, rowavg, colavg);
  functout(temperature, rowavg, colavg);
  return: 0;
}

+   void funcin(float temp[][JMAX]) {
  int i, j;
  for(i = 0; i < IMAX, i++)
    for(j = 0; j < JMAX; j++)
      scanf("%f", &temp[i][j]);
  return;
}

+   b. void funcavg(float temp[][JMAX], float rowavg[], float colavg[]) {
  int i, j;
  for(i = 0; i < IMAX; i++)
  {
    rowavg[i] = 0.0;
    for(j = 0; j < JMAX; j++)
      rowavg[i] += temp[i][j];
  }
  rowavg[i] = rowavg[i]/JMAX;
  for(j = 0; j < JMAX; j++)