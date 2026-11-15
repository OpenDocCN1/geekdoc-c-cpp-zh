38. Write a C++ program to calculate the heat index (HI) using the formula: HI = 0.5 * (T + 61.0 + ((T-68.0)*1.2) + (RH*0.094)), where RH is the relative humidity in percent and T is the temperature in degrees Fahrenheit. Your program should prompt the user for the temperature and relative humidity, and print the heat index. If the calculated heat index is above 80 degrees, your program should recalculate the heat index using the following formula: HI = -42.379 + 2.04901523 * T + 10.14333127 * RH — 22475541 * T * RH — 0.00683783 * T * T — 0.05481717 * RH * RH + 0.00122874 * T * T * RH + 0.00085282 * T * RH * RH — 0.00000199 * T * T * RH * RH and print the second result.

39. Write a C++ program to calculate wind chill and report on frostbite times. Use the following formula: Twc = 35.74 + 0.6215Ta - 35.75V^0.16 + 0.4275TaV^0.16 where Twc is the wind chill index, based on the Fahrenheit scale, Ta is the air temperature, measured in °F, and V is the wind speed, in mph. Prompt the user for required input and print Twc. If the value of Twc is below –19 report a frostbite time of 30 minutes or less. If the value is below –48, report a frostbite time of 5 minutes or less.

40. Modify the program in Problem 38 to print the likelihood of a heat related health disorder given the value of the heat index, HI. Visit the Web site: www.nws.noaa.gov/om/heat/heat_index.shtml for information.

# Point Class

+   41. Determine if three lines can form a triangle. Three lines can form a triangle if the sum of any two lines is greater than the third.

+   42. Determine if a given point lies within a defined rectangle.

+   43. Determine if a given point lies within a defined triangle.