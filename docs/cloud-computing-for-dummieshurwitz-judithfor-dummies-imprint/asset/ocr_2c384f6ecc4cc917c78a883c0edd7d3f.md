# Google App Engine

When you visit the Google App Engine Web site at http://code.google.com/appengine, you will notice four phrases:

+   - No assembly is required.
+   - Google App Engine exposes a fully integrated development environment.
+   - It’s easy to scale.
+   - It’s free to get started.

That really sums up Google’s strategy for PaaS. Google isn’t trying to help customers create every application to run on every platform. It is actually quite focused, helping customers build Web-based applications. The platform is for development and deployment.

![](bbox=[0.1, 0.42, 0.2, 0.52])

In essence, the developer provides the Google App Engine with a URL (Web address) for the application it’s building and the engine maps that code to Google’s development platform. The App Engine handles the Web application lifecycle, including routine tasks such as request logs, checking the application status, updating the application version, operating the underlying database, and handling workflow.

Google has integrated all the development tools into a single integrated environment. When customers tie their development into the lifecycle environment provided by Google, they also gain access to Google’s IaaS. In this way, customers can add more capacity on demand.

# Other Google infrastructure services

In addition to development services, Google also provides other integrated platform services, including but not limited to the following:

+   - Google Accounts for authentication
+   - Google native file system called GFS (Google File System)
+   - BigTable platform (for data management), a distributed storage system that manages very large-scale structured data

It also includes infrastructure services such as

+   - Load balancing
+   - Persistent storage with queries
+   - Sorting and transactions