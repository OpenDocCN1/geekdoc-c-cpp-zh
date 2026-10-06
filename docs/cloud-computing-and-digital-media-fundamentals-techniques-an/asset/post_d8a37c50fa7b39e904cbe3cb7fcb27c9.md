
# Pearly User Interfaces for Cloud Computing ■ 317

(e.g., Simon) who have access to this record. Such visualization is powerful for displaying the dissemination network. This is crucial in health care where security is key.

When clicking on an entity (actor or medical record), details are provided at the right side of the UI. Using check buttons at the bottom of the UI, the user may filter information depending on the social status of the medical record or the state of expertise.

## 12.5 FIELD STUDY

Based on an iterative user-centered approach, we conducted two successive qualitative experiments to evaluate the pearl metaphor. For this purpose, we implemented the PearlyDesktop as a Java prototype based on the Prefuse (Heer et al. 2005) and Vizster (Heer and Boyd 2005) software libraries devoted to interactive visualization.

### 12.5.1 Protocol

Four experts were recruited: three doctors (participants P1, P3, and P4) to validate the characterization of socially augmented data and the relevance of their presentation, and one specialist of medical information systems for gastroenterology (participant P2). Fifty medical records were entered into the database.

Each interview lasted about an hour and was divided into three parts: (1) presentation of the prototype, (2) playing scenarios, and (3) filling a qualitative questionnaire. All interviews were recorded and then transcribed.

The first part consisted in representing the main features of the UI. We chose to represent the fictive professional network of Dr. Roger filled with fictive medical records.

For the second part, participants had to perform three different kinds of tasks identified as representative:

- 1. Search for an expertise
- 2. Search for a private medical record shared with a student
- 3. Control the dissemination of a sensitive medical record

At the end of this part, users were invited to provide comments about the prototype (usability, utility, etc.).

318 ■ Cloud Computing and Digital MediaAt the end of the interview, in order to identify and understand precisely their vision of socially augmented data, participants had fill in a qualitative questionnaire. This questionnaire is divided into four sections, articulated on the following: (1) actors, (2) data, (3) tasks, and (4) relationships between these concepts.

### 12.5.2 Findings

In this section, we summarize the main results related to participants’ perception of social data and their pearl-based representation.

### 12.5.2.1 Pearly UI: A Social Desktop for the Cloud

Gastroenterologists were eager to play with PearlyDesktop. As ephemeral (e.g., related to students) or persistent (e.g., colleagues) medical networks are important aspects of their activity, participants appreciated the work-based visual representation (P1, P2, P3, and P4). “The structure of the interface is: the visualization at the center and the details displayed in the panel on the right. Legends and filters are meaningful and easy to use. They provide a better understanding and are useful to filter at a finer grain” (P2). We can view our closest contacts and shared folders.[etc.] It is interesting to see the referent doctor of a medical record or the specialist to contact for advice” (P1).

Participants suggested improvements as the visualization of the “relationships within families to better detect hereditary diseases” (P2, P3, and P4) or of “similarities between medical records to find the right dosage of a medicine drug or to improve decisionmaking (P4). They also mentioned scalability as critical: How to represent a huge set of data without disrupting the UX? In addition, during the interview, several participants mentioned the importance of the temporal data: access frequency to a medical record, creation of medical records, or doctor’s schedule. They also suggested improvements including an “alphabetical sorting of medical records” (P2), or a “grouping of contacts [within a community] concentric circles around the center” (P1). Another improvement is to make a clear distinction between “active medical records and medical records of dead patients or patients that will never come back” (P2).

### 12.5.2.2 Social Sharing and Browsing

Participants very much appreciated the opportunity to share data, and thus to support a better communication among stakeholders: “situations of information sharing are numerous: between practitioners about a patient, with laboratories, the hospital for admissions, [etc.]” (P4). Lack of sharing today is a real problem: “we do not know who whom” (P4). “We do not have a full access to information about a patient which is crucial to know, for instance, what the medical treatments are, or to know if the process care for a patient is well managed: our colleagues have difficulties to share data” (P3 and P4). This issue may be explained by “the fear of losing control of their data” (P3), especially with the shift to cloud-based solutions.

Thus, the pearl metaphor was found useful to support sharing and communication activities, thanks to a visualization that merges a view on medical data with the professional network. Participants also pointed out the ability of the metaphor to support traceability. It offers “a better visibility of the medical activity” (P2), and allows “controlling the dissemination of data which gives a feeling of safety” (P3). For confidential medical records shared with a student, it is essential to know what happens to this medical record. With another gastroenterologist, the responsibility is shared” (P3). However, if a student “decides to share this medical record with anyone, the doctor is responsible of” (P3).

Browsing medical records is another issue. A gastroenterologist manages “about 90 medical records every month, about 50 records every day” (P4). During his/her entire career, a practitioner usually collects “between 15,000 and 30,000 medical records” (P2 and P4). Adding the social dimension to data may facilitate the browsing. Indeed, participants underlined the fear of browsing a huge amount of medical data, in particular when asked for an “advice by phone” (P1 and P3).

### 12.5.2.3 Social Information Seeking and Refining

Participants appreciated the organization of the workspace according to the communities.

However, participants also pointed out some issues: “This representation is fine because the pearl is small [to find a medical record]. If the pearl is small, we glance through the different medical records, but if the pearl is larger, how to find easily a medical record” (P1). Currently, doctors do “not have time to waste for medical record searching” (P1).

It seems necessary to allow users searching using attributes similarly to pivot browsing: “by age range, type of examination or pathology, by place of examination” (P3). “When we search for a patient by its name, it’s because there is no relevant criteria for this medical record, or pathology has not been informed” (P1). “We do not necessarily remember patient names, but rather a time, a date or a place” (P3). For these situations, our metaphor appears meaningful, as the social worth of data constitutes additional criteria. This idea seems very suitable for “young doctors or doctors managing a large number of patients” (P3).

320 ■ Cloud Computing and Digital Media## 12.6 DISCUSSION AND IMPLICATIONS

Participants’ feedbacks are very positive. Still, these raise issues that must be addressed by future research.

### 12.6.1 Social Desktop for the Cloud

The experimentations point out the limits of data-centered metaphors: Information is fragmented and distributed across different services—e-mail services to manage contacts (actors), health-care information systems to manage medical records (data), and so on. Our PearlyDesktop prototype appears as a promising answer to (partly) satisfies the needs of health-care professionals.

Similar to Pham’s user-created groups (Pham 2010), we promote an enlarged folder metaphor to integrate the social worth of data. Although Pham’s proposal is based on a visualization that only focuses on relations among actors, our approach merges two: data and actors. In addition, depending on the social status of actors and data, and the social relationships among actors, the view on data may be restricted or enlarged. In instance, while access to medical records would be restricted for students, a referent doctor may have a full access to a medical record managed by a gastroenterologist.

Compared to CloudRoom (Terrenghi et al. 2010) that relies on different and disconnected access to data, we foster a metaphor that reveals the context of data such as the social orbits of Sawyer et al. (2012); physical location related to data such as an operating room or a medical office). The temporal dimension constitutes another means to reveal such a context. However, we investigate how to combine this user-centered representation with a timeline, to allow users to zoom and filter, that preserves the representation of the social context of data.
