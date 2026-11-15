# Each vegetation map includes:

+   * station code (character string)
+   * date (character string)
+   * sample radius size (miles)
+   * name of each plant (string)
+   * number of vegetation samples (integer)
+   * vegetation sample data (one sample per line)

Sample data from a vegetation map is shown below:

```
SC-DC
7/10/2014
0.5
BLUEFLAX
COLUMBINE
PENSTEMON
ALPINE-SUNFLOWER
AVALANCE-LILLY
4
39.4642 -106.0490 3058 120 27 103 51 75
39.7607 -105.0141 1596 73 17 92 40 32
38.8339 -104.8214 1831 103 14 43 45 29
39.5792 -105.9347 3487 131 20 76 49 38
```

Our C++ solution will input all data from the vegetation map and generate a report on below average vegetation samples.

We see from a hand example that the average Columbine population is (27+17+14+20)/4 or 19.5. The second vegetation sample has a Columbine population of 17. This sample is (1 - 17/19.5)*100 or 12.8% below average. A full report is provided below.

```
SC-DC
7/10/2014
Samples taken within a 0.5 mile radius
Below average plant samples occurred in the following geographical locations:
Lat:39.7607
Long:-105.014
Elevation:1596
BLUEFLAX: 31.6159% below average
COLUMBINE: 12.8205% below average
ALPINE-SUN: 13.5135% below average
AVALANCE-LILY: 26.4368% below average
```