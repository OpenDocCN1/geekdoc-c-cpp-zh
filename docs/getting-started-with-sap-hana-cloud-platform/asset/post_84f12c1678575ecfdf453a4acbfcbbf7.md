
## Final Thanks

And last, but certainly not least, we'd all like to say thanks to our editor, Kelly Grace Weaver. Kelly's simply the world's greatest editor and an even better person. Her saintliness was certainly put to the test on this project, and we could not and would not have been successful without her. This also goes for the rest of the crew at SAP PRESS who worked tirelessly behind the scenes to make this book a reality.

## PART I

## Foundations

In this chapter, we introduce you to the SAP HANA Cloud Platform and describe its positioning in the evolving SAP technology landscape.

## 1 Introduction to SAP HANA Cloud Platform

Since the initial release of SAP R/3 in 1992, SAP landscapes have primarily existed in isolation, being nestled safely within the nurturing confines of the corporate firewall. However, with the explosion of cloud computing and mobility in recent years, this has begun to change. Now, customers are looking to expand the limits of their SAP landscapes to support integration with cloud applications (provided by SAP or otherwise), mobile access, and the Internet of Things (IoT).

To address this ever-widening gap, SAP introduced SAP HANA Cloud Platform (SAP HCP). In this chapter, we’ll get to know SAP HCP and learn how it will play a central role within the SAP technology landscape in the years to come.

### Further Resources

The main product page for SAP HCP is hcp.sap.com, and serves as a valuable resource for SAP HCP material: trial systems, documentation, and more.

### 1.1 Introducing SAP HANA Cloud Platform

According to the SAP help documentation, SAP HCP is “an open, standards-based, and modular platform as a service for rapid development of on-demand applications.” This definition is a bit of a mouthful, so let’s take this point-by-point:

- First, we find that SAP HCP is a Platform-as-a-Service (PaaS) offering from SAP. Although we’ll have an opportunity to explore this distinction in further detail in Section 1.2, for now, it’s enough to simply note that SAP HCP is a platform that can be used to (rapidly) develop and deploy web applications in the cloud.

- SAP HCP is an open environment that offers developers lots of choice as it relates to the selection of programming languages and models, development tools, and so forth.

- In addition to being open, SAP HCP is also heavily standards-based, being developed from the ground up to support standards from leading standards organizations such as the W3C.

- Finally, we learn that SAP HCP is a modular platform that can be customized to meet the needs of all customer types and use cases.

In simplified terms, you can think of SAP HCP as a platform that customers can rent access to from SAP to develop and deploy applications in the cloud. From a technical perspective, this platform is not so different from application systems that are installed on-premise, such as the SAP Composition Environment. The primary difference is that SAP assumes responsibility for purchasing and maintaining the hardware, software, and other infrastructure-related concerns so that customers can focus on application development concerns.

### A Brief History

Even though SAP HCP more formally came into prominence in the latter part of 2014, it's actually been around for quite some time. In late 2011, we were introduced to the first incarnation of the product, which at that time went by one of several different names: SAP NetWeaver Cloud, SAP NetWeaver NEO, and, in many circles, just NEO. At that time, the product offering was fairly modest, consisting mostly of a Java application server and a series of basic cloud enablement services. This changed considerably over the course of the next 18 to 24 months, as new features and services seemed to be popping up on an almost weekly basis.

![](img/cf7012644082c115a2181376d9b7486d_27_0.png)

By mid-2013, NEO had reached a sufficient level of maturity that SAP began to quietly position it as part of their long-term cloud strategy. Around this same time, SAP decided to drop the NetWeaver/NEO naming in favor of the name we recognize today: SAP HANA Cloud Platform. From here, the product really began to pick up momentum as we saw the scope of the platform expand to include support for native SAP HANA development, HTML5 applications, and much more.

By the time the annual SAP TechEd/d-code conferences rolled around in late 2014, SAP HCP finally hit center stage as a key component in SAP's cloud strategy and vision. In many respects, this milestone marked the end of SAP HCP's infancy. Now, we look ahead to the emergence of SAP HCP as a production-ready platform for deploying cloud applications. With significant commitment and backing from SAP, the future of SAP HCP looks to be very bright indeed.

### 1.2 The Cloud Computing Revolution

Even though it's been a buzzword for quite some time, many people still have a hard time wrapping their heads around what the cloud is exactly. For some, it's a magical place where their music files live. For others, the cloud is a wild frontier that's much too insecure to trust with precious IT resources. Somewhere in the midst of all this chatter is an idea that's so simple and yet so powerful that you almost wonder why we haven't arrived at it before. With that in mind, in this section we'll take a look at the cloud computing revolution.

### 1.2.1 What Is Cloud Computing?

To a large extent, cloud computing is one of those stream of consciousness ideas whose origin is difficult to trace to any one particular individual or organization (see boxed note ahead). Like many economic trends, it's a concept that evolved organically as a result of the convergence of several key market conditions:

- A proliferation of inexpensive hardware components (e.g., multicore CPUs, main memory, and disk storage)

- Expanded availability of high-speed network access

- Continued advances and innovations in the fields of hardware virtualization

**Note**
To a certain extent, Antonio Regalado settled the origin of cloud computing in a 2011 article entitled “Who Coined ‘Cloud Computing’?” (MIT Technology Review, 2011). Here, he traced the origin of the term back to an internal business strategy document published by Compaq Computer Corporation in November 1996.

As these technologies and market conditions converged with one another, it became apparent to many technology companies that it would be possible to bundle access to computer resources and sell this access to customers using an on-demand, pay-as-you-go subscription model.

This idea, in and of itself, is not a novel concept. Indeed, hosting and co-location of server resources have been successful business models in the IT world for quite some time. The difference with cloud computing is that provider companies aren’t just standing up a handful of servers here and there to meet the demands of a particular customer. Instead, providers are building up huge server farms that, due to their overall size and computing power, can scale to meet the needs of hundreds or even thousands of customers at a time. This kind of economies of scale allows providers to provide access to computer resources at a fraction of the cost it would normally take to provision the same resources on premise.

To summarize, we can simply say that “cloud computing” is a term used to describe the packaging and distribution of computing resources as a commodity. Of course, as is the case with most commercial offerings, the way that these resources are bundled can vary greatly. Therefore, in the next section, we’ll consider some of the more prominent service models that have emerged in the cloud computing space.

### 1.2.2 Understanding the Cloud Computing Service Models

As the idea of cloud computing really started to take form in the mid-2000s, it quickly became apparent that there was not a “one-size-fits-all” service model that could possibly satisfy the needs and demands of customers looking to jump onboard the cloud computing bandwagon. Therefore, before too long, lots of specialty shops popped up offering a la carte services, such as online data storage and backup, application hosting, and more. When the dust settled on all this, three broad categories of service models had emerged:
