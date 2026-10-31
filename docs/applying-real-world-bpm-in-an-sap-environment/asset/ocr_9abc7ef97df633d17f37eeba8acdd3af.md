# Results of the Project

With the initial phase of the project completed, Braskem has deployed an integrated payment process that addresses the complete workflow from invoice receipt and approval through payment processing. As a result, invoice registration and processing costs have dropped 30%, and 95% of supplier payments are now made on schedule, which helps Braskem take advantage of discounts and avoid penalties. The ability to process electronic invoices more efficiently is also making individual transactions easier to track (see Table 9.3).

| Key Performance Indicator | Impact |
|---|---|
| Time needed to redesign processes | -20% to -30% |
| Training costs | -20% |
| Invoice registration and processing costs | -30% |
| On-time payment rate improvement | 60% to 95% |

Table 9.3 KPI Tracking

Braskem’s process transformation program is just getting started. The company is now turning its attention to the remaining 12 processes. Braskem’s goals include enhancing traceability in contracting, streamlining sales order entry, and simplifying the company’s critical export processes. Such improvements will play an important role in shaping the future success of this growing chemical company.

# Sample Solution Architecture for an SAP Landscape

With Braskem’s broad SAP software landscape, SAP NetWeaver BPM was a particularly attractive choice, offering native integration and a less costly and complex implementation than alternative technologies.

As shown in Figure 9.12, the payment process initiates with digitalization of Brazilian invoices. The digital invoice image is sent to a service provider who, through an OCR process, recognizes fields from the invoice image and sends it back to Braskem, integrated via an interface with SAP NetWeaver PI.

The service provider sends the invoice picture as a PDF file and the fields recognized from the invoice image as xml data. SAP NetWeaver PI receives this information. The PDF file is then stored in the SAP content server, and the invoice data is sent to a custom Web service that starts the BPM process in SAP NetWeaver CE.