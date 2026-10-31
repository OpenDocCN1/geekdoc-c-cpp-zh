
## Architecture Patterns for Versioning

Services often act as intermediaries between components and back-end systems. Back-end systems often differ in their ability to provide and support multiple versions. This leads to a number of options for evolving the service when its back-end system is upgraded to a new version. The following sections discuss some of these options, all of which are variations on the architecture pattern shown in Figure 7-5.

### Accommodating a Compatible Change

If a change to a back-end system can be accommodated with a compatible change to the service interface, the original service can simply be replaced with the new version presenting the new version 1.1 interface (Figure 7-6). The new service interface supports the original clients as well as clients using the full capabilities of the new interface. Necessary changes are made within the service to utilize the new back-end interface, and the back-end system is replaced with the new version. Note that if there are multiple instances of the service, all must be upgraded to the new version before any of the clients are updated.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_201_0.png)

Figure 7-5: Initial Architecture Pattern

![](img/b8d8132a583ad73d511c4c1bb92e2df7_203_0.png)

Figure 7-7: Incompatible Change Architecture Pattern—Back End Supports Multiple Interfaces

![](img/b8d8132a583ad73d511c4c1bb92e2df7_203_1.png)

Figure 7-8: Incompatible Change Architecture Pattern—Back End Supports a Single Interface

### Versioning SOAP Interface Addresses (Endpoints)

For version management purposes, each interface should have its own SOAP address (endpoint). For maximum flexibility, the address location (URI or JMS destination) should incorporate the major version number. For an HTTP address, you’ll have a URI structure like

```
http://insurance.nouveau.com/paymentManager/claimPayment1
```

For an EMS destination, you’ll have

```
com.nouveau.insurance.paymentManager.claimPayment1
```

If a backwards-compatible change is made, continue to use the same endpoint: The `<major>` version number of the interface has not changed.

If an incompatible change is made, create a new address (endpoint) with the new major version number. For an HTTP address, you’ll have

```
http://insurance.nouveau.com/paymentManager/claimPayment2
```

For an EMS destination, you’ll have:

```
com.nouveau.insurance.paymentManager.claimPayment2
```

### Best Practice: SOAP Address (Endpoint) Versioning

Each interface should have its own address (endpoint) by which it is accessed. The address should include the major version number of the interface. If the interface’s major version changes, a new address (endpoint) should be created with the new version number.

### Versioning the SOAP Action

The SOAP action name (a URI) should incorporate the interface’s major version number. Thus the payClaim operation of the Claim Payment interface would have a SOAP action of

```
http://insurance.nouveau.com/paymentManager/claimPayment1/payclaim
```

If the interface’s major version changes, the SOAP actions associated with its operations should be updated, as in

```
http://insurance.nouveau.com/paymentManager/claimPayment2/payclaim
```

### Best Practice: soapAction Versioning

Incorporate the interface name and interface major version number into the soapAction URI. If the interface major version changes, update the SOAP actions for its operations with the new major version number.

### How Many Versions Should Be Maintained?

The reason for supporting multiple versions is to ease the transition of service clients from one version to the next. This easing takes the form of allowing the clients some flexibility as to when (not if!) they upgrade to the new version. The intent is to avoid “big bang” upgrades that require simultaneous updates to all (or many) of the clients when a service interface undergoes an incompatible change.

Allowing multiple versions raises the question of how many versions of a particular interface ought to be supported in a given environment (development, test, production, etc.). Recognize that the goal is to minimize artificial client releases—releases that are made solely to accommodate service interface changes that arise from another client’s requirements. To minimize these artificial releases, you need to understand how often the client would normally be making a release because of its own changing requirements. The assumption is that upgrading to the new service interface at this time will be significantly less costly than making an artificial release just to accommodate the service interface change.

Determining the number of versions that must be supported depends upon the rate at which clients (service consumers) typically deploy releases due to their own changing requirements. The numbers will be different for each environment, but the calculations are as follows:

1. Determine the interval at which clients typically deploy changes. For example, there might be a production release opportunity every 30 days, but the average client only updates every other release. This means that there is an average of 60 days between client updates.
2. Multiply this interval by two. If a change to the client is already underway when the service interface needs to change, you don’t want to change the client requirements in midstream and force it to use the new interface. You want to make this a requirement for the subsequent release.
3. Determine the interval at which services normally deploy incompatible changes (compatible changes are not an issue since they never require a client upgrade). In a rapidly evolving environment, this interval might be the same as the production release cycle (30 days in the example we are discussing).
4. Calculate the number of versions that need to be supported by dividing twice the client update interval (120 days in the example) by the service update interval (30 days in the example). For the example, this yields four versions of the service that need to be maintained in each environment.

Putting this all together, you get the following formula:

```
numberDeployedVersions = (2 * clientReleaseInterval) / incompatibleServiceReleaseInterval
```

The intent is to minimize client churn and allow service changes to be incorporated into the “natural” release cycle of the clients. In other words, you want to avoid making changes to clients solely to accommodate service interface changes. The conclusion concerning the appropriate number of service versions can only be arrived at by examining the overall impact of service changes. Viewing the problem from the narrow perspective of the service provider will likely lead to a lower number of versions (thus reducing the provider’s costs) at the expense of additional cost for the service consumers. The number of versions to be supported should reflect an overall optimization of IT costs.

The analysis presented here is simplistic: It does not attempt to analyze the cost of client releases versus the cost of maintaining additional existing versions of a service interface. However, it is hard to imagine a situation in which the cost of maintaining an old version of the service interface exceeds the cost of an otherwise unnecessary release of one or more service clients. In such cases, the conclusions presented by this analysis will result in a net cost savings for the overall solution (clients + services) and a simplification in each release cycle (less of a “big bang”).

### Summary

Despite all your best efforts, services will eventually need to be changed. When this occurs, it becomes necessary to keep track of the versions of interfaces and the providers and consumers of those interfaces. It also becomes necessary to track the dependencies.

Some changes to interfaces are backwards compatible: Consumers of the old interface are able to use the updated interface. Backwards-compatible changes are primarily additions to the interface that do not affect the portions of the interface already in use. Interface providers must implement all features of the interface. Consequently, any change to the interface requires a change to the provider. Some provider changes, on the other hand, do not require interface changes.

The OSGi Alliance provides a standardized way of denoting versions that indicates whether or not the change is backwards compatible. The structure of these version numbers is

```
<major>.<minor>.<micro>.<qualifier>
```

A major change is one that is not compatible for either consumers or providers. A minor change is one that is backwards compatible from a consumer perspective. A micro change is one that introduces no compatibility issues for either the provider or consumer. The qualifier is usually used to indicate a particular build.

In indicating a dependency, it is useful to denote ranges of versions. This is done by giving a pair of version numbers and surrounding the pair with brackets that indicate whether or not the specified version is included in the range. The `[` and `]` brackets are used to indicate that the version is included in the range, and `(` and `)` are used to indicate that the version is excluded from the range.

Updating versions for bug fixes can be complex. If the bug fix does not introduce a change to observable behavior, incrementing the `<micro>` number suffices. However, if the observable behavior changes, either the old behavior was different from the specified behavior or the behavior was previously unspecified. In either case, clients consuming the interface will no longer operate properly after the change is made, so the `<major>` number should be incremented. The alternative is to locate all service consumers and update their dependencies to indicate that they will not operate properly with the new version. This only works if you are able to identify all of the current service consumers.
