# 5. TESTING

We will test our program with a file containing the hand example. This produces the following interaction:

```
Storms that Qualify as Hurricanes
Identification   Peak Wind (mph)   Category
153*             135               4
177              76                1
```

# MODIFY!

These problems relate to the preceding program for printing a hurricane intensity report.

+   1. Modify the program so that it only prints the information for the hurricane with the largest wind speed.
+   2. Modify the program so that it also prints the number of storms from the data file.
+   3. Modify the program so that it also prints the number of hurricanes from the data file.
+   4. Modify the program so that it prints the number of hurricanes in each category.

# 5.3 Problem Solving Applied: Molecular Weights

Chemical reactions play an important role in many scientific and engineering systems. Understanding and controlling chemical reactions allows petroleum engineers to improve the efficiency of the refineries necessary to process oil and gas resources. Understanding the behavior and reactions of fully ionized gases at very high temperatures under the influence of strong magnetic fields will be an important step in developing controlled nuclear fusion. In genetic engineering, the identification of amino acids in DNA is a key step in developing techniques to synthesize new products.

Computing the molecular weight from a chemical formula is a common task in any application that involves chemical reactions. Write a program that reads a chemical formula from the keyboard and then computes the corresponding molecular weight. We will assume that this program will be used in a genetic engineering laboratory working with the amino acids in proteins. Amino acids contain only atoms of oxygen (O), carbon (C), nitrogen (N), sulfur (S), and hydrogen (H). For example, the chemical formula for alanine is C3N1H7; thus, alanine contains two atoms of oxygen, three atoms of carbon, one atom of nitrogen, and seven atoms of hydrogen. (Table 5.3 contains the atoms in amino acids.) The input to the program is a set of characters that specifies the chemical formula. The valid characters are the abbreviations O, C, N, S, and H, and we will allow these characters to be either uppercase or lowercase. One or two digits that specify the number of atoms in the element may also follow each element. Thus, the input characters for alanine could include O2C3NH7 or o2c3nh7. Errors occur if the element is not one of the five specified elements or if the formula begins with a number. Use the following molecular weights:

| oxygen | 15.9994 | sulfur | 32.066 |
| carbon | 12.011 | hydrogen | 1.00794 |
| nitrogen | 14.00674 | | |