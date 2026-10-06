# Data Ordering

Ordering and parallelism have a natural tension. When a dataset order can- be impacted, the implementation of how parallel tasks are executed and the results merged narrows considerably, causing a performance decrease. In most cases, the parallel implementation will still be superior in performance to the sequential implementation, but for the best paral-ization, try and limit order dependence.

The key point is that if ordering is required to be predictable, then parallel performance is traded. This can often be minimized by increasing the granularity of the task to run order dependent code in one parallel processing after order dependent code executed sequentially after the parallel processing has been carried out.

# Exceptions—Who Stops When Something Fails?

Exception that occurs in a parallel task offers great challenges. How this exception is trapped and where that exception is marshaled is problematic to design, predict, and implement. Obvious obvious, but avoid exceptions! You have to be prudent and carry out precondition checking to han-dle exception cases in an organized fashion without resorting to throwing an exception or having one raised on your behalf.

# Dealing with These Constraints

Dealing with and understanding the constraints of writing operational par-lel code is an important skill. Microsoft’s Parallel Extensions offers sol-utions to the general challenges, but in order to successfully write code that performs exceptionally in a multicore environment, you often need to explicitly tell the executing framework what your requirements are for your specific case. For example, if the data order needs to be maintained, you need to tell the compiler that is the case. You will pay a performance penalty (maybe slight faster than a sequential algorithm, maybe not), for the final result to be correct, the compiler must be told to maintain the cur-rent data order.

Microsoft has addressed the issues of parallelizing data problems through a specific technology called Parallel LINQ. The technology tackles parallelizing data querying and manipulation in a coherent fashion without causing data corruption or incorrect results. It still has to abide by the constraints and limitations as listed here, but the heavy lifting and consist-ent programming pattern it provides reduces the variation in personal techniques.