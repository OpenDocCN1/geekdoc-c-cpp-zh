ture, however, no additional scaffolding is needed. Since each feature is self-contained, each feature contains all the support code it needs.

The second main advantage is that each newly integrated feature brings about an incremental addition in functionality. This provides evidence that the project is moving steadily forward. It also creates functional software that you can provide to your customers for evaluation or that you can release earlier and with less functionality than originally planned.

A third advantage is that feature-oriented integration works well with object-oriented design. Objects tend to map well to features, which makes feature-oriented integration a natural choice for object-oriented systems.

Pure feature-oriented integration is as difficult to pursue as pure top-down or bottom-up integration. Usually some of the low-level code must be integrated before certain significant features can be.

# T-Shaped Integration

A final approach that often addresses the problems associated with top-down and bottom-up integration is called “T-shaped integration.” In this approach, one specific vertical slice is selected for early development and integration. That slice should exercise the system end-to-end and should be capable of flushing out any major problems in the system’s design assumptions. Once that vertical slice has been implemented—and any associated problems have been corrected—the overall breadth of the system can be developed (such as the menu system in a desktop application). This approach, illustrated in Figure 29-12, is often combined with risk-oriented or feature-oriented integration.

![](bbox=[0.24, 0.65, 0.7, 0.84])

Figure 29-12 In T-shaped integration, you build and integrate a deep slice of the system to verify architectural assumptions, and then you build and integrate the breadth of the system to provide a framework for developing the remaining functionality.