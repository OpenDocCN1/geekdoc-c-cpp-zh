# # Chapter 12 Lazy Evaluation

Such constructs can be designed to form an internal domain-specific programming language—a kind of mini-language within a language.

+   - Streams are sequences that are lazily evaluated and (typically) memoized. Their values are computed only when (and if) needed and, if the stream is memoized, stored for later retrieval.
+   - Streams are well suited to pipelined transformation of data. Being lazily evaluated, they do not require allocation of a separate data structure for each stage of a pipeline.
+   - Streams can also be used to implement sequences that are conceptually infinite, as long as there is never an attempt to evaluate the entire sequence. Infinite streams can often replace mutable objects, such as iterators and stateful generators, with a more functional alternative.
+   - Because of memoization, streams involve a risk of leakage as they grow in memory. Languages may define non-memoized variants that introduce only laziness. They are sometimes called views (but also iterators or even streams, which can be confusing).
+   - In addition to delayed arguments and lazily evaluated data structures, languages may support lazy initialization of fields and local variables. This can be used to delay costly evaluation of code until a value is first used, possibly avoiding an entire computation if a value is never used.