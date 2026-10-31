# Implementing the Solution

The actual implementation of a BPM process starts with an as-is analysis of the end-to-end process including existing weaknesses, media breaks, and errors. The to-be process is described, focusing on business goals including process performance indicators.

After the functional blueprint is completed, the BPMN process is modeled, and required technical services and user interfaces is identified. User interfaces should be modeled and presented to important stakeholders and iterated as required. At the same time, the technical services are modeled according to SOA design time governance and the provider systems are identified. All of this is the input for implementation to follow.

# Sample Solution Architecture for an SAP Landscape

Figure 10.12 shows the sample solution architecture. SAP NetWeaver BPM will be used to execute the process models, which choreograph human interactions via Web-based frontend technologies and enterprise services calls. The Enterprise Services Repository is used to model and design enterprise services according to SOA design time governance. The various backend applications provide their existing functionalities via enterprise services.

![](bbox=[0.12, 0.7, 0.9, 0.9])

Figure 10.12 Sample Solution Architecture