# Chapter 10: Tuning for Performance and Efficiency

Introduction ........................................................................................ 351

Understanding Performance Tuning....................................................... 352

Sorting and Performance ....................................................................... 352

User-Specified Sorting (SORTPGM= System Options)................................... 353

Automatic Sorting............................................................................... 353

Grouping and Performance .................................................................... 354

Splitting Tables ................................................................................. 354

Indexes and Performance....................................................................... 354

Reviewing CONTENTS Output and System Messages ................................... 355

Optimizing WHERE Clause Processing with Indexes ................................... 358

Constructing Efficient Logic Conditions................................................... 359

Avoiding UNIONs ................................................................................ 361

Summary ............................................................................................. 365

# Introduction

A book on PROC SQL would not be complete without some discussion of query optimization and performance. Enabling a query to run efficiently involves writing code that can take advantage of the PROC SQL query optimizer. Because PROC SQL is designed to handle a variety of processes while accommodating small to large database environments, this chapter presents a number of query tuning strategies, techniques, and options to help you to write more efficient PROC SQL code. In this chapter, you will find tips and suggestions to help identify areas where a query’s inefficiencies might exist and to conduct the tuning process to achieve the best performance possible.