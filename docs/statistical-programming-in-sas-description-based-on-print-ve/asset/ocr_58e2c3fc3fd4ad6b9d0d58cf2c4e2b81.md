# *** comment 5

This is a common option that I use in programs. ODS RTF requests the RTF output destination. BODYTITLE includes any title in the body of the RTF file, versus just including a title if it is part of the header information. These options make copying and pasting information into another document easier. A specific file location is provided in this output.

# *** comment 6

The next four PROC PRINT statements display the results of merging the data with various criteria. The first PROC PRINT is for cities in either data set. The second is for cities in both data sets. The third is for cities in the weather data set (first data set). The fourth is for cities in the demography data set (second data set).

The data sets are displayed in Display 2.29. The first data set is the result of the merge operation. The second data set is the result of selecting whether a city was in both data sets. The third data set is the result of selecting cities in the weather data set. The fourth data set is the result of selecting cities in the demography data set. Variables indicating whether the city was in the weather data set or the demography data set are displayed. Two variables from the weather data set (JANTEMP and RAIN) and two variables from the demography data set (MORTALITY and INCOME) are also displayed.

# Display 2.29 PROC PRINT of the data sets created from merging two data sets with a subset of common observations

# city in either weather or demography data set or in both data sets

| Obs | city | weather2_in | demog2_in | JanTemp | Rain | Mortality | income |
|---|---|---|---|---|---|---|---|
| 1 | Akron, OH | 1 | 1 | 27 | 36 | 921.87 | 29560 |
| 2 | Albany-Schenectady-Troy, NY | 0 | 1 | . | . | 997.87 | 31458 |
| 3 | Allentown, Bethlehem, PA-NJ | 1 | 1 | 29 | 44 | 962.35 | 31856 |
| 4 | Atlanta, GA | 1 | 0 | 45 | 47 | . | . |
| 5 | Baltimore, MD | 1 | 1 | 35 | 43 | 1071.29 | 32368 |