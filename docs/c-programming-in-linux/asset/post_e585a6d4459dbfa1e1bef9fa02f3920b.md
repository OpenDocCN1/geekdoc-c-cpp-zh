
## C Programming in Linux

David Haskins

![](img/a0cbda189e54d8cb1121c7e151992506_0_0.png)

David Haskins

## C Programming in Linux

C Programming in Linux  
© 2009 David Haskins & Ventus Publishing ApS  
ISBN 978-87-7681-472-4

## Contents

|  |  |  |
|---|---|---:|
|  | **About the author, David Haskins** | **7** |
|  | **Introduction** | **8** |
|  | **Setting up your System** | **11** |
| **1.** | **Chapter One: Hello World** | **13** |
| 1.1 | Hello Program 1 | 13 |
| 1.2 | Hello Program 2 | 14 |
| 1.3 | Hello Program 3 | 17 |
| 1.4 | Hello Program 4 | 19 |
| 1.5 | Hello World conclusion | 22 |
| **2.** | **Data and Memory** | **23** |
| 2.1 | Simple data types? | 23 |
| 2.2 | What is a string? | 27 |
| 2.3 | What can a string “mean” | 28 |
| 2.4 | Parsing a string | 31 |
| 2.5 | Data and Memory – conclusion | 34 |

![](img/a0cbda189e54d8cb1121c7e151992506_3_0.png)

### Fast-track your career

Please click the advert

### Masters in Management

![](img/a0cbda189e54d8cb1121c7e151992506_3_1.png)

London Business School  
Regent's Park  
London NW1 4SA  
United Kingdom  
Tel +44 (0)20 7000 7573  
Email mim@london.edu  
www.london.edu/mim/

### Stand out from the crowd

Designed for graduates with less than one year of full-time postgraduate work experience, London Business School’s Masters in Management will expand your thinking and provide you with the foundations for a successful career in business.

The programme is developed in consultation with recruiters to provide you with the key skills that top employers demand. Through 11 months of full-time study, you will gain the business knowledge and capabilities to increase your career choices and stand out from the crowd.

**Applications are now open for entry in September 2011.**

**For more information visit www.london.edu/mim/**  
**email mim@london.edu or call +44 (0)20 7000 7573**

|  |  |  |
|---|---|---:|
| **3.** | **Functions, pointers and structures** | **35** |
| 3.1 | Functions | 35 |
| 3.2 | Library Functions | 38 |
| 3.3 | A short library function reference | 39 |
| 3.4 | Data Structures | 41 |
| 3.5 | Functions, pointers and structures – conclusion | 44 |
| **4.** | **Logic, loops and flow control** | **46** |
| 4.1 | Syntax of C Flow of control | 46 |
| 4.2 | Controlling what happens and in which order | 47 |
| 4.3 | Logic, loops and flow conclusion | 57 |
| **5.** | **Database handling with MySQL** | **58** |
| 5.1 | On not reinventing the wheel | 58 |
| 5.2 | MySQL C API | 58 |
| **6.** | **Graphics with GD library** | **63** |
| 6.1 | Generating binary content | 63 |
| 6.2 | Using TrueType Fonts | 66 |
| 6.3 | GD function reference | 68 |

![](img/a0cbda189e54d8cb1121c7e151992506_4_0.png)

### You’re full of *energy and ideas.* And that’s just what we are looking for.

Looking for a career where your ideas could really make a difference? UBS’s Graduate Programme and internships are a chance for you to experience for yourself what it’s like to be part of a global team that rewards your input and believes in succeeding together.

Wherever you are in your academic career, make your future a part of ours by visiting www.ubs.com/graduates.

**www.ubs.com/graduates**

![](img/a0cbda189e54d8cb1121c7e151992506_4_1.png)

Please click the advert

© UBS 2010. All rights reserved.

|  |  |  |
|---|---|---:|
| 7. | Apache C modules | 73 |
| 7.1 | Safer C web applications | 73 |
| 7.2 | Adding some functionality | 76 |
| 7.3 | Apache Modules Conclusion | 77 |
| 8. | The Ghost project | 78 |
| 8.1 | A PHP web site generator project | 78 |
|  | Conclusion | 84 |

Please click the advert

![](img/a0cbda189e54d8cb1121c7e151992506_5_0.png)

## About the author, David Haskins

I was born in 1950 in Chelsea, London, but grew up in New Zealand returning to England in 1966. I have worked in the computer industry since 1975 after a couple of years as a professional drummer.

My first experience was five years as a mainframe hardware engineer for Sperry Univac (now Unisys) followed by 14 years as an analyst programmer with British Telecom in London.

While engaged in a complex task of converting large quantities of geographical data (map coordinate references) I discovered the joys of C – its speed and efficiency. That was in 1985 and I have been a fan of C ever since.

Since 1994 I have been a senior lecturer at the Faculty of Computing, Information Systems and Mathematics at Kingston University, London. This is a mostly technical university that evolved from a former polytechnic college with a long tradition of aeronautical engineering.

I am engaged mainly in teaching many computer languages and internet systems design to a large and multicultural student body.

Most of my academic research and commercial consultancy has been involved with spatial systems design and the large data volumes and necessary processing efficiency concerns has led me to concentrate on C and C++. My teaching web site is at www.ubiubi.org which shows some of this material.

A keen Open Systems enthusiast, I have exclusively centred all my teaching on the Linux platform since 2002 and Kingston University is well advanced in delivering dual boot facilities for all its student labs.

![](img/a0cbda189e54d8cb1121c7e151992506_6_0.png)

I am a keen swimmer and in 2009 completed the annual Lorne *Pier-to-Pub* race in Victoria, Australia which is the largest open-sea swimming race in the world where 4,500 people of all ages swim each January as the shark-spotting planes fly overhead.

When not teaching I am a keen vegetable gardener and amateur musician, playing in jazz groups and in Scottish bagpipe bands. I play the drums, the great highland bagpipe, the clarinet, the guitar and the piano.

## Introduction

### Why learn the C language?

Because the C language is like Latin - it is finite and has not changed for years. C is tight and spare, and in the current economic climate we will need a host of young people who know C to keep existing critical systems running.

C is built right into the core of Linux and Unix. The design idea behind Unix was to write an operating system in C so all you needed to port it to a new architecture was a C compiler. Linux is essentially the success story of a series of earlier attempts to make a PC version of Unix.

A knowledge of C is now and has been for years a pre-requisite for serious software professionals and with the recent popularity and maturity of Open Systems this is even more true. The terseness and perceived difficulty of C saw it being ousted from university teaching during the late 1990s in favour of Java but there is a growing feeling amongst some teaching communities that Java really is not such a good place to start beginners.

Students paradoxically arrive at colleges knowing less about computing than they did ten years ago as programming is seen as too difficult for schools to teach. Meanwhile the body of knowledge expected of a competent IT professional inexorably doubles every few years.

Java is commonly taught as a first language but can cause student confusion as it is in constant flux, is very abstract and powerful, and has become too big with too many different ways to do the same thing. It also is a bit “safe” and insulates students from scary experiences, like driving with air-bags and listening to headphones so you take less care. The core activity of writing procedural code within methods seems impenetrable to those who start from classes and objects.

So where do we start? A sensible place is “at the beginning” and C is as close as most of us will ever need to go unless we are becoming hardware designers. Even for these students to start at C and go further down into the machine is a good idea.

C is like having a very sharp knife which can be dangerous, but if you were learning to be a chef you would need one and probably cut yourself discovering what it can do. Similarly C expects you to know what you are doing, and if you don't it will not warn before it crashes.

A knowledge of C will give you deep knowledge of what is going on beneath the surface of higher-level languages like Java. The syntax of C pretty-well guarantees you will easily understand other languages that came afterwards like C++, Java, Javascript, and C#.

C gives you access to the heart of the machine and all its resources at a fine-grained bit-level.
