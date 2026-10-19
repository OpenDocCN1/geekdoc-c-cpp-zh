Microsoft’s applications division has found that it takes three hours to find and fix a defect by using code inspection, a one-step technique, and 12 hours to find and fix a defect by using testing, a two-step technique (Moore 1992). Collofello and Woodfield reported on a 700,000-line program built by over 400 developers (1989). They found that code reviews were several times as cost-effective as testing—a 1.38 return on investment vs. 0.17.

The bottom line is that an effective software-quality program must include a combination of techniques that apply to all stages of development. Here’s a recommended combination for achieving higher-than-average quality:

+   - Formal inspections of all requirements, all architecture, and designs for critical parts of a system
+   - Modeling or prototyping
+   - Code reading or inspections
+   - Execution testing

# 20.4 When to Do Quality Assurance

> **Cross-Reference** Quality assurance of upstream activities—requirements and architecture, for instance—can be outside the scope of this book. The “Additional Resources” section at the end of the chapter describes books you can turn to for more information about them.

As Chapter 3 (“Measure Twice, Cut Once: Upstream Prerequisites”) noted, the earlier an error is inserted into software, the more entangled it becomes in other parts of the software and the more expensive it becomes to remove. A fault in requirements can produce one or more corresponding faults in design, which can produce many corresponding faults in code. A requirements error can result in extra architecture or in bad architectural decisions. The extra architecture results in extra code, test cases, and documentation. Or a requirements error can result in architecture, code, and test cases that are thrown away. Just as it’s a good idea to work out the defects in the blueprints for a house before pouring the foundation in concrete, it’s a good idea to catch requirements and architecture errors before they affect later activities.

In addition, errors in requirements or architecture tend to be more sweeping than construction errors. A single architectural error can affect several classes and dozens of routines, whereas a single construction error is unlikely to affect more than one routine or class. For this reason, too, it’s cost-effective to catch errors as early as you can.

Defects creep into software at all stages. Consequently, you should emphasize quality-assurance work in the early stages and throughout the rest of the project. It should be planned into the project as work begins; it should be part of the technical fiber of the project as work continues; and it should punctuate the end of the project, verifying the quality of the product as work ends.

![](bbox=[0.166, 0.07, 0.242, 0.128])

![](bbox=[0.166, 0.77, 0.242, 0.833])