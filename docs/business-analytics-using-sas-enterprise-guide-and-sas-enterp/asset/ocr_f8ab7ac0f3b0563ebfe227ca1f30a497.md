# Input the Data Source and Assign Variable Roles

Next, double click on the Data Sources icon (upper left-hand menu, directly under the word *Actions*). The Data Import Wizard will open, asking you to create a SAS Table (Figure 7.4).

**Figure 7.4: Locate Data Source**

![](bbox=[0.141, 0.252, 0.663, 0.473])

Click **Next** ▶ and browse for the DMR_CUSTOMER_BASE data set created in Chapter 3. Once you locate the data, select the data and click **OK**, then click **Next** ▶. The next window shows a summary. Click **Next** ▶. For Meta Data Advisory options, click **Advanced** and **Next** ▶. A window appears that displays the variable characteristics and offers options for exploring the distributions (Figure 7.5).

**Figure 7.5: Assign Variable Roles and Explore Variables**

![](bbox=[0.141, 0.631, 0.795, 0.825])

First, you need to change the role of CUSTOMER_REVENUE and CUSTOMER_SUBSCRIPTION_COUNT to “Rejected.” These are outcome variables that will be used in future chapters. But for now, you do not want to include them in your analysis.