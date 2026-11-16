HotSpot JVM called the SAP JVM. Compared to the default JVM provided by Oracle, SAP JVM offers a number of useful features related to debugging, memory profiling, and instrumentation.

On top of the SAP JVM, we have the Application Runtime Container, shown in the middle of the architecture diagram contained in Figure 2.5. If you're familiar with Enterprise Java development, then you can think of the Application Runtime Container as being analogous to web containers you may have worked with, such as Apache Tomcat or any of the number of leading Java EE application containers on the market. In essence, the Application Runtime Container furnishes our Java-based web applications with all of the libraries and services they need to get the job done.

As of the time of writing, SAP allows us to configure the Application Runtime Container according to three different profiles:

+   - **Java EE 6 Web**
+   This profile provides the full complement of APIs offered by the Java EE 6 Web profile. Here, in addition to Servlets and JavaServer Pages (JSPs), we also have access to Enterprise JavaBeans (EJBs), the Java Transaction API (JTA), the Java Persistence API (JPA), and more. These APIs simplify the enterprise application development process by assuming ownership of lower-level technical concerns, such as transaction management, object-relational persistence, and so on. For more about the Java EE 6 Web profile, see the boxed note ahead.

+   - **Java Web**
+   According to the online help documentation, the Java Web profile offers “a subset of Java EE standard APIs typical for a standalone Java Web Container.” An example of a typical web container is the popular Apache Tomcat container. Such containers provide support for developing Java web applications using Servlets, JSPs, and so on. They do not, on the other hand, support the entire Java EE API. This means that you cannot utilize other Java EE-based technologies (such as EJBs) on the Java Web container. Of course, you still have access to the full Java SE library, as well as all of the custom SAP HCP service APIs.

+   - **Java Web Tomcat 7**
+   This profile (which is in beta release as of the time of writing) offers similar functionality to the Java Web profile. The primary difference is that the web container for this profile leverages the Apache Tomcat 7 web server without