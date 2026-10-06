# 56 SAS Programming with Medicare Administrative Data

Medicare FFS for all twelve months of the 2010 calendar year to help ensure that we have an accurate
picture of their claims data during that time.

# How to Specify the Programming for Continuous Enrollment in Medicare
FS

Depending on your project needs, “continuous enrollment” can be defined in many different ways; it is
just a business rule. We will define continuous enrollment as follows: A beneficiary is considered
continuously enrolled in Medicare FFS throughout 2010 if they were alive for the year, did not
have managed care at any point during the year, and were enrolled in Medicare Parts A and B
all year. Accomplishing this task requires understanding and using the following variables in the Master
Beneficiary Summary File, which will be explained in detail in the remainder of this chapter:

+   * Hospital Insurance (Part A) and Supplementary Medical Insurance (Part B) coverage
variables
* HMO coverage variable
* Date of death variable

# Medicare Part A and Part B Enrollment Variables

The Medicare Part A and Part B Enrollment variables (BENE_HI_CVRAGE_TOT_MONS and
BENE_SMI_CVRAGE_TOT_MONS) describe the number of months that a beneficiary is enrolled in
Part A and Part B. These variables are sometimes referred to by the shortened names
A_CNT and MO_CNT. It is important to determine enrollment because services received when
a beneficiary is not enrolled in Medicare Part A or Part B for a period of time are not contained in the
claims files. Therefore, a distorted picture of say, utilization may result in gaps in coverage are allowed.

Checking the data dictionary for the MBSF, we want to keep only beneficiaries with values of 12
each, denoting that the beneficiary was enrolled in Part A and Part B for all 12 months of the
year. We do not want to keep beneficiaries with a value of less than 12 for either
HI_CVRAGE_TOT_MONS variable or the SMI_CVRAGE_TOT_MONS variable because we
stated that we want to retain only those beneficiaries who have been enrolled in both Medicare
Part A and Part B throughout 2010.

# HMO Coverage Variable

The HMO coverage variable (BENE_HMO_CVRAGE_TOT_MONS) describes the number of months
that a beneficiary was enrolled in a managed care plan (also known as a Health Maintenance
Organization, or HMO) during the year. As stated above, Medicare Part C permits Medicare
beneficiaries to enroll in a private managed care plan instead of participating in traditional
Medicare FFS. Generally, the classes of beneficiaries enrolled in these managed care plans do not appear
in the administrative claims data, so we seek to exclude these beneficiaries from our population.
Another quick check of the MBSF data dictionary shows we want to keep only those beneficiaries with a
value of 0 for the BENE_HMO_CVRAGE_TOT_MONS variable.