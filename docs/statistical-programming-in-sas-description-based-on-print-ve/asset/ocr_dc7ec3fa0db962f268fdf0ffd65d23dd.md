# Display 2.29 (continued)

# city in both weather and demography data sets

| Obs | City | weather2_in | demog2_in | JanTemp | Rain | Mortality | income |
|---|---|---|---|---|---|---|---|
| 1 | Akron, OH | 1 | 1 | 27 | 36 | 921.87 | 29560 |
| 2 | Allentown, Bethlehem, PA-NJ | 1 | 1 | 29 | 44 | 962.35 | 31856 |
| 3 | Baltimore, MD | 1 | 1 | 35 | 43 | 1071.29 | 32368 |

# city in weather data set

| Obs | City | weather2_in | demog2_in | JanTemp | Rain | Mortality | income |
|---|---|---|---|---|---|---|---|
| 1 | Akron, OH | 1 | 1 | 27 | 36 | 921.87 | 29560 |
| 2 | Allentown, Bethlehem, PA-NJ | 1 | 1 | 29 | 44 | 962.35 | 31856 |
| 3 | Atlanta, GA | 1 | 0 | 45 | 47 | . | . |
| 4 | Baltimore, MD | 1 | 1 | 35 | 43 | 1071.29 | 32368 |

# city in demography data set

| Obs | City | weather2_in | demog2_in | JanTemp | Rain | Mortality | income |
|---|---|---|---|---|---|---|---|
| 1 | Akron, OH | 1 | 1 | 27 | 36 | 921.87 | 29560 |
| 2 | Albany-Schenectady-Troy, NY | 0 | 1 | . | . | 997.87 | 31458 |
| 3 | Allentown, Bethlehem, PA-NJ | 1 | 1 | 29 | 44 | 962.35 | 31856 |
| 4 | Baltimore, MD | 1 | 1 | 35 | 43 | 1071.29 | 32368 |

# 2.6 Database Processing with PROC SQL

As an alternative to DATA step manipulation, the SAS implementation of a structured query language in PROC SQL might be a better alternative. (This is above and beyond the obvious applications of querying a data table and constructing summary tables.) In fact, programmers who come to SAS with a broad exposure to database programming