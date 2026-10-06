# Chapter 7: Measuring Utilization of Services

# Algorithms: Measuring Inpatient Hospital Utilization

Our inpatient data are at the claim level, not the stay level. An inpatient stay can be comprised of many claims. CMS offers a stay-level file, with these claims collapsed to a single stay record, but we did not request this data. On past projects, I have been responsible for the complicated process of writing specifications to convert inpatient claims into stay-level records. Luckily, stays comprised of multiple claims records are not common. Independent, stays comprised of multiple claims comprise only one or two percent of all inpatient claims. Therefore, we will proceed with our discussion of stays as:

+   1. To keep the book at the introductory level, we will identify and keep only those claims in our inpatient data set for acute short-stay hospitals (more on below).

+   2. We will treat our inpatient claims as stays and ignore the fact that we have a very small number of hospital stays in our inpatient data that are comprised of multiple claims. We will also ignore that some records represent transfers to others. (See the Exercises below for a question on how to collapse multiple claims into a single record.) We use these claims to calculate the number of inpatient stays, the length of each stay, and the average length for a beneficiary.

In First, 7.5, we focus on delimiting our population to acute short-stay hospitals, as well as keeping only those records with non-negative payment amounts. Medicare distinguishes acute short-stay hospitals between Medicare Prospective Payment System (IPPS) and critical access hospitals (CAHs). IPPS hospitals are paid as an inpatient set prospectively (i.e., determined in advance) based on a patient's condition (i.e., diagnosis) and treatment (i.e., procedures). These payments are based on the Medicare Severity-Related Groups (MS-DRGs). CAHs are limited to 25 or fewer beds and primarily operate in rural areas. They are paid on the basis of cost (i.e., We delimit our inpatient claims data set to these acute short-stay hospitals because these are seen as different hospitals like inpatient rehabilitation, long-term care, and inpatient psychiatric facilities (e.g., CMS's Hospital Compare* only reports on acute short-stay hospitals).

```
* STEP 7.5: IDENTIFY AND KEEP ONLY TH CLAIMS FOR STAY HOSPITALS AND NON-NEGATIVE PAYMENTS *
data util_ip_2010_fnl;
  set util_ip_2010_fnl;
  provtype = substr(provider,3,4);
  if ('0001'<=provtype<=0899') or ('1300'<=provtype<=1399') and pmt_>0;
run;
```

How do we define short-stay hospitals? The PROVIDER variable is the identifier for the hospital and it contains embedded intelligence. Specifically, the first two positions of the PROVIDER variable identify the SSA state code for the hospital's location, and the third and fourth positions identify the category of the hospital. We will use this identifier to find IPPS hospitals and CAHs. IPPS hospitals are identified where the substring of the PROVIDER variable, starting at the third position through the sixth position, is equal to 0001 through 0899. CAHs are identified where the

*