# Infrastructure as a Service (IaaS)

![](bbox=[0.11, 0.15, 0.2, 0.26])

The Infrastructure as a Service layer offers storage and compute resources that developers and IT organizations can use to deliver custom business solutions. A cloud provider wants the provisioning capability associated with the IaaS to be designed as a modular service with published interfaces so it can be used for many different situations.

Say you have a group of applications that you want to run in a public cloud because you want capacity on demand. You sign up with an IaaS provider. Via your Web browser, you can buy this capacity and start running your applications on the service. The service is provisioning the capacity. While you’re running the application, the service provisions hardware to run it and then de-provisions the virtualized servers when you’re done.

![](bbox=[0.1, 0.37, 0.2, 0.48])

As a user of this capacity provisioning service, you don’t need to know how the provider is making the service happen; it is a black box to you. If the cloud weren’t service oriented, you’d have to figure out how to provision your application to the environment. With the cloud, you can use a single provisioning service.

# Platform as a Service (PaaS)

The Platform as a Service layer offers development environments that IT organizations can use to create cloud-ready business applications. This is offered as a set of black-box services that lets developers build applications on top of the compute infrastructure. This might include developer tools that are offered as a service to build services, or even data access and database services, or even billing services.

In these situations, the principles of SOA (such as loose coupling and reusability) have been applied to IT infrastructure components that are delivered as cloud services to PaaS users. Developers in your organization may locate the platform services they need by referencing a service catalog.

# Software as a Service (SaaS)

![](bbox=[0.1, 0.72, 0.2, 0.83])

With Software as a Service, the provider hosts the software for you so you don’t need to install it, manage it, or buy hardware for it. All you have to do is connect to it and use it.

For example, you might make use of CRM as a service or accounting as a service. Many of these providers have created their services in a modular way to enable scalability (because you’re using these services along with perhaps thousands of other clients). A services-oriented approach allows the provider, for example, to swap out functionality easily.