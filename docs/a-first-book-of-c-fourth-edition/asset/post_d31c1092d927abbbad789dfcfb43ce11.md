
# A FIRST BOOK OF C++

FOURTH EDITION

Gary Bronson

This is an electronic version of the print textbook. Due to electronic rights restrictions, some third party content may be suppressed. Editorial review has deemed that any suppressed content does not materially affect the overall learning experience. The publisher reserves the right to remove content from this title at any time if subsequent rights restrictions require it. For valuable information on pricing, previous editions, changes to current editions, and alternate formats, please visit www.cengage.com/highered to search by ISBN#, author, title, or keyword for materials in your areas of interest.

![](img/202cface8244f523c2641baa2e00d7dd_3_0.png)

**A First Book of C++, Fourth Edition**  
Gary Bronson

Executive Editor: Marie Lee  
Acquisitions Editor: Brandi Shailer  
Senior Product Manager: Alyssa Pratt  
Development Editor: Lisa M. Lord  
Copyeditor: Michael Beckett  
Proofreader: Camille Kiolbasa  
Indexer: Michael Brackney  
Editorial Assistant: Jacqueline Lacaire  
Content Project Manager: Lisa Weidenfeld  
Associate Marketing Manager: Shanna Shelton  
Art Director: Faith Broshan  
Print Buyer: Julio Esperas  
Cover Photo: ©istockphoto.com/xmanphoto  
Compositor: GEX Publishing Services

Some of the product names and company names used in this book have been used for identification purposes only and may be trademarks or registered trademarks of their respective manufacturers and sellers.

Any fictional data related to persons or companies or URLs used throughout this book is intended for instructional purposes only. At the time this book was printed, any such data was fictional and not belonging to any real persons or companies.

Course Technology, a part of Cengage Learning, reserves the right to revise this publication and make changes from time to time in its content without notice.

The programs in this book are for instructional purposes only.

© 2012 Course Technology, Cengage Learning

ALL RIGHTS RESERVED. No part of this work covered by the copyright herein may be reproduced, transmitted, stored or used in any form or by any means graphic, electronic, or mechanical, including but not limited to photocopying, recording, scanning, digitizing, taping, Web distribution, information networks, or information storage and retrieval systems, except as permitted under Section 107 or 108 of the 1976 United States Copyright Act, without the prior written permission of the publisher.

> For product information and technology assistance, contact us at  
> **Cengage Learning Customer & Sales Support, 1-800-354-9706**  
> For permission to use material from this text or product, submit all requests online at **www.cengage.com/permissions**  
> Further permissions questions can be emailed to  
> **permissionrequest@cengage.com**

Library of Congress Control Number: 2010939813  
ISBN-13: 978-1-111-53100-3  
ISBN-10: 1-111-53100-5

**Course Technology**  
20 Channel Center Street  
Boston, MA 02210  
USA

They have been tested with care, but are not guaranteed for any particular intent beyond educational purposes. The author and the publisher do not offer any warranties or representations, nor do they accept any liabilities with respect to the programs.

Cengage Learning is a leading provider of customized learning solutions with office locations around the globe, including Singapore, the United Kingdom, Australia, Mexico, Brazil, and Japan. Locate your local office at: **international.cengage.com/region**

Cengage Learning products are represented in Canada by Nelson Education, Ltd.

To learn more about Course Technology, visit  
**www.cengage.com/coursetechnology**

Purchase any of our products at your local college store or at our preferred online store **www.cengagebrain.com**

# BRIEF TABLE OF CONTENTS

# Part One

# Fundamentals of C++ Programming

- Chapter 1: Getting Started
- Chapter 2: Data Types, Declarations, and Displays
- Chapter 3: Assignment and Interactive Input
- Chapter 4: Selection
- Chapter 5: Repetition
- Chapter 6: Modularity Using Functions
- Chapter 7: Arrays
- Chapter 8: Arrays and Pointers
- Chapter 9: I/O Streams and Data Files

# Part Two

# Object-Oriented Programming

- Chapter 10: Introduction to Classes
- Chapter 11: Adding Functionality to Your Classes

# Part One

# Fundamentals of C++ Programming

# Chapter 1

# Getting Started

- 1.1 Introduction to Programming
  - Algorithms and Procedures
  - Classes and Objects
  - Program Translation
- 1.2 Function and Class Names
  - The main() Function
- 1.3 The cout Object
- 1.4 Programming Style
  - Comments
- 1.5 Common Programming Errors
- 1.6 Chapter Summary
- 1.7 Chapter Supplement: Software Development
  - Phase I: Development and Design
  - Phase II: Documentation
  - Phase III: Maintenance
  - Backup

# Chapter 2

# Data Types, Declarations, and Displays

- 2.1 Data Types
  - Integer Data Types
  - Determining Storage Size
  - Floating-Point Types
  - Exponential Notation
- 2.2 Arithmetic Operations
  - Expression Types
  - Integer Division
  - Negation
  - Operator Precedence and Associativity
- 2.3 Variables and Declarations
  - Declaration Statements
  - Multiple Declarations
  - Memory Allocation
- 2.4 Common Programming Errors
- 2.5 Chapter Summary
- 2.6 Chapter Supplement: Bits, Bytes, and Binary Number Representations
  - Bits and Bytes
  - Binary, Hexadecimal, and Octal Numbers

# Chapter 3

# Assignment and Interactive Input

- 3.1 Assignment Operators
  - Coercion
  - Assignment Variations
  - Accumulating
  - Counting
- 3.2 Formatted Output
  - The setiosflags() Manipulator
  - Hexadecimal and Octal I/O
- 3.3 Mathematical Library Functions

# Chapter 4

# Selection

- 4.1 Relational Expressions
- 4.4 The switch Statement
- 4.5 Common Programming Errors
- 4.6 Chapter Summary
- 4.7 Chapter Supplement: A Closer Look at Testing

# Chapter 5

# Repetition

- 5.1 The while Statement
- 5.2 Interactive while Loops
  - Sentinels
  - break and continue Statements
  - The Null Statement
- 5.3 The for Statement
  - Interactive for Loops
  - Nested Loops
- 5.4 The do-while Statement
  - Validity Checks
- 5.5 Common Programming Errors
- 5.6 Chapter Summary

# Chapter 6

# Modularity Using Functions

- 6.1 Function and Parameter Declarations
  - Function Prototypes
  - Calling a Function
  - Defining a Function
  - Placement of Statements
  - Function Stubs
  - Functions with Empty Parameter Lists
  - Default Arguments
  - Reusing Function Names (Overloading)
  - Function Templates
- 6.2 Returning a Single Value
  - Inline Functions
  - Templates with a Return Value

# 1. 引言

随着人工智能技术的快速发展，大语言模型（Large Language Models, LLMs）在自然语言处理领域取得了显著的成就。这些模型通过在海量文本数据上进行预训练，能够捕捉语言的深层语义和结构信息，从而在多种下游任务中展现出强大的能力。

然而，尽管大语言模型在生成流畅文本方面表现出色，它们仍然面临着一系列挑战，包括但不限于：知识时效性、推理能力、以及事实准确性等问题。为了解决这些问题，研究者们提出了多种改进方法，如检索增强生成（Retrieval-Augmented Generation, RAG）和思维链（Chain-of-Thought, CoT）等。

# 2. 相关工作

近年来，研究者们从多个角度探索了提升大语言模型性能的方法。以下是一些具有代表性的工作：

- **检索增强生成（RAG）**：通过引入外部知识库，在生成过程中检索相关信息，以提高回答的准确性和时效性。
- **思维链（CoT）**：引导模型在推理过程中生成中间步骤，从而增强其复杂推理能力。
- **指令微调（Instruction Tuning）**：通过在多样化的指令数据集上进行微调，使模型更好地遵循人类指令。
- **模型压缩与量化**：通过剪枝、量化和蒸馏等技术，降低模型部署成本，同时保持性能。

# 3. 方法

本文提出了一种基于多任务学习框架的增强方法。该方法通过联合优化多个相关任务，使模型能够共享底层表示，从而提升泛化能力。具体而言，我们设计了以下三个主要模块：

1. **共享编码器**：用于提取输入文本的通用语义表示。
2. **任务特定解码器**：针对不同任务设计独立的解码器，以捕捉任务特有的特征。
3. **动态权重调节机制**：根据训练过程中各任务的收敛情况，动态调整损失权重，以避免任务间干扰。

实验结果表明，该方法在多个基准数据集上均取得了优于基线模型的性能。
