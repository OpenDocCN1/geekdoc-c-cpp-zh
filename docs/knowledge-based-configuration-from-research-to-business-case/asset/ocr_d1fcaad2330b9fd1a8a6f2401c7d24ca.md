items had to be transferred to SAP ERP in case of an order. Finally, sellAIR has to be available offline for Boge field sales force and online for dealers and potentially in the future for customers also.

# 18.3.2 sellAIR: Application Architecture

Figure 18.3 shows the architecture of the solution fulfilling the given requirements. The involved systems are SAP ERP, the CRM system SalesAssistant, the system d.3 for archiving documents, sellAIR (offline), and sellAIR Web (online). The offline version of sellAIR is used by the sales force of Boge to perform tasks especially at customer sites. It is connected to the SalesAssistant, which is available on all sales laptops. By using the Lotus Notes API, sellAIR has access to all customer data and the generated quote document is stored at the concrete quote object in CRM. For archiving purposes this quote is stored in the d.3 system later on. The customer data and conditions are regularly synchronized between CRM and ERP.

The online version sellAIR Web has slightly different goals and users. It is used by customers and dealers of Boge products. Therefore, the functionality has to depend on the respective role of the users. Customers can create baskets with products according to their needs. As a result, they will get a document describing these products in more detail. This basket will then be sent via an email as a request for proposal to Boge and the following process is carried out in the CRM and ERP system.

![](bbox=[0.13, 0.45, 0.88, 0.82])

# FIGURE 18.3

Application infrastructure at Boge: distinction between offline version connected to SalesAssistant CRM and online version connected to SAP ERP.