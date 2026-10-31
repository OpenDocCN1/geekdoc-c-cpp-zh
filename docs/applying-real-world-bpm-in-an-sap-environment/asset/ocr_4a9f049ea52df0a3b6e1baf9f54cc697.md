RS Components' process was identified as a candidate for SAP NetWeaver BPM using the CompriseIT composite application checklist; as shown in Table 8.5, the process scored high across all five dimensions. For more detail and information on composite application, please refer to Part III, Chapter 17, Section 17.8.

| Process Requirements | Suitability Ranking for SAP NetWeaver BPM |
|---|---|
| Process crosses internal or external boundaries | High |
| Process requires information to be used or created | High |
| Process required specific steps to be carried out | High |
| Process crosses systems | High |
| Process needs a new channel | High |

Table 8.5 CompriseIT Composite Application Checklist

# As-Is Process

At the time of BMP implementation, all lead time updates were manually input by supply chain personnel into a Standard Attribute Change Request (ACR) form, irrespective of their format. The Content Data team received the ACR form and processed it through several Excel macros, which formatted the data for entry into their preexisting SAP R/3 system. Due to the manual nature of the process, updates from suppliers were often made yearly, which meant that lead times were often not accurate. The delay in supplier feedback had a direct impact on the stock RS Components held and the on-shelf availability of products.

# 8.5.2 BPM Solution

Suppliers were asked to send a file to RS Components via electronic data interchange (EDI) on a monthly basis, containing lead times for the products they supply. They were also able to send ad hoc changes to RS Components. These files were sent in a supplier-specific format, but the integration layer was used to transform the data into a canonical (common) format.

Once this file was received it was processed through a set of business-maintained rules to determine if the system could be updated automatically, as depicted in Figure 8.12.