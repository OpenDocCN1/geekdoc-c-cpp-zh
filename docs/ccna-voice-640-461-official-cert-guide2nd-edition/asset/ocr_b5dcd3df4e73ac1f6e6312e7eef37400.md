![](bbox=[0.106, 0.063, 0.803, 0.493])

Figure 17-3 Sample Output: Users Report

The other reports in the CUC Serviceability Reports list provides insight into the current status, configuration, and utilization of the CUC server.

# Cisco Unified Serviceability: Serviceability Reports Archive

CUC includes a built-in reporting system to monitor server health and performance. These reports are accessed through the Unified Serviceability web application (not to be confused with the CUC Serviceability application). To access these reports, you must first activate the Cisco Serviceability Reporter service. In Unified Serviceability, navigate to Tools > Service Activation. Select the Cisco Serviceability Reporter service and click Save.

The Serviceability Reporter collects data from log files and populates the Serviceability Reports Archive, which stores report information and makes it available on a daily basis. It is a CPU-intensive service, so consider activating it will negatively impact your server health or performance. The type and amount of data collected can be tuned in the CUC Administration interface. Navigate to System Settings > Advanced > Reports to the following:

+   - Enable Audit Log: Unchecking this box stops the logging of stored procedures. The default setting is Enabled.

> Key Topic