
# Standardized Multimedia Data in Health-Care Applications

Pulkit Mehnddiratta, Hemjyotasna Parashar, and Shelly Sachdeva

Jaypee Institute of Information Technology Noida, India

Subhash Bhalla
University of Aizu Fukushima, Japan

+ CONTENTS
13.1 Standardized EHR Databases 326
  13.1.1 Standardized EHR Databases 327
  13.1.2 Multimedia Data and Standardized EHRs 327
  13.1.3 Integration of Imaging Standards 328
  13.1.3.1 Imaging Standard: DICOM 329
13.2 Image Data as Part of EHRs 334
  13.2.1 Image Data for Medical Needs 334
  13.2.2 Considering Multimedia EHRs 335
  13.2.2.1 Adoption of DICOM Standard in EHRs 336
  13.2.2.2 Multimedia Unique Identifier: Standardized Effort 336
13.3 EHRs on Cloud Computing Systems 337
13.4 Issues Related to Multimedia Data in EHRs 338
13.4.1 Bandwidth Requirements 339
13.4.2 Archiving and Storage of Multimedia Data 339
13.4.3 MUIs for Different Needs 340
13.5 Summary and Conclusions: Toward Multimedia EHRs 341
References 342

## 13. INTRODUCTION

Considering the recent developments in network technology, distribution of digital multimedia content through the Internet occurs on a very large scale. Electronic health record (EHR) databases are among the important archives in this vast ocean of data. EHRs are paperless solution to a disconnected-care world that runs on a chain of paper files. The EHRs are expected to be interoperable repositories of data that exist within the data management and decision support system [1]. EHR databases are real-time databases, the state of which keeps on changing with time. It is a complex task for medical expert to retrieve relevant information from the database (in a short period of time). In health-care domain, information sharing and information reachability are limited to the safety of patients. A standardized format for the content of a patient's clinical record helps to promote the integration of care among various health-care providers. Medical practices also also require sharing of data by many agencies over long periods of time. Thus, the structure and content of the life-long EHRs require standardization efforts for improving interoperability.

Although the patient's paper-based medical records are scanned and transferred between the providers in a standard image format, it will not fulfill the functional requirements of EHRs; that is, the data cannot form the electronically exchanged medical data that can support analysis and decision making. There is a large variety of the functions supported by the databases and content of EHRs. The sharing of information between the providers introduces new questions and challenging the data to be exchanged and their format. Text-based EHRs contain large amount of data and provide opportunities for analysis (both quantitative and qualitative). However, programming skills are required. Similarly, the use of standardized diagnostic images creates a scope of storing digital multimedia content and other media as well. It will simplify the data sharing and improve interoperability.

## 13.1.1 Standardized EHR Databases

Health-care domain generates large quantities of data from various laboratories, wards, operating theaters, primary care organizations, and wearable and wireless devices [2]. Its primary purpose is to support an efficient and quality-integrated health care. It contains information that is retrospective, concurrent, and prospective. EHRs need to be standardized for information exchange between different clinical organizations. The existing standards aim to achieve data independence along with semantic interoperability.

The semantic interoperable EHR semantics such as Health Level 7 (HL7) [3], openEHR [4], and CEN/ISO 13606 [5] deal with communication, data representation, and meaning. Many medical experts using the standardized EHR system for diagnosis, analysis, and decision making. There are several reasons behind this hindrance as high cost, system complexity, lack of standardization, and different naming convention.

EHRs must provide support for multimedia device and integrating images, along with alphanumeric, and other forms of data. Currently, multimedia data are not part of any standard EHR functionality [6]. Multimedia data should be integral to standardized EHRs because they can capture information that cannot be easily summarized into the text. Multimedia records are also crucial for providing best advice to patients to improve the health-care services and reduce the human errors. Structured text data cannot efficiently present the whole history and current status of patients, and need more time during analysis and decision making compared to visual data and multimedia data. These limitations of structured text data can potentially be overcome by storing nontextual types of data, such as multimedia data. Diagnostic reports as CT scan, X-ray, waveforms, and audio–video file need to be included in EHRs. Although multimedia data are very useful for better clinical judgments, these types of data can be stored in digital form with good clinical interpretations. It can be widely integrated with the existing standardized EHRs. Apart from technical complexity of incorporation of multimedia into EHRs, there are a few challenges for creating multimedia EHR systems [7].

## 13.1.2 Multimedia Data and Standardized EHRs

Multimedia data represent various types of media contents (text, audio, video, animation, and images). These are often used today. The data contents in the text format are huge when considered in regard to EHRs leading to difficulties in communication and analysis. The overall size can possibly be reduced by storing nontextual type of data.

The addition of these types will enable medical experts to explore and create more accurate analysis. XDS-I lays the basic framework for deploying images within the EHR is taking place in many countries including Canada, the United States, Japan, and several European countries. The Institute of Medicine (IOM) recommends the use of multimedia data in EHR.

## 13.1.3 Integration of Imaging Standards

In order to enable EHRs, the technology should support industry standards, such as Digital Imaging and Communications (DICOM) [9], HL7 [3], and Integrating the Health (IHE). Figure 13.1 shows the approaches for integration:

- DICOM: It permits storing images from multiple modalities and providing EHRs with standardized formats.
- HL7: It can be used for messaging for ordering images, sending results, and updating demographic information.
- IHE: It supports Consistent Time Profile (CT), Cross-Enterprise Document Sharing for Imaging (XDS-I), and Audit Trail and Node Authentication (ATNA).

![](f13dd59d15874e4b22b03a27401)
FIGURE 13.1 Imaging standards for EHRs.

### 13.1.3.1 Imaging Standard: DICOM

DICOM [9] is a standard for storing, handling, printing, and transmitting information in medical imaging. It is also known as the National Electrical Manufacturers Association (NEMA) standard PS3.x and as ISO standard 12052:2006 “Health Informatics—DICOM including workflow and data management." Over the years, many versions and updates have been released and the current versions PS3.1x are in compliance with the latest standards and guidelines set by the IOM.

DICOM provides a set of protocols for devices for proper network communication and exchange of information during the communication. DICOM gives consistency in multimedia storage services, format, and report structures. Using DICOM standard, clinical structured reports can be generated in both multimedia and alphanumeric data are integrated.
