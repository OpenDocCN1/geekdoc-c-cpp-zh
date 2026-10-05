# 24.6 The Sequential Container Classes

Let's walk through the sequential container classes (see Table 24.4):

+   array<ElementType,Size>
A fixed number of elements is stored here. Adding and removing is only possible by overwriting. The elements are stored directly next to each other in memory. Therefore, array is suitable for both few huge and many tiny element types, as it has virtually no memory overhead.

![](bbox=[0.333, 0.303, 0.666, 0.335])

**Figure 24.2** An "array" can grow nor shrink, but it is compact.

+   vector<ElementType>
This all-rounder grows automatically. You can insert anywhere, but efficiently only at the back end.

![](bbox=[0.316, 0.467, 0.682, 0.00529])

**Figure 24.3** Schematic representation of a "vector".

Reading the elements is done sequentially forwards, backward, or randomly by index. Also, vector stores its elements directly next to each other in memory, making it practical for both few large and many tiny elements. Optimally used, it has virtually no memory overhead; in suboptimal cases, it is still acceptable as it does not fragment memory.

+   deque<ElementType>
You easily add elements to the end of a vector, but less easily to the beginning, as all existing elements are shifted one place to the right. The double-ended queue deque is suitable for quickly adding elements at both ends. As a disadvantage, it does not store its elements directly next to each other, but still usually more compactly than list. If possible, prefer vector.

![](bbox=[0.333, 0.823, 0.666, 0.00856])

**Figure 24.4** A "deque" can be extended at both ends, but the elements are not contiguous in memory.