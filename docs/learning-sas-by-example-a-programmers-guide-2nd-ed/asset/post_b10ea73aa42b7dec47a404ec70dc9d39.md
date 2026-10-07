
# 168 Learning SAS by Example: A Programmer's Guide, Second Edition

Notice that there are missing values for the SQRT and LOG functions when the argument to these functions is a negative value. SAS also prints a note in the log to inform you about this fact.

## 11.8 Computing Some Useful Constants

The CONSTANT function returns values of commonly used mathematical constants such as pi and e. For a SAS programmer, perhaps the most useful feature of this function is its ability to compute the largest integer that can be stored in less than 8 bytes. The next program demonstrates some of the more common uses of this function:

Program 11.8: Computing Some Useful Constants with the CONSTANT Function

```
data Constants;
  Pi = constant('pi');
  e = constant('e');
  Integer3 = constant('exact3');
  Integer4 = constant('exact4');
  Integer5 = constant('exact5');
  Integer6 = constant('exact6');
  Integer7 = constant('exact7');
  Integer8 = constant('exact8');
run;
```

Pi and e are computed as shown. To compute the largest integer stored in n bytes, you provide a second argument indicating the number of bytes. Output from this program is shown as follows:

Figure 11.5: Listing of Data Set Constants

| Pi | e | Integer3 | Integer4 | Integer5 | Integer6 | Integer7 | Integer8 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 3.14159 | 2.71828 | 8192 | 209715 | 536870912 | 137438953472 | 3.5184E13 | 9.0072E15 |

To be the exact feature of this function is clear, if you use a LENGTH statement to set the length of a numeric to 3, the largest integer you can represent without losing accuracy is 8,192; with a length of 4, you can represent integers up to 2,097,152. (These values may vary, depending on your operating system.)

## 11.9 Generating Random Numbers

We will discuss only one of the random numbers here—RAND. This function generates random numbers based on any one of 29 probability distributions. Some of the more commonly used distributions are listed in figure 11.6:

# Chapter 11: Working with Numeric Functions

Figure 11.6: Some of the Commonly Used Probability Distributions

| Distribution | Example | Description |
| :--- | :--- | :--- |
| Uniform | X = rand('uniform'); | Uniform random numbers between 0 and 1 |
| Normal | HR = rand('normal',70,10); | Normally distributed numbers with a mean of 70 and a standard deviation of 10 |
| Bernoulli | Heads = rand('Bernoulli',5); | A Bernoulli distribution with p = .5 (simulates a coin toss) |
| Binomial | N = rand('Binomial',3,10) | The number of "successes" in 10 trials with a probability of .3 |

> Note: The RAND function replaces some of the older random number functions as RANUNI (generates uniform random numbers) and RANNOR (generates normally distributed random numbers).

You may wonder why you ever need to generate random numbers. Some uses are to create data sets for benchmarking, select random samples, and to assign subjects to two or more groups.

Computers do not really generate true random numbers. However, they are capable of generating series of numbers that are very close to random (called pseudo-random numbers by snobs). In order to get the computer started, you need to provide a seed number to generate the first number in the random sequence. If you use the RAND function without a seed with a call streaminit(n) command (where n is an integer, preferably a large one), SAS uses the computer's clock to supply the seed. If you choose any positive integer in the call streaminit, that number is used as a seed. SAS recommends you choose a seed of at least 7 digits. If you supply the seed, the program generates the same sequence of random numbers every time you run the program. Without the call to streaminit, the sequence changes every time you run the program. Hopefully, several examples will make this clear.

As the first example, you want to generate 5 uniform random numbers.

# Program 11.9: Program to Generate Five Uniform Random Numbers

```
data Uniform;
  do i = 1 to 5;
    x = rand('uniform');
    output;
  end;
run;
```

First, notice that this DATA step does not read any data. The DO loop causes the RAND function to execute 5 times and output 5 uniform random numbers. It is important that the OUTPUT statement is placed inside the loop, otherwise the program would only output one random number. Let's run this program once and list the output data set:

# 170 Learning SAS by Example: A Programmer’s Guide, Second Edition

**Figure 11.7: Listing of Data Set Uniform (First Run)**

# Listing of Data Set Uniform

| i | X |
| :--- | :--- |
| 1 | 0.54232 |
| 2 | 0.60610 |
| 3 | 0.87571 |
| 4 | 0.12701 |
| 5 | 0.12907 |

Notice that all the random numbers are between 0 and 1. Let’s run the program again and list the data:

**Figure 11.8: Running Program 11.9 and Listing the Results**

# Listing of Data Set Uniform

| i | X |
| :--- | :--- |
| 1 | 0.88584 |
| 2 | 0.62149 |
| 3 | 0.92060 |
| 4 | 0.08345 |
| 5 | 0.36384 |

Notice that the 5 random numbers are different from the first run. The reason is that you did not include the call to streaminit. Let’s run Program 11.9 twice, but specify a seed value with a call to streaminit:

**Figure 11.10: Including a Call to Streaminit**

```
data Uniform;
call streaminit(1234567);
do i = 1 to 5;
  X = rand('uniform');
  output;
end;
run;
```

# Chapter 11: Working with Numeric Functions 171

# Figure 11.9: Listing of Data Set Uniform with Call Streaminit (First Run)

# Listing of Data Set Uniform

| i | X |
| :--- | :--- |
| 1 | 0.88584 |
| 2 | 0.62149 |
| 3 | 0.92060 |
| 4 | 0.08345 |
| 5 | 0.36384 |

# Figure 11.10: Listing of Data Set Uniform with Call Streaminit (Second Run)

# Listing of Data Set Uniform

| i | X |
| :--- | :--- |
| 1 | 0.88584 |
| 2 | 0.62149 |
| 3 | 0.92060 |
| 4 | 0.08345 |
| 5 | 0.36384 |

Notice that by setting a seed value, the program generates the same random sequence each time. You may wonder why anyone would want to do this? One possible reason is to generate random groupings for a clinical trial. When the trial is over, you will want to be able to generate the exact same assignments, so use the same seed value that you used originally.

Suppose you want to select approximately 10% of the data set. You can use the same random numbers like this:

# Program 11.11: Using the RAND function to randomly select

```
data Subset;
  set Learn.Blood;
  if rand('uniform') <= 1;
run;
```

Because values from a uniform distribution are always between 0 and 1, approximately 10% of these numbers will be less than .1 and the observation will be written out to data set. Here is part of the SAS log after this program was run:

NOTE: There were 1000 observations read from the data set LEARN.BLOOD.

NOTE: The data set WORK.SUBSET has 104 observations and 7 variables.

# 172 Learning SAS as Example: A Programmer's Guide, Second Edition

Notice that the Subset data set is not exactly 10% of the Blood data set. If you need an exact 10% sample, use PROC SURVEYSELECT as shown here.

PROC SURVEYSELECT, which is available in SAS/STAT software, is the best (and most efficient) to create random subsets. This procedure is quite flexible and has many options for generating these subsets. As an example, to obtain a random sample of size 100 from the Blood data set, you could use the following:

Program 11.12: Using SURVEYSELECT to Obtain a Random Sample

```
proc surveyselect data=Learn.Blood
out=Subset
method=srs
samplesize=100;
```

The options DATA= and OUT= are pretty clear. METHOD= allows you to choose a method for selecting your sample (SRS is a simple random sample, a sample taken without replacement). SAMPSIZE allows you to choose the size of the sample. One additional option, which is not used here, is SE=. If you supply a value for this option, this value is used as the seed. Also, if you prefer to select a percentage of the original data set, substitute the option SAMPLE=Percent (where Percent is the proportion of the data set you want to sample) instead of SAMPSIZE=. For more details on this procedure, see the SAS Help Center at http://go.documentation.sas.com.

To generate integers in the range from 1 to 10, you could use:

```
RandomInteger = ceil(random()*10);
```

Remember that the CEIL function rounds up to the next highest integer. For example, suppose that your first random number is almost 0 (remember, it can never be). Ten times 0 is also a small number and the CEIL function returns a number almost equal to 1, ten almost 1 is almost 10. However, the CEIL function will return 10 in this case.

## 11.10 Special Functions

The name specials (a SAS category) makes these functions esoteric. That is from the case. The INPUT and PUT functions, in particular, are extremely useful functions that you will use all the time.

The INPUT function enables you to "read" a character value using a SAS or user-defined informat and assign the resulting value to a SAS numeric variable. One of the most common uses of this function is to perform a character-to-numeric conversion. Another is to convert a date as string to a SAS date. Here is an example.

You are given a SAS data set (Chars) that contains the variables Height, Weight, and Date. All three variables are character variables. You want to create a new set called Null with the same variables, except that they are numeric variables.
