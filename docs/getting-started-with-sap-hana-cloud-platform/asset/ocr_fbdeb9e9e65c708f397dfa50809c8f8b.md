In this particular scenario, that's all the setup that's required. In more advanced scenarios, your job would be only slightly harder, in that you would likely have to configure more advanced authentication properties in order to support mutual authentication using certificates, OAuth/SAML assertions, and so on. Specific details for each of these authentication types are provided in the online help documentation.

# Calling the RESTful Service within a Java Application

With your HTTP destination in place, the steps required to set up the call to the Geocoding API service within your incident management application are as follows:

+   1. Define a resource reference to the HTTP destination within the application's web.xml file:

```
<web-app>
    ...
    <res-ref>
        <res-ref-name>GoogleGeocodeDest</res-ref-name>
        <res-type>com.sap.core.connectivity.api.http.HttpDestination
        </res-type>
        <res-auth>Application</res-auth>
    </res-ref>
</web-app>
```

+   2. Use a dependency injection to allocate the HttpDestination object at runtime:

```
public class IncidentBean
{
    @Resource(mappedName="GoogleGeocodeDest")
    private HttpDestination geocodeDestination;
    ...
}
```

+   3. Use the createHttpClient() instance method of the HttpDestination class to obtain a reference to an org.apache.http.client.HttpClient instance. From here on out, you can use this HTTP client connection to invoke the service just as you would outside of SAP HCP.

For brevity's sake, we won't include the detailed HTTP request handling logic in this section. However, if you're interested in seeing how this works, check out the loadGeoCoordinates() method of the com.sappress.hcbook.chp06.persistence.IncidentBean class. There, you can see how we're encoding the location address for transmission, parsing the JSON results, and storing the coordinate data inside of the Address entity object. You can test this feature from within