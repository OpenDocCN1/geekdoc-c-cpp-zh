if you can just quickly stand up an SAP HANA instance on your laptop. Instead, when working with the local runtime environment, you have to make do with something smaller and more lightweight: Apache Derby.

Apache Derby is a lightweight, open-source RDBMS written using pure Java. It’s embedded by default in the SAP HCP local runtime environment, so there’s nothing you have to do to install it. Indeed, if your application scenario is simple and you only use the default data source for persistence using JPA/JDBC, then Apache Derby can be used pretty much out of the box. However, if you plan on testing with multiple data sources and the like, then additional configuration is required.

This configuration can be carried out within the Eclipse IDE by opening up the SAP HCP local runtime configuration in the Project Explorer view, shown in Figure 6.28. Within the CONFIG_MASTER • CONNECTION_DATA folders, the target configuration file is called CONNECTION_PROPERTIES. By default, this properties file will include configuration settings for a “demo” data source. You can use this template to create additional data sources as needed. The new data sources will show up after the server is restarted. From an application perspective, you can bind the new data sources as per usual.

> **Note**
> 
> Technically speaking, it’s also possible to configure data sources against other RDBMSs here (e.g., a local instance of MySQL). However, this approach is generally unsupported by SAP, so proceed at your own risk.

![](bbox=[0.146, 0.606, 0.37, 0.866])

Figure 6.28 Configuring Data Sources for Use with Apache Derby