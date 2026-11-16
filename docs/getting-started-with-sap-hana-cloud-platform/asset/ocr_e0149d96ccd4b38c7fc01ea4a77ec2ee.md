![](bbox=[0.145, 0.105, 0.845, 0.355])

Figure 11.6 SuccessFactors Provisioning Environment Targeted at Professional Services Consultants and Implementation Partners

In this situation, select the EXTENSION MANAGEMENT checkbox. Then, fill in the PRIMARY ADMINISTRATOR USER for MANAGING EXTENSIONS field with the name of your SuccessFactors system admin user. This is the first SuccessFactors user who will be granted permissions to customize extension portal sites in SuccessFactors Admin Tools. Later on, he or she can grant permissions to more administrator users. (In future versions of the SuccessFactors Provisioning tool, this field will become obsolete and will be eliminated altogether. Therefore, don't panic if you don't find it in your version at a later stage.)

The second field to be filled in is SAP HANA CLOUD PLATFORM ADMINISTRATOR USER. It defines one (or more; comma separated) SAP Cloud Identity users who will be granted administrator access to the corresponding SAP HCP extension account. Typically, these are the S-users who report issues to SAP and have the permissions to download software from the SAP Service Marketplace.

In case of error, it's always an option to disable the SAP HCP extensions module by deselecting the EXTENSION MANAGEMENT checkbox, fixing the errors, and selecting it again.

With that, your SAP HCP extension account is created (Figure 11.7). The Extension Package Details section illustrates the current status of the SAP HCP extension account. If onboarding has passed successfully, then you should see EXTENSION PACKAGE STATUS as COMPLETED. This section also includes other details,