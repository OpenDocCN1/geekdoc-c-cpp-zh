called a **double-selection statement** because it selects between two different actions (or groups of actions). The switch selection statement is called a **multiple-selection statement** because it selects among many different actions (or groups of actions).

# Repetition Statements in C++

C++ provides three types of repetition statements (also called **looping statements** or **loops**) for performing statements repeatedly while a condition (called the **loop-continuation condition**) remains true. These are the **while**, **do...while** and **for** statements. (Chapter 5 presents the do...while and for statements, and Chapter 7 presents a specialized version of the for statement that’s used with so-called arrays and containers.) The while and for statements perform the action (or group of actions) in their bodies zero or more times—if the loop-continuation condition is initially false, the action (or group of actions) will **not** execute. The do...while statement performs the action (or group of actions) in its body at **least once**.

Each of the words if, else, switch, while, do and for is a C++ keyword. Keywords **cannot** be used as identifiers, such as variable names, and must be spelled with only lowercase letters. Figure 4.3 provides a complete list of C++ keywords.

| C++ Keywords |  |  |  |  |
|---|---|---|---|---|
| *Keywords common to the C and C++ programming languages* |  |  |  |  |
| auto | break | case | char | const |
| continue | default | do | double | else |
| enum | extern | float | for | goto |
| if | int | long | register | return |
| short | signed | sizeof | static | struct |
| switch | typedef | union | unsigned | void |
| volatile | while |  |  |  |
| *C++-only keywords* |  |  |  |  |
| and | and_eq | asm | bitand | bitor |
| bool | catch | class | compl | const_cast |
| delete | dynamic_cast | explicit | export | false |
| friend | inline | mutable | namespace | new |
| not | not_eq | operator | or | or_eq |
| private | protected | public | reinterpret_cast | static_cast |
| template | this | throw | true | try |
| typedef | typename | using | virtual | wchar_t |
| xor | xor_eq |  |  |  |
| *C++11 keywords* |  |  |  |  |
| alignas | alignof | char16_t | char32_t | constexpr |
| decltype | noexcept | nullptr | static_assert | thread_local |

**Fig. 4.3**  |  C++ keywords.