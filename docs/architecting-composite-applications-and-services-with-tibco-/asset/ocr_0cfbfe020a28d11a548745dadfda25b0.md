use the new interface. You want to make this a requirement for the subsequent release.

+   3. Determine the interval at which services normally deploy incompatible changes (compatible changes are not an issue since they never require a client upgrade). In a rapidly evolving environment, this interval might be the same as the production release cycle (30 days in the example we are discussing).
+   4. Calculate the number of versions that need to be supported by dividing twice the client update interval (120 days in the example) by the service update interval (30 days in the example). For the example, this yields four versions of the service that need to be maintained in each environment.

Putting this all together, you get the following formula:

numberDeployedVersions = (2 * clientReleaseInterval) / incompatibleServiceReleaseInterval

The intent is to minimize client churn and allow service changes to be incorporated into the "natural" release cycle of the clients. In other words, you want to avoid making changes to clients solely to accommodate service interface changes. The conclusion concerning the appropriate number of service versions can only be arrived at by examining the overall impact of service changes. Viewing the problem from the narrow perspective of the service provider will likely lead to a lower number of versions (thus reducing the provider's costs) at the expense of additional cost for the service consumers. The number of versions to be supported should reflect an overall optimization of IT costs.

The analysis presented here is simplistic: It does not attempt to analyze the cost of client releases versus the cost of maintaining additional existing versions of a service interface. However, it is hard to imagine a situation in which the cost of maintaining an old version of the service interface exceeds the cost of an otherwise unnecessary release of one or more service clients. In such cases, the conclusions presented by this analysis will result in a net cost savings for the overall solution (clients + services) and a simplification in each release cycle (less of a "big bang").