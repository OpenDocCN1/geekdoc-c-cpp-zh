# CHAPTER 44

# Windows Communication Foundation

# What’s In This Chapter?

+   - WCF overview
+   - Creating a simple service and client
+   - Defining service, operation, data, and message contracts
+   - Implementing a service
+   - Using binding for communication
+   - Creating different hosts for services
+   - Creating clients with a service reference and programmatically
+   - Using duplex communication
+   - Using routing

# Wrox.com Code Downloads for This Chapter

You can find the wrox.com code downloads for this chapter at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

+   - Simple service and client
+   - WebSockets
+   - Duplex communication
+   - Routing

# WCF Overview

Chapter 42 covered ASP.NET Web API, a communication technology based on Representational State Transfer (REST). The big and older brother for communication between client and server is Windows Communication Foundation (WCF). This technology was originally invented with .NET 3.0 to replace different technologies, such as .NET Remoting for fast communication between .NET applications and ASP.NET Web Services and Web Services Enhancements (WSE) for platform-independent communication. Nowadays, WCF is much more complex compared to ASP.NET Web API, but it also offers some more features, such as reliability, transactions, and web services security. In case you don’t need any of these advance communication features, ASP.NET Web API might be the better choice. WCF is important for these additional features and to support legacy applications.

The major namespace covered in this chapter is System.ServiceModel.