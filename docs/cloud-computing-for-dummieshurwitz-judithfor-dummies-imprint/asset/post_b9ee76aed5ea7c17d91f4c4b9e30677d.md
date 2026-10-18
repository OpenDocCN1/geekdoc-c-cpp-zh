
- **Data integrity:** What controls do you have to ensure the integrity of my data? For example, are there controls to make sure that all data input to any system or application is complete, accurate, and reasonable? What about any processing controls to make sure that data processing is accurate? And, there also need to be output controls in place to ensure that any output from any system, application, or process can be verified and trusted. This dovetails with the next bullet about any specific compliance issues that your particular industry might have.
- **Compliance:** You are probably aware of any compliance issues particular to your industry. Obviously, you need to make sure that your provider can comply with these regulations.
- **Loss of data:** What provisions are in the contract if the provider does something to your data (loses it because of improper backup and recovery procedures, for instance)? If the contract says that your monthly fee is simply waived, you need to ask some more questions.
- **Business continuity plans:** What happens if your cloud vendor’s data center goes down? What business continuity plans does your provider have in place: How long will it take the provider to get your data back up and running? For example, a SaaS vendor might tell you that they back up data every day, but it might take several days to get the backup onto systems in another facility. Does this meet your business imperatives?
- **Uptime:** Your provider might tell you that you will be able to access your data 99.999 percent of the time — however, read the contract. Does this uptime include scheduled maintenance?
- **Data storage costs:** Pay-as-you-go and no-capital-purchase options sound great, but read the fine print. For example, how much will it cost to move your data into the cloud? What about other hidden integration costs? How much will it cost to store your data? You should do your own calculations so you’re not caught off guard. Find out how the provider charges for data storage. Some providers offer a tiered pricing structure. Others offer pricing based on server capacity.
- **Contract termination:** How will data be returned if the contract is terminated? If you’re using a SaaS provider and it has created data for you too, will any of that get turned over to you? You need to ask yourself if this is an issue. Some companies just want the data destroyed. Understand how your provider would destroy your data to make sure that it isn’t floating around in the cloud.
- **Data ownership:** Who owns your data after it goes into the cloud? Some service providers might want to take your data, merge it with other data, and do some analysis.
- **Switching vendors:** If you create applications with one cloud vendor and then decide to move to another vendor, how difficult will it be to move your data? In other words, how interoperable are the services? Some of these vendors may have proprietary APIs and it might be costly to switch. You need to know this before you enter into an agreement.

## Chapter 9

## Discovering Private and Hybrid Clouds

## In This Chapter

- ▶ Defining a private cloud
- ▶ Choosing between public, private, and hybrid cloud environments
- ▶ Investigating private cloud economics
- ▶ Looking at vendor solutions for private and hybrid

While many business executives are attracted to the idea of the public cloud, just as many are interested in achieving the benefits of the cloud but on an internal basis. There are different reasons why companies investigating a cloud might want a private cloud instead of using a public one. The most obvious reason is privacy and security of data. Another reason that some companies are considering the private cloud is that they have already invested in a lot of hardware, software, and space and would like to be able to leverage their investments, but in a more efficient manner.

What if you could avoid the security issue by keeping your data inside your firewall and still gain public cloud benefits? Then consider a private or a hybrid cloud. Many companies are looking at a situation where they actually see the benefits of using a public cloud for some services, a private cloud for others, a hybrid cloud for some situations, and their traditional data center for the rest. Indeed, the world of IT is complicated. We suspect that most organizations will have a combination of approaches — a hybrid of public and private clouds with traditional data centers included.

In this chapter, we explain what a private cloud is and how it can work in tandem with public clouds. We explain the technology and services vendors are offering, and what happens when companies implement a strategy that combines a private cloud behind the firewall or a virtual private network with public cloud services.

## Pining for Privacy

While it may be clear that a private cloud is private and a public cloud is open to anyone, there are nuances that help make the differences evident.

Here are a few examples that might help:

- You’re a company selling a service to retailers that helps them manage their digital gift cards. You might use a public cloud service to enable the retailers to submit information to you, but you want to make sure that the data you’re collecting for them remains confidential and safe. You would, therefore, put that important data in a private cloud behind your company’s firewall.
- You’re a healthcare company in France. Your government requires that your patients’ data be stored within the country. You’d probably want to keep that data in a private cloud.
- You’re a financial services company that has selected a sales management system based on SaaS. However, you’re concerned about the security of your customer data. The SaaS company offers a private cloud version of its service by adding a virtual private network that adds a second layer of security.

### Defining a private cloud

There’s confusion — as well as passionate debate — over the definition of a private cloud. When we say *private cloud*, we mean a highly virtualized cloud data center located inside your company’s firewall. It may also be a private space dedicated to your company within a cloud vendor data center designed to handle your company’s workloads.

The characteristics of the private cloud are as follows:

- Allows IT to provision services and compute capability to internal users in a self-service manner
- Automates management tasks and lets you bill business units for the services they consume
- Provides a well-managed environment
- Optimizes the use of computing resources such as servers
- Supports specific workloads
- Provides self-service based provisioning of hardware and software resources

You might think this sounds a lot like a public cloud! A private cloud exhibits the key characteristics of a public cloud, including elasticity, scalability, and self-service provisioning. (Please refer to Chapter 1 for detailed information on cloud characteristics.) The major difference is *control* over the environment. In a private cloud, you (or a trusted partner) control the service management.

It might help to think of the public cloud as the Internet and the private cloud as the intranet.

If private and public clouds are so similar, why would you develop a private cloud instead of ordering capacity on demand from an Infrastructure as a Service provider or using Software as a Service? Here are several good reasons companies are using a private rather than a public cloud:

- Your organization has a huge, well-run data center with a lot of spare capacity. It would be more expensive to use a public cloud even if you have to add new software to transform that data center into a cloud.
- Your organization offers IT services to a large ecosystem of partners as part of your core business. Therefore, a private cloud could be a revenue source.
- Your company’s data is its lifeblood. You feel that to keep control you must keep your information behind your own firewall.
- You need to keep your data center running in accordance with rules of governance and compliance.
- You have critical performance requirements, meaning you need 99.9999 percent availability. Therefore, a private cloud may be your only option. This higher level of service is more expensive, but is a business requirement.

Some early adopters of private cloud technology have experienced server use rates of up to 90 percent. This is a real breakthrough, particularly in challenging economic times.

## Comparing public, private, and hybrid

We wish we could tell you that there are clear distinctions between private and public clouds. Unfortunately, the lines are blurring between these two approaches. Hybrid approaches also are starting to take hold. For example,
