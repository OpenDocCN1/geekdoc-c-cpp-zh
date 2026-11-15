# PRACTICE!

Assume that we have defined the following variables:

```
int k=6;
double data[]={1,5,3.2,-6.1,9,8,8,7,5,2};
```

Using the max function presented in this section, give the value of each of the following expressions:

+   1. max(data, 6);
+   2. max(data, 5);
+   3. max(data, k-3);
+   4. max(data, k%5);

# 5.2 Problem Solving Applied: Hurricane Categories

Hurricanes are tropical storms with very strong winds and heavy rains. (They are called typhoons in the western North Pacific Ocean and cyclones in the Indian Ocean.) These tropical storms, or cyclones, are low-pressure cells that typically form in the summer and early fall. The large rotating air masses are easily seen on satellite images, and the storms are carefully tracked because of the potential for damage in populated areas. If the storm's winds are between 38 and 74 miles per hour, it called a tropical storm; if the winds exceed 74 miles per hour, the storm is a tropical cyclone, or hurricane. The Saffir-Simpson scale defines categories of hurricane intensity based on the wind speed. In this section, we define the Saffir-Simpson scale in more detail, and we then develop a program that reads a data file containing current storms and their peak wind speeds. Finally we will analyze the wind speeds, and we will print a report with information on the storms that are strong enough to be classified as hurricanes.

The Saffir-Simpson scale of hurricane intensities is used to classify hurricanes according to the amount of damage that the storm is likely to generate if it hits a populated area. The main characteristics of the five categories are as follows:

+   Category 1
+   wind speeds of 74 to 95 mph
+   storm surge of 4 to 5 feet
+   minimal damage to property
+   
+   Category 2
+   wind speeds of 96 to 110 mph
+   storm surge of 6 to 8 feet
+   moderate damage to property
+   
+   Category 3
+   wind speeds of 111 to 130 mph
+   storm surge of 9 to 12 feet
+   extensive damage to property
+   
+   Category 4
+   wind speeds of 131 to 155 mph
+   storm surge of 13 to 18 feet
+   extreme damage to property