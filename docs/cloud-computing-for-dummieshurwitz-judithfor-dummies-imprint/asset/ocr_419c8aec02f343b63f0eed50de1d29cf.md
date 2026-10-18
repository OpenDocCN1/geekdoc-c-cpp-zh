# Getting Inside Anchored Lifecycle Platform as a Service

![](bbox=[0.133, 0.219, 0.21, 0.295])

Why did we distinguish between integrated lifecycle platforms and anchored lifecycle platforms? It is simple, really. Anchored platform as a service is a business application-centric approach to development in the cloud. Therefore, anchored Platform as a Service vendors started out in life as Software as a Service vendors, for the most part.

Because of their heritage, vendors in this space have several characteristics in common:

+   - A large customer base
+   - Defined services such as billing
+   - Security and authentication
+   - Programming languages
+   - Integration services

These services are the same ones the company used to create its own SaaS offerings.

In the next section, we focus on two of the anchored Platform as a Service vendors and how they structure their offerings.

# Salesforce.com’s Force.com platform

Salesforce.com initiated a platform called Force.com as its foray into the cloud platform market. It helps commercial software developers create cloud-based applications based on Salesforce.com’s development environment. In addition, applications built with Force.com’s tools can also take advantage of the CRM applications.

At the heart of this platform is the *multi-tenancy* architecture. This means that applications designed with Force.com assume that users will share a single physical instance. However, those instances and the application code built in those instances are isolated from each other. In addition, this type of multi-tenancy also means that customizations designed by one user will be isolated from customized designs built by any other user.