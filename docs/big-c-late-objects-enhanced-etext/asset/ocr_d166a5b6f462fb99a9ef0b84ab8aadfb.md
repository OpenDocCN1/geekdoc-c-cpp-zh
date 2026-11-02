![](bbox=[0.1, 0.16, 0.22, 0.27])

# WORKED EXAMPLE 6.2

# A World Population Table

**Problem Statement** You are to print the following population data in tabular format and add column totals that show the total world populations in the given years.

**Population Per Continent (in millions)**

| Year | 1750 | 1800 | 1850 | 1900 | 1950 | 2000 | 2050 |
|---|---|---|---|---|---|---|---|
| Africa | 106 | 107 | 111 | 133 | 221 | 767 | 1766 |
| Asia | 502 | 635 | 809 | 947 | 1402 | 3634 | 5268 |
| Australia | 2 | 2 | 2 | 6 | 13 | 30 | 46 |
| Europe | 163 | 203 | 276 | 408 | 547 | 729 | 628 |
| North America | 2 | 7 | 26 | 82 | 172 | 307 | 392 |
| South America | 16 | 24 | 38 | 74 | 167 | 511 | 809 |

# Step 1

First, we break down the task into steps:

+   - Initialize the table data.
+   - Print the table.
+   - Compute and print the column totals.

# Step 2

```
Initialize the table as a sequence of rows:

```c
int data[ROWS][COLUMNS] =
{
  { 106, 107, 111, 133, 221, 767, 1766 },
  { 502, 635, 809, 947, 1402, 3634, 5268 },
  { 2, 2, 2, 6, 13, 30, 46 },
  { 163, 203, 276, 408, 547, 729, 628 },
  { 2, 7, 26, 82, 172, 307, 392 },
  { 16, 24, 38, 74, 167, 511, 809 }
};
```
```

# Step 3

To print the row headers, we also need a one-dimensional array of the continent names. Note that it has the same number of rows as our table.

```
```c
string continents[ROWS] =
{
  "Africa",
  "Asia",
  "Australia",
  "Europe",
  "North America",
  "South America"
};
```
```