![](bbox=[0.25, 0.07, 0.66, 0.3])

# Project Size in Lines of Code

Figure 27-2 As project size increases, errors usually come more from requirements and design. Sometimes they still come primarily from construction (Boehm 1981, Grady 1987, Jones 1998).

![](bbox=[0.115, 0.39, 0.21, 0.46])

On small projects, construction errors make up about 75 percent of all the errors found. Methodology has less influence on code quality, and the biggest influence on program quality is often the skill of the individual writing the program (Jones 1998).

On larger projects, construction errors can taper off to about 50 percent of the total errors; requirements and architecture errors make up the difference. Presumably this is related to the fact that more requirements development and architectural design are required on large projects, so the opportunity for errors arising out of those activities is proportionally larger. In some very large projects, however, the proportion of construction errors remains high; sometimes even with 500,000 lines of code, up to 75 percent of the errors can be attributed to construction (Grady 1987).

![](bbox=[0.115, 0.61, 0.21, 0.68])

As the kinds of defects change with size, so do the numbers of defects. You would naturally expect a project that’s twice as large as another to have twice as many errors. But the density of defects—the number of defects per 1000 lines of code—increases. The product that’s twice as large is likely to have more than twice as many errors. Table 27-1 shows the range of defect densities you can expect on projects of various sizes.

# Table 27-1 Project Size and Typical Error Density

| Project Size (in Lines of Code) | Typical Error Density |
|---|---|
| Smaller than 2K | 0–25 errors per thousand lines of code (KLOC) |
| 2K–16K | 0–40 errors per KLOC |
| 16K–64K | 0.5–50 errors per KLOC |
| 64K–512K | 2–70 errors per KLOC |
| 512K or more | 4–100 errors per KLOC |
| Sources: "Program Quality and Programmer Productivity" (Jones 1977), Estimating Software Costs (Jones 1998). |