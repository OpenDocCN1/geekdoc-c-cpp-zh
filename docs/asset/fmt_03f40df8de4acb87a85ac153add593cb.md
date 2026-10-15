
By providing a configuration and monitoring platform, RightScale simplifies the process of replicating cloud services onto multiple providers. Although this leads to additional costs, it ensures that an organization’s service can persist even if its primary cloud provider experiences downtime. By supporting private as well as public clouds, RightScale also enables organizations to alternate between local computing resources and public or community cloud environments. This enables a new level of control for organizations that may want to manage IT services in-house except for those few occasions where additional IT resources are required.

Some providers take on the work of creating and managing machine images for customers but do not do the heavy lifting of service replication in the same way that RightScale does. For example, JumpBox (`http://jumpbox.com`) and Hyperic (`http://hyperic.com`) publish prebuilt AMIs on the Amazon platform. These prebuilt servers are designed to be run with minimal configuration while providing monitoring and configuration management services. They can facilitate the deployment of management of services but also require a level of expertise and
accounts as well as organizations that use multiple cloud providers. Cloudability offers a free usage tier for customers with less than $2,500 per month in cloud expenditures.

Another service similar in function but different in scope is Ylastic (`http://ylastic.com`; figure 5.6). Focusing primarily on the AWS and Eucalyptus platforms, Ylastic is a subscription service that provides monitoring, backup, service management, and server replication services through an easy-to-use web console. It features management functions in addition to auditing reports, but it functions only with Amazon and Eucalyptus services. As our exploration of PaaS and IaaS services shows, effective management tools that ensure cloud services are durable and easily recoverable are an important aspect of high-quality and sustainable cloud services. Ylastic makes this process easier by providing easy-to-use versions of Amazon services.

Ylastic provides tools that automate many of the complex processes required of Amazon adopters, such as automatic volume snapshots, application monitoring, availability zone migration, automatic image creation, and backup pruning (figure 5.7).

![](img/f597dcda42d1ecd1c6edb1e8e00d8ca1_136_0.png)

#### FIGURE 5.6
Ylastic management service

#### FIGURE 5.7
Ylastic backups

#### FIGURE 5.8
Ylastic monitoring

Ylastic conducts audits of security, cost, backups, and service redundancy services and monitors service availability. Monitoring includes a focus on service downtime and features multiple notification methods. It also tracks use trends and makes recommendations for removing unused cloud resources (figure 5.8).

## Using IaaS for Point-of-Need Service

To this point we have focused on IaaS providers that offer a distinct suite of services. Nevertheless, one of the primary benefits of turning to IaaS solutions is the ability to use distinct elements of the service without large overhead costs. For example, Iglesias and Meesangnil (2010) used Amazon S3 as a storage source for an OAIS-compliant digital object archival system. In combining local and cloud implemented resources they found an inexpensive alternative to SaaS offerings that amounted to a two-thirds reduction in cost per year. Because cloud services involve recurring costs, finding solutions that result in savings of this magnitude can shift the argument away from SaaS solutions. Since this work, Amazon has begun offering an automatic data synchronization service called Amazon Storage Gateway that offers the ability to synchronize locally stored data to Amazon S3 storage automatically.

Whereas Amazon’s focus is on simplifying the synchronization of data at the server level, there are also providers that offer client-level cloud-based data and file system tools. Cyberduck (`http://cyberduck.ch`), for example, is a multiprotocol file transfer and storage mounting service that supports a wide range of cloud storage services including Amazon, Google storage, Rackspace, and Windows Azure (figure 5.9).

Amazon S3 in particular supports advanced file storage service including access control, version control, and event logging. S3 is not a traditional file system, and it can be difficult to use S3 services without a secondary layer or client to facilitate access. Along with server tools that implement S3 integration (e.g., Amanda and KOALA) there are client-centric tools such as CloudBerry (`http://cloudberrylab.com`), JungleDisk (`http://jungledisk.com`), and BucketExplorer (`http://bucketexplorer.com`) that facilitate access to S3 by both implementing FTP, WebDav, or traditional file system volume/disc mounting services and managing services that otherwise can be difficult to manage including file deletion, version control, and access services.

Many of the tools mentioned in this section feature an implementation of Amazon, Microsoft, Rackspace, and other provider interfaces. Although there is a trend for new IaaS providers, particularly private cloud providers, to develop their

![](img/f597dcda42d1ecd1c6edb1e8e00d8ca1_139_0.png)

#### FIGURE 5.9
Cyberduck

command line tools consistent with the commands and parameters of the AWS API toolkit, this approach is far from standardized. As Baun and Kunze (2011, 2) point out, this level of standardization varies across platforms and feature sets. Although Amazon also supports many of the same functions using its web application interface, the command line tools enable automation and advanced access to EBS, S3, and AMI services. We have already explored services supported by Linode, Heroku, Amazon, and Google Apps Engine. Baun and Kunze point to several other PaaS and IaaS tools including GSUtil (`https://developers.google.com/storage/docs/gsutil`), a toolkit that provides direct access to Google Storage.

The inability of cloud subscribers to use a common toolkit to implement cloud services on multiple providers is a significant problem affecting the long-term sustainability and durability of cloud computing. In response to this need, Christian Baun and Marcel Kunze developed KOALA as an open-source product. The KOALA
toolkit both centralizes the management and deployment of cloud services on multiple IaaS platforms using a web service environment and provides a common toolkit library that supports multiple IaaS public and private cloud platforms including Amazon, Google Storage, Eucalyptus, and Nimbus. Unlike RightScale, KOALA is not focused on replicating services across multiple cloud providers but rather provides a common interface to manage disparate cloud providers.

## Configuration

Because this section focuses on combining SaaS, PaaS, and IaaS services to create an IT infrastructure, it is worth spending some time exploring which services need to be present in a cloud-based IT environment. These services include application monitoring, automatic configuration, cross-system backup/restoration, IT management documentation, and service and cost auditing. Although it is unlikely that libraries or IT departments are in the position to put all of these elements into place before adopting cloud-based services, they should ensure that these services are in place before moving toward complex IT service deployments in the cloud. For high-quality and sustainable IT service, these aspects must be accomplished:

- Optimize monitoring, backup, restoration, auditing, and service documentation functions; ensure that these services are bulletproof.
- Implement service documentation and ticket management systems on systems separate from the main service system. When production systems experience downtime, having access to documentation and management tools is essential to calm and quick service restoration.
