# ## 2. Cohesiveness

Another issue that is worth re-stressing, cohesiveness is a measure of functional homogeneity of elements that comprise the modules. This applies to both the components and the relations. One must consider both external and internal views. External cohesion begins with the appropriate naming and meaning of the constituent elements. Internally, the structure and relationships among components are analyzed. For example, coupling through shared data is more cohesive than messages imply a temporal dependency.

# ## 3. Complexity

Two kinds of complexity are identified: functional and behavioral.

Functional complexity is characterized by:

+   - The number of internal functions and relational components.
+   - The goal is to keep these small. Generally, as the number of functions and relations decreases so does the complexity of the design. Note, this does not mean to sacrifice clarity.
+   - Interconnections amongst elements comprising each module.
+   - The earlier discussion of coupling applies here as well. Keep things simple.

Behavioral complexity is characterized by

+   - The number of inputs and outputs.
+   - Once again, the target is a smaller number.
+   - The length and ease of reading and understanding the description of the module.
+   - If several paragraphs or a page of written text (in sub-6-point font) are required to describe the function of one of the modules, that module is probably too complex. To simplify such descriptions, use tables, logical equations, or pseudo-code.
+   - The flow of control through the module and the number and structure of state variables.
+   - Have a single major thread of control through the module and keep the number of states small.

# ## 9.21.1.2 Dynamic Analysis

The objective in performing a dynamic analysis on the system is to determine how it will behave in a context that closely approximates the ultimate working environment. Dynamic analysis considers the following:

+   - Behavior Verification
+     The goal is to ensure that the behavior of system, in its operating environment, meets the operational specification. That is, does it perform the functions it was intended to perform as it was intended to perform them? This verification includes behavior at the boundaries of those functions. To be able to do so, of course, we need a good specification in the first place.
+   - Performance Analysis
+     Performance Analysis ensures that the system, in its operating environment, meets the performance specification. The focus is on specific values for inputs and outputs. We will discuss this in a later chapter.