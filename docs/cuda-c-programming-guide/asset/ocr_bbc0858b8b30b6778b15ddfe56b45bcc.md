| Language Feature | C++11 Proposal | Available in nvcc (device code) |
|---|---|---|
| Extended integral types | N1988 | |

# F.2. C++14 Language Features

The following table lists new language features that have been accepted into the C++14 standard.

# Table 13 C++14 Language Features

| Language Feature | C++14 Proposal | Available in nvcc (device code) |
|---|---|---|
| Tweak to certain C++ contextual conversions | N3323 | 9.0 |
| Binary literals | N3472 | 9.0 |
| Functions with deduced return type | N3638 | 9.0 |
| Generalized lambda capture (init-capture) | N3648 | 9.0 |
| Generic (polymorphic) lambda expressions | N3649 | 9.0 |
| Variable templates | N3651 | 9.0 |
| Relaxing restrictions on constexpr functions | N3652 | 9.0 |
| Member initializers and aggregates | N3653 | 9.0 |
| Clarifying memory allocation | N3664 | |
| Sized deallocation | N3778 | |
| [[deprecated]] attribute | N3760 | 9.0 |
| Single-quotation-mark as a digit separator | N3781 | 9.0 |

# F.3. Restrictions

# F.3.1. Host Compiler Extensions

Host compiler specific language extensions are not supported in device code.

__int128 and __Complex types are only supported in host code.

__float128 type is only supported in host code on 64-bit x86 Linux platforms. A constant expression of __float128 type may be processed by the compiler in a floating point representation with lower precision.