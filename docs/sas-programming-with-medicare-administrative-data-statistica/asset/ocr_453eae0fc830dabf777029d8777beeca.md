# Chapter 5: Request, Receive, Load, and Transform Data

move the data from compressed, encrypted files to flat files, and from flat files to SAS datasets. Planning ahead to ensure that we have the appropriate amount of storage allocated for our project is important. We listed the LIBNames we will use for this project in Chapter 4. As a reminder, we will load the raw data received from CMS's data distribution contractor (or as any other source data) into a library nicknamed SRC. We will transform this data and save it to a library nicknamed ETL.

After loading claims and enrollment data into SAS data sets, we have the following files stored in our library with the alias SRC:

+   - Carrier base claim and line level files (SRC.CARRIER2010CLAIM and SRC.CARRIER2010LINE, respectively)
- DME base claim and line level files (SRC.DME2010CLAIM and SRC.DME2010LINE, respectively)
- Inpatient base claim and claim line files (SRC.IP2010CLAIM and SRC.IP2010LINE, respectively)
- Skilled Nursing Facility base claim and revenue center files (SRC.SNF2010CLAIM and SRC.SNF2010LINE, respectively)
- Outpatient base claim and revenue center files (SRC.OP2010CLAIM and SRC.OP2010LINE, respectively)
- Home health base claim and revenue center files (SRC.HH2010CLAIM and SRC.HH2010LINE, respectively)
- Hospice base claim and revenue center files (SRC.HS2010CLAIM and SRC.HS2010LINE, respectively)
- Master Beneficiary Summary File enrollment data (SRC.MBSF_AB_2010)
- Social Security Administration (SSA) state and county codes, and corresponding state and county names (one on this in Chapter 6)

The above data sets are available on the book's website (http://support.sas.com/publishing/authors/gillingham.html) and represent the starting point for our programming work. Note that the file names and variable names we may differ from those provided by CMS's data distribution contractor.

# Algorithms: Transforming Base Claim and Line Level Data Sets into Single Claim-Level Files

Let's start our programming at the point after we have loaded the data we received from CMS's data distribution contractor into SAS data sets saved in the library with the alias SRC (again, we will not program the actual loading of the data because the data distribution contractor provides the programs for that task). At this point, we have base claim and revenue center level SAS sets for each institutional claim type. In addition, we have base claim and line level SAS sets for each non-institutional claim