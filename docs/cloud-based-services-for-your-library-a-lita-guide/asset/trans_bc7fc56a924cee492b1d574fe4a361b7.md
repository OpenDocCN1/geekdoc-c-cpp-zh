

management tools. Automated backups, automatic configuration, and regular monitoring and notification services go a long way in helping library IT feel more comfortable with IaaS management responsibilities and can lead overall to a more efficient IT organization. Another approach to simplifying an IaaS environment is to identify services, such as database servers, monitoring services, server builds, or e-mail services, that can be outsourced to a PaaS or SaaS platform. By taking these base-level services out of the mix, organizations can focus on running customized services for only the applications that require them.

## Service Cost

IaaS services often cost less than their SaaS and PaaS counterparts, primarily because the latter include value-added services such as IT management, data management, and premium service levels. At the very least, a service cost comparison should include the hard costs of server run-time, storage space, bandwidth, backup, and related infrastructure (e.g., monitoring, documentation, software licensing). A full cost consideration also needs to include hidden or soft costs including those for personnel time, infrastructure management, replication and redundancy plans, and data management. Though planning for and incorporating such soft costs is difficult, even a basic attempt can help organizations fully understand the long-term costs of cloud computing. There are SaaS services such as Cloudability (http://cloudability.com) whose primary focus is on monitoring the use of common SaaS, PaaS, and IaaS services and triggering notifications when services are likely to expire or exceed limits.

## Service Portability and Interoperability

Although interoperability between applications in an IaaS environment is less of an issue than in SaaS or PaaS environments, given the control an IT department has over the infrastructure, ensuring IT system portability and interoperability with other systems is a more complex issue. Operations such as firewall administration, user account management, and service management enable application interoperability and data transfer. The larger issue with IaaS platforms is the challenge of moving the entire service to a new platform. This capability has seen increasing support in recent years, and now many IaaS systems support some form of system migration. In addition, services such as RightScale offer configuration management services that help replicate cloud platforms and data across multiple providers. At the very least, a cloud computing plan should include short-term replication and long-term migration planning elements. This may include documenting the server image and data download and redeployment process, server configuration process, and DNS reassignment process.

## Comparing Costs across Providers

Expertise, organizational fit, and technical features are important, but a cloud service cannot be competitive if it does not have a competitive business model. Comparing services from Amazon, Linode, and Rackspace actually turns out to be rather difficult, because each service takes a different approach to grouping and pricing IT resources. The comparison offered here uses the service with the most bundled IT resources as part of its pricing model (table 5.1). Unlike Amazon and Rackspace, Linode charges on a monthly level and includes specific data transfer capacity in addition to CPU, RAM, and storage resources. For this reason, two Linode servers are used as template servers for comparative purposes.

Table 5.1 shows the comparative cost for these three services based on a small server template. The table includes two entries for Amazon, the first for an unreserved or “on-demand” instance and the other for a reserved instance. Amazon uses server reservations to allow customers to pay a reservation fee that varies based on server size, server region, and expected utilization (i.e., heavy, light, or medium use). For this comparison, reservation fees were used for the U.S. East region and heavy (100 percent uptime) usage. One area of inconsistency in this comparison is with the charges for outgoing traffic. Linode servers include a specified level of data transfer with each server that is not included in Amazon or RackSpace server prices. To compare costs equally, data transfer costs for both Amazon and Rackspace are included at the Linode data transfer levels.

### TABLE 5.1
Comparison of IaaS Provider Costs

| Provider* | Upfront charges | Server costs (monthly) | Bandwidth charges (monthly) | Storage cost (monthly) | Total monthly cost | Yearly cost |
|---|---|---|---|---|---|---|
| Amazon (small) | $0.00 | $14.64 | $24.00 | $0.00 | $38.64 | $463.68 |
| Rackspace (small) | $0.00 | $21.90 | $36.00 | $0.00 | $57.90 | $694.80 |
| Linode (small) | $0.00 | $19.95 | $0.00 | $0.00 | $19.95 | $239.40 |
| Amazon reserved (small) | $62.00 | $8.88 | $24.00 | $0.00 | $32.88 | $456.56 |
| Amazon (medium) | $0.00 | $118.40 | $96.00 | $0.00 | $214.40 | $2,572.80 |
| Rackspace (medium) | $0.00 | $87.60 | $144.00 | $0.00 | $231.60 | $2,779.20 |
| Linode (medium) | $0.00 | $79.95 | $0.00 | $0.00 | $79.95 | $959.40 |
| Amazon reserved (medium) | $390.00 | $23.68 | $96.00 | $0.00 | $119.68 | $1,826.16 |

* Small server = 512 MB RAM, 20 GB storage, and 200 GB data transfer.
Medium server = 2 GB RAM, 80 GB storage, and 800 GB data transfer.

The apples-to-apples comparison in table 5.1 shows Linode as a cost leader for both small and medium-sized servers. In real-world costs, however, libraries may find considerable savings by going with providers that do not bundle data transfer charges with server fees. In fact, in real-world usage over two years with one large and two small servers in operation, the Z. Smith Reynolds Library found that data transfer varied between 100 and 200 GB of data transfer per month and also found that there was more need for storage space and server capacity. Clearly this makes selecting a cloud provider difficult, if only because the growth of services over time can be difficult to map. Our comparison of these IaaS providers found that differences in storage amounts, a lack of specificity of CPU power, and variation in how each company handles value-added services such as system backups, support requests, and server resizing make selecting a provider a matter of local factors. For instance, whereas Linode charges $1 per GB per month for each gigabyte allocated above the included storage amount, Amazon charges $0.10–0.125 and Rackspace charges $0.10. This difference could have a considerable impact in changing the cost for libraries with lower overall outbound data transfer but greater storage requirements for DAMS and discovery services.

## PLATFORM-AGNOSTIC APPROACHES TO CLOUD SERVICES

The idea of mixing and matching cloud service providers to find an optimal mix of cost, control, and service quality may not seem particularly groundbreaking. In practice, though, finding the right mix of service outsourcing, local management, and platform-specific migration can be difficult. In this section we explore some areas in which moving to SaaS or specific IaaS platforms can affect service quality and costs positively. Such approaches are not likely to solve all problems posed in the previous sections, but they may be right for organizations seeking a balance between wholly outsourced and internally managed cloud services. As a framework for this discussion, we should remind ourselves of the NIST reference model with its range of service roles associated with cloud platforms, including auditor, broker, provider, and consumer (see figure 1.1). In addition, this architecture explores elements that contribute to a well-run cloud service, including service provisioning and management and service monitoring.

Though it is important to understand each of these roles and to be able to identify service providers that fill them, it is also important to consider what combination of service providers and functions best fits a particular library's cloud service needs. For example, as important as it is to have monitoring, replication, and auditing services, small cloud deployments may be able to utilize a single provider that meets these needs whereas larger deployments may need to seek out providers with more complex capabilities. Here again, the adage “The perfect is the enemy of the good” can be worth considering when bringing together cloud systems to support your information services. In general, a cloud service needs approaches to service provision (e.g., resource allocation and integration), service monitoring/auditing (e.g., service uptime, system security/privacy, service cost), and service management (e.g., staff access, service create/start/stop/terminate, service aggregation) that are easy to use and sustainable.

## Hybrid IaaS Provider Examples

Many of the previously reviewed providers including Amazon, Linode, Google Apps, and Heroku offer monitoring, auditing, and cost management services, and it is possible that these services will work well in a limited cloud architecture. There are other services, however, that support cross-platform provisioning, monitoring, and auditing services. This section explores cloud services that can provide libraries with alternative or hybrid approaches to creating a robust cloud-based infrastructure. Three classes of service are of particular interest: multiplatform IaaS solutions, SaaS solutions for effective IT service management, and a mix of cloud resources for point-of-need services.

## Multiplatform IaaS Solutions

Unlike other IaaS providers, RightScale focuses on adding management, monitoring, and replication layers on top of IaaS services rather than on providing cloud computing services of its own (figure 5.4). RightScale supports multiple providers including Amazon, Datapipe, Logicworks, Rackspace, and SoftLayer. In addition, it supports private cloud management through support for CloudStack and Eucalyptus systems. RightScale adds value to IaaS providers by providing

