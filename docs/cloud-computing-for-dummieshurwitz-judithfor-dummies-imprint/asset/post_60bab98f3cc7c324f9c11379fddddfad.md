
safely. Unlike a traditional data center, the cloud service provider has to manage both virtual as well as physical components. The provider has to make sure that each customer’s data is well protected and supported. When the provider has done a good job, you may be unaware of it. This is something the customer rarely ever sees.

![](img/2d28ab1e4ea39ed71271c8bf426f216b_256_0.png)

**Figure 20-1:** Various cloud services layers.

## Managing based on services

Management service types depend on the type of cloud service the vendor provides. For example:

- A vendor providing cheap storage may not necessarily have a sophisticated set of management services.
- Another provider might have different levels of customer support and may act more like an outsourced service provider.

## Managing several cloud providers

You may end up working with several different cloud providers — one for a Software as a Service (SaaS) application and another for Infrastructure as a Service (IaaS), for instance. Although each vendor will have its own management services, your organization is responsible for oversight.

Here’s a simple scenario that drives home this point: Assume you have contracted with a SaaS service to manage your sales leads. This company doesn’t have its own cloud center, so they contract an IaaS provider. When something goes wrong, it may be tough to figure out the source. If you’re the customer using the SaaS application, you’ll call your provider. How sophisticated is their service management system? Can they quickly trace the cause of the problem?

It may be harder than it seems. For example, the problem might occur because the platform provider just upgraded to a new version of an operating system

and forgot to upgrade a script or a component. The problem may be a power outage.

![](img/2d28ab1e4ea39ed71271c8bf426f216b_257_0.png)

Many companies today are using emerging cloud providers that offer very inexpensive, or even free, services. While this can dramatically improve your bottom line, it may also cause problems. What happens when your free service quits working? Some free (or nearly so) services provide online service status updates, but many do not.

![](img/2d28ab1e4ea39ed71271c8bf426f216b_257_1.png)

Many of these issues related to service levels and oversight in the cloud are a function of the relative immaturity of the cloud market itself. It may be hard to assess how sophisticated the service management environment of a specific cloud provider is. In fact, you’ll likely sign up with a SaaS provider without knowing anything about the way it manages its own environment. However, this may be one of the most important questions to ask — especially if you’re dependent on the application.

## Customers

If you’re a business manager using a cloud provider, you need visibility into both the computing infrastructure and the applications you’re using in the cloud. You need to understand some key factors so you can manage both your cloud-based services as well as your own data center. (Read more about this topic in the “Gaining Visibility” section later in this chapter.)

From an overall management perspective, you need to at least be able to do what’s described in the following sections.

## Provision resources in the cloud

If you’re using a public or private cloud, you need a mechanism that enables you to provision new resources when you need them. Can this be automated, or does someone have to manually do it? This administrative function includes setting up your cloud environment as well as building and deploying applications in the cloud. This administrative process will be needed regardless of whether you’re using a public or a private cloud.

It is also true, in a slightly different way, in the SaaS environment. The service provider manages the performance levels of the overall environment that might require the addition of servers, increasing processing power, and so on in a compute environment. It may include provisioning a database or mapping your data to your new cloud application.

## Deal with incidents and problems

When your organization begins adopting some cloud computing capabilities, you must have a plan to handle problems such as unexpected outages. Although the cloud computing vendor will have its own infrastructure and tools for this, you have to be proactive too. Know how your provider handles changes to its environment.

Depending on how critical the cloud service is to your business, you have different levels of support. For example, if you’re a large corporation using a cloud service for all your company’s email services, you probably want to establish a plan with your provider for direct support to handle problems.

![](img/2d28ab1e4ea39ed71271c8bf426f216b_258_0.png)

Work with your cloud provider if you’re dependent on these services to run your business. You need to have a process for handling incidents and problems. You also need to explain to your management what happens if and when a service fails.

## Monitor and measure

Of course, you want to make sure that you can see the performance level of the services in the cloud. This monitoring should be incorporated into your overall capacity plan for your company.

You really need these things overall:

- ✔ A dashboard that provides you with insights across the applications and services that are running in your data center and those that are running in a cloud.
- ✔ A service level agreement across your own services and those provided by cloud providers to get a true picture of the service you are providing to your company.

## Bill and other services

All cloud providers will bill your company based on one of the following:

- ✔ How many users are supported
- ✔ How much capacity you use
- ✔ How many services you leverage

As with any service you purchase, it is important that you have oversight. You should be able to “see into” your billing, especially if you’re automatically provisioning capacity. Most service providers will provide customers with an application that will include information about what resources they are being charged for. If the service provider can’t provide this accounting information, something is wrong.

## Hybrid environments

Your company will probably have a *hybrid* environment: a traditional data center, a private cloud, and some cloud services. That hybrid is part of what makes cloud management so complex. They may use virtualized servers as well as dedicated physical servers.

Chapter 17 defines *virtualization* as using computer resources to imitate other computer resources or even whole computers. The term is very broad and can include virtualizing everything from memory to software, but we keep it simple for right now.

This hybrid environment requires management of both the virtual servers and the physical infrastructure beneath. And, because there is a good chance that most enterprises won’t move *all* of their computing resources to the cloud, they have to be concerned with how this hybrid environment gets managed. Two important capabilities need to be in place to manage this hybrid world: the service catalog and the Configuration Management Database (CMBD).

## The service catalog

One of the important factors in managing a cloud is to ensure a way to manage IT assets and activities. Enter the service catalog (defined as part of the *Information Technology Infrastructure Library [ITIL] Service Design* best practice). The catalog is a component list that makes up internal and external services that are available to an organization.

A typical service catalog includes such items as the definition of the service, its service level, who is entitled to use that service, and what components are required to execute that service. Clearly, a service catalog is required for organizations to manage services in a hybrid world — across data centers, private and public clouds, as well as hosted environments. The service catalog is an essential tool for both cloud providers and customers that need a view into the assets they are using. Many cloud providers package a service catalog to help their customers work between their cloud and external resources.

## The Configuration Management Database (CMDB)

To understand what services are being managed across your various computing environments, you should keep track of changes. That is the role of the *Configuration Management Database (CMDB)*. For example, many cloud environments use extensive virtualization to add efficiency. Virtualization enables the abstraction of hardware assets so that these assets can be used for multiple purposes. These varied uses increase the difficulty of tracking changes to these resources. However, it’s important for the cloud provider (even if that’s you in your private cloud) to track these assets and understand what’s been changed and what state that service is in.
