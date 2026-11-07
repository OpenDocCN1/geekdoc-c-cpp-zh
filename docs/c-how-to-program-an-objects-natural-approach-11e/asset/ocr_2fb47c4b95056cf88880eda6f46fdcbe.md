Percentage of wins: 50.2%
Percentage of losses: 49.8%
Percentage of wins/losses based on total number of rolls

| Rolls | % Resolved on this roll | Cumulative % of games resolved |
|---:|---:|---:|
| 1 | 30.10% | 30.10% |
| 2 | 20.80% | 50.90% |
| 3 | 14.10% | 65.00% |
| 4 | 9.80% | 74.90% |
| 5 | 7.40% | 82.30% |
| 6 | 4.60% | 86.90% |
| 7 | 3.70% | 90.60% |
| 8 | 2.40% | 93.00% |
| 9 | 1.90% | 94.90% |
| 10 | 1.10% | 96.00% |
| 11 | 0.90% | 96.90% |
| 12 | 0.80% | 97.70% |
| 13 | 0.80% | 98.50% |
| 14 | 0.30% | 98.80% |
| 15 | 0.30% | 99.10% |
| 16 | 0.30% | 99.40% |
| 17 | 0.50% | 99.90% |
| 25 | 0.10% | 100.00% |

# ### Special Section: Systems Software Case Study—Building Your Own Compiler

In Chapter 7, we introduced the made-up Simpletron Machine Language (SML). In Exercise 7.10, you used simulation to create the Simpletron computer—a **virtual machine**—to execute programs written in SML. In this challenge section, you'll build a "toy" compiler that converts programs written in Simple—a made-up, concise, high-level programming language—to SML. This section "ties" together key pieces of the programming process. You'll:

+   - **write** several Simple high-level language programs,
+   - **compile** the programs using the compiler you'll build, generating SML machine-language code into a file,
+   - **load** the SML machine-language code from that file into the Simpletron's memory, and
+   - **execute** the SML machine-language programs on the Simpletron virtual machine you built in Exercise 7.10.

This section consists of six exercises. The first two cover some key computer-science technology you'll need to implement your compiler. The third introduces the Simple high-level language with some completely coded examples and asks you to write several of your own Simple programs. The fourth guides you through building your **Simple compiler**. The fifth introduces the crucial topic of **compiler optimization**—you'll modify your compiler to reduce the number of SML instructions it generates, which will make your SML programs more memory efficient and enable them to execute faster. The final exercise challenges you to modify your compiler to add more useful features.