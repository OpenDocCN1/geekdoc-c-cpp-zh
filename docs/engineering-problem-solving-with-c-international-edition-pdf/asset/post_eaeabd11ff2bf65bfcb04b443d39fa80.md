
Table 7.2 contains a list of the twelve strongest hurricanes to hit the U.S. during the period 1950 to 2002. (You will find it interesting to obtain more details on these hurricanes using the Internet.)

| Hurricane | Year | Category |
|---|---|---|
| Hazel | 1954 | 4 |
| Audrey | 1957 | 4 |
| Donna | 1960 | 4 |
| Carla | 1961 | 4 |
| Camille | 1969 | 5 |
| Celia | 1970 | 3 |
| Frederic | 1979 | 3 |
| Allen | 1980 | 3 |
| Gloria | 1985 | 3 |
| Hugo | 1989 | 4 |
| Andrew | 1992 | 5 |
| Opal | 1995 | 3 |

Each year there are over 100 storms with the potential to become hurricanes. Write a program that will read a data file containing information on the current storms that consists of an identification number and the highest wind speed (in miles per hour, or mph) measured so far in the storm. The program should print a list of all storms that have wind speeds high enough to make them a hurricane. In addition to the identification number (an integer), also print the peak wind speed and the corresponding hurricane intensity category. Also, print an asterisk after the identification number of the hurricane with the largest wind speed.

### 1. PROBLEM STATEMENT

Determine the storms that are hurricanes using a data file of current storm information.

### 2. INPUT/OUTPUT DESCRIPTION

The I/O diagram shows the data file as the input and the hurricane information as output.

![](img/f2bfa570e453b020c16e048c79a3ea0e_341_0.png)

### 3. HAND EXAMPLE

Assume that the data file contained the following five sets of data:

| Identification | Peak Wind |
|---|---|
| 142 | 38 |
| 153 | 135 |
| 162 | 59 |
| 177 | 76 |
| 181 | 63 |

The corresponding output would then be the following report:

| Storms that Qualify as Hurricanes |
|---|
| Identification | Peak Wind (mph) | Category |
|---|---|---|
| 153* | 135 | 4 |
| 177 | 76 | 1 |

Recall that the asterisk identifies the storm with the largest wind speed.

### 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline because it divides the solution into a series of sequential steps. To print the information for storms that are hurricanes, we do not need an array. We could do that as we read through the file, since the hurricane status is dependent only on the wind speed. However, since we also need to use an asterisk to indicate the storm with the peak wind, we will need to store all the information in arrays. After we have determined the maximum, we can then go back through the data printing the hurricane information with the asterisk for the maximum wind speed.

#### Decomposition Outline

- 1. Read the storm data into arrays, and determine the maximum wind speed.
- 2. Compute the intensity categories and print information for storms that are hurricanes, with an asterisk at the maximum.

We will put the steps that determine the intensity category into a function.

#### Refinement in Pseudocode

```
main: if file cannot be opened
          print error message
else
          read data into arrays, and determine max speed, npts
          set k to 0
          while k < npts-1
            if mph[k] > 74
              if mph[k] = max speed
                print id[k], *, mph[k], category(mph[k])
              else
                print id[k], mph[k], category(mph[k])
            add 1 to k

category(mph):
    category = 1;
    if mph ≥ 96
        category = 2
    if mph ≥ 111
        category = 3
    if mph ≥ 131
        category = 4
    if mph ≥ 155
        category = 5
```

The steps in the pseudocode are now detailed enough to convert into C++.

```cpp
/*
* Program chapter7_5
*/
/* This program reads storm values from a data file */
#include<iostream> //Required for cin, cout, cerr.
#include<fstream> //Required for fin.
using namespace std;
//Function Prototypes.
double category(double speed);
int main()
{
    //Declare and initialize variables.
    const int MAX_SIZE = 500;
    int k(0), npts, id[MAX_SIZE];
    double mph[MAX_SIZE], max(0);
    ifstream fin("storm1.txt");
    if(fin.fail())
    {
        cerr << "Could not open file storm1.txt" << endl;
        exit(1);
    }
    //Read data and determine maximum mph.
    fin >> id[k] >> mph[k];
    while(!fin.fail())
    {
        if(mph[k] > max)
            max = mph[k];
        ++k;
        fin >> id[k] >> mph[k];
    } //end while
    npts = k;

    //Print hurricane report.
    if(max >= 74)
    {
        cout << "Storms that Qualify as Hurricanes \n"
        << "Identification\t Peak Wind(mph)\t Category\n";
    }
    else
    {
        cout << "No hurricanes in the file \n";
    }
    for(k=0; k<npts; ++k)
    {
        if(mph[k] >= 74)
        {
            if(mph[k] == max)
            {
                cout << "\n" << id[k] << "\t" << mph[k] << "\t"
                << category(mph[k]) << endl;
            }
            else
            {
                cout << "\t" << id[k] << "\t" << mph[k] << "\t"
                << category(mph[k]) << endl;
            }
        } //end if k
    } //end for
    fin.close();
    return 0;
}
/******************************************************************/
/* This function determines the hurricane intensity */
/* category. */

double category(double speed)
{
    //Declare variables.
    int intensity(1);

    //Determine category.
    if(speed >= 155)
    {
        intensity=5;
    }
    else if(speed >= 131)
    {
        intensity = 4;
    }
    else if(speed >= 111)
    {
        intensity = 3;
    }
    else if(speed >= 96)
    {
        intensity = 2;
    }
    return intensity;
}
/*...........................................*/
```

### 5. TESTING

We start testing with a file containing the hand example, which gives the following interaction:

| Identification | Peak Wind (mph) | Category |
|---|---|---|
| 153* | 135 | 4 |
| 177 | 76 | 1 |

#### Modify!

These problems relate to the program developed in this section for printing a hurricane intensity report.

- 1. Modify the program so that it only prints the information for the hurricane with the largest wind speed.
- 2. Modify the program so that it also prints the number of storms from the data file.
- 3. Modify the program so that it also prints the number of hurricanes from the data file.
- 4. Modify the program so that it prints the number of hurricanes in each category at the end of the report.
- 5. Modify the program so that it generates a new data file containing information on each hurricane, along with its intensity.

## 7.3 Statistical Measurements

Analyzing data collected from engineering experiments is an important part of evaluating the experiments. This analysis ranges from simple computations on the data, such as calculating the average value, to more complicated analysis. Many of the computations or measurements using data are **statistical measurements** because they have statistical properties that change from one set of data to another. For example, the sine of 60 degrees is an exact value that is the same value every time we compute it, but the number of miles to the gallon that we get with our car is a statistical measurement because it varies somewhat, depending on parameters such as the temperature, the speed that we travel, the type of road, and whether we are in the mountains or the desert.

### Simple Analysis

When evaluating a set of experimental data, we often compute the maximum value, minimum value, **mean** or average value, and the **median**. In this section, we develop functions that can be used to compute these values using an array as input. These functions (stored in a file `stat_lib.cpp`) will be useful in many of the programs that we develop later in the text and in solutions to problems at the end of the chapters. It is important to note that the functions assume that there is at least one value in the array. The functions also assume that the array contains `double` values.

#### Maximum, Minimum.

A function for determining the maximum value in an array was presented in the previous section; a similar function for determining the minimum value is presented here:

```cpp
/*-------------------------------------------------------------*/
/* This function returns the minimum                           */
/* value in an array x with n elements.                        */
/*-------------------------------------------------------------*/

double minval(const double x[], int n)
{
   // Declare objects.
   double min_x;

   // Determine minimum value in the array.
   min_x = x[0];
   for (int k=1; k<n-1; ++k)
   {
      if (x[k] < min_x)
         min_x = x[k];
   }

   // Return minimum value.
   return min_x;
}
/*-------------------------------------------------------------*/
```
