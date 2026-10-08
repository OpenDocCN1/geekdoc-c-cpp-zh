| ACTIVITY | DESCRIPTION |

| TerminateWorkflow | In many workflows (especially the ones with human interaction) there may be some exceptional branches that require terminating your workflow, either with success or failure. |

| This activity terminates the workflow instance, raises the Completed event in the host, and reports error information. Once the workflow is terminated, it cannot be resumed. |

| In WF 3.5 you can use the Terminate activity with the same semantics. |

| Interop | This activity manages the execution of an activity developed in WF 3.0 or WF 3.5 (System.Workflow.ComponentModel.Activity developed type) within a WF 4.0 workflow. The Interop activity will not appear in the workflow designer Toolbox unless the workflow's project has its Target Framework set to .NET Framework 4 (generally, the default is .NET Framework 4 Client Profile). Use the ActivityProperties and ActivityType properties of the Interop class to characterize the WF 3.0 or WF 3.5 activity to execute. |

# # Flowchart-Specific Activities

As you have seen, WF 4.0 supports creating flowchart-like workflows. Other composite activities such as Sequence, Foreach-T, Parallel, Pick, and so on, declare simple control flow strategy. For example, a Sequence activity executes nested activities in the order they are added to the Activities collection.

In contrast, Flowchart allows you to drop several activities to the design surface and draw connections describing the control flow among the nested activities.

Table 11-6 describes the activities that you allow to create flowchart-like workflows.

**Table 11-6:** Flowchart-Specific Activities

| ACTIVITY | DESCRIPTION |

| Flowchart | This activity models workflows using the familiar flowchart paradigm. It uses the Nodes collection to describe all activities within the flowchart. This collection contains FlowNode instances. The StartNode property describes the first activity in the workflow, and each FlowNode instance is capable of defining the next activity to execute. |

| FlowNode | This class is the abstract base class for all the different node types that can be contained within a Flowchart activity. You can develop your own flowchart-aware activities inheriting from this class. |