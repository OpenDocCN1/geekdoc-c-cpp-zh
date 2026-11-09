
So think about the various data centers around the world where companies have swarms of computers—as clouds. Lots of the biggest players in network computing, including Google, Amazon, Microsoft, IBM, and Yahoo, all have thousands of machines connected to networks running all sorts of software. Each of those centers is a cloud, and each processor, each disk drive, is a droplet of water in that cloud. In the cloud world, when you write a program, you don't know what computer it's going to run on. You don't know where the disks that store the data are, and you don't need to care. You just need to know how many droplets you need.

## Cloud to the Developer

Cloud computing is a fundamental change from how computers and software have worked in the past. Traditionally, if you wanted to run an application, you went out and bought a computer and software, set it up on your own premises, and ran your program. You needed to pick out which operating system you were going to run, handle the installation of your software, and maintain your computer—keeping track of software upgrades, security, backups, and so on.

With cloud computing, you don't do any of that. If you're a user of the cloud, you buy access to the application you want and then connect to it from anywhere. Installing the software, maintaining the hardware and software where the application runs, making sure that the data is kept safe and secure—none of that is your concern. In the cloud, you buy software as a service. If you need more storage than a typical user, you buy extra storage from the service provider. If that means buying and installing a new disk drive, that's up to the provider. You just buy storage-as-a-service from them: how they provide it is their problem. You tell them what you need—in both the physical sense ("I need 1TB of storage.") and in less tangible quality-of-service senses ("I need to guarantee that my storage is transactional, so that after I commit a change, data will never be lost."). You tell them your requirements, and some cloud provider will sell you a service that meets those requirements.

What this means is that when you're developing for the cloud, instead of buying a computer and running software on it, you break things down to basic building blocks, buy those pieces from service providers, and put them together however you want to build a system.

The building blocks are the resources you need to run a program or to perform a task. Resources include things like processing time, network

## Cloud versus Client-Server

In many ways, the basic style of development for cloud-based software is similar to programming for client-server computing. Both are based on the idea that you don’t really run programs on your own computer. Your computer provides a window into an application, but it doesn’t run the application itself. Instead of running the program on your computer, all you do on your own computer is run some kind of user interface. The real program is running somewhere else on a computer called a server. You use the server because, for whatever reason, the resources necessary to run the program aren’t available on your local computer: it’s cheaper, faster, or more convenient to run the program somewhere else where the necessary resources are easy to obtain.

The big difference between cloud and client-server development is in what you know: in traditional client-server systems, you might have a specific computer that is your server, and that’s where your stuff is running. The computer may not be sitting on your desk in front of you, but you know where it is. For example, when I was in college, one of the first big computers I used was a VAX 11/780 nicknamed “Gold.” Gold lived in the Rutgers University computing lab in Hill Center. I used Gold pretty much daily for at least a year before I actually got to see it. The data center had at least thirty other computers: several DEC 20s, a couple of Pyramids, an S/390, and a bunch of Suns. But of those machines, I specifically used Gold. Every program that I wrote, I wrote specifically to run on Gold, and that’s the only place that I could run it.

In the cloud, you aren’t confined to a specific server. You have computing resources—that is, someone is renting you a certain amount of computation from some collection of computers somewhere. You don’t know where they are; you don’t know what kind of computers they are. You could have two massive machines with 32 processors each and 64 gigabytes of memory; or they could be 64 dinky little single-processor machines with 2 gigabytes of memory. The computers where you run your program could have great big disks of their own, or they could be diskless machines accessing storage on dedicated storage servers. To you, as a user of the cloud, that doesn’t matter. You’ve got the resources you pay for, and where they are makes no difference as long as you get what you need.

ability to listen to snippets, read reviews, comment on things that they listened to, get suggestions for new things based on what they like, and ultimately select things to purchase. That’s clearly a service, and it makes sense to keep it in the cloud.

### Large computations.

Is your application intended to perform a massive computation, which you could never afford to do if you needed to buy your own computers to run it? If so, the cloud allows you to purchase time on a server farm of computers in an affordable way and run your application. This is great for people like genetics researchers, who need to run massive computations but don’t have the money or other resources to set up a dedicated data center for their computations. Instead, they can purchase time on commercial data centers, which they share with many other users.

## 1.2 Cloud Computing Programming Systems

There are multiple ways of programming the cloud. Before we start actually writing programs, we’ll take a quick look at a few examples to give you a sense of what sorts of options are available.

### Amazon EC2

Amazon provides a variety of cloud-based services. Their main programming tool is called EC2, Elastic Compute Cloud.

EC2 is really a family of related services. Compared to App Engine, which provides a single, narrowly focused suite of APIs, EC2 is completely agnostic about programming APIs. It provides hundreds of different environments: you can run your application in EC2 using Linux, Solaris, or Windows Server; you can store data using DB2, Informix, MySQL, SQL Server, or Oracle; you can implement your code in Perl, Python, Ruby, Java, C++, or C#; you can run it using IBM’s WebSphere or sMash, Apache, JBoss, Oracle WebLogic, or Microsoft IIS. Depending on which combination you prefer and how much of each kind of resource (storage, CPU, network bandwidth) you plan to use, the costs vary from $0.10 per CPU hour and $0.10 per gigabyte of bandwidth to around $0.74 per CPU hour for high-end instances.

### Amazon S3

Amazon provides another extremely interesting cloud service, which is very different from most other cloud offerings. S3, Simple Storage Service, is a pure storage system. It doesn’t provide the ability to run programs; it doesn’t provide any filesystem; it doesn’t provide any indexing. It’s pure block storage: you can allocate a chunk of storage that has a unique identifier, and then you can read and write bytes from that chunk using its identifier.

A variety of systems have been created that use S3 for storage: web-based filesystems, native OS filesystems, database systems, and table storage systems. It’s a wonderful example of the cloud’s resource-based paradigm: the computation involved in storage is completely separated from the actual data storage itself. When you need storage, you buy a bunch of bytes of storage space from S3. When you need computation, you buy EC2 resources.

S3 is a really fascinating system. It’s very focused: it does exactly one thing and does it in an incredibly narrow way. But in an important sense, that’s exactly what the cloud is about. S3 is a perfectly focused service: it stores bytes for you.

S3 charges are based on two criteria: how much data you store and how much network bandwidth you use storing and retrieving your data. Amazon currently charges $0.15 per gigabyte per month and about $0.10 per gigabyte uploaded and $0.17 per gigabyte downloaded.

On a related note, Google provides a very similar cloud service, called Google Developer Storage, which replicates the basic features of S3 in the Google cloud.

### IBM Computing on Demand

IBM provides a cloud service platform based on IBM’s suite of web service development that uses WebSphere, DB2, and Lotus collaboration tools. The environment is the same as the IBM-based environment on EC2, but it runs in IBM’s data centers instead of Amazon’s.

### Microsoft Azure

Microsoft has developed and deployed a cloud platform called Azure. Azure is a Windows-based platform that uses a combination of standard web services technologies (such as SOAP, REST, Servlets, and ASPs) and Microsoft’s proprietary APIs, like Silverlight. As a result,
