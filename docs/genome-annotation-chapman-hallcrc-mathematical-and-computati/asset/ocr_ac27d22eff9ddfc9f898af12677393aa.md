# 178 ■ Genome Annotation

![](bbox=[0.137, 0.076, 0.862, 0.313])

FIGURE 10.4 Galaxy graphical editor of the workflow extracted from Figure 10.3. New tools can be added from the left pane and existing steps/connections edited on the diagram. Labels can be edited in the right pane.

The workflow, which was saved by the user in Galaxy, can be executed or edited graphically as in Figure 10.4. It is recommended to edit the workflow to include meaningful names for the workflow steps and free annotations (right side of the figure), which can contain additional documentation. This maximizes the usefulness of the workflow, revisited later, or by users with whom it is subsequently shared. The workflow can be edited later, for example, to reflect changing analysis needs. The layout of the steps, as well as the tool connection in the dataflow, can be directly manipulated by the workflow diagram. Workflow elements can be removed from the diagram and new ones can be added using the tool selection pane in the left-hand pane of the Galaxy interface (Figure 10.4).

It should be noted that running sequence-based workflows on the public Galaxy server can quickly exceed the allotted disk quotas. Therefore, workflows can be exported and executed on a local installation of Galaxy, but one must ensure that the local installation has the same set of tools enabled as the public portal.

# 10.3.3 Component Repository

Creating a local installation of Galaxy requires at a minimum level of comfort with the command line, a multi-CPU computer, and significant available disk space to store reference databases and user analyses. Beyond avoiding quota limitations, a local installation allows the technically savvy user to deploy new file types and tools in the walled garden. The Galaxy Tool Shed (http://toolshed.g2.bx.psu.edu) is a repository of user-contributed noncommutative extensions to Galaxy. If maintained properly, a local Galaxy installation can