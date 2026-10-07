
## Chapter 5: Predefined Packages

- 5.1 Introduction ................................................................................ 69
- 5.2 Executing FCMP Functions in DS2.................................................................. 71
- 5.2.1 The FCMP Package......................................................................................... 71
- 5.2.2 FCMP Package Example............................................................................... 71
- 5.3 The Hash and Hiter (Hash Iterator) Packages............................................... 76
- 5.3.1 General........................................................................................................... 76
- 5.3.2 Hash Package Example............................................................................... 76
- 5.3.3 Hash Iterator Package Example............................................................... 79
- 5.4 The HTTP and JSON Packages....................................................................... 81
- 5.4.1 General........................................................................................................... 81
- 5.4.2 HTTP Package Specifics............................................................................... 82
- 5.4.3 JSON Package Specifics............................................................................... 85
- 5.4.4 HTTP and JSON Packages Example....................................................... 89
- 5.5 The Matrix Package.................................................................................... 94
- 5.5.1 General........................................................................................................... 94
- 5.5.2 Matrix Package Example........................................................................... 97
- 5.6 The SQLSTMT Package............................................................................... 98
- 5.6.1 General........................................................................................................... 98
- 5.6.2 SQLSTMT Package Example............................................................... 101
- 5.7 The TZ (Time Zone) Package.............................................................. 106
- 5.7.1 General........................................................................................................... 107
- 5.7.2 TZ Package Example............................................................................... 107
- 5.8 Review of Key Concepts............................................................................... 108

### 5.1 Introduction

Chapter 4 introduced the concept of DS2 packages and how they can be used to extend the DS2 language and object-oriented architecture design. It should come as no surprise that the developers at SAS would choose packages as a means of providing new capabilities in DS2, especially when these capabilities are used as objects. Although each predefined DS2 package provides powerful new techniques for processing data, the packages available in your SAS session will depend on the release you are using, as shown in Table 5.1. In this chapter, we will delve into all of the predefined packages that are shipped with DS2 in the SAS 9.4M3 release.

### Table 5.1: DS2 Predefined Packages by SAS Release

| Package | SAS Release | Purpose |
| :--- | :--- | :--- |
| FCMP | SAS 9.4 M0 | Allows calling FCMP functions and subroutines from a DS2 program. |
| Hash | SAS 9.4 M0 | Enables you to use hash objects in your DS2 programs. Hash objects enable you to quickly and efficiently store, search, and retrieve data based on lookup keys. Hash records can also be easily manipulated, sorted, and saved to a table within a DS2 program. |
| Hiter | SAS 9.4 M0 | Enables you to conduct iterative processing of the associated hash object in your DS2 program. You must declare the hash before declaring the associated hiter. |
| HTTP | SAS 9.4 M2 | Provides an HTTP client with methods that allow you to access HTTP web services and capture the returned results in a DS2 program. |
| JSON | SAS 9.4 M3 | Provides the methods necessary to parse and write JSON text and is quite handy for decoding results returned by the HTTP package. |
| Logger | SAS 9.4 M0 | Provides methods to detect which SAS logging facility message levels are active in the current SAS session and to write messages at user-selected levels. This package is pretty simple to use but it does not currently produce output when operating in client/server mode. Therefore, it is not useful when programming in SAS Studio or SAS Enterprise Guide. For these reasons, there will not be a logger section in this book, but it is mentioned here so that we do not forget it exists. |
| Matrix | SAS 9.4 M0 | Implements SAS/IM capabilities in DS2, providing powerful and flexible matrix programming tools. No licensing over Base SAS is required to use the matrix package. |
| SQLSTMT | SAS 9.4 M0 | Provides methods for passing a dynamic FedSQL statement to a database for execution and for accessing any result rows produced without using a SET statement. |
| TZ | SAS 9.4 M3 | Provides methods for facilitating the processing of local time and date values in a DS2 program. |

### 5.2 Executing FCMP Functions in DS2

#### 5.2.1 The FCMP Package

The SAS Compiler procedure (PROC FCMP) enables you to create SAS functions and CALL routines that can be used in other SAS or DATA steps. PROC FCMP builds custom functions using DATA step-like syntax and stores the results in a data set. With the SAS data set, FCMP functions are grouped into “packages” of related functions. These FCMP packages should not be confused with DS2 packages. A FCMP package is a subset of the functions stored in a single data set containing custom methods and data types. When stored in a permanent SAS library, FCMP functions are easily reusable in SAS programs as if they were native functions. After specifying the CMPLIB option to identify the FCMP data set, you can use FCMP functions in your SAS code as if they were native. FCMP functions are an excellent means of standardizing and encapsulating programming methodologies across an enterprise, and mature SAS shops who have invested significant time and effort in building them. PROC FCMP provides an easy, one-time means of creating a wrapper for an existing data set. The wrapper package can subsequently be used to execute FCMP functions transparently from a DS2 program. Modifications to FCMP functions are immediately reflected through DS2 without additional maintenance.

Let’s build a couple of custom functions using PROC FCMP and use them in a DS2 program, and then to check whether the modifications are automatically reflected in our DS2 program. 

### 5.2.2 FCMP Package Example

#### 5.2.2.1 Creating Custom Functions with PROC FCMP

The following FCMP step builds user-defined functions:

```sas
proc fcmp outlib=crs.fcmp_functions;
function ourGMP(GS, Cog);
  /* Gross Margin */
  return ((GS-Cog)/GS);
endsub;
function forBE(GS, Fix, Units);
  /* Break Even (Units) */
  return (ceil(Fix/(GS/Units)));
endsub;
quit;
```

A curious person (like me!) would be tempted to see what is inside the data set created by PROC FCMP. The data set contains variables that indicate the names of the functions, sequence, and so on, and a Variable that contains the source code required for FCMP to execute your function. By default, none of this information is encrypted. Having the data set, our next task is to use our new functions in a traditional SAS DATA step. We will set the CMPLIB system option to point to the SAS data containing the FCMP functions, then we will use the functions in our code as if they were native:

```sas
options cmplib=crs.fcmp_functions;

data work.underperforming_base;
  set crs.Sales_2014;
  /* This code uses the OBE function */
  breakEven=ourOBE(GrossSales,CostOfGoods,Fixed,Units);
  if breakEven > units;
  /* This code uses the custom GMP function */
  GrossMargin=ourGMP(GrossSales,CostOfGoods);
  NetRevenue=GrossSales-CostOfGoods-Fixed;
  format GrossMargin percent.7.1 NetRevenue dollar12.2;
  label Units ='Units Sold'
        Product ID='Product ID'
        GrossMargin='Gross Margin %'
        BreakEven='Break Even (Units)'
        NetRevenue='Net Revenue'
        Fixed Costs='Fixed Costs';
run;

title "Underperforming Sales Items - Base SAS Data Step";
proc print data=work.underperforming_base labels;
var SupplierName ProductName Product_ID Units BreakEven;
var GrossSales CostOfGoods GrossMargin NetRevenue;
run;
title;
```

Figure 5.1: Report Produced Using FCMP Functions in Traditional SAS Processing Underperforming Sales Items - Base SAS Data Step

| SupplierName | ProductName | Product ID | Units | GrossSales | CostOfGoods | Fixed | Gross Margin | NetRevenue |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Carolina Sports | Bat-5Py | 24040200003 | 10000 | 1065 | $80,600.00 | $44,197.2 | 51.6% | -$2,597.20 |
| Nautilus SportsWear Inc | Capsy Hood | 24010100031 | 5000 | 7083 | $24,050.00 | $8,450.00 | 22,098.6 | 64.9% | -$6,498.60 |
| Top Sports Inc | Baseball White Small | 24070200007 | 5000 | 5862 | $33,150.00 | $14,300.00 | 22,098.6 | 56.9% | -$3,248.60 |
| Van Dammermanen Tee | Tee Holder | 24020100021 | 5000 | 11333 | $17,750.00 | $7,800.00 | 22,098.6 | 55.6% | -$12,348.60 |
