# 7.2 Problem Solving Applied: Hurricane Categories

Hurricanes are tropical storms with very strong winds and heavy rains. (They are called typhoons in the western North Pacific Ocean, and cyclones in the Indian Ocean.) These tropical storms, or cyclones, are low-pressure cells that typically form in the summer and early fall. The large rotating air masses are easily seen on satellite images, and the storms are carefully tracked because of the potential for damage in populated areas. If the winds in a storm are between 38 and 74 miles per hour, it called a tropical storm; if the wind exceeds 74 miles per hour, the storm is a tropical cyclone, or hurricane. The Saffir-Simpson scale defines categories of hurricane intensity based on the wind speed. In this section, we define the Saffir-Simpson scale in more detail, and we then develop a program that reads a data file containing current storms and their peak wind speeds. Then, based on the wind speeds, we print a report with information on the storms that are strong enough to be classified as hurricanes.

The Saffir-Simpson scale of hurricane intensities is used to classify hurricanes according to the amount of damage that the storm is likely to generate if it hits a populated area. The main characteristics of the five categories are described below:

+   Category 1
+   wind speeds of 74–95 mph
+   storm surge of 4–5 feet
+   minimal damage to property
+   
+   Category 2
+   wind speeds of 96–110 mph
+   storm surge of 6–8 feet
+   moderate damage to property
+   
+   Category 3
+   wind speeds of 111–130 mph
+   storm surge of 9–12 feet
+   extensive damage to property
+   
+   Category 4
+   wind speeds of 131–155 mph
+   storm surge of 13–18 feet
+   extreme damage to property
+   
+   Category 5
+   wind speeds over 155 mph
+   storm surge greater than 18 feet
+   catastrophic damage to property

Table 7.2 contains a list of the twelve strongest hurricanes to hit the U.S. during the period 1950 to 2002. (You will find it interesting to obtain more details on these hurricanes using the Internet.)

Each year there are over 100 storms with the potential to become hurricanes. Write a program that will read a data file containing information on the current storms that consists of an identification number and the highest wind speed (in miles per hour, or mph) measured so far in the storm. The program should print a list of all storms that have wind speeds high enough to make them a hurricane. In addition to the identification number (an integer), also print the peak wind speed and the corresponding hurricane intensity category. Also, print an asterisk after the identification number of the hurricane with the largest wind speed.