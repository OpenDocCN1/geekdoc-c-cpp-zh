We will use a function that interacts with the user to get the information and then returns it in a structure. The code is as follows:

```
/*----------------------------------------------------------*/
/* This function gets information from the user to enter    */
/* into a tsunami structure.                                */
/*----------------------------------------------------------*/
struct tsunami get_info(void)
{
    /* Declare variables.    */
    struct tsunami t1;

    printf("Enter information for tsunami in following order: \n\n");
    printf("Enter month, day, year, number of deaths: \n");
    scanf("%d %d %d",&t1.mo,&t1.da,&t1.yr,&t1.fatalities);
    printf("Enter location (<20 characters, no spaces): \n");
    scanf("%s",t1.location);
    return(t1);
}
/*----------------------------------------------------------*/
```

+   MODIFY!
+   
+   1. Write a function that reads the user's information for a variable of the structure type hurricane.
+   2. Write a function that prints the tsunami information from a variable of the structure type tsunami.

# 7.3 Problem Solving Applied: Fingerprint Analysis

In this section, we use the new statements presented in this chapter to solve a problem related to fingerprint analysis. Fingerprints can be divided into three categories: loops, whorls, and arches. Approximately 60% to 65% of all fingerprints are loops; approximately 30% to 35% are whorls, and approximately 5% are arches. In order to reduce the number of fingerprints in a database that need to be matched to an unknown fingerprint, we can eliminate matches to fingers that do not have the same category. For example, there is no need to match a fingerprint that is a whorl to a fingerprint that is an arch. In fact, there have been some techniques developed that can look at the categories of all 10 fingers and immediately eliminate much of a database from comparison. These techniques are roughly based on the Henry technique, one of the early methods for doing fingerprint recognition.

Assume that the technique that we are going to implement assigns a number to a fingerprint record with 10 fingers. We are going to assign a number to each fingertip based on whether or not it is a whorl. The fingertips will be identified as R (for right) or L (for left). In addition, a second letter will identify the finger as r (for thumb), i (for index), m (for middle),