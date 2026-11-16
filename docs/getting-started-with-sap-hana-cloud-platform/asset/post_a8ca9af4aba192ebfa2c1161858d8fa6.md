
![](img/cf7012644082c115a2181376d9b7486d_485_0.png)

Figure 11.6 SuccessFactors Provisioning Environment Targeted at Professional Services Consultants and Implementation Partners

In this situation, select the EXTENSION MANAGEMENT checkbox. Then, fill in the PRIMARY ADMINISTRATOR USER for MANAGING EXTENSIONS field with the name of your SuccessFactors system admin user. This is the first SuccessFactors user who will be granted permissions to customize extension portal sites in SuccessFactors Admin Tools. Later on, he or she can grant permissions to more administrator users. (In future versions of the SuccessFactors Provisioning tool, this field will become obsolete and will be eliminated altogether. Therefore, don't panic if you don't find it in your version at a later stage.)

The second field to be filled in is SAP HANA CLOUD PLATFORM ADMINISTRATOR USER. It defines one (or more; comma separated) SAP Cloud Identity users who will be granted administrator access to the corresponding SAP HCP extension account. Typically, these are the S-users who report issues to SAP and have the permissions to download software from the SAP Service Marketplace.

In case of error, it's always an option to disable the SAP HCP extensions module by deselecting the EXTENSION MANAGEMENT checkbox, fixing the errors, and selecting it again.

With that, your SAP HCP extension account is created (Figure 11.7). The Extension Package Details section illustrates the current status of the SAP HCP extension account. If onboarding has passed successfully, then you should see EXTENSION PACKAGE STATUS as COMPLETED. This section also includes other details, such as the name of the SAP HCP extension account and a direct link pointing to the SAP HCP Cockpit on the corresponding landscape.

| Extension Package Details |
|---|
| Extension Package Status | COMPLETED |
| Extension SAP HANA Cloud Platform Account | [Redacted] |
| Extensions API Key | [Redacted] |
| Extensions Admin URL | [Redacted] |

Figure 11.7 Status of SAP HCP Extension Account Onboarding

The EXTENSION PACKAGE Related Features Status section on the same screen provides some details that come into play when troubleshooting integration issues later on. In Figure 11.8, you can see all the SuccessFactors features that are required for proper functioning of the associated SAP HCP extension account.

| Extension Package Related Features Status |
|---|
| OData API: | ENABLED |
| Employee Central OData API: | ENABLED |
| Enable Generic Objects: | ENABLED |
| Enable the Attachment Manager: | ENABLED |
| Configure Custom Navigation: | ENABLED |
| Replication permission: | ENABLED |
| OData Client: | ACTIVE |
| Authorized SP ACS: | CONFIGURED |

Figure 11.8 SuccessFactors Features Required for Proper Functioning of the Associated SAP HCP Extension Account

When you click on Link in the SuccessFactors Provisioning UI (refer back to Figure 11.7), you'll jump to the SAP HCP Cockpit focused on the freshly created SAP HCP extension account for the current SuccessFactors company. Something you'll quickly notice is that the display name of the company allows for quick traceability for what the account is and which particular backend it's configured to extend.

You can examine the account to verify that trust settings are already configured, as shown in Figure 11.9. In upcoming releases of SAP HCP, trust settings and destinations to the extended SAP Cloud solution will become read-only and will be managed automatically by SAP HCP for all extension accounts.

![](img/cf7012644082c115a2181376d9b7486d_487_0.png)

Figure 11.9 SAP HCP Extension Account Trust Settings: Automatically Configured on both the SAP HCP and SuccessFactors Sides

Another aspect worth noting is that SAP HANA Cloud Portal and SAP Web IDE services are automatically enabled for all SAP HCP extension accounts, as shown in Figure 11.10.

![](img/cf7012644082c115a2181376d9b7486d_487_1.png)

Figure 11.10 SAP HCP Services Enabled by Default in SAP HCP Extension Accounts

Your SAP HCP extension account is now fully configured and is ready to run extension applications.

When deploying additional applications, you'll inevitably reach the configured resource quotas for your account. In order to increase those, you have to either purchase additional SAP HCP resources or (if this was already done) assign additional resources to the newly created extension account out of your central SAP HCP resource pool.

## 11.4.3 Deploying Your First SuccessFactors Extension

In order to explore what's possible, the best way to move forward is to look at a particular example and try to derive conclusions. For that purpose, SAP has published an official SuccessFactors extension sample application, available under the Apache 2.0 license on GitHub at http://github.com/SAP/cloud-sf5-benefits-ext. The scenario it covers is called Corporate Benefits. The purpose of the Corporate Benefits sample application is to offer non-monetary perks to employees while at the same time having a simple process for both employees and the responsible HR managers.

There are two roles in this application: Employee and HR Manager. The Employee role is practically everyone with a valid user ID in the underlying SuccessFactors system. This means that we're not going to allow non-authenticated users in the application. The HR Manager role is well defined in SuccessFactors and is simply reused by the application, adding additional responsibilities to it.

Employees are granted a monthly budget of an abstract “currency” called benefit points. These points are used to indicate the value of a large variety of nonmonetary benefits—for example, soccer game tickets, restaurant/fitness studio vouchers, and so on.

Each selection period is called a campaign and has defined start and end dates. Campaigns also have a particular amount of benefit points granted for each employee. As Employee, you can change your benefits selection for each of the active campaigns and view the history of your orders in previous campaigns. In addition, you can browse the benefits catalog and check what the available benefits per campaign are. As HR Manager, you can manage the campaigns: their start date, duration, and so on. You can also manage the benefits of an employee on his or her behalf.

The same application is used as a main exercise in the openSAP course for building SAP product extensions with SAP HCP. The course is available for free for self-study at http://open.sap.com/courses/hanacloud3.

In order to deploy the application, you'll have to go through the following steps:

- 1. Clone the application's Git repository.
- 2. Import the sources as a Maven project in Eclipse. Make sure that your proxy settings in the Maven settings.xml file are properly configured.
- 3. Build the project in Eclipse.
- 4. Deploy the application to SAP HCP.
- 5. Depending on whether you have a SuccessFactors system to experiment with, you have two different options to continue:
  - Assuming that you already have a SuccessFactors system at hand, then you'll proceed directly with the steps defined in Section 11.4.2.
  - If you don't have access to a commercial SuccessFactors account, then you can follow the application readme and leverage the public read-only SuccessFactors API that the SAP HCP team has set live for developers to experiment with.

You can deploy the application using the SAP HCP command-line tool, SAP HCP Tools for Eclipse, or directly from the SAP HCP Cockpit.

## 11.4.4 SuccessFactors Extension Administration

When you log in to your SuccessFactors account as a system administrator after successful enablement of the SAP HCP extension package, you'll notice some changes.

All SuccessFactors accounts provide out-of-the-box access to an embedded extensions marketplace used to feature extension applications provided by SAP and SAP partners. This marketplace is accessible in Admin Tools under COMPANY SETTINGS and then EXTENSIONS, as shown in Figure 11.11.

For SuccessFactors companies for which the SAP HCP extension package is not enabled, the link will open the marketplace directly, as shown in Figure 11.12.
