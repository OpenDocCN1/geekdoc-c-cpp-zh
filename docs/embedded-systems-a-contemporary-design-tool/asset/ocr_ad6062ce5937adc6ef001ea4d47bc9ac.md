tools should be rather straightforward. For those readers not fully versed in Verilog or C, we provide a good introduction to and overview of the fundamentals of both tools.

# ORGANIZING THE BOOK

It is often all too easy to hack together a one-off embedded application that works. Trying to replicate a million or more copies of such a design (with tight time constraints) very quickly runs into the real-world gremlins that are waiting for us. A solid, secure, robust, reliable design must always be based on the underlying theory and a disciplined design and development approach. Such methods are growing increasingly important as we continue to push the design and fundamental physical principles envelop.

This book takes a developer’s perspective to teaching embedded systems concepts. It examines, in detail, each of the important theoretical and practical aspects that one must consider when designing today’s applications. These include the formal hardware and software development process (stressing safety, security, and reliability); the digital and software architecture of the system; the physical world interface cycle; external analog and digital signals; the debug and test throughout the development cycle; and finally improving the system’s performance.

# THE CHAPTERS

# Introduction and Background

The Foreword gives an introductory overview, some of the vocabulary that is part of the embedded world, a bit of background and history, and a few contemporary examples.

# Hardware and Software Infrastructure

With a preliminary background set, the next several chapters cover the essential aspects of the hardware and software necessary for the design and development of contemporary embedded systems. The Verilog hardware design language, UML, structured design models, and HW-SW co-design are introduced as tools in support of the development process.

Chapter 1 provides the first formal look at embedded systems and introduces some basic concepts, approaches, and vocabulary. The chapter begins with the hardware and computing core, which is usually manifest as a microprocessor, microcomputer, or microcontroller, and follows with an introduction to and discussion of the classic von Neumann and Harvard architectures.

Next, at the opposite end of the system hierarchy, methods by which the bits, bytes, and volts can be interpreted as the various and essential kinds of information (numbers, characters, addresses, and instructions) found inside of an embedded system are studied. Building on the instructions, the instruction set architecture (ISA), and register transfer (RTL) levels of the computer are introduced and studied.

Chapters 2 and 3 address a portion of the hardware side of embedded system design and lay the preliminary groundwork for more detailed studies of signal integrity in later chapters. As voltage levels continue to decrease, switching speeds to continue to increase, and the fundamental physics of analog signals joins our designs, corruption to embedded systems signaling becomes a growing problem. These chapters provide an initial foundation for understanding the practical aspects of working with digital circuits and systems in today’s challenging embedded world.