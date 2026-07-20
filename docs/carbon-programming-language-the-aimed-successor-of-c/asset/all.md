![](cover.jpeg)

### Copyright ©2022 DON RICHIE. All rights reserved.

No part of this publication may be reproduced, distributed, or transmitted in any form or by any means, including photocopying, recording, or other electronic or mechanical methods, without the prior written permission of the publisher, except in the case of brief quotations embodied in the critical reviews and certain other noncommercial uses permitted by the copyright law.

Table of Contents

[Copyright ©2022 DON RICHIE. All rights reserved.](#part0000.html__Toc109717866)

[Introduction](#part0001_split_000.html__Toc109717867)

[Launching of Carbon](#part0001_split_001.html__Toc109717868)

[Google’s Carbon programming language aims to replace C++](#part0001_split_002.html__Toc109717869)

[Fast and works with C++](#part0001_split_003.html__Toc109717870)

[Modern and evolving](#part0001_split_003.html__Toc109717871)

[Welcoming open-source community](#part0001_split_005.html__Toc109717872)

[Why build Carbon?](#part0001_split_006.html__Toc109717873)

[Language Goals](#part0001_split_008.html__Toc109717874)

[Project status](#part0001_split_007.html__Toc109717875)

[Generic](#part0001_split_008.html__Toc109717876)

[Memory safety](#part0001_split_009.html__Toc109717877)

[Getting started with Carbon](#part0001_split_011.html__Toc109717878)

[Can Google's New Programming Language 'Carbon' Replace C++ Better Than Rust?](#part0001_split_012.html__Toc109717879)

[A Question we all need the answer](#part0001_split_012.html__Toc109717880)

[Interoperability Philosophy and Goals](#part0001_split_013.html__Toc109717881)

[Background](#part0001_split_013.html__Toc109717882)

[Other interoperability layers](#part0001_split_013.html__Toc109717883)

[Philosophy](#part0001_split_014.html__Toc109717884)

[Language goal influences](#part0001_split_015.html__Toc109717885)

[Performance-critical software](#part0001_split_015.html__Toc109717886)

[Software and language evolution](#part0001_split_015.html__Toc109717887)

[Code that is easy to read, understand, and write](#part0001_split_015.html__Toc109717888)

[Practical safety guarantees and testing mechanisms](#part0001_split_015.html__Toc109717889)

[Fast and scalable development](#part0001_split_015.html__Toc109717890)

[Modern OS platforms, hardware architectures, and environments](#part0001_split_015.html__Toc109717891)

[Interoperability with and migration from existing C++ code](#part0001_split_015.html__Toc109717892)

[Goals](#part0001_split_016.html__Toc109717893)

[Support mixing Carbon and C++ toolchains](#part0001_split_016.html__Toc109717894)

[Compatibility with the C++ memory model](#part0001_split_016.html__Toc109717895)

[Minimize bridge code](#part0001_split_016.html__Toc109717896)

[Unsurprising mappings between C++ and Carbon types](#part0001_split_016.html__Toc109717897)

[Allow C++ bridge code in Carbon files](#part0001_split_016.html__Toc109717898)

[Carbon inheritance from C++ types](#part0001_split_016.html__Toc109717899)

[Support use of advanced C++ features](#part0001_split_016.html__Toc109717900)

[Support basic C interoperability](#part0001_split_016.html__Toc109717901)

[Non-goals](#part0001_split_017.html__Toc109717902)

[Full parity between a Carbon-only toolchain and mixing C++/Carbon toolchains](#part0001_split_017.html__Toc109717903)

[Never require bridge code](#part0001_split_017.html__Toc109717904)

[Convert all C++ types to Carbon types](#part0001_split_017.html__Toc109717905)

[Support for C++ exceptions without bridge code](#part0001_split_017.html__Toc109717906)

[Cross-language metaprogramming](#part0001_split_017.html__Toc109717907)

[Offer equivalent support for languages other than C++](#part0001_split_017.html__Toc109717908)

[Open questions to be resolved later](#part0001_split_018.html__Toc109717909)

[Carbon type inheritance from non-pure interface C++ types](#part0001_split_018.html__Toc109717910)

[CRTP support](#part0001_split_018.html__Toc109717911)

[Object lifetimes](#part0001_split_018.html__Toc109717912)

# Introduction

The newest programming language developed by Google, called Carbon, was revealed on July 20 as an experimental replacement for C++.

Google has developed a number programming languages over the years, some of which have gained significant notoriety and prominence. For instance, Golang (or just Go) was developed to facilitate the creation of servers and distributed systems and has subsequently been embraced by the general public. The Dart programming language, which was first meant to serve as a JavaScript substitute, didn't gain widespread acceptance until the release of Flutter.

At the Cpp North conference in Toronto on July 19, 2022, Googler Chandler Carruth presented the idea for a brand-new programming language named Carbon. To establish

# Launching of Carbon

Carbon is an experimental general-purpose programming language created by Google to be a "C++ successor language". It was first presented to the public by Chandler Carruth at the CppNorth conference in July of 2022\. The language intends to fix several perceived shortcomings of C++ but otherwise provide a similar feature set. The main goals of language are readability and "bi-directional interoperability" so there will not be a language barrier like Rust had. The language will be designed and developed on GitHub, as opposed to the ISO process C++ uses.

| Name | Carbon |
| Family | C |
| Developer | Google |
| First appeared | 19 July 2022; 6 days ago |
| Preview release | 0.1 / 19 July 2022; 6 days ago |
| Typing discipline | Static, nominative, partially inferred |
| Implementation language | C++ |
| OSFilename extensions | Cross-platform.carbon |
| Website | https://github.com/carbon-language/carbon-lang |
| Influenced | C++, Rust |

Carbon, the latest programming language to be built within Google, was unveiled in the month july of 20 as an experimental successor to C++.

Over the years, Google has created a few programming languages, some of which have become more popular and prominent than others. For example, Golang (or simply Go) was created for the purpose of improving the development of servers and distributed systems and has since been adopted by the public. Meanwhile, the Dart programming language, originally intended as something of an alternative to JavaScript, didn’t reach mainstream popularity until the release of Flutter.

On the 19th of july 2022, at the Cpp North convention in Toronto, Googler Chandler Carruth shared the vision for a new programming language called Carbon. To set the scene, Carruth showed how many of today’s most popular programming languages have successors that allow developers to be rapidly productive and also take advantage of modern language design.

Android developers well know that Kotlin serves as a successor to Java, just as iOS developers know Swift is the successor to Objective-C. TypeScript, from Microsoft, has thoroughly enhanced JavaScript, while remaining comfortable to use and able to be “transpiled” back to JavaScript. C++, which sees a significant amount of use within Google, is similarly a successor of sorts to the original C programming language.

While some may suggest that Rust, originally a Mozilla project that has since grown to have a significant public following, is a successor to C++, Carruth wonders if the analogy still follows. While Rust is undeniably a great language to start a new project in, it doesn’t have the same “bi-directional interoperability” of something like Java & Kotlin, making it difficult to steadily migrate.

To that end, while Carbon has many of the same goals as Rust, such as helping developers to create “performance-critical software,” Carbon is also intended to be fully interoperable with existing C++ code. Additionally, the goal is to make migrating from C++ to Carbon as easy as possible, if desired.

As for why a C++ developer may want to consider introducing Carbon to their codebase, Carruth shared quite a few highlights of the language on stage.

Beyond the features of the language itself, the Carbon team drew attention to the development process that will shape Carbon’s future. The project’s code is hosted publicly on GitHub and is open for pull requests, while Carbon’s culture is outlined to be accessible and inclusive for employees of companies and private individuals, alike.

That said, one aspect of the Carbon programming language that’s not particularly well outlined is Google’s involvement. While today’s presentation was shared by a Googler, and the current project leads for Carbon consist primarily — but not entirely — of Googlers, there’s otherwise no mention of Carbon being a Google project.

This is actually intentional, as while Carbon got its start within Google, the team understands and has shared online that for it to have any future success, Carbon needs to be “an independent and community driven project,” not solely driven by Google’s own uses. In the same comment, Carruth further emphasizes that Carbon is currently just an experiment, albeit one that some companies have already shown early interest in.

If you’re interested in getting started with Carbon, you can download the source code and experiment with it on your own device. Or, you can get a feel for the Carbon programming language directly in your browser thanks to integration with the free Compiler Explorer web app.

## Google’s Carbon programming language aims to replace C++

The so called Carbon language (C++ successor) which was released on Tuesday, 19 July 2022, which was said is an experimental replacement for C++.

Carruth said that although many may suggest that Rust is a successor to C++, it lacks the level of “bi-directional interoperability” that Carbon offers.

He said Carbon is intended to be fully interoperable with existing C++ code, adding that the goal is to make the transition from C++ to Carbon as easy as possible.

Highlights of Google’s new programming language include:

Introducer words and a simple grammar, Function input parameters are read-only values, Pointers provide indirect access and mutation,Use expressions to name types, The package is the root namespace, Import APIs through their package name, Explicit object parameter declares a method, Single inheritance — classes are final by default, Powerful, definition-checked generics, Types explicitly implement interfaces

Interestingly, Google noted that for the language to be successful, Carbon must be “an independent community driven project” and not solely for Google’s use.

Therefore, while most of Carbon’s current leads are Google developers, there is no explicit information classifying it as a Google project.

The source code for Carbon is available on GitHub and is open to pull requests.

https://github.com/carbon-language/carbon-lang#carbon-language--an-experimental-successor-to-c

## Modern and evolving

Solid language foundations that are easy to learn, especially if you have used C++

Easy, tool-based upgrades between Carbon versions

Safer fundamentals, and an incremental path towards a memory-safe subset

## Fast and works with C++

Performance matching C++ using LLVM, with low-level access to bits and addresses

Interoperate with your existing C++ code, from inheritance to templates

Fast and scalable builds that work with your existing C++ build systems

## Welcoming open-source community

Clear goals and priorities with robust governance

Community that works to be welcoming, inclusive, and friendly

Batteries-included approach: compiler, libraries, docs, tools, package manager, and more

# Why build Carbon?

C++ remains the dominant programming language for performance-critical software, with massive and growing codebases and investments. However, it is struggling to improve and meet developers' needs, as outlined above, in no small part due to accumulating decades of technical debt. Incrementally improving C++ is extremely difficult, both due to the technical debt itself and challenges with its evolution process. The best way to address these problems is to avoid inheriting the legacy of C or C++ directly, and instead start with solid language foundations like modern generics system, modular code organization, and consistent, simple syntax.

Existing modern languages already provide an excellent developer experience: Go, Swift, Kotlin, Rust, and many more. Developers that can use one of these existing languages should. Unfortunately, the designs of these languages present significant barriers to adoption and migration from C++. These barriers range from changes in the idiomatic design of software to performance overhead.

Carbon is fundamentally a successor language approach, rather than an attempt to incrementally evolve C++. It is designed around interoperability with C++ as well as large-scale adoption and migration for existing C++ codebases and developers. A successor language for C++ requires:

Performance matching C++, an essential property for our developers.

Seamless, bidirectional interoperability with C++, such that a library anywhere in an existing C++ stack can adopt Carbon without porting the rest.

A gentle learning curve with reasonable familiarity for C++ developers.

Comparable expressivity and support for existing software's design and architecture.

Scalable migration, with some level of source-to-source translation for idiomatic C++ code.

With this approach, we can build on top of C++'s existing ecosystem, and bring along existing investments, codebases, and developer populations. There are a few languages that have followed this model for other ecosystems, and Carbon aims to fill an analogous role for C++:

JavaScript → TypeScript

Java → Kotlin

C++ → Carbon

# Project status

Carbon is currently an experimental project. We want to better understand whether we can build a language that meets our successor language criteria, and whether the resulting language can gather a critical mass of interest within the larger C++ industry and community.

Currently, we have fleshed out several core aspects of both Carbon the project and the language:

The strategy of the Carbon Language and project.

An open-source project structure, governance model, and evolution process.

Critical and foundational aspects of the language design informed by our experience with C++ and the most difficult challenges we anticipate. This includes designs for:

*   Generics
*   Class types
*   Inheritance
*   Operator overloading
*   Lexical and syntactic structure
*   Code organization and modular structure

A prototype interpreter demo that can both run isolated examples and gives a detailed analysis of the specific semantic model and abstract machine of Carbon. We call this the Carbon Explorer.

We are currently focused on getting more broad feedback and participation from the C++ community, completing the 0.1 language design, and completing the Carbon Explorer implementation of this design. Beyond that, we plan to prioritize C++ interoperability and a realistic toolchain that implements the 0.1 language and can be used to evaluate Carbon in more detail.

Carbon and C++

If you're already a C++ developer, Carbon should have a gentle learning curve. It is built out of a consistent set of language constructs that should feel familiar and be easy to read and understand.

C++ code like this:

![C:\Users\USER\Desktop\c++.PNG](images/00001.jpeg)

corresponds to this Carbon code:![C:\Users\USER\Desktop\carm.PNG](images/00002.jpeg)

You can call Carbon from C++ without overhead and the other way around. This means you migrate a single C++ library to Carbon within an application, or write new Carbon on top of your existing C++ investment.

Beyond interoperability between Carbon and C++, we're also planning to support migration tools that will mechanically translate idiomatic C++ code into Carbon code to help you switch an existing C++ codebase to Carbon.

# Language Goals

We are designing Carbon to support:

Performance-critical software

Software and language evolution

Code that is easy to read, understand, and write

Practical safety and testing mechanisms

Fast and scalable development

Modern OS platforms, hardware architectures, and environments

Interoperability with and migration from existing C++ code

While many languages share subsets of these goals, what distinguishes Carbon is their combination.

We also have explicit non-goals for Carbon, notably including:

A stable ABI for the entire language and library

Perfect backwards or forwards compatibility

Our detailed goals document fleshes out these ideas and provides a deeper view into our goals for the Carbon project and language.

# Memory safety

Safety, and especially memory safety, remains a key challenge for C++ and something a successor language needs to address. Our initial priority and focus is on immediately addressing important, low-hanging fruit in the safety space:

*   Tracking uninitialized states better, increased enforcement of initialization, and systematically providing hardening against initialization bugs when desired.
*   Designing fundamental APIs and idioms to support dynamic bounds checks in debug and hardened builds.
*   Having a default debug build mode that is both cheaper and more comprehensive than existing C++ build modes even when combined with Address Sanitizer.

Once we can migrate code into Carbon, we will have a simplified language with room in the design space to add any necessary annotations or features, and infrastructure like generics to support safer design patterns. Longer term, we will build on this to introduce a safe Carbon subset. This will be a large and complex undertaking, and won't be in the 0.1 design. Meanwhile, we are closely watching and learning from efforts to add memory safe semantics onto C++ such as Rust-inspired lifetime annotations.

# Generic

Carbon provides a modern generics system with checked definitions, while still supporting opt-in templates for seamless C++ interop. Checked generics provide several advantages compared to C++ templates:

Generic definitions are fully type-checked, removing the need to instantiate to check for errors and giving greater confidence in code.

*   Avoids the compile-time cost of re-checking the definition for every instantiation.
*   When using a definition-checked generic, usage error messages are clearer, directly showing which requirements are not met

Enables automatic, opt-in type erasure and dynamic dispatch without a separate implementation. This can reduce the binary size and enables constructs like heterogeneous containers.

Strong, checked interfaces mean fewer accidental dependencies on implementation details and a clearer contract for consumers.

Without sacrificing these advantages, Carbon generics support specialization, ensuring it can fully address performance-critical use cases of C++ templates. For more details about Carbon's generics, see their design.

In addition to easy and powerful interop with C++, Carbon templates can be constrained and incrementally migrated to checked generics at a fine granularity and with a smooth evolutionary path.

# Getting started with Carbon

You can get started playing with Carbon by checking out the codebase and using the Carbon explorer:

# Install bazelisk using Homebrew.

$ brew install bazelisk

# Install Clang/LLVM using Homebrew.

# Many Clang/LLVM releases aren't built with options we rely on.

$ brew install llvm

$ export PATH="$(brew --prefix llvm)/bin:${PATH}" # Download Carbon's code.

$ git clone [https://github.com/carbon-language/carbon-lang](https://github.com/carbon-language/carbon-lang)

$ cd carbon-lang

# Build and run the explorer.

$ bazel run //explorer -- ./explorer/testdata/print/format_only.carbon

# Can Google's New Programming Language 'Carbon' Replace C++ Better Than Rust?

## A Question we all need the answer

It's difficult for large projects to convert existing C++ codebases into Rust, argue Google engineers — so they've created a new "experimental" open source programming language called Carbon.

Carruth delved into more detail about some of the reasons why Carbon should be considered a powerful successor to the C++ language, including simpler grammar and smoother API imports.

Google's engineers are already building tools to translate C++ into this new language. "While Carbon began as a Google internal project, the development team ultimately wants to reduce contributions from Google, or any other single company, to less than 50% by the end of the year," reports The New Stack, adding that Google ultimately wants to hand off the project to an independent software foundation where development will be led by volunteers:Long the language of choice for building performance-critical applications, C++ is plagued with a number of issues that hamper modern developers, Carruth explained on a GitHub page. It has accumulated decades of technical debt, bringing with it many of the outdated practices that were part of the language's predecessor, C. The keepers of C++ prioritize backward compatibility, in order to continue to support widely-used projects such as Linux and its package management ecosystem, Carruth charged.

The language's evolution is also stymied by a bureaucratic committee process, oriented around standardization rather than design. Which can make it difficult to add new features. C++ has largely a sequestered development process, in which a select committee makes the important decisions, in a waterfall process that can take years. "The committee structure is designed to ensure representation of nations and companies, rather than building an inclusive and welcoming team and community of experts and people actively contributing to the language," Carruth wrote. "Access to the committee and standard is restricted and expensive, attendance is necessary to have a voice, and decisions are made by live votes of those present."

Carruth wants to build Carbon by a more open community-led environment. The project will be maintained on GitHub, and discussed on Discord.... The design team wants to release a core working version ("0.1") by the end of the year.

Carbon will boast modern features like generics and memory safety (including dynamic bounds checks), the article points out. And "The development team will also set out to create a built-in package manager, something that C++ sorely lacks."

The Aimed successor

Over the years, Google has created a few programming languages, some of which have become more popular and prominent than others. For example, Golang (or simply Go) was created for the purpose of improving the development of servers and distributed systems and has since been adopted by the public. Meanwhile, the Dart programming language, originally intended as something of an alternative to JavaScript, didn’t reach mainstream popularity until the release of Flutter.

At the Cpp North convention in Toronto, as shared by Conor Hoekstra who was in attendance and documented the slides, Googler Chandler Carruth shared the vision for a new programming language called Carbon. To set the scene, Carruth showed how many of today’s most popular programming languages have successors that allow developers to be rapidly productive and also take advantage of modern language design.

Android developers well know that Kotlin serves as a successor to Java, just as iOS developers know Swift is the successor to Objective-C. TypeScript, from Microsoft, has thoroughly enhanced JavaScript, while remaining comfortable to use and able to be “transpiled” back to JavaScript. C++, which sees a significant amount of use within Google, is similarly a successor of sorts to the original C programming language.

While some may suggest that Rust, originally a Mozilla project that has since grown to have a significant public following, is a successor to C++, Carruth wonders if the analogy still follows. While Rust is undeniably a great language to start a new project in, it doesn’t have the same “bi-directional interoperability” of something like Java & Kotlin, making it difficult to steadily migrate.

If Rust works for you today, you should use it. But moving a C++ ecosystem to Rust is hard.

To that end, while Carbon has many of the same goals as Rust, such as helping developers to create “performance-critical software,” Carbon is also intended to be fully interoperable with existing C++ code. Additionally, the goal is to make migrating from C++ to Carbon as easy as possible, if desired.

As for why a C++ developer may want to consider introducing Carbon to their codebase, Carruth shared quite a few highlights of the language on stage.

Introducer keywords and a simple grammarFunction input parameters are readonly valuesPointers provide indirect access & mutationUse expressions to name typesThe package is the root namespaceImport APIs through their package nameExplicit object parameter declares a methodSingle inheritance; classes are final by defaultPowerful, definition-checked genericsTypes explicitly implement interfaces

Beyond the features of the language itself, the Carbon team drew attention to the development process that will shape Carbon’s future. The project’s code is hosted publicly on GitHub and is open for pull requests, while Carbon’s culture is outlined to be accessible and inclusive for employees of companies and private individuals, alike.

That said, one aspect of the Carbon programming language that’s not particularly well outlined is Google’s involvement. While today’s presentation was shared by a Googler, and the current project leads for Carbon consist primarily — but not entirely — of Googlers, there’s otherwise no mention of Carbon being a Google project.

This is actually intentional, as while Carbon got its start within Google, the team understands and has shared online that for it to have any future success, Carbon needs to be “an independent and community driven project,” not solely driven by Google’s own uses. In the same comment, Carruth further emphasizes that Carbon is currently just an experiment, albeit one that some companies have already shown early interest in.

If you’re interested in getting started with Carbon, you can download the source code and experiment with it on your own device. Or, you can get a feel for the Carbon programming language directly in your browser thanks to integration with the free Compiler Explorer web app

Google’s New Programming Language is Called Carbon

It will also have a practically safe testing mechanism which would be improved for advanced types of code. Performance critical goal would also be the main goal for the Carbon programming language.

Lastly, I am a C++ programmer for a very long time now and I am super excited to see how the successor of C++ would fulfill its drawbacks. The event also mentioned it would have an underlying mechanism of C++ and Golang. Currently, it is only in its experimental stage and soon it will be launched in its beta stage.

You could also learn more about carbon and get involved in it as it is open source on its official GitHub page.

# Interoperability Philosophy and Goals

## Background

Interoperability with and migration from C++ are a language goal. However, performance and evolution are higher priorities. This interaction of priorities is important to understanding Carbon's interoperability goals and trade-offs.

### Other interoperability layers

Other language interoperability layers that may offer useful examples are:

*   Java/Kotlin should be a comparable interoperability story. The languages are different, but share an underlying runtime. This may be closest to the model we desire for Carbon.

*   JavaScript/TypeScript is similar to C/C++, where one language is essentially a subset of the other, allowing high interoperability. This is an interesting reference point, but we are looking at a different approach with a clearer boundary.

*   C++/Java is an example of requiring specialized code for the bridge layer, making interoperability more burden on developers. The burden of the approach may be considered to correspond to the difference in language memory models and other language design choices. Regardless, the result can be considered higher maintenance for developers than we want for Carbon.

*   C++/Go is similar to C++/Java. However, Go notably allows C++ bridge code to exist in the .go files, which can ease maintenance of the bridge layer, and is desirable for Carbon.

## Philosophy

The C++ interoperability layer of Carbon allows a subset of C++ APIs to be accessed from Carbon code, and similarly a subset of Carbon APIs to be accessed from C++ code. This requires expressing one language as a subset of the other. Bridge code may be needed to map some APIs into the relevant subset, but the constraints on expressivity should be loose enough to keep the amount of such bridge code sustainable.

The design for interoperability between Carbon and C++ hinges on:

*   The ability to interoperate with a wide variety of code, such as classes/structs and templates, not just free functions.
*   A willingness to expose the idioms of C++ into Carbon code, and the other way around, when necessary to maximize performance of the interoperability layer.
*   The use of wrappers and generic programming, including templates, to minimize or eliminate runtime overhead.

These things come together when looking at how custom data structures in C++ are exposed into Carbon, and the other way around. In both languages, it is reasonable and even common to have customized low-level data structures, such as associative containers. For example, there are numerous data structures for mapping from a key to a value that might be best for a particular use case, including hash tables, linked hash tables, sorted vectors, and btrees. Even for a given data structure, there may be slow but meaningful evolution in implementations strategies.

The result is that it will often be reasonable to directly expose a C++ data structure to Carbon without converting it to a "native" or "idiomatic" Carbon data structure. Although interfaces may differ, a trivial adapter wrapper should be sufficient. Many Carbon data structures should also be able to support multiple implementations with C++ data structures being one such implementation, allowing for idiomatic use of C++ hidden behind Carbon.

The reverse is also true. C++ code will often not care, or can be refactored to not care, what specific data structure is used. Carbon data structures can be exposed as yet another implementation in C++, and wrapped to match C++ idioms and even templates.

For example, a C++ class template like std::vector<T> should be usable without wrapper code or runtime overhead, and passing a Carbon type as T. The resulting type should be equally usable from either C++ or Carbon code. It should also be easy to wrap std::vector<T> with a Carbon interface for transparent use in idiomatic Carbon code.

## Language goal influences

### Performance-critical software

Interoperability with C++ will be frequently used in Carbon, whether it's C++ developers trying out Carbon, incrementally migrating a large C++ codebase, or continuing to use a C++ library long-term. In all cases, it must be possible to write interoperable code with zero overhead; copies must not be required.

### Code that is easy to read, understand, and write

Interoperability-related Carbon code will likely be more difficult to read than other, more idiomatic Carbon code. This is okay: aiming to make Carbon code readable doesn't mean that it needs to all be trivial to read. At the same time, the extra costs that interoperability exerts on Carbon developers should be minimized.

### Software and language evolution

Interoperability will require the addition of features to Carbon which exist primarily to support interoperability use cases. However, these features must not unduly impinge the overall evolution of Carbon. In particular, only a subset of Carbon features will support interoperability with C++. To do otherwise would restrict Carbon's feature set.

### Interoperability with and migration from existing C++ code

Carbon's language goal for interoperability will focus on C++17 compatibility. The language design must be mindful of the prioritization; trade-offs harming other goals may still be made so long as they offer greater benefits for interoperability and Carbon as a whole.

Although the below interoperability-specific goals will focus on interoperability, it's also important to consider how migration would be affected. If interoperability requires complex work, particularly to avoid performance impacts, it could impair the ability to incrementally migrate C++ codebases to Carbon.

.

### Practical safety guarantees and testing mechanisms

Safety is important to maintain around interoperability code, and mitigations should be provided where possible. However, safety guarantees will be focused on native Carbon code. C++ code will not benefit from the same set of safety mechanisms that Carbon offers, so Carbon code calling into C++ will accept higher safety risks.

### Modern OS platforms, hardware architectures, and environments

Interoperability will apply to the intersection of environments supported by both Carbon and C++. Pragmatically, Carbon will likely be the limiting factor here.

### Fast and scalable development

The interoperability layer will likely have tooling limitations similar to C++. For example, Carbon aims to compile quickly. However, C++ interoperability hinges on compiling C++ code, which is relatively slow. Carbon libraries that use interoperability will see bottlenecks from C++ compile time. Improving C++ is outside the scope of Carbon.

## Goals

### Compatibility with the C++ memory model

It must be straightforward for any Carbon interoperability code to be compatible with the C++ memory model. This does not mean that Carbon must exclusively use the C++ memory model, only that it must be supported.

### Allow C++ bridge code in Carbon files

Carbon files should support inline bridge code written in C++. Where bridge code is necessary, this will allow for maintenance of it directly alongside the code that uses it.

### Support mixing Carbon and C++ toolchains

The Carbon toolchain will support compiling C++ code. It will contain a customized C++ compiler that enables some more advanced interoperability features, such as calling Carbon templates from C++.

Mixing toolchains will also be supported in both directions:

*   C++ libraries compiled by a non-Carbon toolchain will be usable from Carbon, so long as they are ABI-compatible with Carbon's C++ toolchain.

*   The Carbon toolchain will support, as an option, generating a C++ header and object file from a Carbon library, with an ABI that's suitable for use with non-Carbon toolchains.

Mixing toolchains restricts functionality to what's feasible with the C++ ABI. For example, developers should expect that Carbon templates will be callable from C++ when using the Carbon toolchain, and will not be available when mixing toolchains because it would require a substantially different and more complex interoperability implementation. This degraded interoperability should still be sufficient for most developers, albeit with the potential of more bridge code.

Any C++ interoperability code that works when mixing toolchains must work when using the native Carbon toolchain. The mixed toolchain support must not have semantic divergence. The converse is not true, and the native Carbon toolchain may have additional language support and optimizations.

### Minimize bridge code

The majority of simple C++ functions and types should be usable from Carbon without any custom bridge code and without any runtime overhead. That is, Carbon code should be able to call most C++ code without any code changes to add support for interoperability, even if that code was built with a non-Carbon toolchain. This includes instantiating Carbon templates or generics using C++ types.

In the other direction, Carbon may need some minimal markup to expose functions and types to C++. This should help avoid requiring Carbon to generate C++-compatible endpoints unconditionally, which could have compile and linking overheads that may in many cases be unnecessary. Also, it should help produce errors that indicate when a function or type may require additional changes to make compatible with C++.

Carbon's priority developers should be able to easily reuse the mature ecosystem of C++ libraries provided by third-parties. A third-party library's language choice should not be a barrier to Carbon adoption.

Even for first-party libraries, migration of C++ codebases to Carbon will often be incremental due to human costs of executing and verifying source migrations. Minimizing the amount of bridge code required should be expected to simplify such migrations.

### Support use of advanced C++ features

There should be support for most idiomatic usage of advanced C++ features. A few examples are templates, overload sets, attributes and ADL.

Although these features can be considered "advanced", their use is widespread throughout C++ code, including STL. Support for such features is key to supporting migration from C++ features.

### Support basic C interoperability

C interoperability support must be sufficient for Carbon code to call popular APIs that are written in C. The ability of C to call Carbon will be more restricted, limited to where it echoes C++ interoperability support. Basic C interoperability will include functions, primitive types, and structs that only contain member variables.

Features where interoperability will rely on more advanced C++-specific features, such as templates, inheritance, and class functions, need not be supported for C. These would require a C-specific interoperability model that will not be included.

### Unsurprising mappings between C++ and Carbon types

Carbon will provide unsurprising mappings for common types.

Primitive types will have mappings with zero overhead conversions. They are frequently used, making it important that interoperability code be able to use them seamlessly.

The storage and representation will need to be equivalent in both languages. For example, if a C++ __int64 maps to Carbon's Int64, the memory layout of both types must be identical.

Semantics need to be similar, but edge-case behaviors don't need to be identical, allowing Carbon flexibility to evolve. For example, where C++ would have modulo wrapping on integers, Carbon could instead have trapping behavior on the default-mapped primitive types.

Carbon may have versions of these types with no C++ mapping, such as Int256.

Non-owning vocabulary types, such as pointers and references, will have transparent, automatic translation between C++ and Carbon non-owning vocabulary types with zero overhead.

Other vocabulary types will typically have reasonable, but potentially non-zero overhead, conversions available to map into Carbon vocabulary types. Code using these may choose whether to pay the overhead to convert. They may also use the C++ type directly from Carbon code, and the other way around.

Incomplete types must have a mapping with similar semantics, similar to primitive types.

### Carbon inheritance from C++ types

Carbon will support inheritance from C++ types for interoperability, although the syntax constructs may look different from C++ inheritance. This is considered necessary to address cases where a C++ library API expects users to inherit from a given C++ type.

This might be restricted to pure interface types; see the open question.

## Non-goals

### Never require bridge code

Corner cases of C++ will not receive equal support to common cases: the complexity of supporting any given construct must be balanced by the real world need for that support. For example:

*   Interoperability will target C++17\. Any interoperability support for future versions of C++, including features such as C++20 modules, will be based on a cost-benefit analysis. Exhaustive support should not be assumed.

*   Support will be focused on idiomatic code, interfaces, and patterns used in widespread open source libraries or by other key constituencies. C++ code will have edge cases where the benefits of limiting Carbon's maintenance costs by avoiding complex interoperability outweighs the value of avoiding bridge code.

*   Support for low-level C ABIs may be focused on modern 64-bit ABIs, including Linux, POSIX, and a small subset of Windows' calling conventions.

### Convert all C++ types to Carbon types

Non-zero overhead conversions should only be supported, never required, in order to offer reliable, unsurprising performance behaviors. This does not mean that conversions will always be supported, as support is a cost-benefit decision for specific type mappings. For example, consider conversions between std::vector<T> and an equivalent, idiomatic Carbon type:

*   Making conversions zero-overhead would require the Carbon type to mirror the memory layout and implementation semantics of std::vector<T>. However, doing so would constrain the evolution of the Carbon type to match C++. Although some constraints are accepted for most primitive types, it would pose a major burden on Carbon's evolution to constrain Carbon's types to match C++ vocabulary type implementations.

*   These conversions may not always be present, but std::vector<T> is a frequently used type. As a result, it can be expected that there will be functions supporting a copy-based conversion to the idiomatic Carbon type.

*   An interface which can hide the difference between whether std::vector<T> or the equivalent, idiomatic Carbon type is in use may also be offered for common types.

*   It will still be normal to handle C++ types in Carbon code without conversions. Developers should be given the choice of when to convert.

### Cross-language metaprogramming

Carbon's metaprogramming design will be more restrictive than C++'s preprocessor macros. Although interoperability should handle simple cases, such as #define STDIN_FILENO 0, complex metaprogramming libraries may require a deep ability to understand code rewrites. It should be reasonable to have these instead rewritten to use Carbon's metaprogramming model.

### Support for C++ exceptions without bridge code

Carbon may not provide seamless interoperability support for C++ exceptions. For example, translating C++ exceptions to or from Carbon errors might require annotations or bridge code, and those translations may have some performance overhead or lose information. Furthermore, if Carbon code calls a C++ function without suitable annotations or bridging, and that function exits with an exception, the program might terminate.

### Full parity between a Carbon-only toolchain and mixing C++/Carbon toolchains

Making mixed C++/Carbon toolchain support equivalent to Carbon-only toolchain support affects all interoperability features. Mixed toolchains will have degraded support because full parity would be too expensive.

The feature of calling Carbon templates from C++ code is key when analyzing this option. Template instantiation during compilation is pervasive in C++.

With a Carbon toolchain compiling both Carbon and C++ code, the C++ compiler can be modified to handle Carbon templates differently. Carbon templates can be handled by exposing the Carbon compiler's AST to the C++ compiler directly, as a compiler extension. While this approach is still complex and may not always work, it should offer substantial value and ability to migrate C++ code to Carbon without requiring parallel maintenance of implementations in C++.

With a mixed toolchain, the C++ compiler cannot be modified to handle Carbon templates differently. The only way to support template instantiation would be by having Carbon templates converted into equivalent C++ templates in C++ headers; in other words, template support would require source-to-source translation. Supporting Carbon to C++ code translations would be a complex and high cost feature to achieve full parity for mixed toolchains. Requiring bridge code for mixed toolchains is the likely solution to avoid this cost.

Note that this issue differs when considering interoperability for Carbon code instantiating C++ templates. The C++ templates must be in C++ headers for re-use, which in turn must compile with the Carbon toolchain to re-use the built C++ code, regardless of whether a separate C++ toolchain is in use. This may also be considered a constraint on mixed toolchain interoperability, but it's simpler to address and less likely to burden developers.

To summarize, developers should expect that while most features will work equivalently for mixed toolchains, there will never be full parity.

### Offer equivalent support for languages other than C++

Long-term, it should be anticipated that Carbon will add interoperability with non-C++ languages. However, interoperability discussions will be focused on C++ in order to support the language goal. Although we should work to consider extensibility when building interoperability facilities, C++ should be expected to have more robust support.

Many languages do offer interoperability layers with C. Carbon's C interoperability will likely offer a degree of multi-language interoperability using C as an intermediary.

## Open questions to be resolved later

### CRTP support

Although CRTP is a common technique in C++, interoperability support may require substantial work. Libraries based on use of CRTP may require bridge code or a rewrite for Carbon interoperability.

More analysis should be done on the cost-benefit of supporting CRTP before making a support decision.

### Object lifetimes

Carbon may have a different object lifetime design than C++. For example, Carbon may choose different rules for determining the lifetime of temporaries. This could affect idiomatic use of C++ APIs, turning code that would be safe in C++ into unsafe Carbon code, requiring developers to learn new coding patterns.

More analysis should be done on object lifetimes and potential Carbon designs for it before deciding how to treat object lifetimes in the scope of interoperability.

### Carbon type inheritance from non-pure interface C++ types

Some C++ APIs will expect that consumers use classes that inherit from a type provided by the API. It's desirable to have Carbon support, in some way, inheritance from API types in order to use these APIs.

It may be sufficient to require the parent type be a pure interface, and that APIs with either use bridge code or switch implementations. That will be determined later.