Similarly, if we reverse the independent and dependent variables, we obtain:

log(m_{i1} / m_{i2}) = β₂ + β₃ R_i.

These results show that the loglinear model for the 2 × 2 table implies two logit models, one for the row variable as dependent on the column variable and the other for the column variable as dependent on the row variable.

# 10.3 Loglinear Models for a Four-Way Table

Now let’s look at a much more complicated table, the 2 × 2 × 4 × 4 table that we previously analyzed by way of a logit model in Section 4.5. Our main goal will be to duplicate the results of the logit model with a loglinear model. To refresh your memory, the sample consisted of 4,991 high school seniors in Wisconsin. The dependent variable was whether or not they planned to attend college in the following year. The three independent variables were coded as follows:

+   IQ        1=low, 2=lower middle, 3=upper middle, 4=high
+   SES       1=low, 2=lower middle, 3=upper middle, 4=high
+   PARENT    1=low parental encouragement, 2= high encouragement

In Section 4.5, the data were read in as 32 records, each record containing a unique combination of values of the independent variables, along with the number of seniors who had those values and the number of those seniors who planned to attend college. Unfortunately, that’s not the format we need for a loglinear analysis. Instead, we need 64 records, one for each cell in the four-way table, with values for all the variables and the frequency count in that cell. Here’s a DATA step that inputs the previous data set (WISC) and outputs the new data set in the appropriate format (WISCTAB).

```
DATA wisctab;
  SET wisc;
  college=1;
  freq=coll;
  OUTPUT;
  college=0;
  freq=total-coll;
  OUTPUT;
  DROP total coll;
PROC PRINT;
RUN;
```