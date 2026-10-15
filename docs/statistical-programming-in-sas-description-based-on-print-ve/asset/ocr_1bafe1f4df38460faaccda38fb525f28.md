# Display 2.36 (continued)

```
/* RIGHT outer join */
title "RIGHT outer join";
    select coalesce(w.city, d.city),JanTemp,JulyTemp,Education,income from
        SMSA_subset_weather2 as w
    right join
        SMSA_subset_demog2 as d
    on w.city=d.city;

/* FULL outer join */
title "FULL outer join";
    select coalesce(w.city, d.city),JanTemp,JulyTemp,Education,income from
        SMSA_subset_weather2 as w
    full join
        SMSA_subset_demog2 as d
    on w.city=d.city;
quit;
ods rtf close;
```

# Display 2.37 Results from inner join, left outer join, right outer join, and full outer join

# inner join

| city | JanTemp | JulyTemp | Education | Income |
|---|---|---|---|---|
| Akron, OH | 27 | 71 | 11.4 | 29560 |
| Baltimore, MD | 35 | 77 | 9.6 | 32368 |
| Allentown, Bethlehem, PA-NJ | 29 | 74 | 9.8 | 31856 |

# left outer join with duplicate columns
(edited with columns deleted)

| city | JanTemp | JulyTemp | Rain | city | Mortality | Education | income |
|---|---|---|---|---|---|---|---|
| Akron, OH | 27 | 71 | 36 | Akron, OH | 921.87 | 11.4 | 29560 |
| Allentown, Bethlehem, PA-NJ | 29 | 74 | 44 | Allentown, Bethlehem, PA-NJ | 962.35 | 9.8 | 31856 |
| Atlanta, GA | 45 | 79 | 47 |  | . | . | . |
| Baltimore, MD | 35 | 77 | 43 | Baltimore, MD | 1071.29 | 9.6 | 32368 |