+   2. Enter the RFC for the DATA SOURCE, as shown in Figure 19.117.

![](bbox=[0.142, 0.138, 0.622, 0.33])

**Figure 19.117** Map to Data Source

+   3. The data source parameters will be displayed on the right, as shown in Figure 19.118. You can click the PROPOSE MAPPING button to have the system automatically propose the mapping, or manually drag and drop the fields from the right window to the DATA SOURCE PARAMETER area on the left.

![](bbox=[0.142, 0.481, 0.85, 0.727])

**Figure 19.118** Mapping Data Source Parameters

+   4. Repeat the steps to map the sales order item entity. Once the mapping is complete, click the GENERATE icon to generate the runtime artifacts.

Once the OData service is implemented, we can test it by entering the URI `/sap/opu/odata/sap/ZDEMO_SO_SRV/SalesOrderHeaderSet` in Transaction `/IWFND/GW_CLIENT`. Note that there is no filter value, so the OData service will pick all the doc-