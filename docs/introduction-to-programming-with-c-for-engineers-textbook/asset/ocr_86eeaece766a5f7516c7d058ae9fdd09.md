\begin{tabular}{ccc}
Object & Description & Examples \\
std::chrono:: system\_clock & A wall clock time from the system-wide realtime clock. It may not be monotonic (time can be adjusted at any moment). & The following shows a function to return a string with the current date and time: \\
std::chrono:: steady\_clock & A monotonic clock (not adjustable). The time points of this clock cannot decrease as physical time progresses. Hence, this clock is suitable for measuring intervals. & The following shows a function to return a string with the current date and time: \\
std::chrono:: high\_resolution\_ clock & The clock with the shortest tick period available on a platform.a & The following shows a function to return a string with the current date and time: \\
\end{tabular}