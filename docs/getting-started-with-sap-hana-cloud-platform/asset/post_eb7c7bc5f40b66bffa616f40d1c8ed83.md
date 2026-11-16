
- 10.3.2 Configuring Eclipse .................................................... 440
- 10.4 Implementing a Simple SOAP-to-SOAP Scenario .................... 442
- 10.4.1 Creating an Integration Flow ........................................ 442
- 10.4.2 Configuring Sender and Receiver Systems ........................ 444
- 10.4.3 Importing WSDL Files from SAP PI or Your Local File System ............ 445
- 10.4.4 Creating a Parameters File ........................................ 446
- 10.4.5 Mapping between Sender and Receiver Systems .................... 446
- 10.4.6 Configuring Sender and Receiver Communication Channels ............ 448
- 10.4.7 Deploying the Integration Project ................................. 449
- 10.4.8 Monitoring ........................................................ 449
- 10.5 Introduction to the Web UI for SAP HANA Cloud Integration ......... 450
- 10.5.1 The Discover Section (Integration Content Catalog) .............. 451
- 10.5.2 The Design Section .................................................. 454
- 10.5.3 The Run Section ..................................................... 457
- 10.5.4 The Monitor Section ................................................. 458
- 10.6 Summary ............................................................... 460
- 11 Extension Scenarios with SAP HANA Cloud Platform ................... 461
- 11.1 The Need for Software-as-a-Solution Extensions ..................... 462
- 11.2 The Architecture of an Extension .................................... 464
- 11.2.1 Extension Application Frontend Layer ............................ 468
- 11.2.2 Extension Application Backend Layer ............................. 473
- 11.2.3 Extension Application Connectivity Layer ........................ 476
- 11.3 Integration Points for Extending SAP Cloud Solutions .............. 478
- 11.3.1 Custom Business Objects and Views ............................... 479
- 11.3.2 Workflows ........................................................... 480
- 11.3.3 Roles and Permissions ............................................. 480
- 11.3.4 API Clients ......................................................... 480
- 11.3.5 Rules ............................................................... 481
- 11.3.6 Configurable UIs .................................................... 481
- 11.3.7 Custom Code ......................................................... 481
- 11.3.8 Home Page Tile Configuration ...................................... 482
- 11.3.9 Navigation Configuration .......................................... 483
- 11.4 Extending SuccessFactors with SAP HCP Applications ................ 483
- 11.4.1 SuccessFactors Administration Layers ............................ 484
- 11.4.2 Account Onboarding .................................................. 485
- 11.4.3 Deploying Your First SuccessFactors Extension ................... 489
- 11.4.4 SuccessFactors Extension Administration ......................... 490
- 11.4.5 SuccessFactors APIs ........................ 493
- 11.4.6 Creating Custom MDF Objects and Consuming Them from SAP HCP ........................ 498
- 11.4.7 Creating Custom Home Page Tiles Hosted on SAP HCP ........................ 498
- 11.4.8 Managing Custom Navigation Entries ........................ 502
- 11.4.9 Troubleshooting SuccessFactors Extension Applications ... 503
- 11.5 Summary ........................ 508
- The Authors ........................ 509
- Index ........................ 511
- Service Pages ........................ I
- Legal Notes ........................ III

## Foreword by Matthias Steiner

We live in a time of accelerated change, in a world in which companies fight over market share on a global scale. In this competitive environment, it’s more important than ever for enterprises to focus on their core business, to differentiate themselves from their competitors, and to provide products and services that deliver immediate value to their customers. Software has become a key enabler to help companies adapt to changing market trends by both streamlining and reinventing their internal processes as well as empowering them to develop innovative solutions. As such, it’s up to us developers to lead this digital evolution and shape a world that is driven by software.

Having made a living as a software architect for more than a decade, I understand that developing enterprise software solutions is far from being a trivial task. Complex system landscapes, ever changing business requirements, and pressing timelines are not an exception, but the norm. Consequently, developers need first class tooling that supports them in their daily tasks and enables them to focus on their job: converting business requirements into viable software solutions.

This is the problem space that SAP HANA Cloud Platform addresses: It’s a design and runtime environment designed from the ground up to empower developers to build, extend, and run next generation business applications in the cloud. Based on SAP HANA, SAP’s in-memory technology platform, this Platform-as-a-Service (PaaS) offering provides customers and partners with the comprehensive set of services and capabilities needed to efficiently develop business solutions for an increasingly connected world.

Nowadays, where everything from people (social media), to companies (business networks), up to individual devices (Internet of Things) are connected to each other, the cloud has become the catalyst for a global digital business transformation. It’s the backbone of the mobile movement and the enabler for big data scenarios requiring lots of computing power. With SAP HANA Cloud Platform, SAP offers a cloud platform that enables developers to support their companies—and ultimately their customers—to leverage the opportunities accompanying this transformation.

In this book, James, Krassi, John, and Riley provide a comprehensive overview of SAP HANA Cloud Platform and its related technologies and how they support companies to extend their business into the cloud. Based on their vast experiences gained as development consultants over the last decade, James and John are able to holistically address these aspects and cover both the business and the technical perspective. Their expertise is ideally complemented by the inside view provided by my colleagues Krassi and Riley, who both have been driving their respective topics internally at SAP. Together, their domain knowledge is second to none.

The book focuses on concrete development scenarios and as such primarily targets solution architects and developers interested in understanding how to develop software solutions that excel in hybrid IT landscapes comprising both on-premise systems and cloud solutions. Starting with a general overview of cloud computing and SAP HANA Cloud Platform, the authors move on to address everything from getting started, to key technologies, up to advanced topics such as developing extensions for on-premise solutions and cloud applications alike.

After reading this book, you will understand the full potential of SAP's PaaS offering and how to leverage it for your own needs. Moreover, you'll be equipped with a great set of examples to kick-start your own development projects based on SAP HANA Cloud Platform. As such, I hope you enjoy reading through this book—and I ultimately look forward to welcoming you to the fast-growing community of cloud developers.

Happy coding!

Matthias Steiner
Cloud Platform Evangelist and SAP Mentor
SAP HANA Cloud Platform

## Preface

Since its initial release in late 2012, SAP HANA Cloud Platform (SAP HCP) has flown under the radar for many within the SAP community. However, with the release of the new SAP S/4HANA business suite and a continued push to integrate recent cloud software acquisitions, such as SuccessFactors, Ariba, and Concur, SAP HCP has begun to emerge as one of the key components in SAP’s overall cloud strategy. In essence, you can think of SAP HCP as the hub of the modern SAP technology landscape.

With that being said, if you picked up this book because you want to learn what SAP HCP is all about, your timing couldn’t be better. In the months and years ahead, SAP HCP skills are sure to be in great demand. Whether you’re a seasoned SAP developer looking to transition your skills or a non-SAP developer looking to jump onboard the SAP cloud bandwagon, we think you’ve come to the right place.

## Target Group and Prerequisites

This book is intended for developers who are interested in learning how to develop applications on SAP HCP. Notice that we don’t say Java developers or ABAP developers. Because SAP HCP is an open platform that offers a bring your own language (BYOL) approach to development, developers from all walks of life are welcome here.

Having said that, there are a few important prerequisites for being able to navigate through the material we cover here. Because this is a book about cloud application development, there is a natural expectation that the reader is reasonably familiar with core concepts, such as web application development, Internet technologies, and so forth. Although we do attempt to provide gentle introductions to new technologies wherever possible, this book cannot possibly cover these topics at the depth required to successfully develop cloud applications.
