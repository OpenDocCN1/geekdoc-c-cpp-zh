![](bbox=[0.143, 0.102, 0.592, 0.213])

Figure 11.21 Tool Search Feature in SuccessFactors OneAdmin

If what you're typing doesn't autocomplete, then this means either that there is no such tool or that you don't have the required permissions to access it.

# SFAPI Tracing

SuccessFactors SFAPI is practically the oldest public integration API from SuccessFactors to be exposed publicly. It is based on SOAP and is primarily used for data replication and synchronization with external systems. It is therefore the basis for many of the prepackaged delivered integrations.

It's worth mentioning that SFAPI has to be explicitly enabled in Provisioning and that the corresponding administrator role permissions need to be granted. Those permissions include the following:

+   - Access to the SFAPI Data Dictionary
+   - Access to the SFAPI Audit Log
+   - Access to the SFAPI Metering Details

When planning to use SFAPI, the first thing to consider is the SFAPI Data Dictionary. It shows you all the available fields and objects you can query on. It also describes the fine-grained permissions for each of the fields. You can find it in Admin Tools • COMPANY SETTINGS • SFAPI DATA DICTIONARY (Figure 11.22).

There are entities in the object data model that, although accessible through SFAPI, must be explicitly enabled via Provisioning in order to show up in the data dictionary. One example is employee personal information, which is there but not exposed by default.

If you have a scenario where you need to replicate data from a backend system to SuccessFactors or simply keep SuccessFactors in sync with another system, then you'll most probably end up using SFAPI in combination with SAP HCI, Dell Boomi, SAP Process Orchestration, or yet another integration product you might