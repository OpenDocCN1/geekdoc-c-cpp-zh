# C.15.12

Define a structure of type country with members: name, capital, and population. Assume that the names are less than 100 characters. Suppose that a text file contains the data of several countries. The first line contains the number of countries and the following lines store the data of each country in the form:

name capital population

Write a program that reads the name of the file and uses the country type to store the countries' data in a dynamically allocated memory. Then, the program should read a number and display the countries with higher population than this number.

```
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

typedef struct
{
    char name[100];
    char capital[100];
    int pop;
} country;

int main(void)
{
    FILE *fp;
    country *cntr;
    char str[100];
    int i, num_cntr, pop;
    printf("Enter file name: ");
    read_text(str, sizeof(str), 1);
    fp = fopen(str, "r");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    if(fscanf(fp, "%d", &num_cntr) != 1)
    {
        fclose(fp);
        printf("Error: fscanf() failed\n");
        exit(EXIT_FAILURE);
    }
    /* Dynamic memory allocation to store the countries' data. */
    cntr = (country*) malloc(num_cntr * sizeof(country));
    if(cntr == NULL)
    {
        fclose(fp);
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
```
```