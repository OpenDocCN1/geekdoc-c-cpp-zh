This chapter explores the issues raised when versioning services and presents best practices for dealing with these issues. After reading this chapter you should be able to describe the OSGi Alliance’s semantic versioning model and the best practices for service versioning.

# Dependencies and Compatibility

In a component- or service-based architecture, the interface is the point of contact between the consumer and provider of functionality (Figure 7-1). Both consumer and provider are dependent upon the interface, but in different ways.

The provider must implement all aspects of the interface. Consequently, any change to the interface mandates a change to the provider. Consumers, on the other hand, may only use a portion of the interface. A change to a consumer is only required when the used portion of the interface changes. In particular, additions to the interface do not require any changes to the consumer.

Interface changes that do not require changes to consumers are considered to be *backwards compatible*. Any other change is considered to be *incompatible*.

# Packages

In the OSGi Framework, the unit of assembly is a package containing interfaces, consumers, and providers. The package determines which of these are visible outside the package. Packages bring some complexity to representing version dependencies, as the following example illustrates.

Consider the Event Admin and Event Listener interfaces from the `OSGi.org.osgi.service.eventadmin` package shown in Figure 7-2. When an Event Destination wants to be notified of events, it provides an instance of the Event Listener interface and then registers that

![](bbox=[0.3, 0.85, 0.8, 0.92])

Figure 7-1: Versioned Elements and Their Dependencies