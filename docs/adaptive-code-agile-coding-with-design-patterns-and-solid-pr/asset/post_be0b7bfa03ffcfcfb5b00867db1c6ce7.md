
## The information radiator

The Kanban board acts as an information radiator. Anyone within the business should be able to view the Kanban board. Although its viewers might not entirely understand all of the intricacies of the information without additional context, the general progress of cards should be immediately apparent.

> **Note** *Kanban* means sign board. Technically, this makes the term Kanban board redundant, because the *board* is implied, but Kanban is often used to refer to the process itself.

Figure 2-1 shows the simplest example of a Kanban board. It includes only three columns mapping to the phases of work. It is so simple and general that it can apply to any kind of work at all—from household chores such as vacuuming or washing dishes to more complex projects like writing a book. Work is either not yet started, currently in progress, or completed. These states map to the columns To Do, Doing, and Done, respectively.

| To Do | Doing | Done |
|---|---|---|
|  |  |  |

**FIGURE 2-1** Kanban boards can be incredibly simple, capturing only a high-level process overview.

The popular online work-tracking software Trello uses this same default set of columns, but they are configurable. Figure 2-2 shows a screenshot from the Trello board that was used to track the progress of writing this book. Trello is a good option for tracking the work of projects that use a simple process.

The columns on the Kanban board represent the stages of work in progress. Place the Kanban board in a prominent position as close to the team as possible. All Agile processes rely on transparency to perform to their potential, and Kanban is no exception. In fact, Kanban often exposes deficiencies in process, and these pain points should be made very visible, not hidden away.

![](img/f852e0a12c174e64d91a8e1a05146eab_73_0.png)

**FIGURE 2-2** Trello is a popular online service that offers customizable Kanban boards for free.

Consider the analogy of two opposing ways in which code can fail: noisily and obviously through an uncaught exception, or silently and insidiously through an unintended state transition. In the former example, the service or application fails and is unable to function. In the latter example, it continues to run but with unintended consequences that might cause greater harm. You want your process failures to be loud and obvious, and you also want them to be fast. It is likely that the early stages of integrating a Kanban process will be painful and will highlight many issues with your process. This is intentional and emphasizes the strength of Kanban to iteratively improve on your process.

## Process capture

To start integrating a Kanban process, first capture your current process. It does not matter whether you feel that your current process is wrong, too convoluted, or too manual. By capturing your current process, you show how things are, rather than focusing on how you want them to be.

At this early stage, ignore the activities that are external to the team and focus solely on the parts of the process that team members perform.

Figure 2-3 shows a basic outline of the process for delivering features into a production environment for a software development team. Each column represents a state that work can be in along its journey to delivery. These states are mutually exclusive; all work wholly resides in one column or another—it cannot straddle columns.

| Wait | Analyze | Implement | Verify | Deliver |
|---|---|---|---|---|
|  |  |  |  |  |

**FIGURE 2-3** A Kanban board customized for a simple software development process.

The column headers have been deliberately chosen to state their purpose. Backlog is not as clear as Wait. The former is a noun describing a concept of the process that requires further context. The latter is a verb describing the ultimate purpose of the column and the items therein. It is much clearer to the casual observer or those unfamiliar with software development processes to indicate the activity that is performed in each state. Because this is a good example of a common software delivery process, each column—or state—bears further explanation:

- **Wait** This is the common backlog of work to be started. Work items in this column are not yet in progress but are possible options for future work. Whether the items within it are bugs, features, technical improvements, or tasks, the backlog is a container for "stuff" that might or might not eventually be worked on. Items are ordered by priority so that the next item is at the top of the column and proceeds in a first-in-first-out (FIFO) queued fashion.
- **Analyze** Most items in the backlog are single-sentence ideas or descriptions of the problem at hand. No solutions have been decided, and little detail is present. The Analyze column is where sufficient detail is added to the work so that it becomes ready for development. Although some insight into implementation options might be presented, this column emphasizes what needs to be done rather than how it is to be done.
- **Implement** Implementation can now begin, and developers take over to write the code necessary to add new functionality. This is often the slowest part of the software delivery process and, as this chapter will show, there are ways of optimizing your process to maximize throughput despite this.
- **Verify** Although some degree of unit testing is expected of the developers in the Implement phase, it is likely that manual and/or automated verification forms part of your delivery process. This is the final gate before the work is delivered, so there should be a high bar set to ensure the consistent quality of work products.
- **Deliver** When you deliver software, you realize the value that, to this point, has been in progress. All work is incomplete until you have passed through this phase of the process.

The Kanban board in Figure 2-4 includes a new and important detail. Except for the Wait column, each column has been further split into two halves. Although each half has a label specific to the sub-state that the column represents, in each state, the leftmost column represents work in progress and the rightmost column represents work that is ready and waiting for the next phase. The leftmost label, therefore, represents the activity that is being performed on the work, whereas the rightmost label represents the result of that activity.

| Wait | Analyze |  | Implement |  | Verify |  | Deliver |  |
|---|---|---|---|---|---|---|---|---|
|  | Specifying | Ready for Dev | Coding | Dev Complete | Investigating | Accepted | Deploying | Value Added |

**FIGURE 2-4** Some phases of a process might have sub-states that represent completion of the parent phase.

Figure 2-5 shows a Kanban board with numbers below some of the column heads or sub-column heads. These numbers represent limits on work in progress (WIP).

One of the key tenets of Kanban is the enforcement of limits on work in progress. Each work item placed under a column header counts toward that column’s WIP limit.

| Wait | Analyze |  | Implement |  | Verify |  | Deliver |  |
|---|---|---|---|---|---|---|---|---|
|  | 3 |  | 5 |  | 2 |  |  |  |
|  | Specifying | Ready for Dev | Coding | Dev Complete | Investigating | Accepted | Deploying | Value Added |
|  |  |  |  |  |  |  | 1 |  |

**FIGURE 2-5** Work-in-progress limits can apply to either columns or their sub-columns.

The addition of work items to the board shown in Figure 2-6 shows that the Implement column has reached its WIP limit, and no more items can transition to this state. However, the Analyze column has not yet reached its WIP limit, so another work item can be moved into the Analyze column.

![](img/f852e0a12c174e64d91a8e1a05146eab_76_0.png)

Note that the Wait column does not have an associated WIP limit. This allows an infinite number of work items to be placed into the Wait column. Consider the pros and cons of this approach. This allows many new ideas to be captured as work items on the board without limit. But the column can become overloaded and the team overwhelmed by the amount of apparent work that is upcoming. Perhaps limiting the number of items in the Wait column would be a sensible option because, if something is important enough, it will come up again and will eventually be added to the board.

Similar to the Wait column, the Value Added sub-column does not have a WIP limit. The value of this is not so ambiguous, because you do not want to artificially constrain the amount of work that can be delivered. To do so would not make sense, because you want to complete as much work as possible in any particular timeframe.

## Limiting work in progress

The purpose of setting limits on work in progress is to maximize the throughput of the team. A software feature is not truly done until it has passed through all phases of delivery: analysis, implementation, testing, and deployment. Therefore, it is inefficient to start specifying many more work items than the developers can feasibly handle. By limiting the work that business analysts can do, you match their progress to that of the slowest step. More often than not, the slowest part of software delivery is implementation.

## Protecting against change

Setting WIP limits also protects the team against change. If something occurs during delivery that prevents a feature from being implemented—perhaps a forecasted return on investment (ROI) is discovered to be miscalculated—limiting the amount of work in progress has the advantage of lowering the sunken cost.
