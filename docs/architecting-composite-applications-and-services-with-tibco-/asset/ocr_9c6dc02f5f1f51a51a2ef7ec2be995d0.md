# Solution Architecture

A solution is a working answer to a business problem. It comprises one or more business processes that do the work of solving the problem along with the participants (human and system) who execute those processes. A solution architecture describes the overall structure and organization of the solution: its business processes, its architecture pattern, and the mapping of the processes onto that pattern.

# Solution Architecture Pattern

When a service is used in a solution, it becomes an element in the solution’s architecture pattern. Figure 1-11 shows a solution pattern for a wholesale goods business that utilizes an Account Manager to keep track of customer account balances. The architecture pattern indicates which elements are users of the service and the interface(s) being used. In this example, the Order Manager and Billing Manager are both users of the Account Management Service.

# Solution Business Processes

Solutions implement one or more business processes. It is through these business processes that the solution provides value to the enterprise. In the wholesale goods example we have two business processes: Purchase Goods and Settle Account (Figure 1-12).

Each of these business processes involves the execution of a number of activities. Figure 1-13 shows the activities of the Purchase Goods business process.

# Solution Process Mapping

To complete the solution, each business process has to be mapped onto the elements of the architecture pattern. When a service is involved, some of the activities in the process are performed by the service. In the Purchase Goods process, the updating of the customer account balance is done by the Account Manager (Figure 1-14). This mapping shows the specific operation involved in the interaction. In defining the mapping, the coordination pattern for each interaction is determined.