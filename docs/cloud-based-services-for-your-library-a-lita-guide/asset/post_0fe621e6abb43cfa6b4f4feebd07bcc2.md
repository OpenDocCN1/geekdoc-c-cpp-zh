
This issue can be mitigated by subscribing to dedicated physical or virtual servers, but this tradeoff means that libraries often give up access to administrative control panels to get the ability to install and configure their own software. The benefit of these restrictions is that a server-based PaaS environment is the easiest approach to implement for libraries getting started with cloud and virtualized computing.

Careful attention must be paid to the SLA to ensure that the company has a commitment to providing a high level of service. Even uptime guarantees of 99.9 percent still allow 40 minutes of downtime per month. To understand what a company's uptime assurance means it is important to calculate the actual allowed downtime using an uptime calculator (http://easyuptimecalc.com) and to understand fully how service configuration impacts uptime assurance. In server-based PaaS environments it is possible to find site reviews or recommender services (http://webhostingtop.org, http://en.wikipedia.org/wiki/Web_hosting_service, www.tophosts.com) that provide information on site uptime not provided by the hosting company. Uptime assurances should be contained in the SLA, where they likely refer to the company’s service infrastructure as opposed to your specific application space. In addition to the SLA, PaaS providers may specify other licensing or contract agreements during the registration process.

## Things to Look for in a PaaS Contract

Understanding service contracts for PaaS providers is of particular importance because one's web applications depend on the hardware, software, and IT management services provided by the hosting company. Searching for the following items in provider SLA and license agreements may help guide platform selection:

- **System uptime:** What system uptime is assured or indicated? Are there specific guidelines or restrictions to this assurance? Are there contractual dependencies?
- **Service features:** What IT services are provided? Are there restrictions to specific services (e.g., SSH access)? Does the provider specify a means for managing software versions, dependencies, and other platform-specific functions?
- **Data ownership and privacy:** Does the provider give any assurance of data ownership or system isolation? Is the service located on its own hardware, or is it shared with other subscribers? Does the provider have policies regarding the monitoring of subscribers? What legal recourse is provided for subscribers with claims or complaints?
- **Security provisions:** How does the provider assure system security? Which security elements are the subscriber's responsibility? Does the system support encryption at all levels (e.g., service login, service configuration, service deployment)? What response procedures and communication plans are in place to address a breach in security?

## Service Cost

Two of the key advantages of hosting services are their relative low cost and ease of setup and management. For example, simple web-hosting providers charge five to ten dollars per month with first-year subscription rate discounts. These base charges may, however, mask second-year or ongoing costs and may not reflect advanced services such as SSL or dedicated IP addresses (important for DNS mapping). In addition, automated backups, additional storage space, and other premium services are likely to be additional charges. For this reason, comparing hosting services at a cost level can be difficult and should be approached with a list of required features.

Table 4.1 shows a cost comparison between different types of PaaS providers based on a simple web-hosting platform with limited data and space requirements and support for dedicated IP and SSL. Rows one and two include costs for two web-hosting companies. Row three documents the cost for a virtual server with dedicated memory and hard drive space. Row four shows costs for a dedicated physical server with specified memory, CPU, and hard disk specifications. Row five documents a provider that supports preconfigured virtual private servers in a PaaS environment and was selected to be roughly equivalent to the dedicated private server in row four. For comparative purposes, rows six and seven include costs for IaaS Amazon web service servers. As the chart shows, simple web hosting is much cheaper than reserved, private, or IaaS server platforms. This cost savings comes with limitations such as lack of reserved CPU or memory and lower levels of assured IT service and could feature additional charges for add-on services such as system backups. In addition, important value-added services such as dedicated IP addresses and SSL security can be more expensive and do increase the total cost of PaaS services.

### TABLE 4.1
Cost Comparison of Small Servers from PaaS and IaaS Providers

| Hosting type | Yearly subscription | SSL support (private IP, SSL) | Total yearly cost |
|---|---|---:|---:|---:|
| Shared virtual server (Provider 1) | $95.40 | $75.00 | $170.40 |
| Shared virtual server (Provider 2) | $107.40 | $62.40 | $169.80 |
| Virtual private server (Provider 2) (256 MB RAM) | $299.40 | $15.00 | $314.40 |
| Dedicated server (Provider 2) (2 GB RAM) | $1,188.00 | $15.00 | $1,203.00 |
| Virtual private server (Provider 3) (1.7 GB RAM) | $1,023.00 | $15.00 | $1,038.00 |
| Virtual private server (Provider 4) (1.7 GB RAM, no reservation) | $702.72 | $15.00 | $717.72 |
| Virtual private server (Provider 4) (1.7 GB RAM, yearly reservation) | $335.52 | $15.00 | $350.52 |

## Service Portability and Interoperability

Easy configuration, deployment, and management are important benefits of server-based PaaS solutions, but they often come at the expense of portability and scalability. When selecting a PaaS solution, it is important to understand what system migration options exist and to document the process for implementing your production environment in a selected PaaS provider. These elements include

## Creating a Fail-Forward Plan

Having a good fail-back and fail-forward plan is key to taking on the responsibility of managing your own IT services. A good fail-forward plan should include documentation on

- Application elements
- Core application requirements (e.g., Linux, MySQL, PHP, additional libraries)
- Application version and dependencies
- Application backups (e.g., executable scripts, customized files, database files)
- System configuration (e.g., DNS mapping, user account creation)

This documentation should not just be abstract but should include a plan for implementing your service in a new environment. This may seem unnecessarily complex, but if you are depending on a PaaS server environment it is important to be prepared to migrate to a new provider if the current provider has significant technical problems or goes out of business.

system configuration (e.g., users, open ports, DNS settings, application versions), database and file system contents (e.g., exported database files, backed-up file system), and web server configuration (e.g., home directory, virtual hosts). Though some services such as database and file system elements can be replicated using system export and import functionality, other services such as user management, firewall configuration, and DNS service are likely only configured through the managed web portal. Thoroughly documenting these elements and ensuring that proper backups are created are of great help and simplify the migration process. As a result of the limitations associated with hosted PaaS environments, single-application migrations may be fairly easy, but highly customized applications that depend on specific software elements and versions or on multiple configuration elements (e.g., DNS, database, firewall, web server) are much more difficult to migrate when compared to other cloud platforms.

## USING PAAS SOLUTIONS AS AN APPLICATION PLATFORM

In this approach to PaaS, services are geared not toward providing a broad web-hosting platform but rather toward supporting a specific technology stack hosting specific web services. Examples include Google Apps Engine, Heroku, Salesforce, and certain elements of Amazon Web Services (AWS) (e.g., Elastic Beanstalk). These services focus on the “single-platform” method, often supporting limited web application frameworks, databases, and database connection methods. Though the IT stack is limited, the service can provide a more robust cloud infrastructure, ability to scale in response to user requests, and ability to integrate closely with a development environment. For example, Google Apps Engine restricts the developer to versions of Java, Python, and Go and further limits development options by supporting only an NoSQL database on its platform. These tradeoffs enable Google to offer a highly scalable service at very low cost to subscribers. Likewise, Amazon Elastic Beanstalk supports limited deployment frameworks including Java, PHP, Python, and .NET and relies on databases and persistent data to run on other parts of the AWS service infrastructure. By supporting a specific type of deployment, Amazon is able to incorporate the benefits of PaaS environments such as replication and automatic scaling in response to service load. Likewise, by supporting a specific approach to packaging and deploying applications, Elastic Beanstalk enables support version control over the application, enabling easy testing and deployment of new application versions.
