
/* Read and print information from the file. */
storms = fopen(FILENAME,"r");
if (storms == NULL)
    printf("Error opening data file. \n");
else
{
    while (fscanf(storms,"%s %d %d",h1.name,&h1.year,
        &h1.category) == 3)
    print_hurricane(h1);
}
fclose (storms);
/* Exit program. */
return 0;
}

/*-----------------------------------------------------*/
/* This function prints the hurricane information.     */
/*-----------------------------------------------------*/
void print_hurricane(struct hurricane h)
{
    printf("Hurricane: %s \n",h.name);
    printf("Year: %d, Category: %d \n",h.year,h.category);
    return;
}
/*-----------------------------------------------------*/

When functions are written to modify the value of a data member within a structure, we must use a pointer to the structure as the function argument. This allows the function direct access to the data members of the structure. When data members are accessed via a pointer to the structure, the pointer operator (->) is used instead of the structure member operator. This technique is demonstrated in Section 7.6, where we present dynamic data structures.

## Functions that Return Structures

A function can be defined to return a value of type struct. After the function is called, an entire structure is returned to the calling function. To illustrate, we present a new structure that relates to tsunamis. Assume that we are working with information related to a tsunami. The information includes the date (month, day, year) of the tsunami, its maximum height in feet, the number of fatalities, and the location. The month, day, year, and number of fatalities are represented by integers, a floating-point number represents the maximum height, and the location is represented by a character string. Thus, a structure to represent the information could be defined as follows:

```
struct tsunami
{
    int mo, da, yr, fatalities;
    double max_height;
    char location[20];
};
```

We now present a function that reads information entered from the keyboard, saves it in the structure, and then returns the information to the main function. Assume that the preceding structure is defined in the main function and that a function prototype is defined with the following statement:

```
struct tsunami get_info(void);
```

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

- MODIFY!
- 1. Write a function that reads the user's information for a variable of the structure type hurricane.
- 2. Write a function that prints the tsunami information from a variable of the structure type tsunami.

## 7.3 Problem Solving Applied: Fingerprint Analysis

In this section, we use the new statements presented in this chapter to solve a problem related to fingerprint analysis. Fingerprints can be divided into three categories: loops, whorls, and arches. Approximately 60% to 65% of all fingerprints are loops; approximately 30% to 35% are whorls, and approximately 5% are arches. In order to reduce the number of fingerprints in a database that need to be matched to an unknown fingerprint, we can eliminate matches to fingers that do not have the same category. For example, there is no need to match a fingerprint that is a whorl to a fingerprint that is an arch. In fact, there have been some techniques developed that can look at the categories of all 10 fingers and immediately eliminate much of a database from comparison. These techniques are roughly based on the Henry technique, one of the early methods for doing fingerprint recognition.

Assume that the technique that we are going to implement assigns a number to a fingerprint record with 10 fingers. We are going to assign a number to each fingertip based on whether or not it is a whorl. The fingertips will be identified as R (for right) or L (for left). In addition, a second letter will identify the finger as t (for thumb), i (for index), m (for middle), r (for ring), and p (for pinky, or little finger). The value for each fingertip is assigned as below:

- If Rt or Ri is a whorl, its value is 16.
- If Rm or Ri is a whorl, its value is 8.
- If Rp or Lt is a whorl, its value is 4.
- If Li or Lm is a whorl, its value is 2.

All other values are zero.

We now compute the following fraction:

```
overall category = (Ri + Rr + Lt + Lm + Lp + 1)/
(Rt + Rm + Rp + Li + Lr + 1)
```

Note that this category cannot be 0, and the denominator cannot be 0. When this category is computed, it is then stored in the record with the fingerprints. Once the category of the unknown fingerprint is computed, then there is a small range of categories that could match from the database. Thus, a search for a match only need to compare a few thousands fingerprints instead of many millions. This search would then compare the details of the minutiae points of the unknown to the minutiae points of the fingerprints with an overall category value close to the unknown's overall category value.

In this section, we will develop a C function that receives the set of information on a fingerprint that is stored in a structure. We will compute the overall category of the fingerprint and store that in the structure. Thus, this function could be used to assign the overall category number to an unknown, or it could be used in a loop to compute the overall category numbers for the fingerprints in a database.

![](img/02c4582f051c5b51776411c92b079035_365_0.png)

### 1. PROBLEM STATEMENT

Write a function that will compute the overall category number for a fingerprint.

### 2. INPUT/OUTPUT DESCRIPTION

The following diagram shows that the inputs to the program are the categories for the 10 fingerprints. The output is the overall category computed from this information.

![](img/02c4582f051c5b51776411c92b079035_365_1.png)

### 3. HAND EXAMPLE

Assume that the whorls from a 10-print occur in the right thumb, right ring finger, and left middle finger. The values of the individual fingers are all 0, with these exceptions:

- Rt = 16
- Rr = 8
- Lm = 2

If we then compute the overall category, we have:

overall category = (8 + 2 + 1)/(16 + 1) = 11/17 = 0.65

### 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline because it divides the solution into a set of sequential steps.

### Decomposition Outline for function

1. Get the fingerprint data from the function inputs.
2. Compute the overall category from the fingerprint information.
3. Store the overall category in the fingerprint structure.

We will also need to develop a program that can be used to test this function. The decomposition outline for the test program is the following:

### Decomposition Outline for the test program

1. Read fingerprint information from the user.
2. Use function to compute the overall category.
3. Print the overall category.

These are straightforward algorithms, so we can go directly to the C code from the decomposition outlines.

```
/*----------------------------------------------------------*/
/* Program chapter7_4                                     */
/*                                                        */
/* This program stores fingerprint information in a structure. */
/* It then references a function to compute the overall category.*/

#include <stdio.h>

/* Define a structure for the fingerprint information.    */
/* The order for fingertips is right hand, thumb to pinky,  */
/* and left hand, thumb to pinky. The codes are L for loops, */
/* W for whorls, and A for arches.                          */
struct fingerprint
{
    int ID_number;
    double overall_category;
    char fingertip[10];
};

int main(void)
{
    /* Declare and initialize variables.                   */
    struct fingerprint new_print;
    double compute_category(struct fingerprint f);
