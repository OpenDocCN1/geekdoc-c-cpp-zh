
Capturing the current business process and simplifying it to the desired state was a key objective realized during the FOVISSSTE business process modeling. Key process owners were interviewed during the discovery phase to develop the as-is and the to-be business process model. A user interface mockup was developed in SAP NetWeaver CE using Web Dynpro to simulate the end-user experience. The business process provided the capability to handle business exceptions such as collaboration between branch offices to resolve issues related to a specific loan application. Additionally, operational reports were developed to provide process statistics and KPIs such as the number of processes waiting on a business step per branch or region.

In the to-be process (see Figure 8.1), the process participants were branch executives from the 17 branches, the executive responsible for the FOVISSSTE process at headquarters, and the commercial department.

![](img/30a88f75957f887ca511028d178ca5c7_166_0.png)

The branch executive processed the loan application file through its various stages. All files from the various branches were sent to Mexico City to the FOVISSSTE executive, who then registered them into the FOVISSSTE Web portal provided by the Mexican Federal Government. The Commercial department authorized payments to the third-party notary service provider. Upon the receipt of the property title document (“testimony”) up to six months later, the FOVISSSTE loan application process was completed.

Establishing the reference architecture for future process implementations was another key objective of this project. Table 8.2 gives a consolidated view of the reference architecture.

| Capability | Product/Architecture Principle |
|---|---|
| Business process modeling and orchestration | SAP NetWeaver BPM: provides the capability for implementing user-centric business processes across roles and user profiles. |
| UI presentation platform | SAP NetWeaver CE: provides portal capability for secure, consistent, and unified access to backend applications. |
| UI technology for each business activity | Web Dynpro: the UI for each process step is developed independently, allowing for reuse across other business processes with similar tasks. |
| Service-oriented architecture | Enterprise-class services were leveraged from SAP for Banking and Microsoft .NET-based legacy applications for implementing process steps. |
| Custom enterprise services | Where needed, custom enterprise services were modeled in an enterprise services repository, implemented in backend applications, and published in a service registry. |
| Business rules | SAP NetWeaver BRM will enable automation in enforcing checking for the presence of mandatory loan documents, checking the document validity dates with respect to loan tenure, and checking the status of the house if it has pre-existing loans. |

Table 8.2 FOVISSSTE Reference Architecture

## Implementing the Solution

Because BPM was a new approach for Patrimonio, the implementation was conducted in phases to achieve specific milestones at the completion of each phase. The SAP NetWeaver CE landscape was installed in the typical three-instance configuration, consisting of development, quality, and production instances.

For each BPM step, the user interface screen was defined in terms of screen elements, information capture logic, business logic, and end-user interaction. The user experience for each step was then implemented in Web Dynpro as mock user-interface screens and associated with the appropriate manual steps in the BPM process flow.

FOVISSSTE process owners were then walked through the screen flow of the process; the BPM model was further refined and simplified based on the feedback they provided. The user-interface mockup captured the handoff between the bank branch and head office, which allowed all process participants to visualize the process choreography. After the key process owners approved the baseline business process, the SAP NetWeaver BPM realization phase was started. Each BPM activity was implemented as an independent Web Dynpro component; the input and output context parameters were kept simple and generic to promote reuse across other similar loan origination business processes. The agile development process ensured that each Web Dynpro component was developed independently, such that the customer could see the final process being assembled in a shorter time frame.

The key process owners were involved in acceptance testing of the developed BPM process. Once testing was completed, the production go-live was conducted as a "soft launch" across a few branches; the process was gradually deployed across all of the bank branches.

## Results of the Project

The production rollout of the FOVISSSTE process across Patrimonio provided immediate business value. Process tracking and traceability have vastly improved. Operational reports provide macro indicators on processes through the company and highlight process bottlenecks. The process is integrated with the SAP IS-Banking platform and has eliminated the need for manual entry of loan application information. User adoption has been swift; the "train-the-trainer" approach was used, where the key user in each branch was trained by the core implementation team. The process is being consistently refined with subflows to handle additional scenarios such as management of third-party notary agents, who provide notary services to loan applications.

Patrimonio is now working toward implementing additional business processes to be managed with SAP NetWeaver BPM, such as individual loan origination, loan servicing, and collection management.

## Sample Solution Architecture for an SAP Landscape

Figure 8.2 maps the SAP components for implementing business processes similar to the FOVISSSTE process at Patrimonio.

![](img/30a88f75957f887ca511028d178ca5c7_169_0.png)

Figure 8.2 Suggested Solution Architecture for BPM-Based Composite Applications Related to SAP for Banking

As depicted in Figure 8.2, the solution architecture can be thought of in terms of a presentation layer for managing user interactions, an orchestration layer for managing the end-to-end business processes, an integration layer for integrating system-to-system process steps, and an application layer where many of the business functions required for automatic process steps reside. The presentation layer consists of the user-interaction capabilities for displaying data, obtaining user input, validating frontend data, and printing data. The SAP components deployed are the SAP NetWeaver Portals, Universal Worklist, Web Dynpro, and Adobe Forms.

In the orchestration layer, SAP NetWeaver BPM provides user-centric workflow capabilities. The workflow allows allocation of activities to different actors through role-based authorizations.

The integration layer handles integration between the SAP NetWeaver CE server and the enterprise systems such as SAP ERP Central Component (SAP ECC). The FOVISSSTE implementation uses SAP enterprise services and Web services through direct consumption. Enterprise Services Repository (ES Repository) and the Services Registry are key components for enabling the SOA-based integration.

Within the application layer reside the enterprise systems such as SAP ECC, Microsoft.NET, and Lotus that participate in the business scenario. Integration options based on the enterprise system capability have to be explored for optimum integration.

## 8.2 Coca-Cola Erfrischungsgetränke AG: Promotion Material Planning and Procurement as an Extension of SAP Trade Promotion Management

> *SAP NetWeaver BPM enhances our global standard processes to meet our unique requirements. The optimized demand planning process offers seamless integration of activities across marketing, sales, and procurement.*  
> *— Alexander Grobe, Manager Enterprise Architecture and Innovation, CCE AG*

Coca-Cola Erfrischungsgetränke AG (CCE AG) needed a cost- and time-efficient approach to localize a global template solution named Coke One. They used BPM tools and methods to effectively implement the bottler-specific language and define legal and local business requirements. Demand determination for promotional material was the first live process CCE AG implemented with SAP NetWeaver BPM. The goal was to optimize marketing budget allocation for promotional materials, and the solution was to create a single environment in which to plan and order promotional material.

### 8.2.1 Background

CCE AG is the largest German beverage company, selling about 3.4 billion liters per year (2009). Since 2007, CCE AG has been the only franchisee of The Coca-Cola Company (TCCC, Atlanta) in Germany. CCE AG's business is the production (25 facilities) and distribution (70 facilities) of Coca-Cola products to about 95,000

![](img/30a88f75957f887ca511028d178ca5c7_170_0.png)
