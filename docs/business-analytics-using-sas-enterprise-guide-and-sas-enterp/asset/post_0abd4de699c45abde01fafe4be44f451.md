
Because whole books on SAS Enterprise Guide basics are available, this book focuses on what is required for typical marketing analysis. For an excellent general reference, see *The Little SAS Book for Enterprise Guide* by Lora D. Delwiche and Susan J. Slaughter (2010).

## Exploratory Analysis

First, import the spreadsheet that contains the customer data.

### Importing the Data

Depending on your systems and storage, you may want to seek help from your IT department for access to the data. In our example, the DMR Publishing customer data is stored in the SASUSER library in the form of a Microsoft Excel spreadsheet. As shown in Figure 5.2, click **File > Import Data**. When the input data window opens, click the up arrow to browse to the folder in which the spreadsheet, DMR Customer Base, is stored. Highlight the spreadsheet and click **Open**.

**Figure 5.2: Import Data into SAS Enterprise Guide**

![](img/976d9b992e82c4ac7d195d03a30b4915_77_0.png)

A menu will open to allow you to manage the import of the data. With regard to Steps 1 through 4, you are not advising anything in this process, so click **Finish**. Once the spreadsheet is imported, a window will open that displays the data set.

### Viewing the Data

The data appears to be in good condition and self-explanatory. Note that most data will require some cleaning. For information about this important process, see *Cody's Data Cleaning Techniques Using SAS* by Ron Cody (2008).

You will see seven variables, a few of which require definitions:

- The CUSTOMER_ID is a unique ID number that helps the company track the customer. You won't be using it in this analysis.
- CUSTOMER_SUBSCRIPTION_COUNT is the total number of current magazine and journal subscriptions held by the customer.
- CUSTOMER_REVENUE is the total revenue for the last year.

> **TIP:** Once the data is imported, you should save the project. Look for the icon on the top menu bar. The first time you do so, a menu will open and ask you to select a location and name the project. Once the project has been named, you can click that icon anytime, and the project will be saved under the same name.

### Exploring the Data

Once you have viewed the data to your satisfaction, close the data set by clicking the X in the upper right-hand corner of your screen. You can reopen it any time by right-clicking or double-clicking the data set icon that appears in both the Project Tree and the main work area.

Before you create reports, let's look at a helpful SAS Enterprise Guide option that allows you to send all output to a rich text format (RTF) file. Click **Tools ▶ Options ▶ Results**. When the Results section opens, you have several options for the format of the output data, as shown in Figure 5.3. The default is **SAS Report**. This default may be sufficient, but if you have Microsoft Word on your computer, you might click the box next to RTF near the top. This option allows you to share the documents in Microsoft Word format with all default settings that work well for most reports. You can also select **PDF**, **HTML**, or **Text Output**. You can explore these selections to see which works best for your projects.

**Figure 5.3: Format Options for Results**

![](img/976d9b992e82c4ac7d195d03a30b4915_79_0.png)

To view the data characteristics, you have several options. The fastest and simplest is to place your cursor on the data set in the work area and select **Tasks ▶ Describe ▶ Characterize Data** (Figure 5.4). This task is designed to give you a complete overview of every variable in your data set, in a useful format.

**Figure 5.4: Task Menu in SAS Enterprise Guide to Characterize Data**

![](img/976d9b992e82c4ac7d195d03a30b4915_79_1.png)

When the first menu appears, click **Finish**.

> **NOTE:** If you have a categorical variable with more than 30 levels, such as *zip code*, Enterprise Guide will limit the output to the most frequent 30 levels. This option can be changed.

Once the process is complete, you can view the output by clicking on a tab at the top of the work area. If you have Microsoft Word on your computer, then you can access the RTF output by clicking the Microsoft Word icon. It will open the results in Microsoft Word outside of the project.

Output 5.1 is an example of the output of categorical variables in a frequency table. The results shown in Output 5.2 are fairly self-explanatory: males, with a count of 9,372, represent 59% of the sample; females, with a count of 6,140, represent 38% of the sample. Approximately 3% of the file has an unknown value (U) for gender.

**Output 5.1: Categorical Data Analysis of Gender**

| Variable | Label | Value | Frequency Count | Percent of Total Frequency |
|---|---|---|---:|---:|
| GENDER |  | M | 9372 | 58.5055 |
|  |  | F | 6140 | 38.3295 |
|  |  | U | 507 | 3.1650 |

Output 5.2 provides results for continuous or interval variable AGE.

**Output 5.2: Interval or Continuous Data Analysis of Age**

| Variable | Label | N | NMiss | Total | Min | Mean | Median | Max | StdMean |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| AGE |  | 16019 | 0 | 579193 | 18 | 36.16 | 34 | 92 | 0.10 |

For AGE, the following measures are available:

- *N* is the number of customers.
- *NMiss* is the number of missing values for Age. The value here is zero because missing values are represented by the value ‘U’ in our data set.
- *Total* equals the value if you sum age. It has no meaning in our analysis.
- *Min* and *Max* are the lowest value and the highest value.
- *Mean* equals the mathematical average or arithmetic mean (with missing values stripped).
- *Median* is the age of the customer at 50% of the file when sorted by age; it is the middle number when the observations are put in order.
- *StdMean* equals the standard error variation of the mean.

The graph in Output 5.3 shows the general distribution of the customer base by age. You can see that most of the customers are younger, with a heavy concentration between ages 21 and 40. In addition, there appear to be some outliers, or extreme values, represented by a few customers older than age 90. Outliers can cause problems with some types of analyses, especially regression models.

**Output 5.3: General Distribution of a Company’s Customer Base by Age**

![](img/976d9b992e82c4ac7d195d03a30b4915_81_0.png)

## Segmentation and Profile Analysis

The next step is to partition the customer base by CUSTOMER_REVENUE to compare the characteristics of the customers with the highest revenue to the rest of the customers.

Highlight the DMR Customer Base data set and select **Tasks ▶ Describe ▶ Distribution Analysis**. A window will open in which you can select the variables. Click CUSTOMER_REVENUE and move it to the area below Analysis Variables (Figure 5.5). In the left-hand column, select **Tables**. Check the box next to **Quantiles**. Click **Run**.

**Figure 5.5: Selection of Variable for Distribution Analysis of Customer Revenue**

![](img/976d9b992e82c4ac7d195d03a30b4915_82_0.png)

Output 5.4, captured from the RTF Output, shows the quantiles of the CUSTOMER_REVENUE distribution. A standard method that companies use to understand the drivers of revenue is to compare the characteristics of the top 25% of customers to the bottom 75%, on the basis of revenue. According to the Q3 value at the 75th percentile, anyone with more than $100 in revenue is in the top 25%.

**Output 5.4: Quantiles of a Customer-Based Revenue Distribution**

Quantiles (Definition 5)

| Level | Quantile |
|---|---|
| 100% Max | 1040 |
| 99% | 260 |
| 95% | 180 |
| 90% | 140 |
| 75% Q3 | 100 |
| 50% Median | 60 |
| 25% Q1 | 30 |
| 10% | 15 |
| 5% | 15 |
| 1% | 15 |
| 0% Min | 15 |

Next, you will create a binary variable that will allow you to split the file between the top 25% and the bottom 75% for analysis.

To create a new variable, use the Advanced Expression function within the Query Builder. Right-click the DMR Customer Base data set, then select Query Builder (Figure 5.6). Put your cursor on the data set name, t1 (DMR_CUSTOMER_BASE, in the left-hand column), and drag it, together with all the variables, over to the right side under Select Data.
