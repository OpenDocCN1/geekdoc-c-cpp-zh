
or industry-standard applications but pose challenges for traditional library applications. Server-based PaaS platforms are largely designed to fit the needs of small and medium-sized users, and application-based platforms are designed to be transparent and highly available.

## REFERENCES

Bryant, Sally, and Grace Ye. 2012. "Implementing OCLC's WMS (Web-Scale Management Services) Circulation at Pepperdine University." Journal of Access Services 9 (no. 1): 1–17. doi:10.1080/15367967.2011.629921.

Code4Lib. 2012. "Anyone Implementing Common LIS Applications on PaaS Providers?" Code4Lib Listserv archive, March 29, 2012. http://serials.infomotions.com/code4lib/archive/2012/201203/0983.html.

De Wilde, Max. 2012. "Collective Access on Red Hat OpenShift." http://homepages.ulb.ac.be/~svhoolan/redhat_ca_install.pdf.

Hoofman, Matt. 2012. "Wordpress-Heroku." https://github.com/mhoofman/wordpress-heroku.

Liu, Cricket, and Paul Albitz. 2006. DNS and Bind. Sebastopol, CA: O'Reilly.

Loo, Jeffery. 2010. "Library Instruction through Online Video and Social Media." Chemistry and Chemical Engineering Library, University of California, Berkeley, last modified July 16, 2010. www.lib.berkeley.edu/CHEM/instruction/video/index.htm.

Matienzo, Mark A. 2012. "Blacklight on Heroku." https://github.com/projectblacklight/blacklight/wiki/Blacklight-on-Heroku.

OCLC. 2012. "University of Delaware Chooses OCLC Worldshare." OCLC press release, January 18. www.oclc.org/news/releases/2012/20125.htm.

Stein, T. J. 2011. "Running WordPress on Heroku + Amazon RDS." http://tjstein.com/2011/09/running-wordpress-on-heroku-and-amazon-rds/.

Van Hooland, Seth, and Bram Wierckx. 2011. Open Source Software Platform Collective Access as a Service Solution." DISH (Digital Strategies for Heritage) 2011 conference, December 7, Rotterdam, Netherlands.

## Infrastructure as a Service

For libraries with a background in managing traditional IT resources, an IaaS approach to cloud computing is likely to be a good fit. IaaS providers simplify the process of reserving, starting, and managing IT resources including servers, storage space, network tools, and monitoring tools. This makes it possible for libraries to create an IT infrastructure tuned to specific needs and applications. In addition, these systems often support customization of specific resources such as operating system, application platform, disk space, and memory.

Like dedicated PaaS systems, IaaS systems require a level of investment in the computing environment and have some complicated elements that require familiarity with IT systems and development platforms that are not common skill sets in libraries. With this expertise, the ability to use IaaS resources to create and manage a flexible and robust computing environment can be transformative for libraries seeking new ways to address their IT needs. This also means that IaaS solutions require greater attention to security, backup, and service restoration procedures than PaaS or SaaS solutions and place the burden of ensuring scalability and sustainability on the library rather than the cloud service provider.

In this chapter we review IaaS solutions from two perspectives: using IaaS resources to replicate traditional service architectures, and using them to create cloud-aware service architectures. Before we explore these solutions in depth, it is worth defining a few generic resource types that are common to each of the IaaS solutions. The following list may be familiar, but here they contextualize the discussion of IaaS examples throughout the chapter.

### 32 bit vs. 64 bit operating system
These numbers refer to the underlying architecture on which the operating system runs. These different hardware architectures require different versions of the operating system, capable of different levels of CPU and memory management. Many IaaS providers base the type of operating system on the server size selected and use some method to automatically scale a 32 bit system to a 64 bit system. Amazon does, however, support operating 64 bit computing images on 32 bit platforms, making it preferable to select a 64 bit operating system distribution if scaling to larger servers is a potential need.

### Application programming interface (API)
In cloud environments, an API is a standardized programmatic mechanism for interacting with a web service. All IaaS providers have some form of API and often provide enhanced service and functionality through programmatic tools that implement the API functions. There is some effort to begin standardizing cloud API using open-source approaches.

### Backup/restore
IaaS providers typically have some systemwide method for handling server and storage space backups. Some vendors provide a managed backup solution (e.g., Linode); others simply provide cloud infrastructure backup tools (e.g., Amazon).

### Bandwidth/transfer in and out
IaaS vendors monitor and charge for traffic to and from server instances. It is becoming less common for vendors to charge for incoming traffic, but all vendors discussed in this chapter charge for outgoing traffic. Some vendors (e.g., Linode) include base data transfer levels with server instances.

### Cloud file system
Cloud file systems are differentiated from traditional file systems in that they are accessible via APIs rather than via traditional disk or mounting mechanisms. Cloud file systems may feature automatic replication, version control, and other value-added services that make them more reliable than traditional storage.

### Configuration profile
Configuration profiles are sets of instructions that facilitate the configuration and deployment of cloud resources. This is an emerging feature of IaaS providers and is implemented differently in each IaaS solution explored in this chapter. The basic concept is similar to automatic configuration platforms such as Puppet and Chef, except

that they tend to be used only during system launching rather than on an ongoing basis.

### Domain name service (DNS)
DNS is a global Internet application that resolves domain names (mycompany.com) to IP addresses (10.10.10.10). Cloud providers offer DNS solutions that are turned to the specific needs of cloud users, such as multiregion routing.

### Endpoint
In cloud computing, an endpoint is the point at which the private cloud meets the Internet. Amazon offers multiple cloud regions, each of which serves as an endpoint for traffic from its internal cloud.

### File bucket/container
The bucket or container is a unit of storage related to cloud-based file systems. Files can be uploaded only once identified with a specific bucket or container. Cloud providers may also associate access control with a bucket or container.

### Load balancers
Cloud providers often support some automated method for implementing a load-balanced application. Load balancers monitor traffic on a given service and reroute traffic or scale server resources as needed.

### Machine images
Machine images are the root of the launched servers in IaaS environments. Some providers (e.g., Amazon) allow users to upload, publish, and download images in a community portal; others (e.g., Rackspace, Linode) offer a smaller suite of vetted machine images. All services offer some mechanism by which customized machine images can be saved to the customer's cloud service and reused or repurposed.

### Messaging or queuing service
These services provide independent means for sending messages to users or applications. Amazon offers multiple forms including Simple Email Service (SES) and Simple Notification Service (SNS). Messaging services can replace the need to run traditional e-mail and other messaging services on a machine image.

### Mountable volume
Some IaaS providers offer a more traditional form of storage that can be mounted as a disk or volume on server resources. Amazon's form of this storage (elastic block storage, EBS) features user-controlled size, format, attach/detach services, and long-term storage.

### Public/private keys
In addition to password-based security, cloud providers may support the generation or use of public/private keys for resource
