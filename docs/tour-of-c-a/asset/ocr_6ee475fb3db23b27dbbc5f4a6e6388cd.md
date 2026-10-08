+   [7] Prefer resource handles with specific semantics to smart pointers; $15.2.1.

+   [8] Don't use unique_ptr to shared_ptr as will do; $15.2.1.

+   [9] Prefer unique_ptr to shared_ptr as arguments or return values to transfer ownership responsibilities; $15.2.1; [CG: F2.6]; [CG: F.27].

+   [11] Use make_unique() to construct unique_ptrs; $15.2.1; [CG: R.22].

+   [12] Use make_shared() to construct shared_ptrs; $15.2.1; [CG: R.23].

+   [13] Prefer pointers to garbage collection; $6.3, $15.2.1.

+   [14] Prefer spans to pointer-plus-plus interfaces; $15.2.2; [CG: F.24].

+   [15] Use spans range-for; $15.2.2.

+   [16] Use array when you need a sequence with constexpr size; $15.3.1.

+   [17] Prefer array over built-in arrays; $15.3.1; [CG: SL.con2].

+   [18] Use bitset when you need N bits and N is not necessarily the number of bits in a built-in integer type; $15.3.2.

+   [19] Don't use pair and tuple; named structs often lead to more readable code; $15.3.3.

+   [20] When using pair, use template argument deduction or make_pair() to avoid redundant type specification; $15.3.3; [CG: T.44].

+   [21] When using tuple, use template argument deduction or make_tuple() to avoid redundant specification; $15.4.1.

+   [22] Prefer variant to explicit use of unions; $15.4.1; [CG: C.181].

+   [23] When selecting among a set of alternatives using a variant, consider using visit() and overloaded(); $15.4.1.

+   [24] If more alternative is possible for a variant, optional, or any, check the tag access; $15.4.