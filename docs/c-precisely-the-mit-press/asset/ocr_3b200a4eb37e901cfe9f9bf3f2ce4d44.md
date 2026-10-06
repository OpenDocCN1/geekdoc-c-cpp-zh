# Example 36 Creating Dimensional Arrays

This example shows two ways (r1, r2) to create the rectangular array and three ways (t1, t2, t3) to create the jagged array in section 9.2. One cannot create a jagged array in one operation (as in t4).

```
double[], r1 = { 0.0, 0.1 }, { 1.0, 1.1 }, { 2.0, 2.1 };
double[], r2 = new double[3,2];
for (int i=0; i<3; i++)
  for (int j=0; j<2; j++)
    r2[i,j] = i + 0.1 * j;
```

```
double[][] row0 = { 0.0 }, row1 = { 1.0, 1.1 }, row2 = { 2.0, 2.1, 2.2 };
double[][] t1 = { row0, row1, row2 };
double[][] t2 = { new double[0], new double[1], new double[2.0, 2.1, 2.2] };
double[][] t3 = new double[3]; // Creates first-dimension array
for (int i=0; i<3; i++)
  t3[i] = new double[i+1]; // Creates second-dimension array
  for (int j=0; j<=i; j++)
    t3[i,j] = i + 0.1 * j;
double[][] t4 = new double[3][]; // Illegal array creation
```

# Example 39 Using Multidimensional Arrays

To store the exchange rate between U.S. dollars and euros (SUS per euro) for every day in the years 2000–2009 using an array rate of type double[][]; a two-dimensional rectangular array of one-dimensional arrays with element type. The array[y,m] holds the exchange rate for year y+2000, month m+1, day d+1. The array of type double[][][] is used because each of the ten years has 12 months (rectangular), but not all months have the same number of days (jagged).

```
double[][][] rate = new double[10][12];
rate[0, 0] = new double[31]; // Jan 2000 has 31 days
rate[1, 0] = new double[29]; // Feb 2000 has 29 days
rate[2, 0] = new double[31]; // Mar 2000 has 31 days
rate[3, 0] = new double[30]; // Apr 2000 has 30 days
rate[4, 0] = new double[31]; // May 2000 has 31 days
...
```

```
rate[0,1][27] = 0.3748; // 28 Feb 2000
rate[0,1][28] = 0.9722; // 29 Feb 2000
rate[0,2][0] = 0.9651; // 1 Mar 2000
```

```
for (int y=0; y<rate.GetLength(); y++)
  for (int m=0; m<rate[y].GetLength(); m++)
    if (rate[y,m] != null)
      for (int d=0; d<rate[y,m].Length; d++)
        if (rate[y,m][d] > 0)
          Console.WriteLine("{0:D4}-{1:D2}-{2:D2}: {3:F4} SUS/euro",
            y+2000, m+1, d+1, rate[y,m][d]);
```