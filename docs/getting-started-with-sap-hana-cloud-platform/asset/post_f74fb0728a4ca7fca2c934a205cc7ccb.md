
In this chapter, we'll take a look at what it takes to get up and running with SAP HCP application development. By the end of this chapter, you'll have everything you need to begin developing live applications on the platform.

## 2 Getting Up and Running

Now that you have a feel for what SAP HCP is from a conceptual perspective, you're probably itching to take it for a test drive and see what it can do. We'll have a chance to do just that in Chapter 3. However, in the meantime, there are several administrative items that we need to sort out.

First of all, in order to do any real work on SAP HCP, we need to get our hands on an SAP HCP developer account. This account will be used to log onto the platform, allocate and assign resources, deploy applications, and more. We'll explore the account provisioning process in Section 2.1. In Section 2.2, we'll take a quick inventory of what's included in an SAP HCP account. Finally, in Section 2.3, we'll show you how to set up SAP HCP development tools on your local machine. With these tools in place, you'll be ready to hit the ground running in Chapter 3 when we start getting our hands dirty with application development.

### 2.1 Obtaining an SAP HCP Account

In order to access SAP HCP, we must apply for an account with SAP. In this section, we'll take a look at the various account types offered by SAP and see how they differ from one another. We'll also show you how to set up a free developer account that you can use to take SAP HCP for a test drive.

### 2.1.1 Understanding the SAP HCP Account Concept

In many ways, SAP HCP accounts are not unlike the accounts you set up with utility companies, such as your local electricity or Internet service provider. If you have ever had the pleasure of setting up one of these accounts, then you’re no doubt familiar with the basic procedure:

- 1. First, you choose among the various account types and/or service plans offered by the service provider.
- 2. Then, you enter into some form of contract agreement whereby you as the customer agree to pay a certain fee, and the provider agrees to provide the requested services according to the service level agreements (SLAs) set forth in the contract.

In the context of SAP HCP, accounts are used to determine the scope of resources/services a customer wishes to procure from SAP. Once a customer registers for an account, the account becomes the key to accessing the platform, deploying applications, and much more.

At the time of this writing, SAP offers three different account types: developer, customer, and partner. These account types differ in terms of pricing model, the amount of cloud-based resources allocated, and usage conditions. Let’s take a look at each of the available account types in detail.

### Developer Accounts

The first account type that we’ll take a look at is the free developer account. This account type is provided for developers who wish to explore SAP HCP and see what it has to offer. Unlike other SAP trial accounts that you may have worked with in the past, the SAP HCP developer account never expires, so you can continue to use it as a trial or sandbox account indefinitely.

For the most part, developer accounts provide access to the majority of features and services provided by SAP HCP. However, because this is a free account, SAP does limit the amount of resources you can consume using this account. In particular, as of the time of writing, developer accounts come with the following limitations:

- You can only run a limited number of applications at a time.
- Only 1 GB of database storage and 1 GB of document storage is provided.
- Only one user can exist per account.

### Customer Accounts

As the name suggests, customer accounts are accounts that customers purchase from SAP in order to host productive applications in the cloud. Unlike the more limited developer accounts, customer accounts offer full access to SAP HCP productive services as well as 24-7 support from SAP.

In order to support a wide range of customer types, SAP offers a multitude of configuration options, which allow customers to choose the configuration that best meets their needs. You can obtain a pricing sheet and browse through the various configuration options by logging onto the SAP HANA Marketplace at http://marketplace.saphana.com/New-SAP-HANA-App-Services/p/1808. In most cases, you can choose the target configuration and purchase the customer account right from within the SAP HANA Marketplace. After the initial purchase, customers have the option over time to purchase more resources from SAP as the need arises.

> **Tip**
> To ensure fast response times for productive applications, customer accounts are hosted in regional data centers that are in close proximity to the target user base. At the time of this writing, SAP has three data centers, covering the Americas, Europe, and Asia Pacific regions.

### Partner Accounts

This account type is provided for SAP partners who are interested in building cloud-based applications and selling them to customers. Access wise, partner accounts are similar to customer accounts in that they have access to the full set of SAP HCP productive services. However, because these types of accounts are normally used for development and prototyping, the amount of allocated resources tends to be less than for your average customer account. That being said, SAP will allow partners to purchase more resources as needed.

For more information about this account type and the SAP PartnerEdge program, log on to https://www.sapappsdevelopmentpartnercenter.com.

### 2.1.2 Registering for a Free Developer Account

If this book is your first foray into the world of SAP HCP, then it probably makes sense to start your journey by registering for a free developer account. The steps required to sign up for a developer account are as follows:

- 1. Log onto the SAP HCP trial account landing page at https://account.hanatrial.ondemand.com, as shown in Figure 2.1.

![](img/cf7012644082c115a2181376d9b7486d_43_0.png)

Figure 2.1 Registering for a Free SAP HCP Developer Account: Part 1

- 2. From the landing page, click on the Log On button. This will bring up the Log On page shown in Figure 2.2. From here, you have one of two options. If you already have an SAP ID or SAP SCN account, then you can plug in your account credentials into the Log On form and click on the Log On button to link this account with your SAP HCP developer account. A quick acceptance of the license agreement, and you’re up and running.

![](img/cf7012644082c115a2181376d9b7486d_44_0.png)

Figure 2.2 Registering for a Free SAP HCP Developer Account: Part 2

- 3. If you don’t yet have an SAP ID and/or an SAP SCN account, then you’ll need to create one by clicking on the REGISTER Now button shown on the left-hand side of the screen in Figure 2.2. This will open up the REGISTRATION window shown in Figure 2.3. Here, you must specify a minimal amount of contact information and agree to the terms and conditions in order to register. After you submit the form, you’ll receive a confirmation email, via which you can confirm the registration and activate your account.

## Registration

To register for SAP HANA Cloud Platform, provide the required information below.

### Tell Us About Yourself

- First Name * Andrea
- Last Name * Wood
- E-mail *
- Phone

### Set Password

Your password must contain at least eight characters including three of

- Uppercase letters
- Lowercase letters
- Numbers
- Symbols

- Password *
- Re-Enter Password *

I acknowledge that I have read SAP's Privacy Statement and consent to the processing of my personal data in accordance with the terms of the Privacy Statement. This includes, without limitation, that SAP may collect, store and process any personal data voluntarily provided by me on this Web site and aggregate it with other information about me that SAP collects from other sources. The purposes for which such data will be processed are described in the Privacy Statement and on this Web site. In accordance with the terms of the Privacy Statement and on this Web site, SAP may further track my use of SAP's Web sites and aggregate it with my personal data. I acknowledge that I can, at any time, request information on my personal data held by SAP and that I can have SAP update and correct such data and withdraw my consent given hereby by contacting SAP at account@sap.com.

Figure 2.3 Registering for a Free SAP HCP Developer Account: Part 3

Regardless of the approach you take, the account creation process ends with you logged onto the SAP HCP Cockpit application shown in Figure 2.4. As you can imagine, we'll be spending a considerable amount of time in this cockpit as we develop and deploy applications, provision resources, and so on. Therefore, it's a good idea to bookmark the cockpit's page for future use: https://account.hanatrial.ondemand.com/cockpit. Also, if this is the first time you've ever accessed SAP HCP we'd encourage you to take a look around the cockpit and become acquainted with the various tab pages, which will give you a sense of what's included with your SAP HCP account.
