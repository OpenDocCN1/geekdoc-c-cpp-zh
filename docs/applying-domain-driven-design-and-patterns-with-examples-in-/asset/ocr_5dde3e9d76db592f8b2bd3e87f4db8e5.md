![](bbox=[0.196, 0.073, 0.807, 0.34])

The Service assembly should contain at least one façade object that implements some basic interfaces to support basic CRUD, `IvbDBOReq` being the most important; see Figure A-7.

# Figure A-7. Architecture for the façade

![](bbox=[0.193, 0.507, 0.807, 0.735])

This façade isn't generated; instead, you inherit all base functionality (from `FacadeBase`), including the implementation of the mentioned interfaces.

When it comes to persistent storage, the presence of a relational database system (RDBMS) is as sure as the presence of the file system itself at the site. In fact, the RDBMS was an unspoken requirement, and if I wanted proper backup handling of my application's data, I'd better use one.