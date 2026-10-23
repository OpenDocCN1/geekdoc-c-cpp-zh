# encoway

# CHAPTER 23

Thorsten Krebs
encoway GmbH, Bremen, Germany

Abstract: This chapter describes the basics of the encoway configuration environment. encoway is working with a set of tools that best suits the heterogeneous system landscapes and their very different needs that encoway encounters in real-life customer projects. In the following we give a brief introduction of the configuration environment, including a scientific background, an architecture description, and typical system landscapes in which encoway integrates configuration applications.

# 23.1 Introduction

This chapter describes the basics of the encoway¹ configuration environment. encoway is working with a set of tools for the different tasks of data integration and maintenance, product modeling and configuration, representing and displaying configuration decisions and related rich content, as well as quote generation and handling transaction data in general. This set of tools best suits the heterogeneous system landscapes and their very different needs that encoway encounters in real life customer projects.

The remainder of this chapter is organized as follows. Section 23.2 presents an overview of encoway’s history and its roots within the scientific community. Section 23.3 briefly discusses the configuration and reasoning methods that are implemented within encoway’s configuration environment. Section 23.4 presents an overview of encoway’s system architecture and typical system landscapes in which encoway integrates configuration applications. Section 23.5 describes the necessary data required for such configuration applications. Section 23.6 discusses the quote generation process in which configuration plays a key role between selecting configurable products and generating quote documents. Finally, Section 23.7 summarizes and concludes this chapter.

# 23.2 History and Scientific Basis

encoway uses methods from structure-based (component-oriented) configuration that have a long history in the research area of Artificial Intelligence (see e.g., Günter, 1995). The declarative approach of representing products by means of structure-based configuration is especially well suited for managing large amounts of product variants and configuring complex products. encoway itself is deeply rooted in research. The company was founded as a spin-off from the research institute TZI (Center for Computing

¹ http://www.encoway.de.