from the namespace URI—it should be concatenated instead. Thus the namespace URI in Figure 7-4 is

```
http://nouveau.com/address/schema/address1
```

# Version Numbers in soapAction Names

In the XML data structure that is exchanged between service consumers and providers, the soapAction field indicates the operation to be performed. Since operations are part of interfaces and you are versioning the interfaces, it is good practice to indicate the interface version in the soapAction field value. Following the recommended naming practices for the soapAction field (discussed in the next chapter), the resulting field name for the payClaim() operation of Figure 4-6 with major version 1 of the interface would be

```
http://insurance.nouveau.com/paymentManager/claimPayment1/
 payclaim
```

# Best Practice: WSDL and XML Schema Versioning

Place major and minor version numbers in WSDL and schema filenames. Place major version numbers in the namespace URI. Place major version numbers in the interface name in the soapAction fields. Update the filename version for all WSDL and schema changes. Update the namespace URI and soapAction only when major (incompatible) changes are made.

# Backwards-Compatible WSDL and XML Schema Changes

Certain kinds of WSDL and schema changes are backwards compatible when service consumers and providers are independently deployed (i.e., not in the same ActiveMatrix composite). The following sections describe some of these changes.

# Adding Definitions to a WSDL

Adding message, interface (port type), and operation definitions to a WSDL is always backwards compatible. The service provider must