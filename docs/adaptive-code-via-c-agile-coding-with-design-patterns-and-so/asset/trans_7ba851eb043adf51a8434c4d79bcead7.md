

# Adaptive
Code via C#

使用设计模式和 SOLID 原则进行敏捷编码

![](img/65c1bad7a6b3cffae8cbb79664f0708b_0_0.png)

![](img/65c1bad7a6b3cffae8cbb79664f0708b_0_1.png)

Professional

![](img/65c1bad7a6b3cffae8cbb79664f0708b_0_2.png)

Gary McLean Hall

# Adaptive
Code via C#

使用设计模式和 SOLID 原则进行敏捷编码

Gary McLean Hall

Microsoft

Professional

![](img/65c1bad7a6b3cffae8cbb79664f0708b_1_0.png)

![](img/65c1bad7a6b3cffae8cbb79664f0708b_1_1.png)

# Adaptive Code via C#

# 使用设计模式和 SOLID 原则进行敏捷编码

Gary McLean Hall

![](img/65c1bad7a6b3cffae8cbb79664f0708b_2_0.png)

PUBLISHED BY
Microsoft Press
A division of Microsoft Corporation
One Microsoft Way
Redmond, Washington 98052-6399

Copyright © 2014 by Gary McLean Hall. All rights reserved.

No part of the contents of this book may be reproduced or transmitted in any form or by any means without the written permission of the publisher.

Library of Congress Control Number: 2014943458
ISBN: 978-0-7356-8320-4

Printed and bound in the United States of America.

First Printing

Microsoft Press books are available through booksellers and distributors worldwide. If you need support related to this book, email Microsoft Press Book Support at mspinput@microsoft.com. Please tell us what you think of this book at http://aka.ms/tellpress.

This book is provided “as-is” and expresses the author’s views and opinions. The views, opinions and information expressed in this book, including URL and other Internet website references, may change without notice.

Some examples depicted herein are provided for illustration only and are fictitious. No real association or connection is intended or should be inferred.

Microsoft and the trademarks listed at http://www.microsoft.com on the “Trademarks” webpage are trademarks of the Microsoft group of companies. All other marks are property of their respective owners.

Acquisitions Editor: Devon Musgrave
Developmental Editor: Devon Musgrave
Project Editor: Devon Musgrave
Editorial Production: Online Training Solutions, Inc. (OTSI)
Technical Reviewer: Jeremy Johnson
Copyeditor: Kathy Krause (OTSI)
Indexer: Krista Wall (OTSI)
Cover: Twist Creative • Seattle and Joel Panchot

For Amelia Rose

—GARY McLEAN HALL

# Contents at a glance

Introduction

# PART I AN AGILE FOUNDATION

CHAPTER 1 Introduction to Scrum

CHAPTER 2 Dependencies and layering

CHAPTER 3 Interfaces and design patterns

CHAPTER 4 Unit testing and refactoring

# PART II WRITING SOLID CODE

CHAPTER 5 The single responsibility principle

CHAPTER 6 The open/closed principle

CHAPTER 7 The Liskov substitution principle

CHAPTER 8 Interface segregation

CHAPTER 9 Dependency injection

# PART III ADAPTIVE SAMPLE

CHAPTER 10 Adaptive sample: Introduction

CHAPTER 11 Adaptive sample: Sprint 1

CHAPTER 12 Adaptive sample: Sprint 2

Appendix A: Adaptive tools

Appendix B: GitHub code samples online

Index

About the author

# Contents

Introduction

# PART I AN AGILE FOUNDATION

# Chapter 1 Introduction to Scrum

Scrum versus waterfall

Roles and responsibilities

Product owner

Scrum master

Development team

Pigs and chickens

Artifacts

The Scrum board

Charts and metrics

Backlogs

The sprint

Release planning

Sprint planning

Daily Scrum

Sprint demo

Sprint retrospective

Scrum calendar

Problems with Scrum and Agile

Maladaptive code

Conclusion

# Chapter 2 Dependencies and layering

The definition of dependency

A simple example

Modeling dependencies in a directed graph

Managing dependencies

Implementations versus interfaces

The new code smell

Alternatives to object construction

The Entourage anti-pattern

# The Stairway pattern

# Resolving dependencies

# Dependency management with NuGet

# Layering

# Common patterns

# Cross-cutting concerns

# Asymmetric layering

# Conclusion

# Chapter 3 Interfaces and design patterns

# What is an interface?

# Syntax

# Explicit implementation

# Polymorphism

# Adaptive design patterns

# The Null Object pattern

# The Adapter pattern

# The Strategy pattern

# Further versatility

# Duck-typing

# Mixins

# Fluent interfaces

# Conclusion

# Chapter 4 Unit testing and refactoring

# Unit testing

# Arrange, Act, Assert

# Test-driven development

# More complex tests

# Refactoring

# Changing existing code

# A new account type

# Conclusion

# PART II WRITING SOLID CODE

# Chapter 5 The single responsibility principle

# Problem statement

Refactoring for clarity

Refactoring for abstraction

SRP and the Decorator pattern

The Composite pattern

Predicate decorators

Branching decorators

Lazy decorators

Logging decorators

Profiling decorators

Asynchronous decorators

Decorating properties and events

Using the Strategy pattern instead of switch

Conclusion

# Chapter 6 The open/closed principle

Introduction to the open/closed principle

The Meyer definition

The Martin definition

Bug fixes

Client awareness

Extension points

Code without extension points

Virtual methods

Abstract methods

Interface inheritance

“Design for inheritance or prohibit it”

Protected variation

Predicted variation

A stable interface

Just enough adaptability

Conclusion

# Chapter 7 The Liskov substitution principle

Introduction to the Liskov substitution principle

Formal definition

LSP rules

Contracts

# Preconditions

# Postconditions

# Data invariants

# Liskov contract rules

# Code contracts

# Covariance and contravariance

# Definitions

# Liskov type system rules

# Conclusion

# Chapter 8 Interface segregation

# A segregation example

# A simple CRUD interface

# Caching

# Multiple interface decoration

# Client construction

# Multiple implementations, multiple instances

# Single implementation, single instance

# The Interface Soup anti-pattern

# Splitting interfaces

# Client need

# Architectural need

# Single-method interfaces

# Conclusion

# Chapter 9 Dependency injection

# Humble beginnings

# The Task List application

# Constructing the object graph

# Inversion of Control

# Beyond simple injection

# The Service Locator anti-pattern

# Illegitimate Injection

# The composition root

# Convention over configuration

# Conclusion

# PART III ADAPTIVE SAMPLE

# Chapter 10 Adaptive sample: Introduction

+   - Trey Research
+     - The team
+     - The product
+   - Initial backlog
+     - Finding stories in prose
+     - Story point estimation
+     - Summary

# Chapter 11 Adaptive sample: Sprint 1

+   - Planning
+   - “I want to create rooms for categorizing conversations.”
+     - The controller
+     - The room repository
+   - “I want to view a list of rooms that represent conversations.”
+   - “I want to view the messages that have been sent to a room.”
+   - “I want to send plain text messages to other room members.”
+   - Sprint demo
+     - First demonstration of Proseware
+   - Sprint retrospective
+     - What went well?
+     - What went badly?
+     - Things to change?
+     - Things to keep?
+     - Surprises?
+     - Summary

# Chapter 12 Adaptive sample: Sprint 2

+   - Planning
+   - “I want to send markdown that will be correctly formatted.”
+   - “I want to filter message content so that it is appropriate.”
+   - “I want to serve hundreds of users concurrently.”
+   - Sprint demo
+   - Sprint retrospective
+     - What went well?
+     - What went badly?
+     - Things to change?

Things to keep?

Surprises?

Summary

Appendix A: Adaptive tools

Appendix B: GitHub code samples online

Index

About the author

# What do you think of this book? We want to hear from you!

Microsoft is interested in hearing your feedback so we can continually improve our books and learning resources for you. To participate in a brief online survey, please visit:

microsoft.com/learning/booksurvey

# Introduction

本书标题的前半部分 Adaptive Code 很好地描述了应用本书原则后的结果：代码能够适应任何新需求或不可预见的场景，同时避免大量的返工。本书的目的是将 C# 编程与 Microsoft .NET Framework 世界中当前的许多最佳实践汇集到一卷中。虽然部分内容在其他书籍中也有涉及，但那些书籍要么在理论上侧重过重，要么不具体针对 .NET 开发。

编程可能是一个缓慢的过程。如果你的代码具有适应性，你将能够比使用阻碍更改的代码库时更快、更轻松、且错误更少地对其进行更改。需求，如每个开发人员所知，可能会发生变化。变化的管理方式是成功软件项目与因范围蔓延而衰退的项目之间的关键区别因素。开发人员可以以多种方式对需求变化做出反应，两种对立的观点突出了两者之间的连续性。

首先，开发人员可以选择僵化的观点。在这种方法中，从开发过程到类设计，项目就像 50 年前使用穿孔卡实现的项目一样不灵活。水fall 方法论是显而易见的罪魁祸首，确保软件无法自由更改。它们坚持分析、设计、实现和测试阶段必须明确且单向，使得客户在实现开始后更改需求变得困难——或至少昂贵。然后，代码不需要为更改而构建：流程几乎禁止了更改。

第二种方法，敏捷方法论，不仅是对这种僵化方法论的替代，而且是对其的反应。敏捷流程的目标是把变化作为客户与开发人员之间合同的必要部分来拥抱。如果客户想要更改他们正在付费的产品中的某些内容，时间和财务成本应与更改的大小相关，而不是与当前正在进行的流程阶段相关。与物理工程不同，软件工程使用一种可塑的工具：源代码。构成房屋的砖石在施工过程中实际上是融合在一起的。更改房屋设计的费用必然与建筑阶段的完成相关。如果项目尚未开始——如果它仍只是蓝图——更改相对便宜。如果窗户已安装，电线已布线，管道已安装，将楼上浴室移到厨房旁边可能代价高昂。对于代码来说，移动功能和重新设计用户界面的导航不应该如此重要。不幸的是，这并不总是如此。仅时间成本本身就常常禁止此类更改。我发现这在很大程度上是由于代码缺乏适应性所致。

本书展示了第二种方法，并通过真实世界的示例解释了实现自适应代码的实际操作。

# Who should read this book

本书旨在弥合理论与实践之间的差距。本书的读者是寻求设计模式、SOLID 原则、单元测试和重构等更多实际示例的经验丰富的程序员。

希望填补知识空白或对行业最佳实践如何结合有疑问和问题的有能力的中间程序员将从中受益最多

