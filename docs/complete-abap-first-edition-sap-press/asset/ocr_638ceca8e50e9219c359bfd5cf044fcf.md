![](bbox=[0.142, 0.103, 0.787, 0.349])

**Figure 19.88** Test Web Service Definition

# 19.5.2 Consuming Web Services

A web service is consumed using the web service client proxy. The *client proxy* takes care of creating valid SOAP messages and evaluates received responses. It also acts as a transfer program and takes care of connecting to the server of the required web service.

In the following subsections, we'll walk through the process of consuming a web service.

# Creating a Web Service Consumer

The following steps walk you through creating a web service consumer:

+   1. In Object Navigator, select CREATE • ENTERPRISE SERVICE from the context menu of the package.
+   2. This will open the ENTERPRISE SERVICES wizard. Select the SERVICE CONSUMER radio button, as shown in Figure 19.89, and click Cont.
+   3. Select EXTERNAL WSDL/SCHEMA, as shown in Figure 19.90.
+   4. Select URL as the WSDL/SCHEMA SOURCE, as shown in Figure 19.91. This allows you to use the URL of the web service as the source.