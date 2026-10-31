# ## ActiveMatrix Service Bus Load Distribution  
## Using Virtual Bindings

If you recall, communications between ActiveMatrix Service Bus nodes occurs via an EMS server that has a configuration managed by the ActiveMatrix Administrator. This communications takes place via JMS queues. If you use ActiveMatrix Service Bus Virtualization bindings and deploy a service consumer on one node and a number of service providers on other nodes, the workload will be distributed among the service providers by the queue (Figure 11-8).

# ## ActiveMatrix Service Bus Load Distribution  
## of Promoted Services

Communications between SCA promoted services and the components that implement them occurs via JMS queues if the promoted service and implementing components are deployed on different ActiveMatrix Service Grid nodes. For example, Figure 11-9 shows a LoadDistribution composite comprising a promotedService and a serviceProvider. If the promotedService is deployed on one ActiveMatrix Service Grid node and the serviceProvider is deployed on another, then the communications between them will occur via a JMS queue whose configuration is managed by the ActiveMatrix Administrator.

The fact that this communications occurs via a JMS queue makes it possible to do load distribution by deploying more than one instance of the service provider on different nodes (Figure 11-10). This approach works regardless of the transport binding used for the promoted

![](bbox=[0.105, 0.679, 0.916, 0.9])

**Figure 11-8:** *ActiveMatrix Service Bus Load Distribution Using Virtualization Bindings*