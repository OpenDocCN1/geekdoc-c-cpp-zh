Broadly speaking, you have a choice between two approaches for coordination: orchestration or choreography.² With orchestration, one of the components managers the delivery of the overall behavior: It directs the other components, telling them specifically what actions to take and when to take them. Figure 13-2 illustrates the concept, with the service playing the role of the process manager. The service directs each of the participants to perform their tasks, ensures that they complete successfully, and returns the response to the original request. The service is in charge of the overall composite behavior.

Although the orchestration example shows participants A and B to be part of the composite, the same pattern applies when they are not. The only difference is in the specification of the composite. If the participants are external to the composite, then they will be shown in the composite specification, as will the service’s interactions with them. If they are part of the composite, then they will not be indicated in the specification, only in the service architecture document.

With choreography, there is no overall process manager. Instead, the wiring of the components, combined with the behavioral specification of

![](bbox=[0.2, 0.66, 0.8, 0.88])

Figure 13-2: Example of the Orchestration Design Pattern

2. Stephen A. White and Derek Miers, BPMN Modeling and Reference Guide: Understanding and Using BPMN, Lighthouse Point, FL: Future Strategies Inc. (2008), pp. 29–31.