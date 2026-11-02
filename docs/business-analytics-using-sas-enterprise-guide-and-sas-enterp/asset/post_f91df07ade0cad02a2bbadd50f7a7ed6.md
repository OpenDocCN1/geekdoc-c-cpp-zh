
Figure 7.3: View SAS Enterprise Miner Workspace

![](img/976d9b992e82c4ac7d195d03a30b4915_108_0.png)

## Input the Data Source and Assign Variable Roles

Next, double click on the Data Sources icon (upper left-hand menu, directly under the word *Actions*). The Data Import Wizard will open, asking you to create a SAS Table (Figure 7.4).

**Figure 7.4: Locate Data Source**

![](img/976d9b992e82c4ac7d195d03a30b4915_109_0.png)

Click **Next** ▶ and browse for the DMR_CUSTOMER_BASE data set created in Chapter 3. Once you locate the data, select the data and click **OK**, then click **Next** ▶. The next window shows a summary. Click **Next** ▶. For Meta Data Advisory options, click **Advanced** and **Next** ▶. A window appears that displays the variable characteristics and offers options for exploring the distributions (Figure 7.5).

**Figure 7.5: Assign Variable Roles and Explore Variables**

![](img/976d9b992e82c4ac7d195d03a30b4915_109_1.png)

First, you need to change the role of CUSTOMER_REVENUE and CUSTOMER_SUBSCRIPTION_COUNT to “Rejected.” These are outcome variables that will be used in future chapters. But for now, you do not want to include them in your analysis.

> **NOTE:** It is necessary to have an ID variable for clustering in order to track the observations in each cluster.

Highlight AGE and click **Explore**. A large window opens and has four quadrants. Maximize the quadrant in the lower left to get Output 7.1.

Output 7.1: View Distribution of the Age Variable

![](img/976d9b992e82c4ac7d195d03a30b4915_110_0.png)

For clustering, you want variables to have a bell-shaped curve that represents a normal distribution. Because AGE is not normally distributed, you can use the **transform** function. Because AGE is skewed to the right, or positively skewed, you should use a log transformation after all the variables are explored.

> **NOTE:** To close the **Results** window in SAS Enterprise Miner, click the **X** in the upper right-hand corner. It will close only the results window; the main project will remain open.

Explore the two remaining continuous variables, HOUSEHOLD_INCOME and YEARS_AS_CUSTOMER, by following the same process. Because both variables are skewed to the right, these variables will also need to be transformed with use of the log transformation. But first, you must complete the import process. Click **Next** several times and then **Finish**.

Once the DMR_CUSTOMER_BASE data source is created, the data set name will appear under Data Sources in the upper diagram as shown in Figure 7.6.

Figure 7.6: Open Project View with Data Source in Clustering Diagram

![](img/976d9b992e82c4ac7d195d03a30b4915_111_0.png)

Next, you want to create a workspace for your cluster analysis. Go to the top menu and click **File > New > Diagram**. When the box opens, name the diagram Clustering and click **OK**. A work area will appear on the right. Place your cursor on the data set, DMR_CUSTOMER_BASE, and drag it into the clustering work area on the right.

## Transform Variables

Next, look at the menu above the diagram and click the **Modify** tab. The last icon in the row above is **Transform Variables**. Drag the **Transform Variables** icon to the **Diagram** and connect it to DMR_CUSTOMER_BASE data set with an arrow (Figure 7.7).

Figure 7.7: Use the Transform Variable Icon

![](img/976d9b992e82c4ac7d195d03a30b4915_111_1.png)

To connect the DMR Customer data to the Transform Variables node, right-click on the **Transform Variables** node and select **Run**. When offered to view the results, click **OK**.

With the Transform Variables node still highlighted, look to the lower left of the work area shown in Figure 7.8.

**Figure 7.8: Locate the Transform Variable Formula Menu**

| Property | Value |
|---|---|
| **General** | |
| Node ID | Trans |
| Imported Data | |
| Exported Data | |
| Notes | |
| **Train** | |
| Variables | |
| Formulas | |
| Interactions | |
| SAS Code | |
| **Default Methods** | |
| Interval Inputs | None |
| Interval Targets | None |
| Class Inputs | None |
| Class Targets | None |
| Treat Missing as Level | No |
| **Sample Properties** | |
| Method | First N |
| Size | Default |
| Random Seed | 12345 |

Under Train, next to Formulas, click the three dots to the right. A window will open that shows all the variables and each distribution, depending on which variable is selected (Figure 7.9).

Figure 7.9: View the Transformation Overview

![](img/976d9b992e82c4ac7d195d03a30b4915_113_0.png)

Highlight the variable AGE. In the upper left-hand corner, click the Create icon. The word ‘Create’ will appear when you hover over the icon. The box in Figure 7.10 will appear.

Figure 7.10: Transform the Age Variable

![](img/976d9b992e82c4ac7d195d03a30b4915_113_1.png)

To the right of Property under Value, change the name from TRANS_01 to AGE_LOG. Repeat the process for HOUSEHOLD_INCOME and YEARS_AS_CUSTOMER, using similar Names and log transformations based on the formulas in Figure 7.10. After each formula is typed in, click OK. Note that the log of HOUSEHOLD_INCOME becomes HH_INCOME_LOG and equals log (HOUSEHOLD_INCOME+100). The name for log of YEARS_AS_CUSTOMER is YEARS_AS_CUST_LOG.

The transformation formulas appear at the bottom of the Formulas window as shown in Figure 7.11.

**Figure 7.11: Create the Transformation Formulas for Age, Household Income, and Years as Customer**

![](img/976d9b992e82c4ac7d195d03a30b4915_114_0.png)

Click **OK**. Then, right-click on the **Transform Variables** icon and hit **Run**. After the run is complete, click **OK**.

## Filter Data

Because clustering is sensitive to outliers, you will get better results if you run your variable through a filtering process. Above your diagram, click on the Sample tab and go to the fourth icon, **Filter**. Drag it onto the diagram and connect it with an arrow (Figure 7.12).

Figure 7.12: Filter the Data

![](img/976d9b992e82c4ac7d195d03a30b4915_115_0.png)

Right click on the Filter node and select **Run**.

To look for potential outliers, highlight the filter icon, go to the lower left menu, and click the three dots to the right of **Interval Variables** (Figure 7.13).

Figure 7.13: Locate the Filter Menu

| Property | Value |
|---|---|
| **General** | |
| Node ID | Filter |
| Imported Data | |
| Exported Data | |
| Notes | |
| **Train** | |
| Export Table | Filtered |
| Tables to Filter | Training Data |
| Distribution Data Sets | Yes |
| **Class Variables** | |
| Class Variables | |
| Default Filtering Method | Rare Values (Percentage) |
| Keep Missing Values | Yes |
| Normalized Values | Yes |
| Minimum Frequency Cutoff | 1 |
| Minimum Cutoff for Percent | 0.01 |
| Maximum Number of Levels | 25 |
| **Interval Variables** | |
| Interval Variables | |
| Default Filtering Method | Standard Deviations from ... |
| Keep Missing Values | Yes |

This dropdown option opens a window that allows you to view each distribution (Figure 7.14). For HH_INCOME_LOG, set the **Filter Lower Limit** to 8 and click **Apply Filter**.

**Figure 7.14: Specify Filter Variables**

![](img/976d9b992e82c4ac7d195d03a30b4915_116_0.png)

Click **OK**. Then right-click the **Filter** icon and select **Run**. When it completes, click **OK**.

## Build Clusters

Above the diagram window, go to the **Explore** tab and pick the second icon, **Cluster**. Drag the **Cluster** icon onto the diagram and connect it with the **Filter** node (Figure 7.15).

**Figure 7.15: Add the Cluster Process**

![](img/976d9b992e82c4ac7d195d03a30b4915_116_1.png)

When you highlight the **Cluster** icon, the Property menu appears on the lower left (Figure 7.16).

Figure 7.16: View the Property Menu for the Add-Cluster Process

![](img/976d9b992e82c4ac7d195d03a30b4915_117_0.png)

Continuous variables come in different scales, such as counts, minutes, and dollars. You will want to standardize these variables for clustering. Otherwise, the variables with the higher scale will have an advantage. Under Train, change Internal Standardization to Range. This option standardizes the values for each variable to a value between 0 and 1. For Clustering Method, select Centroid. This method is usually better than the Ward method for handling contrasting data. Change the Seed Initialization Method to Full Replacement to select seeds that are well-separated. Right click, then click Run. When the run is complete, click on Results.

Output 7.2 shows the upper left and lower left quadrants of the Results window's four quadrants. Each quadrant offers insights into the results of the process as defined:

- *Segment Plot*—the upper left quadrant displays a segment plot of the clustering variables with the highest importance. The results show how the values of age, log, and gender are distributed among the clusters. To see the value of the segment and other statistics, place your cursor on the color within each segment.
