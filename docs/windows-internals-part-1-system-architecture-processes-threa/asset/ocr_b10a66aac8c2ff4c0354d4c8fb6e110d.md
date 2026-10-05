the algorithm keeps searching for the next-closest node, and so, until all nodes in the current group have been exhausted. (Recall that Windows allows a thread to have affinity only on a single group.) If this process fails to find any candidates, the function returns NULL and the processor enters the idle thread in the case of a wait (which will skip idle scheduling). If this work was already being done from the idle scheduler, the processor enters a sleep state.

# Processor selection

We've described how Windows picks a thread when a logical processor needs to make a selection (or when a selection must be made for a given logical processor) and assumed the scheduling routines have an extensive database of ready threads to choose from. We'll see how this database gets populated in the first place—in other words, how Windows chooses LP's ready queues to associate with a given ready thread. Having described the multiprocessor systems supported by Windows as well as thread-affinity and idle processor settings, we're now ready to examine how this information is used for this purpose.

# Choosing a processor for when there are idle processors

When a thread becomes ready to run, the KiDeferredReadyThread scheduler function is called. This prompts Windows to perform two tasks:

+   - Adjust priorities and refresh quantums as needed (explained in the "Priority boosts" section)
- Pick the best logical processor for the thread.

Windows first looks up the thread's ideal processor and then computes the set of idle processors within the thread's affinity mask. This is then pruned as follows:

+   1. Any idle processors that have been parked by the core-parking mechanism are removed. (See Chapter 6 for more information on core-parking) If this causes no idle processors to remain, idle processor selection is aborted, and the scheduler behaves as if no idle processors were available (in the next section).
2. Any idle processors that are not on the ideal node (defined as the node containing the ideal processor) are removed (unless this would cause all idle processors to be eliminated).
3. On an SMT system, any non-ideal SMT sets are removed, even if this might cause elimination of the ideal processor itself. In other words, Windows prioritizes a non-ideal, idle SMT set over another.
4. Windows checks whether the ideal processor is among the remaining set of idle processors. If not, it then finds the most appropriate idle processor. To do this, it first checks whether the processor that the thread last ran on is part of the remaining idle set. If so, it considers this processor to be a temporary ideal processor and selects it (Recall that the ideal processor attempts to maximize processor cache hits, and picking the last processor a thread ran on is a good way of doing so.) If the last processor is not part of the remaining idle set, Windows checks whether the current processor (that is, the processor currently executing this scheduling code) is part of this set. If so, it applies the same logic as before.