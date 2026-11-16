
- Infrastructure-as-a-Service (IaaS)

IaaS is a service model in which providers offer access to base-level computing resources: servers, disk storage, and so on. Although the resources themselves are normally virtualized, the end product looks and behaves for consumers in almost identical fashion to infrastructure resources configured on-premise. Some of the more prominent IaaS providers in the market as of the time of writing include Amazon, Microsoft, and Google.

- Platform-as-a-Service (PaaS)

As the name suggests, the PaaS service model offers customers a full-fledged computing platform. Here, in addition to virtualized hardware resources (as part of an IaaS offering), PaaS also includes an installed operating system (OS), one or more programming environments, and general-purpose services, such as database access. Collectively, these platform resources offer developers everything they need to develop applications within the cloud. Some of the more prominent PaaS solutions in the market as of the time of writing include Amazon Web Services (Amazon AWS), Force.com, Google App Engine, and Microsoft's Windows Azure.

- Software-as-a-Service (SaaS)

SaaS is just that: software that's provided to customers as a service. Here, as opposed to commercial off-the-shelf (COTS) packages customers have historically installed on-premise, the installation and maintenance of SaaS solutions is managed exclusively by the software provider. This frees customers from the headaches of maintenance, but also restricts their ability to customize the software. Although most SaaS solutions are somewhat configurable, the scope of what can be enhanced is fairly limited by comparison.

The positioning of these three service models within the cloud computing paradigm is shown in Figure 1.1. This service stack provides customers with the flexibility they need to choose the model that works best for them. Starting from the bottom up, it's important to note that the higher you go within the service stack, the more abstracted the offering becomes. For example, when customers purchase licenses for a SaaS solution, they're not only buying access to the software itself; included in this offering are the underlying platform and infrastructure resources upon which the software's deployed. In addition to simplifying the buyer experience, this also makes it possible for customers to be up and running with a particular software package in mere minutes as opposed to the days, weeks, or months that are normally required to stand up a new server and install software packages on-premise.

![](img/cf7012644082c115a2181376d9b7486d_31_0.png)

Figure 1.1 Understanding the Cloud Computing Service Model

Because this is a book about SAP software, you're probably wondering how SAP's various cloud-based offerings fit into the service model diagram shown in Figure 1.1. These relationships are highlighted in Figure 1.2.

![](img/cf7012644082c115a2181376d9b7486d_31_1.png)

Figure 1.2 Overview of the SAP Cloud Strategy

Considering the overview diagram contained in Figure 1.2, let's focus in on some of the various components that make up SAP's cloud strategy:

### IaaS

As opposed to traditional IaaS offerings, which provide generalized access to hardware resources, SAP's IaaS offerings consist mostly of hosting services. This starts with the SAP HANA Enterprise Cloud (SAP HEC), which is a hosting service that allows customers to run their SAP Business Suite and/or SAP Business Warehouse (SAP BW) systems on a private cloud that's managed by SAP.

In addition to SAP HEC, SAP also provides SAP HANA-related infrastructure services as part of SAP HCP. For customers who have previously purchased an SAP HANA license, SAP provides SAP HANA Infrastructure Services. Net new customers have the option of subscribing to SAP HANA DB Services, which bundles infrastructure and license subscriptions together. In either case, SAP provides the hardware infrastructure to stand up an SAP HANA instance in the public cloud.

### PaaS

As noted earlier, SAP HCP is SAP's PaaS offering. As you can see in Figure 1.2, SAP HCP runs in the public cloud and undergirds SAP's SaaS solutions by providing a rich set of application services that can be used to develop extension applications and the like.

### SaaS

Over the course of the past several years, SAP has built up a fairly large cloud application portfolio that blends core ERP functions with applications that were attained via acquisitions (e.g. SuccessFactors, Concur, Ariba, and so forth). In early 2015, this portfolio of applications was given a common name: SAP S/4HANA. SAP S/4HANA is the next generation of SAP Business Suite, and will ultimately unite these applications into a full-scale cloud application suite. As you can see in Figure 1.2, SAP S/4HANA customers will have the option of deploying SAP S/4HANA on-premise, on the public cloud, or privately as part of a managed cloud solution. This flexibility allows customers to slowly move to the cloud and choose how much control they wish to delegate to SAP in terms of maintenance.

Though SAP S/4HANA represents the future of SAP's SaaS offering, we should also make mention of another SaaS offering that exists at the time of this writing for small/mid-size businesses: SAP Business ByDesign is an integrated, turn-key offering that allows small businesses to stand up a lightweight SAP Business Suite in the public cloud.

Throughout the course of this book, our focus will be on SAP HCP and, more specifically, the SAP HANA App Services portion of the overall SAP HCP services offering. This distinction is highlighted in Figure 1.3 and Figure 1.4. As you can see, SAP HANA App Services builds on top of the infrastructure services provided as part of the aforementioned SAP HANA Infrastructure Services and SAP HANA DB Services to include all of the services you would expect to find in a PaaS offering: application containers, enablement services, and so forth.

![](img/cf7012644082c115a2181376d9b7486d_33_0.png)

Figure 1.3 Overview of the SAP HCP Services Model (© 2015 by SAP SE. All rights reserved.)

![](img/cf7012644082c115a2181376d9b7486d_33_1.png)

Figure 1.4 SAP HCP Services Model in Detail (© Copyright 2015. SAP SE. All rights reserved.)

## 1.2.3 Some Historical Perspective

In his book *The Big Switch: Rewiring the World from Edison to Google* (W. W. Norton & Co., 2013), Nicholas Carr tells the story of Samuel Insull, a brilliant businessman who was among the first to see the practical benefits in packaging and selling electrical energy as a commodity. Such a notion might seem obvious in these modern times, but the concept was met with a considerable amount of opposition at the turn of the twentieth century. Indeed, among these opponents was Thomas Edison, Insull's former boss and long-term mentor. Believing that direct current (DC) was the only way to reliably transmit electricity, Edison felt that it was impractical to attempt large-scale distribution, because DC couldn't be transmitted very far.

Insull saw things very differently. With ever-improving electrical dynamos and the advent of Nikola Tesla's alternating current (AC), he felt that all of the foundational pieces were in place to establish large-scale power plants that could reliably transmit electricity for miles. Insull followed through with his vision and established the Commonwealth Edison Company, a prototype for modern electrical utility companies in the United States and eventually around the world.

After building up his infrastructure, Insull initially found that driving customer adoption was difficult. At the time, power supply systems were mostly built and managed internally by customers. Because even the smallest of power outages was viewed as a huge risk to production operations, customers were naturally very concerned about stability and generally felt that it was best to manage this risk in-house. Through a bit of shrewd marketing and negotiating, Insull was eventually able to convince a few strategic customers to give his services a try. Once the word of success spread, it didn't take long for other customers to see the viability of the model and jump on board.

Over the course of the next 30 years or so, this trend would continue to the point that hardly any companies in the United States operated their own power supply systems. Through centralization and economies of scale, electrical utilities were able to produce electrical power much more efficiently and reliably at a fraction of the cost. In time, companies simply could no longer afford to go it on their own.

Fast-forwarding about 100 years, we find that cloud computing is experiencing some of the same growing pains that the electrical utility industry faced in the early twentieth century. As a relatively new and somewhat abstract concept,
