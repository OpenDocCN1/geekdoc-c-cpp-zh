
Data destruction controls to ensure that when data is permanently deleted it is deleted from everywhere — including all backup and redundant storage sites.

## Securing data for transport in the cloud

Regarding data transport, keep two things in mind:

- Make sure that no one can intercept your data as it moves from point A to point B in the cloud.
- Make sure that no data leaks (malicious or otherwise) from any storage in the cloud.

None of these concepts are new; the goal of securely transporting data has been around as long as the Internet.

In the cloud, the journey from point A to point B might take on three different forms:

- Within a cloud environment
- Over the public Internet between an enterprise and a cloud provider
- Between clouds

The security process may include segregating your data from other companies’ data and then encrypting it by using an approved method. In addition, you may want to ensure the security of older data that remains with a cloud vendor after you no longer need it.

A *virtual private network (VPN)* is one way to manage the security of data during its transport in a cloud environment. A VPN essentially makes the public network your own private network instead of using dedicated connectivity. A well-designed VPN needs to incorporate two things:

- *A firewall* to act as a barrier between the public Internet and any private network (like at your enterprise).
- *Encryption* to protect your sensitive data from hackers; only the computer that you send it to should have the key to decode the data.

## Looking at Data, Scalability, and Cloud Services

The need to process continually increasing amounts of data is one of the key factors driving the demand for cloud services.

For example, until YouTube, virtually all public video was stored by TV networks. The explosive amount of video (a type of data) currently available through YouTube was unimaginable prior to its creation in 1995. Today, you store videos, watch videos, and search for videos by using YouTube as your video provider (to handle the streaming of the video to your Web site).

A number of emerging technologies for managing these increasing volumes and diversity of data are worth mentioning:

- ✓ **Resources to support large-scale processing and data mining in the cloud:** One example of this type of computing-intensive application is scientific research for computational genomics. Other examples include business services for tracking and analyzing radio frequency identification tags, analyzing news feeds in real time, providing real-time stock quotes to trading floors, and analyzing product data to provide real-time pricing promotions. Organizations supporting these types of applications are often in critical need of more IT infrastructure, computing power, and data management capabilities than they have internally.

- ✓ **Databases and data stores in the cloud:** New databases are being created for the cloud environment. Some companies may just want to store their data there; others may be building services on top of the data.

- ✓ **Data archiving in the cloud:** Archiving data offsite has been popular for a number of years. Some cloud providers are trying to put a new spin on this.

In the following sections, we examine each of these technologies.

### Large-scale data processing

The lure of cloud computing is its elasticity: You can add as much capacity as you need to process and analyze your data. The data might be processed on clusters of computers. This means that the analysis is occurring across machines.

Companies are considering this approach to help them manage their supply chains and inventory control. Or, consider the case of a company processing product data, from across the country, to determine when to change a price or introduce a promotion. This data might come from the point-of-sale (POS) systems across multiple stores in multiple states. POS systems generate a lot of data, and the company might need to add computing capacity to meet demand.

This model is large-scale, distributed computing and a number of frameworks are emerging to support this model, including

- MapReduce, a software framework introduced by Google to support distributed computing on large sets of data. It is designed to take advantage of cloud resources. This computing is done across large numbers of computers, called clusters. Each cluster is referred to as a node. MapReduce can deal with both structured and unstructured data. Users specify a map function that processes a key/value pair to generate a set of intermediate pairs and a reduction function that merges these pairs.

- Apache Hadoop, an open-source distributed computing platform written in Java and inspired by MapReduce. It creates a computer pool, each with a Hadoop file system. It then uses a hash algorithm to cluster data elements that are similar. Hadoop can create a map function of organized key/value pairs that can be output to a table, to memory, or to a temporary file to be analyzed. Three copies of the data exist so that nothing gets lost.

### Databases and data stores in the cloud

Given the scale of some of these applications, it isn’t surprising that new database technologies are being developed to support this kind of computing.

Some database experts believe that relational database models may have difficulty processing data across large numbers of servers — in other words, when the data is distributed across multiple machines. Performance can be slow when you’re executing complex queries that involve a join across a distributed environment. Additionally, in an old-style database cluster, data must either be replicated across the boxes in the cluster or partitioned between them. According to other database experts, this makes it hard to provision servers on demand.

In response, some large cloud providers have developed their own databases. Here’s a sample listing:

### Data archiving

Data backup and archiving is nothing new. In fact, many companies are used to archiving static, seldom-used data offsite. Much of this is driven by compliance regulations that require companies to archive records for a number of years.

The cloud has different data archiving models. In some models, the archive may be available on demand. In others, this may not be the case.

## Sorting Out Metadata Matters

![](img/2d28ab1e4ea39ed71271c8bf426f216b_107_0.png)

Metadata is of critical importance to the ongoing reliability and integrity of your data in cloud environments. This is because metadata provides the means for your data to be understood in context with its intended use or meaning. Metadata is defined as the definitions, mappings, and other characteristics used to describe how to find, access, and use a company’s data (and software) components.

One example of metadata is data related to an account number. This might include the number, description, data type, name, address, phone number, and privacy level. The term account number may be defined differently depending on the application, and it may be interpreted differently across multiple end-user companies or cloud service providers.

Metadata helps make sense of the varied definitions and creates a consistent level of understanding about the data. Metadata — whether supplied and maintained by your company or your cloud service provider — can be used as the traffic cop to ensure that the data traffic is directed to the appropriate location at the right time.

## Talking to Your Cloud Vendor about Data

You’re thinking about using some of the data services in the cloud. Before you sign the contract, remember that data (especially your company’s data) is a precious asset and you need to treat it as such.

![](img/2d28ab1e4ea39ed71271c8bf426f216b_107_1.png)

In addition to issues surrounding security and privacy of your data that we cover earlier in the chapter, we recommend asking your potential vendor about the following topics:
