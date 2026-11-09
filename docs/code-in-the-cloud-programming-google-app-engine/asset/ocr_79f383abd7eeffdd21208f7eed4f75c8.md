# Amazon S3

Amazon provides another extremely interesting cloud service, which is very different from most other cloud offerings. S3, Simple Storage Service, is a pure storage system. It doesn’t provide the ability to run programs; it doesn’t provide any filesystem; it doesn’t provide any indexing. It’s pure block storage: you can allocate a chunk of storage that has a unique identifier, and then you can read and write bytes from that chunk using its identifier.

A variety of systems have been created that use S3 for storage: web-based filesystems, native OS filesystems, database systems, and table storage systems. It’s a wonderful example of the cloud’s resource-based paradigm: the computation involved in storage is completely separated from the actual data storage itself. When you need storage, you buy a bunch of bytes of storage space from S3. When you need computation, you buy EC2 resources.

S3 is a really fascinating system. It’s very focused: it does exactly one thing and does it in an incredibly narrow way. But in an important sense, that’s exactly what the cloud is about. S3 is a perfectly focused service: it stores bytes for you.

S3 charges are based on two criteria: how much data you store and how much network bandwidth you use storing and retrieving your data. Amazon currently charges $0.15 per gigabyte per month and about $0.10 per gigabyte uploaded and $0.17 per gigabyte downloaded.

On a related note, Google provides a very similar cloud service, called Google Developer Storage, which replicates the basic features of S3 in the Google cloud.

# IBM Computing on Demand

IBM provides a cloud service platform based on IBM’s suite of web service development that uses WebSphere, DB2, and Lotus collaboration tools. The environment is the same as the IBM-based environment on EC2, but it runs in IBM’s data centers instead of Amazon’s.

# Microsoft Azure

Microsoft has developed and deployed a cloud platform called Azure. Azure is a Windows-based platform that uses a combination of standard web services technologies (such as SOAP, REST, Servlets, and ASPs) and Microsoft’s proprietary APIs, like Silverlight. As a result,