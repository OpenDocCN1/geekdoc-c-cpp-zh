# 54 SAS Programming with Medicare Administrative Data

Recall that we have been asked to evaluate the 2010 outcomes of a pilot program to incentivize providers to reduce costs and improve quality. In order to do so, we will compute simple measures of payment, utilization, and quality outcomes for those providers that interacted with the beneficiaries in our sample population. The pilot program operated for the full year of 2010. Although a population of providers (and associated beneficiaries) participating in the pilot program was chosen at the outset of the demonstration, we have been asked to perform analyses only on those beneficiaries who were continuously enrolled in Medicare Fee-for-Service (FFS) throughout twelve months of 2010. Therefore, we must write and execute SAS code that delim our population to those beneficiaries continuously enrolled in Medicare FFS throughout twelve months of year 2010.¹1 In subsequent chapters we will also use this file to delimit our year 2010 claims data. We will then develop algorithms that will query the data to produce summaries of payment, utility, and quality. Given this, we will use the MBSF data to do the following:

+   * Identify beneficiaries continuously enrolled in Medicare FFS throughout twelve months of year 2010, and use this information to delimit our 2010 MBSF data set to continuously enrolled beneficiaries.
* Create or obtain elements for displaying the following beneficiary characteristics:
    * Medicare coverage characteristics in 2010
    * Sex
    * Age groups (less than 65, 65-74, 75-84, 85-94, and 95 and older)
    * Beneficiary geographic information, defined by Social Security Administration (SSA) state and county codes, along with the corresponding state and county names
* Create a file of beneficiary enrollment and demographic information distilled from the MBSF data for 2010 that we will use for the remainder of our programming for our research project. This file will be at the beneficiary level, with one record per beneficiary.

# Review and Approach

# Basics of Medicare Enrollment Data

In Chapter 2 through 5, we discussed the following characteristics of Medicare enrollment, the Master Beneficiary Summary File, and programming with Medicare administrative data:

+   * The majority of Medicare beneficiaries are eligible for Medicare insurance because they are aged 65 and over. However, under certain circumstances, Medicare also includes beneficiaries who are permanently disabled or ESRD or ALS.
* Beneficiaries can enroll in Medicare Parts A and B Medicare Part C. Parts A and B are FFS programs, while Medicare Part C is a managed care program (Medicare Advantage).
* Medicare Part C permits Medicare beneficiaries to enroll in a managed care organization instead of participating in traditional Medicare FFS. Medicare Part A pays for care that is provided in an institutional setting, like inpatient hospitals. Medicare Part B helps pay for care that is