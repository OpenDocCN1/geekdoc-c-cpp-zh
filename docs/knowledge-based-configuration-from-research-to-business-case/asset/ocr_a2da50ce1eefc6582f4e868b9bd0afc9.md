# KONWERK

# CHAPTER 24

Lothar Hotz and Andreas Günter
HITeC e.V., University of Hamburg, Hamburg, Germany

Abstract: This chapter presents the domain-independent configuration tool KONWERK. KONWERK provides hybrid configuration representation facilities implemented in so-called basic modules. Enhancement modules provide aspects such as modeling of complex requirements or creating spatial configurations. These modules can be used for developing diverse applications.

# 24.1 Overview

KONWERK¹ is a domain-independent hybrid configuration tool developed at the University of Hamburg (Günter, 1995; Hotz et al., 2006). This tool provides basic modules for knowledge representation and reasoning with four different types of knowledge: (1) conceptual knowledge, (2) constraint knowledge, (3) task knowledge (in the following denoted as task description), and (4) procedural knowledge (see Günter and Cunis, 1992). The conceptual knowledge is represented in an ontology. Taxonomic (isA) and compositional (hasParts) relations are available. Restrictions between knowledge base elements are defined using constraints. Task descriptions represent the user requirements by providing a configuration goal. On the basis of procedural knowledge, a default order for configuration decisions can be defined. The configuration process can be structured into several subtasks to guide the user. Different interaction styles can be realized; for example, a configuration wizard that presents decisions one after another or a more flexible process where the user receives guidance about which configuration steps should be taken next. The outcome of a configuration, using KONWERK, is a detailed description of all components and their attribute values.

The basic modules of KONWERK partially served as a blueprint for the commercial configuration tool EngCon (see Krebs, 2014)² and Hollmann et al. (2000)³. Research activities extended these modules by enhancement modules that support additional aspects of configuration tasks such as resource-based configuration, fuzzy computations, and spatial reasoning.

The remainder of the chapter is organized as follows. In Section 24.2, we provide an overview of the knowledge representation and reasoning supported by KONWERK. Section 24.3 introduces the

¹ KONWERK (Konfigurierungs-Werkzeug, Configuration Tool) was developed in the German government-funded research project Prokon.
² Chapter 23.
³ KONWERK itself is a successor of PLAKON; see Hotz et al. (2014a, Chapter 2) and Neumann (1988).