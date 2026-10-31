
## Appendices 637

A IT Performance and Value Management Research 639

B Value Driver Processes Sorted After Strategic, Tactical, and Operational Levels 641

C Bibliography 657

D The Authors 673

Index 687

Service Pages I

Legal Notes III

## Foreword

Over the past decade, we've seen our planet grow smaller as companies, their customers, and the world's economies become more interconnected. The rise of these business networks has dramatically increased the pace of business and thus the need to quickly respond to challenges and opportunities.

No recent event illustrates this more than when the world's economy literally went into freefall in the autumn of 2008, and companies suddenly found themselves and their customers without credit or liquidity. As the world works through these economic challenges, we are faced with a new uncertainty. Now, more than ever, corporate leaders need the capacity to adapt to change not only defensively, but to realize opportunities for growth and capture market share while their competitors lag behind.

For nearly 40 years, over 100,000 global companies have relied on SAP for the software that runs their core operations, enabling them to optimally run through business processes based on best practices. Building upon that foundation, SAP now strives to help its customers manage processes across their complete business network, breaking the boundaries of individual organizations.

Business Process Management (BPM) directly improves business performance by orchestrating the work of people and software systems in a way that can be understood and managed from a business perspective. BPM is a key pillar of SAP's strategy to help our customers become more agile. This approach and associated methodologies, pre-packaged process-based implementation content, tools, and technologies provide the basis for our customers to quickly deploy new people-centric business applications in support of business process improvement, business network optimization, and business model transformation.

I'm proud to present to you our second book about SAP's BPM approach, a comprehensive reference to the application of real-world BPM in an SAP environment, with insights from SAP's customers who have taken the process transformation journey with SAP.

## Foreword

By following the approach outlined in this book, as illustrated by the experiences of others, we hope that you will find your own opportunities for transformation, an inspiration to aspire to excellence, and a clear path to achievement.

With best regards,
**Jim Hagemann Snabe**
Co-CEO, SAP AG

## Introduction

Business process management is reaching a state of mainstream acceptance and is a key discipline within SAP-centric business IT environments today. The first book from SAP PRESS on the topic, *Business Process Management–the SAP Roadmap* by Jim Hagemann Snabe, Ann Rosenberg, Charles Møller, and Mark Scavillo (SAP PRESS 2009), helped readers prepare their company and their teams for the venture of starting a BPM initiative. It helped to answer such questions as: What are the strategic prerequisites? Which goals should we set for BPM within our organization? What would be a good set-up for a BPM Governance Framework? Is it possible to break this huge transformation down to digestible pieces for the people involved? What does SAP offer to support such an initiative?

What we see today is an increasing number of companies that are now ready to actually start the project of revamping their processes and their systems. This new book is therefore mainly focused on how to apply BPM within SAP implementation projects. It explains how BPM and standard software work together, how to prepare your company for the project, and how to put BPM technology, methodology, governance, and the philosophy behind it in action. Extensive use cases from well-known SAP customers, which include technical and process details, make this book a true real-world experience.

The book is structured into four parts:

In Part I, we introduce business process management as an approach for driving innovation and value creation. We advance this topic by exploring vital aspects missing from many BPM projects today: The concepts of value identification, creation and realization, and how to identify the essential processes and activities that provide competitive differentiation. With this foundation, we then suggest a method for innovating business models and business processes to achieve further business value. Part I closes by exploring business drivers for BPM, the importance of connecting the value lifecycle with the process lifecycle, and how to define process and value drivers.

Part II presents real-world examples from SAP customers, which explains how each company has used BPM to improve its business. These stories provide in-depth insight into their business challenges, BPM-enabled solutions, the lessons they learned, and the benefits that were realized. We also explore the commonalities across BPM implementations and present you with a practical approach for identifying and qualifying potential BPM projects.

Part III provides essential guidance to help you in applying BPM in all its aspects in your SAP-centric business IT environments. It explains how to prepare your company for the process-based implementation; and how to apply SAP's new implementation methodology, implementation technology, pre-packaged process-based implementation content, governance frameworks, skills, and the philosophy behind BPM in action.

In Part IV we present topics of interest from SAP researchers and other thought leaders, which explore potential future trends related to BPM. You will explore the six ideas that can be the heart of BPM's future, and you will be able to explore the in-depth details through a number of BPM articles. These articles are bonus material, and are available on this book's catalog pages on www.sap-press.com or www.sap-press.de.

While this book can certainly be read cover to cover, depending on where you are in your BPM journey, you may wish to choose a different path. If your company is ready to begin a BPM project, or has already begun its journey, start with Part I to learn about some important but often neglected components of a holistic BPM approach. If you are looking for inspiration, we recommend starting with Part II, where you will discover the motivations and results of other companies that have gone on the BPM journey. Finally, when you begin planning a BPM program or process-based implementation that includes your SAP practice, Part III will provide you with all the guidelines you need.

Part IV provides a future outlook for everyone who would like to explore the glimpse of BPM's future beyond the realm of the structured processes that we have today.

**Ann Rosenberg, Greg Chase, Rukhshaan Omar,**
**James Taylor, and Mark von Rosing**

## PART I
Business Process
Transformation

If there is one constant in the market, it is that things are always changing faster and are more dynamic. The pressures on organizations and enterprises around the world to keep up with these changes are increasing. Markets are crowded; margins are squeezed. New challenges pop up seemingly overnight on all fronts. All of this is nothing new, but the question remains: How can companies tackle multiple business changes in globalization, productivity, innovation, compliance, information overload, and the changing nature of people and work, plus not forget the golden rule of business: customers first?

Most companies see process effectiveness, efficiency, and innovation to align to their business model and strategy as one of the essential answers to creating long-term competitive advantage. The need for value creation and realization is certainly not new, especially with any topics related to process modeling, process optimization, and process innovation. But companies are struggling to adapt their business models at this accelerating pace to identify where and how to create the needed value. Everything around them seems to be changing faster than they are able to keep pace. In such changing times, many things are important to consider when you want to create superior value. And the internal change alignment (active and reactive) can be initiated from many areas to create the needed value within an organization.

This explains why business process management (BPM) is growing from a hype-cycle into a mature concept, where according to many market analysts, BPM is the fastest growing initiative in today's IT market. The level of interest and the
