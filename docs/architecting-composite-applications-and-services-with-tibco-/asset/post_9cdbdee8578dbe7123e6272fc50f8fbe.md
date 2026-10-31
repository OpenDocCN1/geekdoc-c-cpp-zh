
## H
HTTP Connector
default SOAP / HTTP thread usage, 345–347
process starters in ActiveMatrix BusinessWorks using, 359
starting jobs from ActiveMatrix Service Bus, 361–363
thread pools, 344–345
thread usage with threading policy set, 353–356
worker thread assignments, 345
HTTPComponent thread pool, 358
Hybrid role-process approaches, 247–248

## I
I/O activities, ActiveMatrix BusinessWorks, 362–365, 367–368
I5/OS, using TIBCO Adapter for IBM i, 61–62
IBM i platforms
TIBCO Adapter for Files, 62–63
TIBCO Adapter for IBM i, 61–62
ICANN (Internet Corporation for Assigned Names and Numbers), 186
Idealized name structures, 191–192
Identity pattern, inter-site failover with same-host, 391
Immediate payments, case study
behavior, 136, 139, 146–147
Claim Payment Service Implementation, 296
composite mappings of, 299, 302
coordination, 76, 138–140
manage payments process and, 75–76
nonfunctional behavior and, 140
orchestrating, 298
overview of, 83–85
Payment Manager architecture pattern, 145–147
Payment Manager service interfaces for, 130–132
thread usage with threading policy set, 354–356
utilization scenario, 129–130
Implementation
TIBCO ActiveMatrix composite, 307–308
understanding composite, 294
Implementation architecture
ActiveMatrix Service Bus using Mediation, 27
architectural distinctions and, 12
services or components, 9, 11
Implementing SOA: Total Architecture in Practice (Brown), 425
In-memory Job pool, ActiveMatrix BusinessWorks, 362
In-Only architecture pattern
orderDelivered() operation, 104
orderShipped() operation, 102–103
overview of, 33–34
In-Out architecture pattern, 34
Incompatible change
architecture pattern for deploying, 166–167
defined, 152
versioning and bug fixes resulting in, 155
versioning SOAP interface addresses (endpoints), 168
in WSDLs and XML schemas, 163–164
Inconsistencies, reconciling data, 287–289
Individual activity benchmarks, 326
Information models
creating XML schema with, 229–232
domain models vs., 218–219
Information retrieval design patterns, 304–306
Information Storage and Management: Storing, Managing, and Protecting Digital Information (Somasundaram and Srivastava), 333
Input rates
determining operating capacity, 316–317
documenting test results, 322–324
identifying capacity limit, 327–328
misleading benchmark results on, 314–316
Instance names, distinguishing type names from, 189
Integration and testing, solution architecture documenting, 416–417
Intended utilization scenarios
service specification contents, 125
service specification documentation, 420–421
service specification example, 129
Intents, mainframe interaction, 59
Inter-site failover pattern, ActiveMatrix BusinessWorks, 388–389
Inter-site failover with different-host identity pattern, 378–379
Inter-site failover with same-host identity pattern
ActiveMatrix Service Bus failover, 391
EMS multi-site with message persistence pattern, 393–396
EMS multi-site with no message persistence pattern, 391–393
generic site failover, 380–381
Interaction patterns
basic, 33–34
event-driven, 34
external system access, 37–39
Interface definitions
service specification contents, 125
service specification documentation, 421
service specification example, 129–132
WSDL, 176–178
Interface major version numbers, structured name design, 191
Interfaces
dependencies and compatibility of, 152
distinct WSDL namespace URI for, 190
Payment Manager, 82–83
solution architecture decisions, 240–243
solution architecture documentation, 414
UML Class Diagram notation for, 428–429
Internal engine architecture, ActiveMatrix BusinessWorks, 358–359
Internet Corporation for Assigned Names and Numbers (ICANN), 186
Internet naming system
general-to-specific structure of, 183–185
hierarchical naming authorities in, 185–186
notational convention for domain names, 194
technology constraints on, 205
Internet Server, TIBCO Managed File Transfer, 56
Intra-Site Cluster Failover Pattern, 374–376
ActiveMatrix BusinessWorks built-in, 387–388, 390–391
ActiveMatrix BusinessWorks cluster, 388–389
ActiveMatrix Service Bus cluster, 391
with different host identity pattern, 378–380
EMS strategy for, 382–384
recovery point objectives, 373
with same hostname pattern, 380–381
Invoke Partner thread pool, 358, 365–366
IOPS (I/O operations per second), disk performance, 331–334
IP redirectors, load distribution, 266
ISeries, 58–63

## J
JCA thread pool, 342–343
JDBC, external access interaction via, 39
JMS Binding thread pool
ActiveMatrix nodes, 343
default JMS thread usage, 347–349
default node-to-node communications thread usage, 349–351
thread usage with threading policy set, 355–356
thread usage with virtualize policy set and initiation of, 352–353
worker thread assignments, 345
JMS (Java Message Service)
ActiveMatrix BusinessWorks Service Engine thread usage, 361–364
asynchronous request-reply interactions, 257–261
Deferred JMS Acknowledgement Pattern, 373–374
load distribution, partitioning between servers, 267–269
load distribution, two-tier, 279–280
load distribution, with queues, 266
name requirements, 183
naming constraints, 205
naming principles, 201
JMS process starters, 360–361
JMSCorrelationID property, asynchronous request-reply, 258–261
JMSReplyTo property, asynchronous request-reply, 258–261
JNDI lookups, partitioning JMS message load, 268
Jobs, ActiveMatrix BusinessWorks
Activation Limit parameter, 367–368
Flow Limit parameter, 368
Max Jobs parameter, 365–367
processing, 362–366
starting from Service Bus, 361–364
Step Count parameter, 368–369
Joins, UML activity diagrams, 438

## K
Keep Alive Time parameter, thread pools, 343–344

## L
Licenses, message service, 27
Lines of business
naming authority complications, 206
naming complications in complex organizations, 206–209
naming principles for WSDL and XSD filenames, 196
naming principles in functional context for, 193–194
Load distribution
EMS client connections, 269–271
IP redirectors for, 266
JMS queues for, 266
objectives, 265–266
partitioning JMS message load between servers, 267–269
patterns preserving partial ordering, 278–280
patterns preserving total sequencing, 275–279
sequencing problem, 273–275
with Service Bus, 271–273
summary review, 280–281
Logging, Hawk Event Service, 55–56
Lookup and cross reference, information retrieval, 306

## M
MagicDraw tool, 434
Mainframe-related products, and iSeries interaction, 58–63
Major version numbers
namespace names and, 159–160
OSGi versioning and, 153–154
rules for WSDLs and schemas, 164, 191
Manage payments, case study
Payment Manager specification, 74
Payment Manager specification, domain model, 77, 81
process coordination, 76–77
processes of, 75–76
Managed File Transfer product portfolio, TIBCO®, 56–58
Manufacturer schema, 447–448
Mapping processes. See Process mapping
Master-Data-Management pattern, 288–289
Max_connections parameter, EMS client load distribution, 270–271
Max Jobs tuning parameter, ActiveMatrix BusinessWorks, 365–367
Max Pool Size parameter
default SOAP/HTTP thread usage, 347
JCA thread pool, 342
named thread pools, 344
Maximum size parameter, thread pools, 343–344
Mediation patterns
ActiveMatrix BusinessWorks, 30
ActiveMatrix Service Bus, 27–28
ActiveMatrix Service Grid, 29
overview of, 36–37
Memory limits
interpreting benchmark results, 335–336
setting Max Jobs parameter in ActiveMatrix BusinessWorks, 367–368
using benchmark results on, 337
Message format specifications, solution architecture, 417
Messages
avoiding deep data structure for, 222
avoiding flattened data structure for, 223
using shallow data structures for, 223–224
Micro version numbers, OSGi, 154
Microagent interfaces, Hawk, 54–55
Migration, solution architecture documenting, 416
Milestone-level status, service interfaces, 107–108
Minimum size parameter, JMS Binding thread pool, 343
Minor version numbers
OSGi, 154
placement for WSDLs and XML schemas, 159–160
rules for versioning WSDLs and XML schemas, 164
structured names incorporating interface, 191
Multi-word fields, name structure with, 189–190

## N
Named thread pools, ActiveMatrix nodes, 343–344
Namespace URLs, WSDL and schemas, 159–160
Namespaces, responsibility for subordinate, 186
Naming authorities
complications of, 206
hierarchical, 185–186
Naming principles
functional context, 192–194
idealized name structures, 191–192
operation names, 200
port type, service, and binding names, 198–200
schema locations, 197
schema shared data types, 204–205
schema types specific to interface and operation, 203–204
SOAP action names, 203
SOAP address location, 200–202
WSDL and XSD filenames, 195–196
WSDL and XSD namespace URLs, 194–195
WSDL names, 196–197
WSDL-specific schema location, 197–198
WSDL message names, 197–198
Naming standards
abstract services concept, 174–175
avoiding acronyms and abbreviations, 188
basing on business processes, 187
basing on domain concepts, 187
basing on enterprise identifiers, 187–188
in complex organizational structures, 206–209
defining routing strategies, 181–182
defining search strategies, 181
