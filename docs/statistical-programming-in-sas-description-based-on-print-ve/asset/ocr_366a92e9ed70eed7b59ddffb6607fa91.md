# Display 2.38 Table comparing merges of data sets using the DATA step with joins of data sets using PROC SQL

| Location of CITY | DATA Step | PROC SQL |
|---|---|---|
| Either in the weather or demography data set | data in_either;
merge
  SMSA_subset_weather2 (in=in1)
  SMSA_subset_demog2 (in=in2);
by city;
weather2_in = in1;
demog2_in = in2;
run; | proc sql;
title "FULL OUTER JOIN";
select coalesce(w.city, d.city),
  JanTemp, JulyTemp, Education, income
from
  SMSA_subset_weather2 as w
full join
  SMSA_subset_demog2 as d
on w.city=d.city;
quit; |
| In both the weather and demography data sets | data in_both;
set in_either;
if weather2_in=1 and demog2_in=1;
run; | proc sql;
title "INNER JOIN";
select
  w.city, JanTemp, JulyTemp, Education, income
from
  SMSA_subset_weather2 as w,
  SMSA_subset_demog2 as d
where
  w.city=d.city;
quit; |
| In weather data set | data in_weather;
set in_either;
if weather2_in=1;
run; | proc sql;
title "LEFT OUTER JOIN";
select coalesce(w.city, d.city),
  JanTemp, JulyTemp, Education, income
from
  SMSA_subset_weather2 as w
left join
  SMSA_subset_demog2 as d
on w.city=d.city;
quit; |
| In demography data set | data in_demog;
set in_either;
if demog2_in=1;
run; | proc sql;
title "RIGHT OUTER JOIN";
select coalesce(w.city, d.city),
  JanTemp, JulyTemp, Education, income
from
  SMSA_subset_weather2 as w
right join
  SMSA_subset_demog2 as d
on w.city=d.city;
quit; |

From this table, you can see that an inner join is equivalent to a merge that requires observations to be in both data sets. A full outer join is equivalent to the default merge in which observations are included if they are in either or both of the data sets. The left or right outer join is equivalent to a merge with specified restrictions about whether an observation is included from the first or second data set in a merge.

There are times when you are interested in the complete Cartesian product of the observations in two data sets (i.e., all rows from one data set paired with all rows from another data set). Consider a toy example in which you want to enumerate the sample