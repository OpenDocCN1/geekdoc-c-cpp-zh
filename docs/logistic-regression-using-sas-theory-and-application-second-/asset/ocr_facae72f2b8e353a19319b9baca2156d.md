Although it’s usually desirable to adjust for matching in the analysis, the appropriate adjustment methods are quite different for treatment-control and case-control matching. In brief, there are several ways to do it for treatment-control matching, but there is only one way for case-control matching. Let’s begin with a treatment-control example. Metraux and Culhane (1999) constructed a data set of 8,402 women who stayed in family shelters in New York City for at least one 7-day period during 1992. The data contained information on several pre-stay characteristics, events that occurred during the stay, and housing type subsequent to the stay. As our dependent variable, we’ll focus on whether or not the woman exited to public housing (PUBHOUSE), which was the destination for 48% of the sample. Our principal independent variable is STAYBABY, equal to 1 if a woman gave birth during her stay at the shelter, and 0 otherwise. Nine percent of the sample had a birth during the stay. Other independent variables are

+   BLACK — 1=black race, 0=nonblack
+   
+   KIDS — Number of children in the household
+   
+   DOUBLEUP — 1=living with another family prior to shelter stay, 0 otherwise
+   
+   AGE — Age of woman at beginning of shelter stay
+   
+   DAYS — Number of days in shelter stay

The conventional approach to analysis would be to estimate a logistic regression model for the entire sample of 8,402 women. Results for doing that with PROC LOGISTIC are shown in Output 8.19. We see that although the odds of exiting to public housing increase with the number of children in the household, a birth during the stay reduces the odds by about 33 percent. Both of these effects are overshadowed by the enormous impact of the length of stay. Each additional day increases the odds of exiting to public housing by about 1%. (Not surprisingly, DAYS also has a correlation of .25 with STAYBABY—the longer a woman’s stay, the more likely it is that she gave birth during the stay.)