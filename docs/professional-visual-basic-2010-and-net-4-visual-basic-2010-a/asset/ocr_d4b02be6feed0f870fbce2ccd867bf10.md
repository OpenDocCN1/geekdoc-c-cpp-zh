When the minimum distance has been determined, the Send(SqlDataRecord) method of the SqlPipe class is used to write the data to the output stream, returning it to the calling function.

The CopyRow function is used to create the SqlDataRecord to return. The first step in creating a SqlDataRecord is to define the columns of data. The constructor for the SqlDataRecord requires an array of SqlMetaData objects that define each column. The preceding code uses the List generic collection to make defining this array easier. Once the columns are defined, the data returned from the GetValues method is used to populate the columns of the new SqlDataRecord.

# Exposing Web Services from SQL Server

Another feature of SQL Server is the capability to expose Web services directly from the server. This means there is no requirement for IIS on the server, as the requests are received and processed by SQL Server. You define what ports will be used to host the Web service. The structure of the Web service is defined based on the parameters and return data of the function or stored procedure you use as the source of the Web service.

> Exposing Web services directly from SQL Server is supported only on the Standard and higher editions. The Express and Compact editions do not support creating Web services in this manner.

When you are architecting a scenario and plan to expose Web services from SQL Server, keep in mind at least one important question: Why do you think you need to expose this database functionality outside of the SQL Server? It’s not a trivial question. It means that you plan on hanging data off of the server, possibly for public access. That’s a potentially dangerous scenario not to be taken lightly. Most of the scenarios for which it makes sense to provide Web services directly from a SQL Server involve systems entirely behind a firewall, where Web services are used as the conduit between departments (typical A2A integration). This would be useful if the target departments were using another platform or database, or where security considerations prevented them from directly accessing the SQL Server.

Following is the basic syntax of the CREATE ENDPOINT command. Although both AS HTTP and AS TCP are shown, only one can occur per CREATE ENDPOINT command.

```
CREATE ENDPOINT endPointName [ AUTHORIZATION login ]
STATE = ( STARTED | STOPPED | DISABLED )
AS HTTP (
    PATH = 'url',
    AUTHENTICATION = ( { BASIC | DIGEST | INTEGRATED | NTLM | KERBEROS } [ , . . . n ] ),
    PORTS = ( { CLEAR | SSL } [ , . . . n ] )
    [ SITE = { '*' | '+' | 'webSite' }, ]
    [ , CLEAR_PORT = clearPort ]
    [ , SSL_PORT = SSLPort ]
    [ , AUTH_REALM = { 'realm' | NONE } ]
    [ , DEFAULT_LOGON_DOMAIN = { 'domain' | NONE } ]
    [ , COMPRESSION = { ENABLED | DISABLED } ]
)
AS TCP (
    LISTENER_PORT = listenerPort
    [ , LISTENER_IP = ALL | (<4-part-ip> | <ip_address_v6> ) ]
)
FOR SOAP(
    [ { WEBMETHOD [ 'namespace' . ] 'method_alias'
        [ NAME = 'database.owner.name' ]
        [ , SCHEMA = { NONE | STANDARD | DEFAULT } ]
        [ , FORMAT = { ALL_RESULTS | ROWSETS_ONLY } ]
    } [ , . . . n ] ]
    [ BATCHES = { ENABLED | DISABLED } ]
```