# encoway: From ERP-Based to Sales-Oriented Configuration

# CHAPTER 18

Björn Höfling

encoway, Bremen, Germany

Abstract: ERP-based product configuration is often used for supporting business execution processes in companies. Reusing the underlying product configuration models in sales-oriented scenarios leads to additional challenges. In this chapter we describe a sales application called sellAIR, which is the outcome of joint project work of encoway and the German company Boge. With this application, Boge has succeeded in closing the gap between ERP-based product configuration and sales-oriented configuration.

# 18.1 Introduction: ERP-Based Configuration

Systems for enterprise resource planning (ERP) are integrated software applications for the automation of business processes. Typical examples of such processes in ERP systems are quote and order processing or production planning. For those companies that produce or deal with complex products with a high number of variants, some ERP systems support knowledge-based configuration. Depending on the specific market or supported scenarios, different knowledge representation and reasoning techniques are implemented in these systems. One of the major challenges to be addressed when manufacturing complex products can be summarized by the concept of mass customization, which tries to combine the advantages of mass production with the flexibility of individual customization (see Piller and Blazek, 2014¹). Configuration systems are a key-enabling technology of mass customization. A simple way of categorizing the application areas of (knowledge-based) product configuration in ERP systems can be shown along with the order fulfilment process. Make to stock (MTS) is a build-ahead production approach that supports mass production. In contrast, individual customization can be done in project-oriented production. In between, the scenario of make to order (MTO) is placed, which can be supported with the help of product configuration. Here, the production process is triggered by a sales order that includes the specific definition of the configurable products in the order.

The German software corporation SAP AG is a big player in the enterprise application software market (see also Haag, 2014²). Its enterprise resource planning application is called SAP ERP, which includes a variant configurator called LO-VC (module logistics, variant configuration). Variant configuration is a basic technique that can be used in different business processes inside SAP ERP. The LO-VC can be applied in the modules PP (Production Planning), SD (Sales and Distribution),