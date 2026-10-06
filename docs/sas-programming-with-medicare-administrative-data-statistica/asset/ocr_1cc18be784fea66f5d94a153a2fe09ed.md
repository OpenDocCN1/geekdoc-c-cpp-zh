# Chapter 10: Presenting Output and Project Disposition 125

of the work that we performed in Chapter 6 to add state and county names to our file of continuously enrolled beneficiaries.

The algorithms that we will develop in the chapter are by no means exhaustive, and we do not endeavor to summarize all of the analyses that we computed in prior chapters. We could think of many, additional ways of looking at the output we created. For example, we could present analyses of outcomes that are broken out by provider specialty; we could compare the measurements for the population of providers in our finder against other providers that did not participate in the program we are studying; or we could compare results over time to look for significant changes in outcomes. The purpose of this text is to lay the groundwork for the reader to be able to independently answer these questions. Therefore, one of the chapter exercises listed below asks you to think of some additional questions we might answer with our data.

# Algorithms: Presenting Selected Measurements of Utilization, Cost to Medicare, and Quality Outcomes

Let's start by simply displaying the following pieces of our utilization, cost to Medicare, and quality outcomes of the work that we performed in Chapter 7 through Chapter 9, respectively:

+   - Drawing on our work in Chapter 7, we will present ambulance utilization information by beneficiary age.
- Drawing on our work in Chapter 8, we will present Medicare payments for E&M services summarized by the providers in our study population.
- Drawing on our work in Chapter 9, we will present rates of diabetes and COPD in our population of continuously enrolled beneficiaries.

Again, we have easily chosen to present other information that we calculated in previous chapters, like the total costs to Medicare that were associated with home health agency services. One of the chapter exercises listed below asks you to choose and present information that was calculated in Chapter 7, 8, or Chapter 9 other than what we chose as an example for our work in this section.

# Presenting Ambulance Utilization

One interesting presenting of output is to examine beneficiaries with at least one claim for ambulance services, along with the age of each beneficiary. This type of algorithm provides a good example for analyzing relevant summary information that may be used to guide further analyses.

In Step 10.1, we begin to present ambulance utilization by our merge of continuously enrolled beneficiaries (ENR_CONTENT_2010_FNL) with the analytic summary file UTL_AMB_UTIL created in Step 7.11 of Chapter 7 (we are also in our formatting of age categories that you will recognize from our work in Chapter 6). The file UTL_AMB_UTIL contains one record per beneficiary with at least one claim for an ambulance service. Because both files are already sorted by BENE_ID, there is no need for a pre-merge sort. The output file, called FNL_PRESENT_AMB, contains one record for each of the beneficiaries in UTL_AMB_UTIL (we use an “if” merge), as well