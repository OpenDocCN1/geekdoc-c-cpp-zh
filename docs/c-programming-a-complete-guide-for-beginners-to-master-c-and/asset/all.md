C++ programming

A complete guide for beginners to master c++ and build robust programs

Lena neill

© copyright 2024 all rights reserved.

The content contained within this book may not be reproduced, duplicated or transmitted without direct written permission from the author or the publisher.

Under no circumstances will any blame or legal responsibility be held against the publisher, or author, for any damages, reparation, or monetary loss due to the information contained within this book, either directly or indirectly.

Legal notice:

This book is copyright protected. It is only for personal use. You cannot amend, distribute, sell, use, quote or paraphrase any part, or the content within this book, without the consent of the author or publisher.

Disclaimer notice:

Please note the information contained within this document is for educational and entertainment purposes only. All effort has been executed to present accurate, up to date, reliable, complete information. No warranties of any kind are declared or implied. Readers acknowledge that the author is not engaging in the rendering of legal, financial, medical or professional advice. The content within this book has been derived from various sources. Please consult a licensed professional before attempting any techniques outlined in this book.

By reading this document, the reader agrees that under no circumstances is the author responsible for any losses, direct or indirect, that are incurred as a result of the use of information contained within this document, including, but not limited to, errors, omissions, or inaccuracies.

Table of contents

[Introduction](#index_split_003.html_id_Toc157765041)

[Chapter one: getting started with c++ programming](#index_split_004.html_id_Toc157765042)

[Chapter two: basic concepts in object oriented programming](#index_split_012.html_id_Toc157765043)

[Chapter three: working with classes and objects](#index_split_017.html_id_Toc157765044)

[Chapter four: extending classes via inheritance](#index_split_019.html_id_Toc157765045)

[Chapter five: polymorphism](#index_split_022.html_id_Toc157765046)

[Chapter six: constructors and destructors](#index_split_023.html_id_Toc157765047)

[Chapter seven: templates](#index_split_024.html_id_Toc157765048)

[Chapter eight: c++ input and output streams](#index_split_025.html_id_Toc157765049)

[Chapter nine: exception handling](#index_split_027.html_id_Toc157765050)

[Final words](#index_split_028.html_id_Toc157765051)

[References](#index_split_029.html_id_Toc157765052)

## Introduction

This o,bject o,riented pro,gramming co,urse in c++ language presents learners with the co,ncepts and techniques necessary to, effectively design, develo,p and implement a ro,bust pro,gram mo,del. as a learner, yo,u will be able to, grasp practical kno,wledge o,n ho,w to, apply the fundamental co,ncepts o,f o,bject o,riented analysis and design and so,lve vario,us pro,blems in yo,ur day to, day activities.

Yo,u will learn ho,w to, apply the co,ncept o,f data abstractio,n, encapsulatio,n, inheritance and po,lymo,rphism when creating o,bjects. yo,u will be in a po,sitio,n to, create classes that define an o,bject and its behavio,ur, create o,bjects fro,m a class definitio,n and also, be able to, establish co,mmunicatio,n between the o,bjects. yo,u will also, learn ho,w to, apply the o,bject o,riented co,ncepts in perfo,rming vario,us tasks and the benefits o,f do,ing do,.

This bo,o,k will help yo,u to, understand functio,n definitio,n and declaratio,n, ho,w to, pass arguments to, the functio,n and ho,w to, call bo,th inline functio,ns and member functio,ns. class and o,bjects are an impo,rtant feature in c++ pro,gramming and kno,wing ho,w to, create class definitio,ns and declaring o,bjects as instance o,f a class will make yo,ur pro,gram develo,pment pro,cess easier.

we will teach yo,u to, understand the co,ncept o,f inheritance and po,lymo,rphism. yo,u will be able to, understand the impo,rtance o,f co,de reusability and ho,w it makes yo,ur wo,rk mo,re efficient. in the related chapter, yo,u will learn vario,us ways that inheritance is achieved and ho,w to, declare private, public and pro,tected members in a class. thro,ugh the inheritance feature, yo,u will be able to, implement the co,ncept o,f po,lymo,rphism.

Co,nstructo,rs and destructo,rs is also, ano,ther impo,rtant co,ncept in the c++ develo,pment framewo,rk. this tuto,rial will enable yo,u to, understand ho,w to, declare co,nstructo,rs and destructo,rs. yo,u will also, be able to, wo,rk with functio,n uplo,ads and managing dynamic data using the co,ncept o,f co,nstructo,rs and destructo,rs.

All pro,grams created are sto,red in the disk drive and kno,wing ho,w to, manage file o,peratio,ns and handling the input/o,utput system will make yo,ur wo,rk mo,re effective. in this co,urse, yo,u will learn ho,w to, use vario,us c++ streams, class streams, and ho,w to, use manipulato,rs in managing input and o,utput data. yo,u will also, be in a po,sitio,n to, o,pen an existing file, write into, the file, and read fro,m the file.

Yo,u will also, be able to, detect file erro,rs using vario,us erro,r handling functio,ns. at the end o,f the co,urse, yo,u will learn abo,ut exceptio,n handling mechanisms and ho,w to, use thro,w and catch erro,rs techniques.

## Chapter o,ne: getting started with c++ pro,gramming

C++ is o,ne o,f the mo,st co,mpetitive general-purpo,se pro,gramming languages o,n the market. it has features o,f imperative pro,gramming paradigm and can o,perate in any platfo,rm.

o,bject o,riented fundamentals

o,bject o,riented pro,gramming (o,o,p) in c++ language revo,lves aro,und data created using o,bjects. o,bjects are real-time entities that represent data and metho,ds o,r functio,ns used in the manipulatio,n o,f the data.

C++ language uses o,bjects to, execute pro,grams. as the pro,gram is executed, o,bjects co,mmunicate with each o,ther thro,ugh passing messages. each o,bject do,esn’t have to, kno,w the implementatio,n details o,f ano,ther o,bject.

C++ utilizes features o,f o,o,p to, execute a pro,gram. the main key features include:

*   o,bjects.
*   Classes.
*   Data abstractio,n and encapsulatio,n.
*   Inheritance.
*   Po,lymo,rphism.

A true o,o,p language uses o,bjects to, represent data in any pro,gram. altho,ugh c++ suppo,rts all the o,o,p features, it is said to, be a partial o,o,p language fo,r the fo,llo,wing three reaso,ns:

1.  Uses glo,bal variables

C++ suppo,rts the co,ncept o,f glo,bal variables. yo,u can declare glo,bal variables o,utside o,f a class so, that o,ther entities o,f the pro,gram can access the variables. tho,ugh declaring glo,bal variables vio,lates encapsulatio,n co,ncept, c++ can suppo,rt encapsulatio,n thro,ugh the use o,f classes and o,bjects.

1.  o,ptio,nal creatio,n o,f classes o,r o,bjects

The main functio,n is a mandato,ry feature in any c++ pro,gram and it sho,uld be created o,utside o,f the class. therefo,re, it’s no,t necessary to, create classes o,r o,bjects as lo,ng as yo,u have the main ().

o,mitting classes o,r o,bjects vio,lates o,o,p language co,ncept in that data is represented in the fo,rm o,f o,bjects.

1.  Suppo,rts friend functio,n

C++ allo,ws yo,u to, create a friend class o,r functio,n that enables yo,u to, access the pro,tected members o,r private members o,f a certain class. this vio,lates the features o,f o,o,p language.

Even tho,ugh c++ suppo,rts the abo,ve features, it is referred as a partial o,bject o,riented pro,gramming language because it so,metimes wo,rks against the features.

Pro,gramming paradigms

A pro,gramming paradigm is a pro,gramming mo,del that uses distinct co,ncepts to, shape ho,w pro,grammers design, o,rganize and write a pro,gram. pro,gramming paradigms are aimed at so,lving certain pro,blems using vario,us pro,gramming languages.

There are different types o,f paradigms and each fulfils a specific functio,n based o,n the pro,gramming language. these paradigms are divided into, two,: declarative pro,gramming paradigm; and imperative pro,gramming paradigm.

![00214.jpeg](images/00214.jpeg)

Declarative pro,gramming paradigm

A declarative pro,gramming paradigm is divided into, three co,mpo,nents: lo,gic; functio,nal; and database o,r data driven. declarative pro,gramming expresses pro,gram lo,gic witho,ut fo,cusing o,n the co,ntro,l flo,w o,f the pro,gram. the pro,grams develo,ped fo,cus o,n what to, do, rather than ho,w to, do, it. these paradigms emphasize what actio,n needs to, be do,ne and declares the results to, be achieved. fo,r example, expressing co,mputatio,ns include:

Lo,gic pro,gramming paradigm

This pro,gramming paradigm fo,cuses o,n so,lving lo,gical co,mputatio,n pro,blems like a pro,gram to, so,lve a puzzle o,r series o,f data. lo,gic pro,gramming paradigm relies o,n the kno,wledge base which is already kno,wn and passes it to, a machine learning to,o,l to, pro,duce results. the lo,gic paradigm relies o,n artificial intelligence and machine learning to, so,lve pro,blems.

Functio,nal pro,gramming paradigm

This is a language independent pro,gram and has its ro,o,ts in mathematical functio,ns. the main principle in this paradigm is executio,n o,f mathematical functio,ns. data is co,upled into, functio,ns which hides the implementatio,n details. the functio,ns can be replaced with values and this do,esn’t change the meaning o,f the pro,gram.

Database o,r data driven pro,gramming paradigm

This pro,gramming paradigm fo,cuses o,n the use o,f data and mo,vement. all the pro,gram statements are defined using data. it is event driven and pro,vides data o,peratio,n mechanisms like file creatio,n, writing into, files, updating files and databases, pro,ducing queries and repo,rting. there are a variety o,f pro,grams develo,ped fo,r database applicatio,ns, like the structured query language (sql), amo,ng o,thers.

Imperative pro,gramming paradigm

Imperative pro,gramming paradigm uses a step by step pro,cess to, achieve a specific go,al. it emphasizes ho,w to, do, a particular task like ho,w to, execute several statements and sto,re the results. the paradigm wo,rks thro,ugh change o,f pro,gram state by assigning statements.

Advantages:

*   Simple to, implement
*   Uses lo,o,ps, variables, functio,ns, and structures to, execute pro,gram statements

Disadvantages:

*   Co,mplex pro,grams increase the co,mplexity o,f this paradigm
*   Parallel pro,gramming is no,t po,ssible in this paradigm
*   Less efficient and pro,ductive

The imperative paradigm has three bro,ad catego,ries: pro,cedural; parallel pro,cessing; and o,o,p.

Pro,cedural paradigm

Just as the name suggests, this paradigm fo,cuses o,n step by step pro,cesses fo,r perfo,rming specific functio,ns. it allo,ws co,de reusability and it is very easy to, implement. it is used to, so,lve simple pro,blems.

Parallel pro,cessing paradigm

In this type o,f paradigm, pro,gram instructio,ns are pro,cessed using multiple pro,cesso,rs. a parallel pro,cessing paradigm has several pro,cesso,rs aimed at running a pro,gram in the sho,rtest time po,ssible. so,me c++ library functio,ns suppo,rt this technique.

o,bject o,riented pro,gramming (o,o,p)

This uses a co,llectio,n o,f classes and o,bjects to, write a pro,gram. an o,bject is the smallest entity where all co,mputatio,ns takes place. the paradigm fo,cuses o,n the use o,f data rather than pro,cedures to, so,lve real wo,rld pro,blems. o,o,p slips the pro,blem into, a number o,f entities represented by o,bjects and then builds data and functio,ns based o,n these o,bjects. it can so,lve co,mplex pro,blems abo,ut real life scenario,s. c++ is a go,o,d example o,f o,o,p that attempts to, eliminate so,me o,f the disadvantages o,f co,nventio,nal pro,gramming languages.

![00215.jpeg](images/00215.jpeg)

Each o,f the o,bjects wo,rk independently and they’re encapsulated within mo,dules. o,bjects co,mmunicate with each o,ther thro,ugh ‘message passing technique’. these o,bjects are o,rganized into, several classes in which they can inherit metho,ds and variables needed to, perfo,rm certain functio,ns such as:

*   Advantages.
*   Impro,ved data security.
*   Co,de reusability.
*   Ability to, use inheritance.
*   Data abstractio,n.

o,bject o,riented develo,pment framewo,rk

o,bject o,riented paradigm

An o,bject o,riented paradigm relies heavily o,n system theo,ry as part o,f its co,nceptual backgro,und. a system represents a co,llectio,n o,f entities that interact to,gether to, achieve a co,mmo,n o,bjective. these entities may include an individual, an o,bject o,r an equipment, and abstract entities such as data files and functio,ns.

o,bject o,riented paradigm fo,cuses o,n o,bjects that encapsulate data and pro,cedures. these o,bjects play a majo,r ro,le in the so,ftware develo,pment pro,cess.

o,bject o,riented analysis

o,bject o,riented analysis (o,aa) invo,lves techniques used in determining the so,ftware requirements o,f an o,bject, its behavio,r and interactio,ns. o,bject o,riented design co,nverts the so,ftware o,o,a requirements into, specificatio,ns fo,r the o,bjects and generates a class hierarchy fo,r o,bject creatio,n. o,bject o,riented pro,gramming (o,o,p) implements the pro,gram using o,bjects using o,o,p language like c++.

Develo,ping pro,gram specificatio,ns ensures there is a clear and well o,rganized statement o,f the pro,ject pro,blem.

o,bject-o,riented no,tatio,n and graphs

The graphical no,tatio,n is very impo,rtant in pro,ject design and develo,pment pro,cesses. these no,tatio,ns represent o,bjects, classes, subclasses and their inter-relatio,nships. the co,mmo,n graphical no,tatio,ns include:

●  instances o,f o,bjects.

●  message co,mmunicatio,n between o,bjects within a class.

●  inheritance relatio,nships.

●  hierarchical chart.

●  client-server relatio,nship.

●  classificatio,n relatio,nship.

o,bject o,riented analysis pro,vides us with po,werful mechanisms to, identify o,bjects which are used as the building blo,cks in the develo,pment o,f the so,ftware. analysis invo,lves deco,mpo,sitio,n o,f the so,ftware pro,blem into, vario,us co,mpo,nent parts. it then establishes a lo,gical mo,del which evaluates the system functio,ns.

#### Steps in o,bject o,riented analysis:

1.  Identifying the pro,ject pro,blem.
2.  Creatio,n o,f a requirement specificatio,n do,cument fo,r the users and the so,ftware itself.
3.  Identifying the pro,ject o,bjects and their attributes.
4.  Identify what services each o,bject is to, perfo,rm.
5.  Establishing co,mmunicatio,n between the o,bjects. o,bjects sho,uld be able to, interco,nnect with each o,ther and exchange messages.

![00216.jpeg](images/00216.jpeg)

Pro,blem definitio,n

This is the first step in the system develo,pment life cycle. it invo,lves understanding the pro,blem the user is facing and writing a pro,blem statement. the pro,blem statement sho,uld be refined and redefined using co,mputer system engineering. a well-defined pro,blem statement enables the pro,grammer to, co,me up with a requirement specificatio,n do,cument fo,r bo,th the user and the so,ftware.

Requirement specificatio,n

After clear definitio,n o,f the pro,blem, yo,u need to, understand the o,bjectives o,f the pro,po,sed system and what it’s suppo,sed to, do,. this will help yo,u to, generate the system requirements and user requirements in the pro,po,sed system.

The requirement specificatio,n do,cument sho,uld state:

●  the o,utputs which are required.

●  the pro,cesses to, be used to, in o,rder to, pro,duce these o,utputs.

●  the inputs required.

●  the reso,urces required to, achieve desired results.

#### o,bject identificatio,n

This step invo,lves the identificatio,n o,f real wo,rld o,bjects and abstract o,bjects. these o,bjects can be fo,und in the applicatio,n and are analyzed by the use o,f data flo,w diagrams (dfd) and textual analysis (ta).

#### Data flo,w diagrams

A data flo,w diagram uses vario,us symbo,ls that represent data, and they are used to, indicate the flo,w o,f data fro,m o,ne po,int to, ano,ther. the dfd has input/o,utput symbo,ls, decisio,n symbo,l and the pro,cess symbo,l which acts as the data sto,re fo,r all o,bjects.

#### Textual analysis

This includes a detailed textual descriptio,n o,f the pro,blem with o,ne o,r two, paragraphs o,r several sentences based o,n the co,mplexity o,f the pro,blem.

1.  Identify o,bject services: o,nce o,bjects are identified, the next step is to, determine the set o,f services each o,bject is suppo,sed to, perfo,rm.
2.  Establish a co,nnectio,n between o,bjects: after determining what services each o,bject will o,ffer, a co,mmunicatio,n is established between o,bjects based o,n the services each o,bject o,ffers and receives. yo,u can use an entity relatio,nship diagram o,r info,rmatio,n flo,w diagram to, list info,rmatio,n being co,mmunicated by each o,bject.

o,bject o,riented design

The design pro,cess invo,lves mapping o,ut o,bjects and creating a co,nceptual mo,del o,f the system. this uses a bo,tto,m-up appro,ach to, build the system structure, o,r uses a to,p-do,wn appro,ach by designing the class member functio,n that pro,vides the services to, the system.

When designing o,bjects, it’s impo,rtant to, co,me up with class hierarchies, identify any abstract class and the simply messaging passing pro,cess between the o,bjects.

When mapping o,ut co,ntent, put into, co,nsideratio,n the reusability o,f classes if yo,u had previo,us designs, and the classificatio,n o,f the o,bjects into, subsystems.

#### Steps in o,bject o,riented design:

1.  Evaluate o,bjects created during the analysis phase.

Evaluating the o,bjects identified in the pro,blem space enables yo,u to, refine the o,bjects based o,n their attributes and their o,peratio,ns. it also, enables yo,u to, identify o,ther o,bjects that can help yo,u o,btain mo,re so,lutio,ns to, the pro,blem.

1.  Specify class dependencies.

Analysis o,f the relatio,nship between the classes is very impo,rtant, as it enables yo,u to, determine the appro,priate class to, represent the o,bjects and establish relatio,nships between the o,bjects. the majo,r relatio,nships necessary in the design stage include:

●  inheritance relatio,nship: this allo,ws a class to, inherit the pro,perties and behavio,rs o,f ano,ther class. in this case, an o,bject can inherit so,me members fro,m ano,ther class.

●  co,ntainment relatio,nship: in this type o,f relatio,nship, an o,bject o,f class a is used as a member o,f class b.

●  use relatio,nship: this type o,f relatio,nship pro,vides info,rmatio,n o,n the vario,us classes a particular class uses and ho,w it uses the classes. fo,r example, class a can use class b and c in the fo,llo,wing ways:

○  class a reads the members o,f class b.

○  class a calls the members in class c.

○  class a uses new o,perato,r to, create class b.

If yo,u’re planning to, o,verride so,me attributes o,r functio,ns, it is highly reco,mmended to, use an inheritance relatio,nship.

1.  o,rganize classes into, hierarchies.

After creating an inheritance relatio,nship between the o,bjects, yo,u have to, re-examine the relatio,nships and create class hierarchies. this allo,ws yo,u to, reuse data and functio,ns that have been established. identifying similar attributes and functio,n within a gro,up o,f related classes helps in o,rganizing the classes into, hierarchies. a new class can be fo,rmed fro,m the related classes, and it’s called the super class. the o,ther classes are subo,rdinate classes. if an o,bject is created by co,mbining all the class attributes, then it’s called an abstract class.

1.  Design classes.

This step defines the metho,ds to, be used o,n the created class to, make it mo,re useful. so,me o,f the functio,ns used in a class include:

●  management functio,ns: ho,w to, create an o,bject and ho,w to, destro,y an o,bject.

●  implementatio,n functio,n: the o,peratio,ns perfo,rmed o,n the class data types.

●  access functio,ns: this is a functio,n o,f accessing the internal variables o,f a class.

●  utility functio,n: this invo,lves ho,w to, handle erro,rs and access co,ntro,l.

1.  Design class member functio,ns.

Member functio,ns define so,me o,f the tasks to, be perfo,rmed o,n an o,bject. these functio,ns wo,rk like o,ther no,rmal functio,ns. yo,u can use a to,p-do,wn functio,n deco,mpo,sitio,n appro,ach to, design member functio,ns.

1.  Determine the driver pro,gram.

The main() functio,n is the standard c++ driver pro,gram. all functio,n calls are made in the main() functio,n. the driver pro,gram is respo,nsible fo,r:

●  receiving users’ input.

●  creating o,bjects fro,m a class definitio,n.

●  displaying pro,gram o,utput based o,n the users’ requirements.

●  making calls to, the member functio,ns.

Pro,gram implementatio,n

This pro,cess invo,lves co,ding and testing the develo,ped pro,gram. the pro,gram co,de is written using class member functio,ns and the driver pro,gram. o,nce yo,u finish co,ding the pro,gram, yo,u have to, test it fo,r erro,rs and to, determine whether it functio,ns as expected.

Pro,gram testing is an essential feature in the so,ftware develo,pment pro,cess. yo,u sho,uld co,me up with a detailed testing plan o,f what to, test and ho,w the testing will be carried o,ut. test all the class dependencies and interfaces fo,r any erro,rs. the ultimate go,al o,f pro,gram testing is to, ensure the pro,gram perfo,rms its functio,ns as intended.

C++ pro,gramming building blo,cks

Built-in data types in c++

When declaring variables, yo,u have to, define the data type fo,r each variable. the data type indicates what kind o,f data is sto,red in the variable. in c++ pro,gramming, the co,mpiler allo,cates memo,ry space fo,r each variable created based o,n the data type. different data types require different memo,ry sizes.

Data types

There are three c++ data types:

1.  Primitive data types
2.  Derived data types
3.  Abstract o,r user defined data types

#### Primitive data types/ built-in data types

A primitive data type is a predefined o,r built-in data type that is used directly to, declare a variable. the mo,st co,mmo,n built-in data types include:

**Data type**

Keywo,rd

**Range**

Character

Char

-127 to, 127 and fro,m 0 to, 255

Integer

Int

-2147483648 to, 2147483647

Flo,ating po,int

Flo,at

+-3.4e +/-38( 7 digits)

Bo,o,lean expressio,n

Bo,o,l

Sto,res value as either true o,r false

Do,uble flo,ating po,int

Do,uble

+/-1.7e +-308(15 digits)

Valueless

Vo,id

Indicates no, type

Wide character

Wchar_t

1 wide character

Character and integer data types can be mo,dified further using the fo,llo,wing c++ mo,difiers:

●  signed

●  unsigned

●  sho,rt

●  lo,ng

These mo,difiers indicate ho,w much memo,ry space is needed to, sto,re these variables.

Specifying the data type fo,r all variables created tells the co,mpiler ho,w much space to, allo,cate fo,r each variable. any variable definitio,n specifies the data type and the variable list.

Syntax

Datatype variable_list;

Example:

int a, b, c;

char y, n;

flo,at salary;

#### Derived data type

As the name suggests, this data type is derived fro,m the built-in data types. they include:

●  arrays.

●  po,inters.

●  functio,ns.

●  reference.

#### Abstract data types

This is a data type defined by the user, thus the name user-defined types. these data types include:

●  enumeratio,n.

●  structure.

●  unio,n.

●  class.

**Enumerated types**

Enumerated data types use ‘enum’ variable to, declare an o,ptio,nal data type and a list o,f identifiers that sho,w the values o,f the data type.

Enum enum_name {list o,f names}

Where,

The enum_name is the enumeratio,n data type name. yo,u can have o,ne o,r mo,re lists o,f names separated by co,mmas.

Fo,r example, we can define an enumeratio,n fo,r class rectangle and call it rectangle and pass variable l to, be assigned to, length.

Enum rectangle {length, width} l=length;

Variable sco,pe

A variable is declared either inside a functio,n (lo,cal variables) o,r o,utside a functio,n (glo,bal variables).

Lo,cal variables: defined variables within a blo,ck o,r inside a functio,n are kno,wn as lo,cal variables. o,nce declared, o,nly statements within the functio,ns can execute o,r access the variables.

Example:

#include <io,stream>

Using namespace std;

Int main ()

{

// declaring lo,cal variables:

int x, y;

int z;

// initializatio,n o,f variables

x = 20;

y = 15;

z = x - y;

co,ut << z;

return 0;

}

Glo,bal variables: glo,bal variables are declared o,utside the functio,n and can be called o,r accessed by any functio,n. the variables are usually declared at the to,p o,f the pro,gram after the namespace library thus making it accessible thro,ugho,ut the entire pro,gram.

Example:

#include <io,stream>

Using namespace std;

// declaring glo,bal variables

Int m;

Int main ()

{

// declaring lo,cal variables:

int x, y;

// initializatio,n o,f variables

x = 5;

y = 10;

m= x + y;

co,ut << m;

return 0;

}

C++ arrays

If yo,u have multiple variables to, sto,re values, yo,u can create an array that allo,ws yo,u to, declare a single variable instead o,f declaring individual variables fo,r each value. an array is a data structure that sto,res a co,llectio,n o,f variables o,f the same data type.

Arrays are accessed thro,ugh the use o,f an index. each array element is made o,f co,ntiguo,us memo,ry allo,catio,n with the lo,west memo,ry address allo,cated to, the first element o,f the array, and the highest memo,ry address allo,cated to, the last element.

When declaring an array, yo,u have to, specify the data type, array variable name, and the number o,f elements to, be sto,red in that array variable.

Syntax

Type arrayname [arraysize]

This type o,f an array is a single-dimensio,n array. type is the data type o,f the array element and arraysize must be an integer number that is greater than 0. fo,r example, to, declare an array with 3 elements, yo,u can write it as fo,llo,ws:

String cars [3];

**Initializing arrays**

Yo,u can initialize the arrays created by allo,cating values to, the array elements. these values are added inside braces { } and they sho,uldn’t be larger than the number o,f elements declared between the square brackets [ ].

Syntax

Type arrayname [size] = {values}

Example:

String cars [3] = {“bmw”, “rav4”, “vo,lvo,”};

If yo,u want to, create an array fo,r integer numbers, yo,u can write:

int num[5] = {5, 10, 25, 20, 35};

Declaring the array size tells the co,mpiler to, create a memo,ry allo,catio,n to, ho,ld 5 elements. if yo,u do,n’t specify the array size, a huge chunk o,f memo,ry is created to, ho,ld the initialized variables.

Arrays use index to, represent variables with 0 index representing the first element. yo,u can represent the abo,ve array as fo,llo,ws:

Index

0

1

2

3

4

Num

5

10

25

20

35

Accessing arrays

Yo,u can access array element by indexing the array name. this can be do,ne by placing the index number o,f the element yo,u want to, access within the square brackets after the array name.

Example:

Int num[5] = {5, 10, 25, 20, 35};

Co,ut<< num[1];

// o,utput 10

Using lo,o,ps in arrays

Yo,u can use fo,r lo,o,p to, execute array elements.

Example:

#include <io,stream>

#include <string>

Using namespace std;

Int main()

{

string cars[3] = {"bmw", "rav4", "vo,lvo,"};

fo,r(int a = 0; a < 4; a++)

{

Co,ut << cars[a] << "\n";

}

return 0;

}

// o,utput

Bmw

Rav4

Vo,lvo,

Multi-dimensio,nal arrays

Multidimensio,nal is an array o,f arrays which sto,res data in the fo,rm o,f tables with bo,th ro,ws and co,lumns (ro,ws*co,lumns), also, kno,wn as the matrix. it can be either a two,-dimensio,nal o,r three-dimensio,nal array.

Syntax

Type arrayname [size1] [size2] … [sizen];

Example:

Int m [5] [12];

Int n [2] [2] [3];

To, get the number o,f elements sto,red in a multidimensio,nal array, multiply the size o,f all array dimensio,n. in the array o,f int m [5] [12], yo,u can sto,re (5*12) = 60 elements.

#### Two,-dimensio,nal array

A two,-dimensio,nal array is the simplest array fo,rmat. this array fo,rmat uses ‘r’ number o,f ro,ws and ‘s’ number o,f co,lumns to, fo,rm a table. the table ranges fro,m 0 to, r-1 fo,r the ro,ws and the fro,m 0 to, s-1 fo,r the co,lumn number range.

Datatype arrayname [r] [s];

Two,-dimensio,n elements in an array are represented by r[x] [y], where ‘x’ is the ro,w number while ‘y’ is the co,lumn number.

The table belo,w sho,ws a two,-dimensio,nal array with three ro,ws and five co,lumns.

![00217.jpeg](images/00217.jpeg)

example o,f two,-dimensio,nal array:

int x [2] [3];

Yo,u can initialize the array by passing values to, the array element as fo,llo,ws:

int x [2] [3] = {0, 2, 3, 5, 8, 12}

This array can also, be initialized as fo,llo,ws:

Int x [2] [3] =

{

{0, 2, 3},

{5, 8, 12}

};

Example:

#include <io,stream>

Using namespace std;

Int main()

{

int testingarray[3][3] =

{

{2, 3, 4},

{4, 6, 8},

{6, 4, 6}

};

Fo,r(int a = 0; a < 3; ++a)

{

fo,r(int b = 0; b < 3; ++b)

{

co,ut<< testingarray[a][b]<<" ";

}

co,ut<<"\n";

}

Return 0;

}

// o,utput

2 3 4

4 6 8

6 4 6

Po,inters

Po,inters are very essential in the implementatio,n o,f c++ pro,grams. they help in the dynamic allo,catio,n o,f memo,ry space, thus making it easy fo,r the pro,grams to, execute efficiently.

When yo,u declare a variable, a memo,ry lo,catio,n is created to, sto,re the values. each o,f the allo,cated memo,ry has a defined address which makes it easy to, access the variable. using po,inters simplifies pro,gram executio,n by ho,lding the memo,ry address o,f the sto,red variable.

A po,inter variable po,ints to, the data type o,f the variable and it is created using the asterisk (*) o,perato,r. therefo,re, befo,re using po,inters, yo,u have to, declare them.

Syntax

Type *variable-name;

Where,

Type is valid c++ data type and variable-name is the po,inter variable name.

Example 1: let’s create a po,inter named ‘ptr’ that po,ints to, an integer variable.

Int *ptr;

When assigning memo,ry address to, the po,inter variable, an ampersand (&) o,perato,r is used.

Int *ptr = &variable-name.

Example 2: create a pro,gram that defines a po,inter variable and assign memo,ry address to, the po,inter variable. add a co,de to, allo,w the co,mpiler access to, the value o,f the po,inter variable in the allo,cated address.

#include <io,stream>

Using namespace std;

Int main ()

{

int num = 12;

int *ptr;

// assign memo,ry address to, po,inter variable

ptr = &num;

co,ut << " the value o,f the num variable is: ";

co,ut << num << endl;

co,ut << "the memo,ry address sto,red in ptr variable is: ";

co,ut << ptr << endl;

co,ut << " the value o,f *ptr variable is: ";

co,ut << *ptr << endl;

return 0;

}

//o,utput

The value o,f num variable is: 12

The memo,ry address sto,red in ptr variable is: 0x28fef8

The value o,f *ptr variable is: 12

Dynamic free sto,re o,perato,rs

Free sto,re is unallo,cated memo,ry dynamically assigned to, a pro,gram during its executio,n time. each pro,gram has a large po,o,l o,f free memo,ry it can utilize during its running time.

All o,bjects allo,cated to, the free sto,re memo,ry require po,inters to, indirectly manipulate them since the free sto,re memo,ry is unnamed. yo,u also, have to, manually initialize the free sto,re memo,ry in o,rder to, use it.

Dynamic free sto,re memo,ry is manually allo,cated o,n the heap while no,n-static memo,ry with lo,cal variables is allo,cated at the stack.

The allo,catio,n o,f free sto,re memo,ry is via the new o,perato,r, and it is deactivated using delete o,perato,r. the new and delete o,perato,rs are system variables available fo,r manipulatio,n by the pro,grammers.

When using data structures like lists and trees, dynamic allo,catio,n o,f free sto,re memo,ry is essential. the new o,perato,r is used to, request dynamic allo,catio,n o,f free sto,re memo,ry.

Syntax

Po,inter= new data-type;

o,r

Po,inter= new data-type [number-o,f-elements]

Where,

Po,inter-variable specifies the po,inter o,f type data type and datatype is any built-in c++ data type.

Number-o,f-elements is an integer value used when a sequence o,f several elements o,r an array o,f elements is needed. o,therwise, if yo,u o,nly need to, allo,cate free memo,ry fo,r a single element, use po,inter= new type expressio,n.

Free sto,re o,bjects created using the new o,perato,r are independent within the sco,pe and are available until destro,yed by the delete o,perato,r.

o,o,p classes are dynamically allo,cated free sto,re memo,ry, and they’re accessed thro,ugh the use o,f po,inters and references.

Example:

// a po,inter initialized with null values

Flo,at *ptr = new flo,at;

// initialize memo,ry using the new o,perato,r

Int *ptr = new int(15);

// allo,catio,n o,f blo,ck memo,ry with an array o,f 5 integers

Int *ptr = new int[5]

// using delete o,perato,r fo,r single expressio,n

Delete ptr;

// delete o,perato,r fo,r an array o,f elements

Delete[ ] ptr;

C++ functio,ns

a functio,n o,r metho,d is a gro,up o,f statements that execute a particular task. c++ functio,ns are divided into, two,:

1.  Library functio,ns
2.  User-defined functio,ns

Library functio,ns

These are pre-defined o,r built-in c++ functio,ns that perfo,rm a number o,f tasks. fo,r example, main (). yo,u can use the library functio,ns by directly invo,king it o,rder to, execute an instructio,n.

Example:

![00218.jpeg](images/00218.jpeg)

// o,utput

Enter a number to, get the square ro,o,t: 60

Square ro,o,t o,f 60 = 7.74597

The sqrt() is a library functio,n used to, calculate the square ro,o,t o,f a number. while #include <cmath> is the header file.

Every c++ pro,gram has the main() functio,n. fo,r any pro,gram to, begin its executio,n, it has to, make a system call to, the main(). that is, the executio,n starts fro,m the main functio,n.

User-defined functio,ns

C++ pro,gram allo,w users to, define their o,wn functio,ns. a user can specify a functio,n and write a blo,ck o,f statements to, be executed o,nce the functio,n is called.

Functio,n definitio,n and passing arguments

Functio,n declaratio,n is very impo,rtant when defining functio,ns. it tells the co,mpiler abo,ut the functio,n name and ho,w to, call the functio,n.

Syntax

Type functio,n_name (arguments)

{

Functio,n bo,dy/statements;

}

Where,

Type is the data type returned by the functio,n. if the functio,n executes witho,ut any value to, be returned after an executio,n, use vo,id as the return type fo,r the functio,n.

Functio,n_name is the actual name o,f the functio,n executed.

Arguments o,r parameter is the value passed to, the functio,n. the parameters are o,ptio,nal since a functio,n can have a list o,f parameters passed to, it o,r no,t.

Statements o,r bo,dy o,f the functio,n is a blo,ck o,f statements that explain what the functio,n do,es.

Example:

//functio,n call

Flo,at sum (flo,at a, flo,at b)

{

flo,at sum;

sum= a+b;

return sum;

}

In the abo,ve example, two, parameters (flo,at a, and flo,at b) are passed to, functio,n when calling it.

Calling functio,n

When declaring a functio,n, yo,u have to, state what the functio,n will do, o,n the blo,ck o,f statements. to, use the declared functio,n, yo,u have to, make a call to, the functio,n. when the pro,gram makes a call to, the functio,n, the full co,ntro,l o,f the pro,gram is transferred to, that functio,n. as a result, the functio,n executes the defined task under its functio,n bo,dy until the end o,f the functio,n then returns the co,ntro,l back to, the main pro,gram.

When calling the functio,n, yo,u can pass the parameters needed by the functio,n to, execute.

Example:

![00219.jpeg](images/00219.jpeg)

// o,utput

Enter two, numbers: 10 6

Sum = 16

Functio,n pro,to,type

If yo,u want to, define yo,ur o,wn functio,n (user-defined functio,n), yo,u have to, do, this o,utside the main () o,therwise the co,mpiler will generate an erro,r. the co,mpiler do,esn’t reco,gnize user-defined functio,ns and their arguments passed thro,ugh the main functio,n.

To, so,lve this, yo,u can declare a functio,n pro,to,type o,utside the main(). functio,n pro,to,type is declared witho,ut the functio,n bo,dy to, enable the co,mpiler to, kno,w abo,ut the user-defined functio,n in the pro,gram. in the abo,ve example, functio,n pro,to,type is declared as:

Flo,at add (flo,at, flo,at);

Therefo,re, it is impo,rtant to, define a functio,n pro,to,type if user-defined functio,ns exist in the pro,gram and they sho,uld be defined befo,re the main () functio,n.

**Call by value and call by reference**

Yo,u can pass data to, functio,n using either a call by value o,r a call by reference. in a call by value, the o,riginal value o,f the functio,n argument is no,t mo,dified, while in call by reference, its o,riginal value is mo,dified.

**Call by value**

In call by value, the passed value is lo,cally sto,red in the stack memo,ry. if yo,u change the parameters, the changes o,nly apply to, the current functio,n o,nly. the value o,f the variable inside the main () functio,n will no,t change when yo,u call the functio,n.

Call by value is the mo,st used metho,d o,f calling functio,ns, and any changes made to, the functio,n parameters will no,t have any effect o,n the call to, that functio,n.

In call by value, o,nly a co,py o,f the value is passed to, the functio,n.

**Call by reference**

When yo,u pass parameters by reference, the o,riginal value o,f the variable changes. passing arguments by references mo,difies the o,riginal address o,f the variable. the o,riginal address o,f the variable is mo,dified with the new variables passed to, the functio,n.

When yo,u change the value o,f arguments in a functio,n, it changes the value o,f the variable bo,th inside and o,utside o,f the main () functio,n.

Inline functio,ns

When yo,u make a call to, a functio,n, the functio,n takes so,me time to, execute a blo,ck o,f statements and sto,re the functio,n return values in the predefined memo,ry allo,catio,n befo,re transferring the co,ntro,l back to, the pro,gram. the pro,gram co,ntro,l is switched between the functio,n call and functio,n executio,n.

So,metimes a functio,n call can take mo,re time than the time it takes to, execute a task. the switching time between the functio,n call and the functio,n executio,n time can create an o,verhead. to, so,lve this pro,blem, c++ pro,gramming implements the use o,f inline functio,n to, reduce the o,verhead time.

Inline functio,ns reduce calling time fo,r small functio,ns. whenever a call is made to, the functio,n, the co,mpiler expands the functio,n and replaces the functio,n with a co,rrespo,nding co,de that reduces o,verhead time o,n the functio,n call.

Syntax

Inline return-type functio,n-name (parameters)

{

Functio,n bo,dy

}

When yo,u insert an inline keywo,rd befo,re the functio,n, it sends a request to, the co,mpiler and its no,t a co,mmand. the co,mpiler can decide to, decline the request based o,n the fo,llo,wing co,nditio,ns:

●  the functio,n has static variables.

●  yo,u’re using recursive functio,n.

●  the functio,n uses lo,o,p co,ntro,l structures like fo,r, while, and do,-while.

●  yo,u use switch o,r go,-to, statements in the functio,n.

●  there is no, return statements and the functio,n return type is no,t vo,id.

Example:

#include <io,stream>

Using namespace std;

//declaring inline functio,n

Inline int area(int l, int w)

{

Return l*w;

}

Int main()

{

Co,ut << "the area o,f rectangle is: " << area(3, 5) << "\n";

Return 0;

}

Inline functio,ns can be used inside classes. o,nce yo,u define a functio,n inside a class it auto,matically beco,mes an inline functio,n and all the restrictio,n o,f inline functio,n also, apply to, functio,ns inside the class.

When defining inline functio,n in a class, yo,u have to, declare the functio,n inside the class then define it o,utside the class using the keywo,rd inline.

Class rectangle

{

Public:

Int area (int l, int w)

};

Inline int rectangle:: area(int l, int w)

{

return l*w;

}

**Data structures**

Data structure is the co,llectio,n o,f elements and variables within a single unit. all data elements o,f different data types need to, be pro,cessed and sto,red to,gether under o,ne name. fo,r example, a student’s info,rmatio,n file sho,uld have details abo,ut name, scho,o,l id, co,ntacts, co,urse, class, marks, and grading info,rmatio,n.

Structures wo,rk the same as arrays, and the o,nly difference is that structures represent a co,llectio,n o,f variables o,f different data types under a single name, while arrays represent a co,llectio,n o,f variables o,f the same data type.

To, declare structures, use the keywo,rd struct fo,llo,wed by the structure name which is also, called a “tag”. then define data members o,r variables inside the o,pen and clo,sing braces ({}). after the clo,sing braces, enter the o,bject name (structure-variables) altho,ugh this is o,ptio,nal.

Syntax

Struct structurename

{

type membername1;

Type membername2;

Type membername3;

.

.

} o,bjectname;

The struct keywo,rd tells the co,mpiler that a structure is being defined. the o,bject_name allo,ws a user to, directly declare an o,bject o,f structure type, that is, be able to, instantiate different o,bjects in a single o,bject.

Example 1:

Struct perso,n

{

Char fname[15], lname[15];

Int age, co,de;

Flo,at salary;

} samuel, antho,ny, paul;

The abo,ve example defines a structure tag called perso,n, and sto,res variables o,f different data types to,gether with o,bjects passed to, the structure.

Example 2: creating a structure with an array o,f 10 o,bjects

Struct pro,ducts

{

Char pro,dname [20];

Int weight;

Flo,at price;

} items [10];

Ho,w to, access structure memo,ries

o,nce yo,u define and declare structure variables, yo,u can wo,rk directly with their members. to, access structure members, use the do,t (.) o,perato,r which is also, kno,wn as the access o,perato,r.

The access o,perato,r is inserted between the o,bject_name and the member_name.

Mango,. price;

**Initializing structure elements**

Yo,u can initialize the elements o,f a structure by assigning values to, them. yo,u can initialize the elements by using separate assignment statements o,r using array no,tatio,n.

Fo,r example, if yo,u want to, assign value 50 to, the price o,f mango, fruit, this can be do,ne as fo,llo,ws:

Mango,.price = 50;

When using an array no,tatio,n, yo,u can initialize the elements as fo,llo,ws:

Type student = {10, 15.6, 50.0, ‘b’};

The array type initializatio,n o,nly wo,rks if the structure variable is already defined. the type in the abo,ve statement is the data type specifier o,f the structure student which is declared and initialized simultaneo,usly. all the values assigned to, the structure members sho,uld be enclo,sed with o,pen and clo,sing braces.

Example:

#include<io,stream.h>

#include<co,nio,.h>

#include<stdio,.h>

Struct student

{

int studno,;

char studname[30], co,urse [20], class [2];

flo,at marks[4];

char grade;

}student_var;

Vo,id main()

{

flo,at sum = 0;

flo,at average;

co,ut<<"enter student's number: ";

cin>>student_var.studno,;

co,ut<<"enter student's name: ";

cin>>student_var.studname;

co,ut<<"enter student’s co,urse: ";

cin>>student_var.co,urse;

co,ut<<"enter student's class: ";

cin>>student_var.class;

co,ut<<"enter student’s marks o,n 4 subjects:\n";

fo,r(int m=0; m<4; m++)

{

co,ut<<"subject "<<m+1<<": ";

cin>>student_var.marks[m];

sum = sum + student_var.marks[m];

}

average = sum / 4;

if(average<50)

{

student_var.grade = 'fail';

}

else if(average<65)

{

student_var.grade = 'pass';

}

else if(average<80)

{

student_var.grade = 'credit';

}

else

{

student_var.grade = 'distinctio,n';

}

co,ut<<"\nstudent result:\n";

co,ut<<"\nstudno,: "<<student_var.studno,<<"\t\t\t student name: "<<student_var.studname;

co,ut<<"\nco,urse: "<<student_var.co,urse<<"\t\t\t class: "<<student_var.class;

co,ut<<"\nto,tal marks: "<<sum<<"\tgrade: "<<student_var.grade;

return 0;

}

// o,utput

Enter student’s number: 05

Enter student's name: sebastian mo,nro,e

Enter student’s co,urse: eco,no,mics

Enter student’s class: b2

Enter student’s marks o,n 4 subjects:

Subject 1: 68

Subject 2: 74

Subject 3: 86

Subject 4: 94

Students result:

Studno,: 05 student name: sebastian mo,nro,e

Co,urse: eco,no,mics class: b2

To,tal marks: 322 grade: distinctio,n

**References in c++**

C++ reference is an alternative name assigned to, an existing variable. o,nce yo,u initialize a variable name with a reference, yo,u may use the variable name o,r the reference to, call a variable.

There are three types o,f references suppo,rted in c++ pro,gramming language. they include:

●  no,n-co,nstant references: these are simply called references and are declared to, no,n-co,nstant values.

●  co,nstant references: these co,nsist o,f co,nstant values

●  r-value references: these help to, avo,id repetitive co,pying and assist fo,rwarding functio,ns.

In no,n-co,nstant references, variables are declared as references using the ampersand (&) o,perato,r which is declared between the variable name and the reference type.

Int &ref = {value};

The ampersand o,perato,r in this case will mean ‘reference to,’ and no,t ‘address o,f’. these references wo,rk the same as the values their referencing. that is, it acts as an alias o,f the referenced o,bject.

Example 1:

int prd= {5};

int &x = {prd};

int &y = {x};

In the abo,ve example, ‘x’ is a reference to,  prd variable while ‘y’ is also, a reference to, ‘x’.

Example 2:

#include<io,stream>

Using namespace std;

Int main()

{

do,uble price = 100;

do,uble &ref = price;

// change the price to, 120

ref = 120;

co,ut << "price = " << price << endl ;

// no,w change the price to, 150

price = 150;

co,ut << "ref = " << ref << endl ;

return 0;

}

// o,utput

Price = 120

Ref = 150

Applicatio,n o,f references

1.  To, mo,dify the parameters o,f a functio,n: if yo,u want to, change the parameters passed to, a functio,n during functio,n call, yo,u can reference the variables. in the abo,ve example, referencing the variable, mo,dified the price value fro,m the o,riginal 100 to, 120.
2.  To, avo,id co,pying large structures: if yo,u have a functio,n that executes a large number o,f o,bjects, then passing parameters to, it witho,ut referencing them creates a co,py o,f o,bject-variables. this results in wastage o,f cpu time and memo,ry. to, avo,id this duplicatio,n o,f o,bjects, yo,u can use references.

Example:

Struct emplo,yee

{

string empnames, address;

int empno,;

}

Vo,id print (co,nst emplo,yee &em)

{

co,ut << em.empnames << “ “ << em.address << “ “ << em. empno,;

}

If we remo,ve the reference to, o,perato,r, it will create a new co,py o,f the emplo,yee o,bject. the co,nst keywo,rd prevents any accidental update to, the pro,gram.

1.  To, mo,dify o,bjects in fo,r each lo,o,p: yo,u can use references to, mo,dify all elements in fo,r lo,o,p o,r to, avo,id co,pying o,f o,bjects when wo,rking with large o,bjects.

**Chapter summary**

C++ is a general purpo,se pro,gramming language and o,ne o,f the mo,st co,mpetitive o,bject o,riented pro,grams in the market. the language utilizes features o,f o,bject o,riented pro,gramming to, design a pro,gram and manipulate data. the co,mmo,nly used features include: o,bjects, classes, data abstractio,n, encapsulatio,n, inheritance and po,lymo,rphism.

With the help o,f pro,gramming paradigms, pro,grammers can easily design, o,rganize and build a pro,gram that so,lves vario,us pro,blems. there are two, types o,f pro,gramming paradigm; a declarative pro,gramming paradigm and an imperative pro,gramming paradigm. c++ language is an imperative pro,gramming language since it relies o,n o,o,p co,ncepts to, execute functio,ns.

The majo,r key elements in this chapter included:

●  learning vario,us built-in data types and ho,w to, use them in writing a pro,gram.

●  ho,w to, use user-defined types to, execute co,mplex pro,grams.

●  ho,w to, declare variables in c++ and allo,cate memo,ry lo,catio,n fo,r the user variables.

●  ho,w to, declare arrays to, ho,ld data elements, initializing arrays, accessing array elements as well as kno,w ho,w to, wo,rk with bo,th two, dimensio,nal arrays and multidimensio,nal arrays.

●  using po,inters to, po,int to, a specific sto,rage lo,catio,n and allo,w yo,u to, determine the reference address o,f the variable.

●  learning ho,w to, use dynamic free sto,re o,perato,rs to, allo,cate memo,ry space fo,r yo,ur pro,grams.

●  ho,w to, use c++ functio,ns to, build pro,grams and implement co,de reusability features to, make co,mplex pro,grams mo,re effective.

●  learn functio,n definitio,ns, ho,w to, declare functio,ns, make functio,n calls, and ho,w to, use functio,n pro,to,types and inline functio,ns.

●  learning ho,w to, use references when dealing with large o,bjects to, enable yo,u reduce the o,verhead time in functio,n calls. references will help yo,u minimize cpu executio,n time and save o,n memo,ry space since it prevents duplicatio,n o,f o,bjects whenever a functio,n call is made.

●  ho,w to, use structures and references to, access o,bjects. data structures allo,w yo,u to, wo,rk with variables o,f different data types under a single unit.

●  creating variables with different return types and data elements under a single name to, avo,id co,de repetitio,n.

●  making calls to, structure functio,ns and pass arguments o,f different data types.

In the next chapter yo,u will learn basic co,ncepts o,f o,bject o,riented pro,gramming including the use o,f classes, o,bjects, data abstractio,n and encapsulatio,n, po,lymo,rphism and inheritance feature.

## Chapter two,: basic co,ncepts in o,bject o,riented pro,gramming

It is necessary to, understand the basic co,ncepts used in o,bject-o,riented pro,gramming. see figure belo,w.

![00220.jpeg](images/00220.jpeg)

**Class**

A class is an expanded co,ncept o,f data structure and a building blo,ck fo,r c++ pro,gramming language. it co,nsists o,f lo,gical metho,ds fo,r o,rganizing data and functio,ns in the structure. the ‘class’ keywo,rd deno,tes the data structure with functio,ns represented as members.

A class co,nsists o,f two, parts: class header and bo,dy. a class header defines the class name and the base class, whereas the class bo,dy defines the class members suppo,rted by each class. the class uses user-defined data type to, ho,ld its o,wn data members and member functio,ns. class members and functio,ns are accessed by creating an instance o,f the class.

Class members: they represent the data variables in that class and specify ho,w class o,bjects are represented.

Member functio,ns: describes the functio,n pro,to,type used in manipulating these data variables. it specifies class o,peratio,ns which is also, referred to, as the instance o,f the class.

Bo,th member functio,ns and data members define the pro,perties and behavio,r o,f an o,bject in a class.

Class members fall under three access permissio,ns: public, private and pro,tected.

Public members: data members in this class are accessible by every class member and fro,m anywhere as lo,ng as the class is visible.

Private members: in this class, data members are o,nly accessible by the class members o,r o,ther members o,f the same class.

Pro,tected members: these are o,nly accessible within the class members and o,ther members fro,m a derived class.

Syntax

Class classname

{

Access specifier:

Member(s);

Access specifier 2:

Members(s);

Access specifier n:

Member(s);

};

Where,

*   Class is the keywo,rd that deno,tes class declaratio,n.
*   Classname is a valid name identifier o,f class.
*   Access specifier is the access permissio,n granted to, that class: either private, public o,r pro,tected.
*   Members defines the class members and member functio,ns o,f the class.

Example:

Class cars

{

Char carname[30], brand[30];

Flo,at speedlimit, mileage;

Public:

Vo,id getdata(vo,id);

Vo,id display(vo,id);

};

In this example, the data members will be carname, brand, speedlimit and mileage. the member functio,n is getdata, display, a functio,n to, apply breaks o,r even a functio,n to, increase the speed o,f the car.

Fro,m the abo,ve data, we can deduce that a class is the blue-print that defines a gro,up o,f o,bjects with similar pro,perties and behavio,rs.

o,bjects

In c++, an o,bject is an entity o,r variable which po,ssess so,me characteristics and behavio,rs. it represents an instance o,f the class. that is, when yo,u define a class, there is no, memo,ry allo,catio,n but if the class is instantiated (declaring variables), a memo,ry allo,cated is created and allo,cated to, the specific o,bjects created.

An o,bject can represent a perso,n, a car, o,r bank acco,unt. o,bjects include bo,th data members and their asso,ciated member functio,ns, kno,wn as metho,ds.

When creating a class, yo,u have to, determine the attributes o,f the o,bject yo,u’re creating, co,mmo,nly kno,wn as the data members o,f the class. fo,r example, class cars (o,bject) has attributes like car mo,del, year o,f manufacturer, engine po,wer, and co,lo,r. its asso,ciated member functio,ns o,r metho,ds include; start(), sto,p() and mo,ve().

Yo,u may have mo,re than o,ne instance o,f the o,bject created. the car o,bjects include: to,yo,ta, rav4, fielder, land ro,ver, etc.

An instance is an actual o,bject which is created during run time. fo,r example, to,yo,ta is an instance o,f class cars.

To, determine the behavio,r co,mpo,nents o,f the o,bjects, yo,u have to, determine what message the o,bjects can receive and what kind o,f o,peratio,ns need to, be perfo,rmed. the behavio,r co,mpo,nent o,f the class type o,bject describes a co,llectio,n o,f member functio,ns which send a message to, the o,bject and pro,mpt a certain actio,n to, be taken.

No,te: all messages are sent fro,m o,ne o,bject to, ano,ther by calling o,r invo,king member functio,ns.

Syntax

Identifier. message ([arg1, arg2])

Where,

●  identifier is the o,bject name.

●  do,t represents the member access o,perato,r.

●  message is the type o,f message sent.

●  arg is an o,ptio,nal list o,f arguments to, be returned o,r the message co,ntent.

The do,t between the identifier and the message type is the member access o,perato,r that identifies the data members and member functio,ns o,f the o,bject.

Fo,r example:

Class perso,n

{

char fname [25], lname[25];

int age;

Public:

vo,id getdetails()

vo,id display()

};

Vo,id perso,n :: getdetails()

{

co,ut<<”enter yo,ur first name and last name”;

cin>>fname, lname;

co,ut<<”enter yo,ur age”;

cin>>age;

}

Vo,id perso,n :: display()

{

co,ut<<”yo,ur name is:”<<fname<<lname<<aged”<<age;

}

Int main()

{

perso,n p; //p is an o,bject

p.getdetails(); //call to, enter names and age functio,n

p.display(); // call to, display yo,ur names and age

return 0;

}

o,bjects created generate a memo,ry space fo,r sto,ring data. when yo,u run the abo,ve pro,gram, the o,bjects interact by sending messages to, each o,ther thro,ugh a message passing technique.

Each o,f the o,bjects has data and the co,de needed to, manipulate the data. o,bjects can send messages to, o,ne ano,ther witho,ut kno,wing the co,ntent o,f each o,ther’s data o,r the executio,n co,de.

The class perso,n has two, private member attributes (names and age), and public member functio,ns (getdetails() and display()). these functio,ns are declared within the class as the pro,to,type.

The functio,n name is fo,llo,wed by a do,uble co,lo,n which identifies getdetails() and display() as functio,n member to, class perso,n.

If a class is created, the class name defines a new data type called an o,bject p.

Fro,m the example abo,ve, perso,n p is an o,bject created o,f the class perso,n where p sends a call to, the functio,n getdetails (p.getdetails();).

When yo,u call this functio,n, the co,mpiler pro,mpts yo,u to, enter the first name, last name and the age o,f the perso,n and sto,re them in the class private members.

P.display() is a call to, retrieve the sto,red data o,n the names and age o,f the perso,n.

Data abstractio,n

Data abstractio,n is ano,ther impo,rtant feature in c++ pro,gramming. data abstractio,n pro,vides needed info,rmatio,n witho,ut presenting the entire details. it o,nly displays the info,rmatio,n needed while hiding the backgro,und data details.

Classes helps in implementing abstractio,n in c++. using access specifiers, yo,u can gro,up a class based o,n member functio,ns and data members. this makes it easy to, kno,w which data member will be visible to, the users and what data remains hidden.

Abstractio,n can also, be applied o,n header files. fo,r example, when using po,w() in calculating the po,wer o,f a certain number yo,u o,nly call the functio,n po,w() fro,m math.h header file and pass the parameters to, it. yo,u do,n’t have to, kno,w ho,w the functio,ns wo,rk o,n the backgro,und, yo,u’re o,nly interested in what the functio,n do,es and the results o,f the calculatio,n.

Data encapsulatio,n

Data encapsulatio,n is the pro,cess o,f wrapping data and functio,ns under a single unit called a class. that is, wrapping data to,gether with its manipulatio,n metho,ds o,r functio,ns.

In encapsulatio,n, yo,u can’t access data directly. yo,u can o,nly access it via a functio,n inside the class.

When wo,rking with data, encapsulatio,n ensures data is no,t directly accessible and can o,nly be accessed thro,ugh a functio,n pro,to,type inside a class. this makes the co,ncept o,f data hiding po,ssible.

Fo,r example, if yo,u’re an acco,untant and want to, o,btain sales data fo,r a particular week, yo,u do,n’t have access to, all data in the sales sectio,n. yo,u can co,ntact the sales manager in charge o,f sales sectio,n and request him to, retrieve sales fo,r a specific week. the sales data and sales manager are wrapped under a single class called ‘sales sectio,n’.

Encapsulatio,n makes it easy to, create the co,ncept o,f data hiding o,r data abstractio,n. fo,r example, hiding data that is no,t required in the sales class.

![00221.jpeg](images/00221.jpeg)

Po,lymo,rphism

Po,lymo,rphism is representatio,n o,f data in mo,re than o,ne fo,rm. it allo,ws functio,ns and variables o,f different  types to, be used at different times. that is, a variable o,r functio,n can exhibit a different behavio,r at different instances.

When perfo,rming an o,peratio,n, a simple functio,n call can give different results depending o,n the data type o,f the variables passed. po,lymo,rphism allo,ws o,perato,rs to, exhibit different behavio,rs.

There are two, types o,f po,lymo,rphism:

●  o,perato,r o,verlo,ading

●  functio,n o,verlo,ading

o,perato,r o,verlo,ading: this is where an o,perato,r sho,w different results in different instances.

Functio,n o,verlo,ading: this is where a single functio,n name perfo,rms different types o,f tasks.

Example: yo,u can write a functio,n to, calculate a sum o,f numbers with different parameters. create functio,n 1 & 2 and pass two, parameters o,f integer type to, the first functio,n, and supply the seco,nd sum functio,n with three parameters o,f integer type. when yo,u make a call to, the sum functio,n, it will give different instances. therefo,re, po,lymo,rphism allo,ws yo,u to, use the same metho,d and pass different parameters to, it.

![00222.jpeg](images/00222.jpeg)

**Inheritance**

This is a co,ncept where yo,u develo,p a new class fro,m an existing class o,r fro,m a base class. the new class derived will have the characteristics o,f the base class. the base class will act as the parent o,r super class while the derived class will act as the child class o,r a sub-class.

The sub-class inherits all the pro,perties and characteristics o,f the super class (parent class).

Inheritance suppo,rts the co,ncept o,f co,de reusability. this is very impo,rtant as it helps in reducing the o,verall co,de written to, perfo,rm a certain task, thus making it a great feature in o,bject o,riented pro,gramming. if yo,u want to, create a new class that uses so,me o,f the co,de in ano,ther class, yo,u can derive a new class fro,m the existing class. this allo,ws yo,u to, re-use the variables and metho,ds in the existing class.

o,ther features

Dynamic binding

When yo,u make a call to, a functio,n, the co,de to, the functio,n is executed at runtime. this pro,cess is kno,wn as dynamic binding. c++ uses virtual functio,ns to, suppo,rt dynamic binding.

Message passing

Message passing is a technique in which o,bjects co,mmunicate with o,ne ano,ther. an o,bject sends a message to, ano,ther o,bject requesting executio,n o,f a certain pro,cedure. this triggers a functio,n in the receiving o,bject to, send back the desired results.

When an o,bject is co,mmunicating with ano,ther o,bject, it has to, specify its name, the functio,n name, and the message to, be sent.

C++ language suppo,rts static message passing, that is, when yo,u invo,ke an o,bject’s metho,d, the target o,bject sho,uld also, have the invo,ked metho,d. o,therwise, the co,mpiler will generate an erro,r message. message passing is made thro,ugh the help o,f vtables.

To, use dynamic message passing o,n o,bjects, yo,u sho,uld:

*   Declare a glo,bal functio,n that will act as a signature to, the message being passed between o,bjects.
*   Inherit o,bject pro,perties fro,m dmp::o,bject.
*   Create a class co,nstructo,r and add a single message o,r mo,re to, the o,bject by using add_message metho,d.
*   Use invo,ke(signature, …parameters) to, send a message to, an o,bject.

Ho,w message passing wo,rks

Each c++ o,bject has a shared_ptr to, a particular map. that is the map’s key act as a po,inter to, the message signature. its value po,ints to, an internal message structure that ho,lds the po,inter o,f the message metho,d to, invo,ke.

o,nce the o,bject metho,d is invo,ked, it retrieves the appro,priate message structure fro,m the map. as a result, it invo,kes the o,bject metho,d using this as the o,bject target.

The o,bjects share the message map amo,ng themselves to, increase efficiency amo,ng themselves. if the map is no,t unique, it will be duplicated after mo,dificatio,n o,f a message map.

Chapter summary

In this chapter, yo,u have learned basic co,ncepts o,f o,bject o,riented pro,gramming including:

*   Learning ho,w to, wo,rk with c++ o,bjects and initialize them.
*   Ho,w to, create classes and class definitio,n.
*   Applying the co,ncept o,f data data abstractio,n and encapsulatio,n to, extend the po,wer o,f pro,gramming language.
*   Learning ho,w pro,grammers can create user-defined data types and ho,w encapsulatio,n and abstractio,n wo,rk in o,rder to, pro,vide the needed info,rmatio,n to, the user witho,ut the need to, present pro,gram details.
*   Learning ho,w the co,ncept o,f data hiding is made po,ssible thro,ugh encapsulatio,n.
*   Ho,w to, use o,o,p po,lymo,rphism feature to, create o,bjects with mo,re than o,ne data type o,r fo,rm.
*   Ho,w to, use functio,n o,verlo,ading and o,verlo,aded o,perato,r in po,lymo,rphism.
*   Learning ho,w c++ suppo,rts inheritance feature by allo,wing the pro,perties and characteristics o,f a class (base class) be used in building ano,ther class (derived class).
*   Dynamic binding feature and ho,w message passing wo,rks.

In the next chapter yo,u will learn ho,w to, build base classes and derived classes as well as ho,w to, wo,rk with data members and member functio,ns.

## Chapter three: wo,rking with classes and o,bjects

In the previo,us chapter, yo,u learned abo,ut classes as user-defined data type that acts as a blueprint fo,r creating o,bjects. classes extended the co,ncept o,f data structures and just like data structures, they have data members and additio,nal member functio,ns.

**Using classes**

When wo,rking with co,mplex class functio,ns, defining member functio,ns inside the class makes it difficult to, manage the class.

Class headers and class bo,dy

C++ pro,gramming language allo,ws co,de reuse by putting class definitio,n in the header file. this pro,mpts co,de reuse in multiple files o,r pro,jects. just like declaring functio,ns in the header file so, as to, use the functio,n in multiple pro,jects, a class definitio,n is put in the header file with the same name as the class.

The member functio,ns o,f this type o,f class are defined o,utside o,f the class and sto,red in a .cpp file with the same name as the class.

A class header file co,nsists o,f class definitio,n with its data members and member functio,n pro,to,types.

No,te: putting all member functio,ns inside the header file may cause clutter in yo,ur class definitio,n. all functio,ns defined inside a class are implicitly inline, and if yo,u’re dealing with a co,mplex functio,n that is invo,ked mo,re o,ften, it will slo,w do,wn the executio,n time o,f the functio,n co,de.

If yo,u change so,me functio,n co,de in the header file, then yo,u have to, make the same changes in every file that includes the header. o,therwise, it will affect the reco,mpilatio,n pro,cess o,f the pro,ject.

But if yo,u change so,me functio,n co,de in a .cpp file, yo,u o,nly need to, reco,mpile the .cpp file.

Definitio,n and declaratio,n o,f class

In c++, a class co,nsists o,f related functio,ns and data. data and functio,ns in a class are co,mbined to,gether to, fo,rm a data type that is used in creating o,bjects o,f the type. the classes created represent real wo,rld entities  made o,f vario,us data type pro,perties and behavio,r (that is, their asso,ciated o,peratio,ns).

Syntax

Class class-name {

Access-specifier 1:

Member1;

Access-specifier 2:

Member 2;

…

} o,bject-names;

Where,

●  the class keywo,rd specifier indicates the new data-type and it is fo,llo,wed by the class-name which is the specific name that identifies that class.

●  the bo,dy o,f the class is made o,f bo,th private and public access specifiers.

#### Private

The private access specifier helps in implementatio,n o,f data hiding co,ncept. this is achieved by using the keywo,rd ‘private’ when declaring member values. the data members and functio,ns declared under the private keywo,rd can o,nly be accessed fro,m within that class itself.

The data hiding co,ncept is a security technique that prevents unautho,rized users fro,m perfo,rming any data o,peratio,n like read/write o,peratio,n o,r mo,dificatio,n o,f data. therefo,re, private data declaratio,n, hides data fro,m unautho,rized users and any accidental manipulatio,n.

Public

In public access specifier, bo,th data and functio,ns can be accessed o,utside the class. member functio,ns declared in the class are generally public and as a result, yo,u can access them fro,m o,utside the class.

Class definitio,n fo,r bo,th private and public members is sho,wn belo,w.

Class class-name

{

Private: variable declaratio,n (data members);

functio,n declaratio,n (member functio,n);

Public: variable declaratio,n;

functio,n declaratio,n;

Pro,tected: variable declaratio,n;

functio,n declaratio,n;

};

Syntax

Class mytest

{

private:

int x;

do,uble y;

string *name;

vo,id getx () {x=25;}

…;

public:

int co,unt;

vo,id gety () {y=15;}

…;

};

Where,

●  in this example, x, y, and the names are defined inside the class thus, they are private members which can be accessed within that class.

●  co,unt is a public data member which can be accessed fro,m anywhere o,utside the class.

Data members and member functio,n definitio,ns

Data members are any variables declared in a class using the standard data types like char, int, flo,at, do,uble, etc. o,r using derived data types like class, po,inters, and structures.

a class member functio,n co,nsists o,f functio,n definitio,n o,r pro,to,type within the class. the functio,n pro,to,type wo,rks o,n any o,bject o,f the class it is in and also, has access to, all o,ther data members in the class. there are two, types o,f member functio,n definitio,n: class; and class metho,d

#### Class definitio,n

This describes the data members and member functio,ns o,f the class.

#### Class metho,ds definitio,n

This describes ho,w a pro,gram is to, perfo,rm certain tasks. it sho,ws ho,w member functio,ns are co,ded. the member functio,n co,de can be written in two, ways:

●  using inside class definitio,n

●  using o,utside class definitio,n by the use o,f sco,pe reso,lutio,n o,perato,r (::)

In this case, the functio,n co,de is the same but the functio,n header is different in bo,th cases.

Inside class definitio,n

If yo,u define a member functio,n inside the class, there is no, need to, place the membership label within the functio,n name. to, easily implement this, yo,u can use inline functio,ns.

When yo,u use inline functio,ns, the co,mpiler inserts the functio,n bo,dy co,de at the specific po,int where the functio,n is invo,ked o,r called. this ensures fast executio,n o,f the pro,gram.

Example: creating class rectangle to, access the class members using the member functio,n instead o,f accessing the members directly.

Syntax

Class rectangle

{

public:

flo,at length;

flo,at width;

flo,at getarea (vo,id)

{

return length*width;

}

};

##### o,utside class definitio,n using sco,pe reso,lutio,n o,perato,r (::)

In this class defines, the functio,n is declared o,utside the class as demo,nstrated belo,w.

Syntax

Type class-name:: functio,n-name(parameters)

{

Functio,n bo,dy

}

The :: o,perato,r allo,ws yo,u to, define member functio,ns o,utside the class. the o,perato,r was earlier used to, identify a glo,bal variable in situatio,ns where the glo,bal variable had the same name as the lo,cal variable.

Example:

Class rectangle

{

public:

flo,at length;

flo,at width;

flo,at getarea (vo,id)

};

Flo,at rectangle ::getarea (vo,id)

{

return length*width;

}

To, call the member functio,n, yo,u have to, use a do,t o,perato,r (.) as sho,wn in o,ur previo,us chapter. the do,t o,perato,r allo,w yo,u to, manipulate data in an o,bject and make a functio,n call to, the o,bject.

Syntax

Rectangle rect; // create a rectangle o,bject

Rect.getarea (); // make a call to, the member functio,n o,f the o,bject

Example:

#include<io,stream.h>

#include<string>

Using namespace std;

Class pro,duct

{

String prd_name;

Flo,at weight, price;

Public:

Vo,id mgetdata()

Vo,id mfdisplay ()

} item;

vo,id pro,duct::mfgetdata()

{

co,ut<<"enter the pro,duct name";

cin>>prd_name;

co,ut<<"enter the pro,duct weight and price";

cin>>weight>>price;

}

vo,id pro,duct::mfdisplay()

{

co,ut<<"pro,duct name is"<<prd_name<<"weight is"<<weight<<"and the price"<<price<<endl;

}

//calling class member functio,ns

Int main()

{ pro,duct item;

Item.mfgetdata();

Item.mfdisplay();

Return 0;

}

To, access the private data members, yo,u have to, create getter and setter functio,n (mfgetdata() and mfdisplay()) in o,rder to, get and set the value o,f the private data members. the setter functio,n sets the value o,f the parameter passed to, the private data member while the getter functio,n returns the value o,f the private data member that needs to, be used. bo,th getter and setter functio,ns must be defined public.

Using pro,tected data members

In a pro,tected data member functio,n, data members and member functio,ns are used by that current class o,r by the derived class where they are declared.

Yo,u can access pro,tected data members using the do,t (.) o,perato,r within a subclass o,f the current class. just like the public class, yo,u can access pro,tected members fro,m a class, friend functio,n, o,r fro,m a derived class.

If class members are declared as pro,tected then:

●  o,nly the member functio,ns o,f the o,riginal class that declared it can have access to, the variables.

●  o,nly the friends o,f the class that o,riginally declared the members as pro,tected access class members.

●  they are accessed directly by a privately derived class that has private access to, the pro,tected members.

●  o,nly classes derived with either public o,r pro,tected access fro,m a class where the data members were o,riginally declared can use them.

When using base classes, then the pro,tected keywo,rd indicates that bo,th the public and pro,tected members o,f the base class are pro,tected data members o,f the derived class.

The pro,tected data members are no,t as private as the private data members o,r mo,re public than the public data members which can be accessed fro,m any functio,n.

Yo,u can declare pro,tected data members as static, meaning they will be accessible to, friend functio,n o,r member functio,n o,f a derived class. if the members are no,t static, then they can be accessed in the friend functio,n and derived member functio,ns using po,inters o,r references.

Types o,f class member functio,ns

There are several member functio,ns which can be utilized to, manipulate data members and functio,ns in c++. these special member functio,ns include:

1.  Simple functio,ns.
2.  Static functio,ns.
3.  Co,nst functio,ns.
4.  Inline functio,ns.
5.  Friend functio,ns.

Simple member functio,ns

These are the basic member functio,ns declared in c++. they do,n’t use any special keywo,rds like static as they’re prefix. the general fo,rmat o,f the basic o,r simple member functio,ns is sho,wn belo,w.

Syntax

Type functio,n_name (arguments)

{

functio,n bo,dy;

}

Static member functio,ns

These member functio,ns uses keywo,rd static and it’s asso,ciated with bo,th data members and member functio,ns. static means so,mething that ho,lds the same po,sitio,n.

To, make a functio,n static, use the keywo,rd static fo,llo,wed by the functio,n name. static functio,ns wo,rks fo,r the entire class rather than fo,r a specific o,bject o,f the class.

Static functio,ns are called using o,bject and direct member access o,perato,r (.). yo,u can also, call static member functio,n using the class name, a sco,pe reso,lutio,n o,perato,r, o,r by itself.

Syntax:

Class s

{

public:

static vo,id fxn ()

{…}

};

int main() {

// call the member functio,n directly with its class name.

s::fxn ()

}

The abo,ve functio,n can o,nly access static data members and static member functio,ns. the o,rdinary data members o,r functio,ns can’t be accessed.

Co,nst member functio,ns

Co,nst keywo,rd is used to, declare co,nstant variables. o,nce a variable is defined as co,nstant, its values can’t be changed. when co,nst is used with member functio,ns, tho,se functio,ns can’t mo,dify the data o,bjects o,r the related data members.

Syntax

Vo,id x () co,nst

{

// functio,n bo,dy

}

1.  inline functio,ns

When yo,u define member functio,ns inside a particular class, the functio,n auto,matically beco,mes an inline functio,n.

2.  friend functio,ns

Friend functio,ns pro,vides private access to, no,n-class functio,ns. these functio,ns are no,t a class member functio,n. friend functio,n allo,ws yo,u to, declare a glo,bal functio,n as a friend o,r a member functio,n o,f ano,ther class as a friend.

Syntax:

Class friendclass

{

int x;

public:

friend vo,id fn() //set glo,bal functio,n as a friend

];

vo,id fn()

{

friendclass fc;

// accessing private data member

fc.x=10;

co,ut<<fc.x;

}

int main() {

fn ()

}

A friend functio,n will be able to, access the private member functio,n thro,ugh creatio,n o,f class o,bjects. yo,u can also, make yo,ur entire class as a friend class. if yo,u make a class to, be a friend class, then all the member functio,ns auto,matically beco,me a friend functio,n.

Example:

Class ano,therfriendclass

{

vo,id fn();

};

Class friendclass

{

private:

int x;

public:

vo,id getdata(); //

// make the class functio,n ano,therfriendclass

friend vo,id ano,therfriendclass::fn();

// e co,mplete class as friend

friend class ano,therfriendclass;

};

**Building classes**

When creating classes, there are two, types o,f classes yo,u can create: base class and derived class.

**Base class and derived class**

A base class is a class which allo,ws building o,f o,ther classes fro,m it. that is, it allo,ws o,ther classes to, be derived fro,m it. a base class facilitates creatio,n o,f a new class that reuses the co,de inherited fro,m the o,riginal base class. the derived class inherits bo,th pro,perties and metho,ds o,f the base class. yo,u can extend the functio,nality o,f base class by o,verriding members in the derived class.

A base class is also, called a parent class o,r super class while the derived class is called child o,r subclass.

Any class built fro,m the base class inherits bo,th the data and behavio,r o,f the base class.

Pro,perties o,f a base class:

●  base classes are instantiated auto,matically befo,re building derived class.

●  during instantiatio,n, a derived class co,mmunicates with base class thro,ugh calling the base class co,nstructo,r with similar parameter list.

●  members o,f the base class are accessed fro,m the derived class by the use o,f an explicit cast.

●  defining abstract metho,ds in the base class so, that the class auto,matically beco,mes an abstract class. a no,n-abstract class fro,m derived class can o,verride data members in the abstract class.

The base class members have private, public, and pro,tected access mo,difiers where the private members are accessible within the class. public members are accessed o,utside the class while the pro,tected members are accessed within the class o,r by a subclass.

A derived class can o,nly access the public and pro,tected members o,f the base class. private members are inaccessible.

Chapter summary

In this chapter yo,u learned ho,w to, use classes to, so,lve vario,us pro,blems, including:

●  ho,w to, use class headers and class bo,dy when defining o,bjects, and ho,w to, define and declare classes.

●  ho,w to, differentiate between data members and member functio,ns.

●  ho,w to, declare bo,th data members and member functio,n, and determine whether they sho,uld be declared as private, public o,r pro,tected members.

●  ho,w to, access the private, public and pro,tected members in a class, as well as make calls to, the member functio,ns.

●  ho,w to, wo,rk with different class member functio,ns when invo,king specific functio,ns.

●  ho,w to, build classes using the base class and derived classes. fro,m the base class o,r the parent class, yo,u can derive a child class which inherits the behavio,r and pro,perties o,f the base class.

●  yo,u will be able to, kno,w mo,re detailed info,rmatio,n abo,ut ho,w the derived class inherits these pro,perties in o,ur next chapter.

In the next chapter yo,u will learn abo,ut class inheritance, including ho,w the derived class inherits pro,perties. at the end o,f the chapter yo,u will be able to, derive new classes fro,m an existing class, learn ho,w to, apply different types o,f inheritance to, so,lving pro,blems, identify relatio,nships between classes, learn ho,w to, apply inheritance in co,nstructo,rs and destructo,rs, and lastly be able to, manage dynamic data.

## Chapter fo,ur: extending classes via inheritance

Deriving new classes fro,m existing classes

Inheritance is an o,bject o,riented pro,gramming feature that allo,ws a class to, bo,rro,w the members o,f o,ther classes witho,ut repetitio,n o,f its members. it allo,ws o,ne class (derived class o,r subclass) to, acquire the pro,perties and metho,ds o,f ano,ther class (base class o,r superclass). a class who,se pro,perties are inherited is called the base, parent o,r superclass while the class that inherits these pro,perties is called a derived, subclass o,r child class.

When a class inherits pro,perties o,f ano,ther class, the variables and functio,ns o,f the base class are available to, the new class, hence pro,mo,ting co,de reusability. the derived class inherits all members except the private members.

Impo,rtance o,f inheritance:

1.  Suppo,rts co,de reusability
2.  Suppo,rt o,verriding metho,d
3.  Uses virtual keywo,rd

**Base class and derived class**

When inhering members o,f ano,ther class, the public members o,f the superclass will remain public while the pro,tected members will remain pro,tected. in a private inheritance, bo,th public and pro,tected members o,f a superclass will remain private in a subclass.

Syntax

Class subclass: access_mo,de superclass

The superclass sho,uld be declared first, that is, befo,re yo,u define the subclass. the access mo,de (private, public o,r pro,tected) specifies what superclass pro,perties are to, be inherited by subclass.

Fo,r example, assume yo,u have a class emplo,yee and class manager, where the manager is also, an emplo,yee  who, has additio,nal respo,nsibilities. yo,u can apply inheritance co,ncept to, avo,id repeating data members and member functio,ns in emplo,yee class to, the manager class.

The manager class can be declared as sho,wn belo,w.

Class manager: public emplo,yee

{

Public:

// additio,nal manager member co,mpo,nents

…

};

Inheritance helps yo,u declare manager class witho,ut repeating tho,se member co,mpo,nents inside the emplo,yee class. emplo,yee is the base class while manager is the derived class.

Class student

{

char* studname, co,urse;

int age;

char* department;

pro,tected:

student(char* studname);

vo,id display();

};

class ho,d : pro,tected student

{

studentlist students;

pro,tected:

ho,d(char* studname, student* peo,ple);

vo,id display();

};

Types o,f inheritance

**Single inheritance**

Single inheritance is o,ne o,f the simplest types o,f inheritance where a class is derived fro,m a single class. the derived class will inherit member co,mpo,nents fro,m o,nly a single class. fo,r example, class b inherits pro,perties and behavio,rs o,f class a. class b inherits bo,th the public and pro,tected members o,f class a.

![00223.jpeg](images/00223.jpeg)

Syntax

Class b: public a {/*…*/};

o,r

Class b: pro,tected a {/*…*/};

Multiple inheritance

In multiple inheritance, a class can inherit members fro,m two, o,r mo,re direct base classes. fo,r example, yo,u can create derived class c fro,m class a & b base classes.

![00224.jpeg](images/00224.jpeg)

Syntax

Class c: public a, public b {/*…*/};

Example:

#include<io,stream.h>

Class po,lygo,n

{

Pro,tected:

Int width, height;

Public:

vo,id setvalues (int w, int h)

{

width=w, height=h;

}

};

Class o,utput

{

Public:

Vo,id o,utput (int);

};

Vo,id o,utput::o,utput (int i)

{

Co,ut<<'i'<<endl;

}

Class rectangle:public po,lygo,n, public o,utput

{

Public:

Int area()

{

return width*height;

}

};

Class triangle: public po,lygo,n, public o,utput

{

Int area()

{return (width*height/2);}

};

Int main()

{

Rectangle rect;

Triangle tri;

Rect.setvalues (6,4);

Tri.setvalues (6,4);

Co,ut<< "area o,f rectangle is:"<<rect.o,utput(rect.area);

Co,ut<< "area o,f triangle is:"<<tri.o,utput (tri.area);

Return 0;

}

**Multi-level inheritance**

This is a where a derived class inherits fro,m a class which also, inherited pro,perties o,f ano,ther base class. fo,r example, if a is the base class o,f b while class b is the base class o,f c, then c will be the derived class o,f b and b will be a derived class o,f a.

![00225.jpeg](images/00225.jpeg)

**Hybrid inheritance/virtual inheritance**

Hybrid is a co,mbinatio,n o,f several inheritance types. fo,r example, class b and c are the derived classes o,f base class a. fro,m the derived class b and c, yo,u can create a new derived class d. this fo,rms a hybrid inheritance since it co,mbines multiple inheritance types to, fo,rm a new class.

![00226.jpeg](images/00226.jpeg)

**Hierarchical inheritance**

Hierarchical inheritance has multiple subclasses which inherit pro,perties o,f a single base class. class b, c, and d inherit the pro,perties o,f single class a.

![00227.jpeg](images/00227.jpeg)

Relatio,nships

C++ suppo,rts encapsulatio,n in which data is bundled to,gether with the specific functio,ns that o,perate o,n it, thus fo,rming a single unit. this pro,cess ensures data is o,nly accessed by functio,ns o,perating o,n it and no,t o,utside the class. this pro,tects the class member functio,ns fro,m being accessible o,utside.

To, access the private and pro,tected members o,utside the class, yo,u have to, use the special feature called the friend functio,n o,r class to, access the private members. the friend functio,n allo,ws yo,u to, access no,n-public members o,f a class. that is, a class can allo,w o,ther no,n-member functio,ns and o,ther classes to, access its private members by making them friends.

To, make the private and pro,tected classes accessible, yo,u have to, declare a pro,to,type o,f the external class allo,wing it to, gain access to, the private members o,f ano,ther class. the friend keywo,rd is placed o,n the functio,n declaratio,n o,f the friend functio,n and no,t in the functio,n definitio,n. the friend functio,n is invo,ked witho,ut any o,bject since the functio,n has its o,wn arguments as o,bjects.

Syntax

Class class-name

{

…

…

Friend type functio,n_name (arguments)

}

example:

#include<io,stream.h>

Class square;

Class rectangle

{

Int length, width;

Public:

Int area()

{

return (length*width);

}

Vo,id co,nvert (square s);

};

Class square

{

Private:

Int side;

Public:

Vo,id setsize (int a)

{

size= a;

}

Friend class rectangle

};

Vo,id rectangle::co,nvert (square s)

{

Length= s. length

width=s.side;

}

Int main()

{

rectangle.rect

Square. sqr

sqr.setvalues (a);

Rect. co,nvert (sqr);

co,ut<<rect.area();

Return 0;

}

Example 2:

#include <io,stream.h>

Class xyz

{

Private:

int x, y;

Public:

vo,id text()

{

x=50, y=75;

}

friend int co,mpute (xyz e1,e2)

};

Int co,mpute (xyz e1)

{

return int (e1.x+e2.y)-5;

}

Int main()

{

xyz e

e.test

co,ut<< "the result is:"<<co,mpute(e)

return 0;

}

Co,nstructio,n and destructio,n o,f derived o,bjects

Co,nstructo,rs and destructo,rs are c++ to,o,ls used fo,r creating o,bjects. co,nstructo,rs initialize member variables in an o,bject while a destructo,r is used in destro,ying that o,bject. whenever an instance o,f a class is created, it invo,kes the co,nstructo,r metho,d.

Co,nstructo,rs use the same name like class and no, return type, while a destructo,r uses the same fo,rm o,f naming as class but it has  ['~']  at the beginning o,f the class declaratio,n.

During pro,gram executio,n, the co,mpiler auto,matically calls the co,nstructo,r and destructo,r variables. if the base class has no, parameters passed to, it, then the derived class do,esn’t need any co,nstructo,r. if the base class has a parameter list, then the derived class sho,uld have a co,nstructo,r.

The derived co,nstructo,r class will pass its arguments to, the base class co,nstructo,r. when using inheritance co,ncept, yo,u can declare o,bjects using the derived class. o,nce yo,u declare o,bjects in a derived class, the co,nstructo,r o,f the base class and derived class are auto,matically executed.

Co,nstructo,rs and destructo,rs in base and derived classes

Inheritance o,f destructo,r o,bjects execute in reverse o,rder during executio,n o,f a co,nstructo,r. when the o,bject gets o,ut o,f sco,pe, the destructo,r is executed. see belo,w fo,r an example o,f co,nstructo,r and destructo,r pro,gram using multiple inheritance.

Syntax

#include<io,stream.h>

#include<co,nstream.h>

Class base1

{

public:

base()//co,nstructo,r with zero, arguments

{

co,ut<<"zero, arguments co,nstructo,r /n";

}

~base()

{

co,ut<<"destructo,r o,f base1 class/n";

}

};

Class base2

{

public:

base2()

{

co,ut<< "zero, argument co,nstructo,r fo,r base2 class/n";

}

~base3()

{

co,ut<< "destructo,r o,f base2 class/n";

}

};

Class base3: public base1, public base2

{

public:

base3()

{

co,ut<<"zero, argument co,nstructo,r fo,r a derived class /n";

}

~base3()

{

co,ut<<"destructo,r o,f the derived class /n";

}

};

Int main ()

{

clrscr ();

base3 o,bj; //declaring o,bject

return 0;

}

//o,utput

Zero, arguments co,nstructo,r

Destructo,r o,f base1 class

Zero, argument co,nstructo,r fo,r base2 class

Destructo,r o,f base2 class

Zero, argument co,nstructo,r fo,r a derived class

Destructo,r o,f the derived class

In the abo,ve pro,gram, base1 and base2 are the superclass while base3 is the derived class. the co,nstructo,rs o,f the superclass are executed first befo,re executing the derived class. the destructo,r o,f the derived class is executed befo,re executing the superclass.

Yo,u can call the superclass co,nstructo,r in a derived class co,nstructo,r. when yo,u create a derived class o,bject fro,m an existing base class, the base class beco,mes a co,nstructo,r by default, and it is executed first then fo,llo,wed by the derived class.

When making a call to, a base class co,nstructo,r with parameters inside the derived class co,nstructo,r which also, has parameters, then yo,u have to, explicitly mentio,n it when declaring the parameters o,f the derived class co,nstructo,r.

Base class is the default co,nstructo,r which is present in all types o,f classes. see example belo,w.

Syntax

Class co,nstruct

{

Int x;

Public:

co,nstruct()

{

co,ut << "building default co,nstructo,r\n";

}

};

Class child : public co,nstruct

{

Int y;

Public:

Child()

{

co,ut << "default derived co,nstructo,r\n";

}

// co,nstructo,r with parameters

child(int z)

{

co,ut << "parameterized derived co,nstructo,r\n";

}

};

Int main()

{

co,nstruct c;

Child c1;

Child c2(10);

}

//o,utput

Building default co,nstructo,r

Default derived co,nstructo,r

Building default co,nstructo,r

Parameterized derived co,nstructo,r

In the abo,ve example, the base class is the default co,nstructo,r class which is called to,gether with o,bjects fro,m derived/child class. the example belo,w sho,ws base class co,nstructo,r with parameters.

Syntax

Class co,nstruct

{

Flo,at x;

Public:

co,nstruct(flo,at i)

{

x=i;

co,ut << "parameterized co,nstructo,r\n";

}

};

Class child : public co,nstruct

{

Flo,at y;

Public:

child(flo,at j): co,nstruct(j)

{

y=j;

co,ut << "parameterized derived co,nstructo,r\n";

}

};

Int main()

{

child (10);

}

// o,utput

Parameterized co,nstructo,r

Parameterized derived co,nstructo,r

An explicit call to, the parameterized base co,nstructo,r class permits a call to, the parameterized derived class co,nstructo,r. a co,nstructo,r base class is called inside the derived class. this allo,ws the co,nstructo,r to, initialize the o,bject in the class.

A derived class co,nstructo,r can o,nly access its o,wn class members while a derived class o,bject inherits the characteristics and pro,perties o,f the base class. a base class co,nstructo,r initializes the members o,f the base class.

Upcasting in c++

The use o,f superclass reference o,r a po,inter to, po,int to, a subclass o,bject is kno,wn as upcasting. that is, co,nverting the subclass reference address o,r po,inter to, its superclass reference address.

![00228.jpeg](images/00228.jpeg)

Syntax

Class baseclass

{

Int i;

Public:

Vo,id base()

{

co,ut << "this is a superclass";

}

};

Class derived:public baseclass

{

Int j;

};

Int main()

{

Baseclass* ptr;// po,inter to, base class

Derived o,bj;

Ptr = &o,bj;

Baseclass &ref;// baseclass's reference address

Ref=o,bj;

}

In a do,wncasting, the base class’s reference o,r po,inter is co,nverted into, a derived class reference o,r its po,inter.

No,te: co,nstructo,rs and destructo,rs are no,t inherited. the assignment o,perato,r (=) can be o,verlo,aded but it canno,t be inherited by a subclass.

Inheritance and static functio,ns

1.  The static functio,ns can be inherited into, the derived class.
2.  If static member functio,ns are redefined in a derived class, then o,ther o,verlo,aded functio,ns in the super class are hidden.
3.  All static member functio,ns canno,t be virtual.

Hybrid inheritance and virtual class

When a derived class inherits pro,perties o,f mo,re than o,ne base class, it results in multiple inheritance. see example belo,w.

Syntax

Class basea

{

Vo,id print();

};

Class baseb:public basea

{

// derived class definitio,n

};

Class basec:public basea

{

// derived class definitio,n

};

Class based:public baseb, public basec

{

// class definitio,n

};

Int main()

{

D o,bj;

o,bj.print();

}

Class baseb and basec inherit the print() functio,n in class basea. class based inherits two, co,pies o,f the print() functio,n. when yo,u call the print() in the main() functio,n, it results in ambiguity since the co,mpiler do,esn’t kno,w which print() functio,n to, call. to, avo,id this, a virtual functio,n is used. this is do,ne by inserting the virtual keywo,rd when the class is being inherited.

Class baseb: virtual public basea

{

// derived class definitio,n

};

Class basec: virtual public basea

{

// derived class definitio,n

};

Class based:public baseb, public basec

{

// class definitio,n

};

The virtual keywo,rd tells the co,mpiler to, call any o,f the two, functio,ns.

Managing dynamic data

C++ allo,ws yo,u to, dynamically allo,cate memo,ry space fo,r yo,ur pro,gram. initially, a pro,grammer can determine the memo,ry space o,f the pro,gram by defining the variables befo,re the pro,gram executes. there are cases where the memo,ry can o,nly be determined during run time o,r it is based o,n user input needs. in this case, the memo,ry is dynamically allo,cated to, pro,grams. dynamic memo,ry determines ho,w the data is pro,cessed and sto,red.

Po,inters are also, used fo,r memo,ry allo,catio,n and ho,ld the memo,ry address o,f a variable. when yo,u declare a variable it has two, co,mpo,nents:

●  the address o,f the variable

●  the value which is sto,red in the variable. fo,r example: int y= 200\.

The abo,ve example tells the co,mpiler to,:

1.  Create a space in memo,ry to, sto,re the value o,f the variable.
2.  Asso,ciate the variable y  with the reserved memo,ry lo,catio,n.
3.  Sto,re value 200 at the reserved memo,ry lo,catio,n.

Po,inters is o,ne o,f the useful features in c++ language, and o,nce utilized in a pro,gram, it enables:

1.  Direct access and manipulatio,n o,f the memo,ry lo,catio,n.
2.  Allo,catio,n o,f dynamic memo,ry into, a variable.
3.  Impro,vement o,f efficiency in so,me ro,utine pro,grams.

Allo,cating and deallo,cating memo,ry with new and delete o,perato,rs

C++ pro,gram integrates the new and delete o,perato,rs to, dynamically allo,cate the memo,ry. the new o,perato,r fo,llo,wed by the data type specifier dynamically allo,cates the memo,ry o,f a pro,gram.

If the user input has a sequence o,f mo,re than o,ne element, then the new[] o,perato,r is need to, allo,cate a blo,ck o,f memo,ry.

Syntax

Po,inter = new return-type

o,r

Po,inter = new return-type [size]

The new o,perato,r allo,cates memo,ry fo,r a single element o,n the memo,ry heap.

The new [] o,perato,r allo,cates memo,ry to, an array/blo,ck o,f elements with the size being an integer value that represents the o,bjects returned.

Syntax

int *mem;

mem = new int [4];

When yo,u run the pro,gram, the system dynamically allo,cates memo,ry space o,f the 4 elements o,f integer type and returns an array o,f elements assigned to, po,inter mem. therefo,re, mem po,ints directly to, a memo,ry blo,ck with fo,ur elements o,f integer (int) type.

Yo,u can access the first element in the array by calling mem [0], while the seco,nd element is accessed by mem [1].

Yo,u can also, initialize the memo,ry with the new o,perato,r, as seen belo,w.

Syntax

Po,inter-variable= new return-type (value);

Example:

int *ptr = new int (30);

flo,at *r = new flo,at (15)

There exists a difference between a no,rmal array and a blo,ck o,f memo,ry allo,cated dynamically using the new o,perato,r. in a no,rmal array, the array size is a co,nstant expressio,n which is determined during variable declaratio,n (befo,re running the pro,gram), whereas the dynamic memo,ry allo,catio,n is perfo,rmed using the new o,perato,r that assigns memo,ry space to, a pro,gram during run time. it uses any variable value as the size fo,r the blo,ck o,f elements.

The system dynamically allo,cates memo,ry to, a pro,gram fro,m the memo,ry heap. no,n-static and lo,cal variables are allo,cated memo,ry o,n stack.

Fo,r any dynamically allo,cated memo,ry (int *mem= new int[4]) the pro,grammer has to, deallo,cate the memo,ry after the pro,gram executio,n. o,therwise, if the memo,ry space is no,t deallo,cated, it will result in a memo,ry leak. the memo,ry sho,uld be deallo,cated after the pro,gram executio,n terminates.

#### Delete o,perato,r

In c++, the o,perato,r delete deallo,cates the already allo,cated memo,ry space to, a pro,gram. this makes the memo,ry available fo,r the next request to, dynamically allo,cate space.

Syntax

delete po,inter-variable;

o,r

delete [] po,inter-variable;

If yo,u dynamically allo,cated space to, a single element using the new o,perato,r, then use delete po,inter-variable to, free the memo,ry. to, free a memo,ry allo,cated to, a blo,ck o,f elements, yo,u use delete []. the arguments passed to, the delete o,perato,r sho,uld be either a po,inter that po,ints to, a blo,ck o,f elements o,r a null po,inter. passing a null po,inter has no, effect to, the delete o,perato,r.

Fo,r example, delete [] ptr; o,r delete ptr;

#include <io,stream>

#include <new>

Using namespace std;

Int main ()

{

int l,m;

int * ptr;

co,ut << "enter the numbers yo,u want to, print:";

cin >> l;

ptr= new (no,thro,w) int[l];

if (ptr == nullpo,inter)

Co,ut << "erro,r: unsuccessful memo,ry allo,catio,n";

else

{

Fo,r (m=0; m<l; m++)

{

co,ut << "enter number: ";

cin >> ptr[m];

}

Co,ut << "the numbers entered are: ";

Fo,r (m=0; m<l; m++)

co,ut << ptr[m] << ", ";

Delete[] ptr;

}

return 0;

}

// o,utput

Enter the numbers yo,u want to, print: 3

Enter number: 25

Enter number: 50

Enter number: 72

The numbers entered are: 25, 50, 72

If the system co,uld no,t allo,cate the memo,ry space requested fo,r example, requesting a large memo,ry allo,catio,n then the system will return an erro,r message. erro,r: unsuccessful memo,ry allo,catio,n. the new request will thro,w a standard bad_allo,c exceptio,n, unless yo,u use the no,thro,w with the new o,perato,r. this exceptio,n type handle erro,rs by checking the po,inter value o,r thro,ugh catching exceptio,ns.

Handling erro,rs with try and catch

Co,mputer memo,ry is a limited reso,urce and so,metimes it’s no,t a guarantee whether the request to, dynamically allo,cated memo,ry to, a pro,gram using the new o,perato,r will be successful. the memo,ry gets exhausted so,metimes.

C++ uses two, standard mechanisms to, determine if the memo,ry allo,catio,n was successful o,r no,t. if memo,ry allo,catio,n fails, an exceptio,n is thro,wn. the no,thro,w exceptio,n is used to, handle the erro,rs in the pro,gram instead o,f thro,wing bad_allo,c exceptio,n which terminates the pro,gram after an erro,r o,ccurred. these will be discussed later in detail.

Syntax

ptr= new (no,thro,w) int[l];

To, kno,w whether the blo,ck o,f memo,ry allo,catio,n fails, yo,u can detect the failure thro,ugh checking whether the po,inter variable is null.

Avo,iding memo,ry leaks

When a pro,grammer creates a memo,ry in the heap and fo,rgets to, delete it, it creates a memo,ry leak. to, avo,id having a memo,ry leak, yo,u sho,uld free the memo,ry allo,cated o,n the heap when no, lo,nger needed. always make sure to, use the right o,perato,r (delete o,r delete []) to, deallo,cate the memo,ry.

If there is a memo,ry leak, then the memo,ry usage increases. this makes the limited memo,ry reso,urce very co,stly thus creating mo,re pro,blems later. the example belo,w is a pro,gram to, sho,w a memo,ry leak.

Syntax

#include <io,stream.h>

Using namespace std;

Vo,id memo,ry_leak()

{

Int *p = new int(4);

Return; // return metho,d witho,ut deallo,cating the po,inter variable p

}

Int main()

{

// calling the functio,n

// functio,n to, get the memo,ry leak

Memo,ry_leak();

Return 0;

}

Smart po,inters can also, be used to, free the memo,ry. yo,u do,n’t have to, manually manage the memo,ry. instead  o,f declaring char* yo,u can use std::string which manages the internal memo,ry. this makes it faster and well-o,ptimized co,mpared to, when managing memo,ry manually.

Yo,u can also, reduce memo,ry leaks by reducing the new/delete calls.

**Chapter summary**

Inheritance is o,ne o,f the impo,rtant features o,f o,bject o,riented pro,gramming. it allo,ws pro,grammers to, reuse co,de instead o,f rewriting the same co,de again. in this, o,ne class inherits the pro,perties and metho,ds o,f ano,ther class (base class). in this chapter, yo,u have learned:

●  ho,w to, derive new classes fro,m existing classes so, as to, pro,mo,te co,de reusability.

●  ho,w to, use inheritance to, suppo,rt o,verriding metho,ds as well as learn ho,w to, wo,rk with bo,th base and derived classes.

●  ho,w yo,u can specify what pro,perties are to, be inherited by the subclass using the access mo,de. this requires yo,u to, define the base class first befo,re defining the subclass.

●  abo,ut different types o,f inheritance and ho,w to, use each type in creating o,bjects.

●  ho,w to, use co,nstructo,rs and destructo,rs in deriving o,bjects.

●  ho,w to, access a class using the base and derived co,nstructo,rs.

●  ho,w yo,u can call a base class co,nstructo,r in a derived class co,nstructo,r. when yo,u create a derived class o,bject fro,m an existing base class, the base class beco,mes a co,nstructo,r by default, and it is executed first then fo,llo,wed by the derived class.

●  ho,w to, make a call o,f the base class inside the derived class co,nstructo,r that has parameters like the base class co,nstructo,r.

●  ho,w to, use upcasting feature in c++ to, allo,w yo,u to, reference yo,ur base class.

●  ho,w to, use a po,inter to, po,int directly to, a subclass.

●  ho,w to, dynamically allo,cate memo,ry space fo,r yo,ur pro,gram during run-time.

●  ho,w to, use new and delete o,perato,rs to, allo,cate and deallo,cate memo,ry when no,t needed.

●  ho,w to, use delete o,r delete [] o,perato,rs to, help yo,u avo,id memo,ry leaks in yo,ur pro,gram.

●  ho,w to, use try catch exceptio,ns to, test whether memo,ry allo,catio,n is successful o,r has failed.

In the next chapter yo,u will learn abo,ut po,lymo,rphism. at the end o,f the chapter yo,u will kno,w what po,lymo,rphism is and ho,w to, apply different types o,f po,lymo,rphism during co,mpile and runtime. yo,u will also, learn ho,w to, create abstract classes and virtual functio,ns.

## Chapter five: po,lymo,rphism

Po,lymo,rphism is an o,o,p feature that allo,ws an o,bject to, have mo,re than o,ne fo,rm. if yo,u have multiple classes that relate to, each o,ther by inheritance, the classes are using the po,lymo,rphism co,ncept. when using inheritance, po,lymo,rphism is executed by use o,f o,verriding functio,n. that is, bo,th the superclass and subclass have same declared member functio,n but different functio,n definitio,n.

In o,ur previo,us chapter, the inheritance feature allo,wed us to, create a new derived class that inherited attributes and pro,perties o,f ano,ther class. po,lymo,rphism uses similar metho,ds to, perfo,rm different tasks. it allo,ws yo,u to, perfo,rm a single task using different fo,rms. fo,r example, a wo,man can have different characteristics depending o,n the situatio,n, like being a wife, a mo,ther, and an emplo,yee.

Po,lymo,rphism is divided in two,:

●  runtime po,lymo,rphism

●  co,mpile time po,lymo,rphism

![00229.jpeg](images/00229.jpeg)

Co,mpile time po,lymo,rphism

Co,mpile time po,lymo,rphism is also, kno,wn as static po,lymo,rphism, and it indicates the existence o,f an entity in mo,re than o,ne physical fo,rm. in static po,lymo,rphism, functio,ns are bo,und based o,n their signature (data type and the number o,f parameters present). the functio,n calls represent an early binding because they’re made o,n the basis o,f data type and the sequence o,f parameters passed.

Co,mpile time po,lymo,rphism is implemented using o,verriding functio,n and o,perato,r o,verlo,ading.

o,verlo,ading functio,n

Functio,n o,verlo,ading is a situatio,n where yo,u have multiple functio,ns with the same name but different parameters. these functio,ns have parameters with different data types o,r changes in the number o,f parameters being passed.

Syntax

Int area (int x);

Int area (int x, int y);

See example belo,w.

#include <io,stream.h>

Using namespace std;

Class additio,n {

Public: flo,at sum(flo,at x, flo,at y){

return x+y;

}

flo,at sum(flo,at x, flo,at y, flo,at z){

return x+y+z;

}

};

Int main() {

additio,n o,bj;

// a call to, sum functio,n with two, parameters

co,ut<<"to,tal sum: "<<o,bj.sum(8.80, 15.20)<<endl;

//call to, the seco,nd functio,n with three parameters

co,ut<<"to,tal sum: "<<o,bj.sum(18.5, 26.4, 30.0);

return 0;

}

// o,utput

To,tal sum: 24.0

To,tal sum: 74.9

o,verlo,ading functio,ns impro,ve co,de readability as well as co,de reusability as sho,wn abo,ve. yo,u can perfo,rm the same task to, functio,ns with a different parameter list.

o,perato,r o,verlo,ading

o,perato,r o,verlo,ading allo,ws yo,u to, o,verlo,ad o,perato,rs. fo,r example, yo,u can use o,perato,r (+) to, jo,in two, strings to,gether. if yo,u use the additio,n o,perato,r between two, integers, it adds them but when the o,perato,r is  placed between strings, it co,ncatenates o,r jo,ins them.

To, o,verlo,ad an o,perato,r, yo,u have to, declare a class member functio,n who,se name is o,perato,r and then fo,llo,w with the o,perato,r sign yo,u want to, use.

Type o,perato,r-sign (parameters)

Fo,r example: xyz o,perato,r + (xyz) / using o,perato,r o,verlo,ading

Syntax

#include<io,stream.h>

Using namespace std;

Class xyz

{

Private:

Int a,b;

Public:

Xyz()

Vo,id getvalues()

{

co,ut<<"enter value o,f a and b";

cin>>a>>b;

}

Vo,id setvalues(flo,at x, flo,at y)

{

x=a;

y=b;

}

Vo,id setvalues(do,uble num1, do,uble num2)

{

num1=a;

num2=b;

}

Vo,id display()

{

co,ut<<"the value fo,r a is:"<<a<<"the value fo,r b is:"<<b<<endl;

}

Do,uble additio,n()

Xyz o,perato,r + (xyz)

};

Xyz xyz::o,perato,r +(xyz)

{

Return (a+b)

}

Int main()

{

Xyz x1,x2,x3;

X1.getvalues(10,15);

X2.setvalues(6,8);

X3.setvalues(12,8);

Co,ut<<x1.additio,n();

Co,ut<<x2.additio,n();

Co,ut<<x3.additio,n();

Return 0;

}

Run-time po,lymo,rphism

Run time po,lymo,rphism is also, dynamic po,lymo,rphism. in this type o,f po,lymo,rphism, functio,ns change their fo,rm depending o,n the situatio,n. if a functio,n exists in different fo,rms and respo,nds to, different functio,n calls made dynamically during running time, then it fo,rms dynamic po,lymo,rphisms.

Runtime po,lymo,rphism suppo,rts dynamic binding and makes pro,grams mo,re flexible when being executed.

In dynamic binding, a functio,n call is made at run-time and it depends o,n the functio,n po,inter co,ntent at run-time. if yo,u change the co,ntents o,f the functio,n po,inter, yo,u will end up with different functio,ns that share the same name but have different functio,n bo,dy.

A dynamic po,lymo,rphism changes an entity based o,n the situatio,n. a functio,n exhibits dynamic po,lymo,rphism if it exists in different fo,rms. the functio,n calls to, these types o,f po,lymo,rphism are made dynamically during the executio,n time.

Dynamic binding is also, kno,wn as late binding, and it impro,ves the flexibility o,f a pro,gram being executed. the calls to, the functio,n are made o,n the basis o,f co,ntent o,f functio,n po,inter. all po,lymo,rphic functio,ns have the same name but with different data types o,r sequence o,f parameters.

Static binding is mo,re efficient than dynamic binding in so,me cases. if yo,u have a static functio,n yo,u do,n’t need a run-time search, while dynamic functio,ns calls fo,r run-time search. mo,st functio,n calls in dynamic binding are reso,lved at executio,n time.

Dynamic po,lymo,rphism is implemented using o,verriding functio,ns and virtual functio,ns.

o,verriding functio,n

Functio,n o,verriding allo,ws yo,u to, have the same functio,n name in the superclass and subclass. the subclass inherits the data members and member functio,ns in the superclass. yo,u can create an o,verriding functio,n in the subclass by creating the same member functio,ns with the same argument list.

Functio,n o,verriding is do,ne o,nly in the derived class, and it is achieved during run time. o,verriding functio,n is redefining a base class inside the derived class with the same return type and parameters.

Syntax

Class super

{

Public:

vo,id print()

{

co,ut << "this is a base class";

}

};

Class subclass: public super

{

Public:

Vo,id print()

{

co,ut << "this is a derived class";

}

};

The print () in the base class is o,verridden in the derived class.

Ho,w to, call o,verriding functio,n

Yo,u can make a call to, the o,verriding functio,n in the main () functio,n. the functio,n call and the functio,n bo,dy co,nnects thro,ugh the binding pro,cess. if the co,nnectio,ns o,ccur befo,re run time it is called early binding, static o,r co,mpile-time binding.

Syntax

Class super

{

Public:

vo,id print()

{

co,ut << "this is a base class";

}

};

Class subclass: public super

{

Public:

Vo,id print()

{

co,ut << "this is a derived class";

}

};

Int main ()

{

super b; //creating o,bject fo,r base class

subclass d; // creating o,bject fo,r derived class

b.print(); // static binding

d.print();

return 0;

}

//o,utput

This is a base class

This is a derived class

See belo,w fo,r an example o,f calling the abo,ve base functio,n using po,inters.

Int main ()

{

super *b; //creating o,bject po,inter fo,r base class

subclass d; // creating o,bject fo,r derived class

b = &d;

b -> print (); // static binding

}

In the abo,ve example, we have made a call to, the o,verridden functio,n using base o,bject and derived o,bject. the b.print () o,bject will call the base functio,n while d.print () o,bject will call the derived class functio,n.

Virtual functio,ns

A virtual functio,n is a base class member functio,n which is o,verridden in the derived class. the functio,n call results in late binding. that is, it instructs the co,mpiler to, perfo,rm late binding o,n the o,verridden functio,n.

To, make member functio,ns o,f the base class virtual, a virtual keywo,rd is used when declaring the functio,n. a late binding call is made at run time. therefo,re, the co,mpiler determines the o,bject type during run time and makes the functio,n call.

Virtual vo,id functio,n-name()

{//functio,n bo,dy}

Example:

#include <io,stream.h>

class car

{

public:

virtual vo,id make()

{

co,ut<<"member functio,n o,f the car base class is accessed";

}

};

class 4wheel: public car

{

public:

vo,id make()

{

co,ut<<"accessing virtual member functio,n o,f the 4wheel derived class";

}

};

vo,id main()

{

car *a, *b;

a = new car();

a -> make(); //an o,bject po,inter which is equivalent to, *a.make();

b = new car();

b -> make();

}

If a member o,f the class is redefined inside the derived class, it is called a virtual member. in the abo,ve example, functio,n make() is a virtual functio,n inside the base class. a 4wheeler is a derived class o,f the base class car.

If the member functio,n is no,t declared as virtual then it will result in static binding where the functio,n call is bo,und during co,mpile time. but if the functio,n is declared as virtual, the functio,n address is bo,und during run-time making it a dynamic binding.

To, achieve dynamic binding co,ncept, the co,mpiler creates a v-table every time a virtual functio,n is declared. the v-table co,ntains info,rmatio,n abo,ut the functio,n po,inters fro,m each o,f the o,bjects in the derived class and o,ther functio,n class info,rmatio,n. this info,rmatio,n is made available whenever a call is made to, the virtual functio,n.

Ho,w to, access private member functio,ns in a derived class using virtual keywo,rd

Using virtual keywo,rd, yo,u can easily call the private member functio,n in a derived class with a po,inter that po,ints to, the base class. in this case, the co,mpiler will lo,o,k at the access specifier mo,de during co,mpile time.

During late binding when the pro,gram is running, the co,mpiler do,esn’t check the access specifier o,f the functio,n being called.

Syntax

Class super

{

Public:

virtual vo,id print()

{

co,ut << "this is a base class";

}

};

Class subclass: public super

{

Public:

Virtual vo,id print()

{

co,ut << "this is a derived class";

}

};

Int main ()

{

super *b;

subclass d;

b = &d;

b -> print ();

}

// o,utput

This is a derived class

No,tes:

1.  o,nly the base class functio,n is declared with a virtual keywo,rd.
2.  If yo,u declare a functio,n as virtual in the base class, then the functio,n will auto,matically be virtual in all o,f the derived classes.

**Abstract classes**

An abstract class is a type o,f class which co,nsists o,f at least a pure virtual functio,n. abstract class pro,vides an interface to, a derived class. if a class inherits pro,perties o,f an abstract class, then yo,u must define the pure virtual functio,n, o,therwise, the derived class will beco,me an abstract class.

Characteristics o,f abstract class:

1.  Even tho,ugh yo,u can create po,inters and references in an abstract class, it canno,t be instantiated.
2.  Abstract class has bo,th variables, functio,ns and a pure virtual functio,n.
3.  Abstract classes are suitable in perfo,rming upcasting so, as to, allo,w the subclass to, use its interface.
4.  All classes that inherit the pro,perties o,f an abstract class must implement the pure virtual functio,n, to, avo,id beco,ming abstract to,o,.

Pure virtual functio,n

A virtual functio,n with no, definitio,n is kno,wn as the pure virtual functio,n. a pure virtual functio,n has no, functio,n bo,dy and it uses the virtual keywo,rd at the beginning and ends with a no,tatio,n =0 since it has no, bo,dy.

Virtual vo,id functio,n-name () =0;

Bo,th virtual and pure functio,ns wo,rks the same way except that the pure virtual functio,n has no, functio,n definitio,n.

The example belo,w demo,nstrates an abstract class.

Class bpo,lygo,n

{

Pro,tected:

Flo,at width, height;

Public:

Vo,id setvalues(flo,at x, flo,at y)

{

width=x; height=y;

}

Virtual flo,at area()=0;

};

Class brectangle:public bpo,lygo,n

{

Public:

Flo,at area()

{

return (width*height);

}

};

Class btriangle:public bpo,lygo,n

{

Public:

Flo,at area()

{

return ((width*height)/2);

}

};

Int main()

{

Brectangle rect;

Btriangle tri;

Bpo,lygo,n *p1=&rect;

Bpo,lygo,n *p2=&tri;

P1 -> setvalues(8,6);

*p2.setvalues(8,6);

Co,ut<<p1 ->area()<<endl;

Co,ut<<p2 ->area()<<endl;

Return 0;

}

**Chapter summary**

In this chapter yo,u have learned what po,lymo,rphism is and the different types o,f po,lymo,rphisms. yo,u’re no,w able to,:

●  differentiate between the co,mpile time po,lymo,rphism and run time po,lymo,rphism using examples.

●  use static binding o,r early binding to, make system calls to, the member functio,n and ho,w to, use dynamic binding to, make a functio,n call during pro,gram executio,n.

●  use functio,n o,verlo,ading and o,perato,r o,verlo,ading to, increase pro,gram efficiency.

●  make functio,n calls using o,verriding functio,ns and virtual functio,ns as well as o,verride a functio,n inside a derived class.

●  declare virtual functio,ns in yo,ur pro,gram and kno,w ho,w to, use abstract classes.

●  access the private member functio,ns using the virtual keywo,rd as well as differentiate between a virtual functio,n and a pure virtual functio,n.

In the next chapter yo,u will learn abo,ut co,nstructo,rs and destructo,rs. by the end o,f the chapter, yo,u will be able to, declare class co,nstructo,r and destructo,r and kno,w ho,w to, use different types o,f co,nstructo,rs.

## Chapter six:  co,nstructo,rs and destructo,rs

o,verview

A co,nstructo,r is a member functio,n which initializes the o,bjects o,f a class type and has the same name as the class name. the co,nstructo,r class can accept arguments o,r no,t accept arguments, and it allo,cates memo,ry space to, class o,bjects.

Co,nstructo,r’s member functio,n perfo,rms co,nstructio,n wo,rk. that is, building values in an o,bject thro,ugh auto,matic initializatio,n. a co,nstructo,r is auto,matically invo,ked whenever a new instance o,f a class is created. yo,u can define the arguments o,f the class manually o,r leave it witho,ut any arguments.

The name o,f the co,nstructo,r is always the same as the name o,f the class and the co,nstructo,r has no, return type.

Class co,nstructo,rname

{// class bo,dy};

o,n the o,ther hand, a destructo,r is a member functio,n that is co,mplementary to, the co,nstructo,r. a destructo,r de-initializes an o,bject after it has been destro,yed. the destructo,r functio,n call is made when an o,bject within a class has go,ne o,ut o,f sco,pe, o,r when its memo,ry space is de-allo,cated with the use o,f delete o,perato,r.

The destructo,r de-allo,cates memo,ry space fo,r the o,bject. a destructo,r do,esn’t have any parameters, therefo,re it canno,t be o,verlo,aded. it is usually called in reverse to, co,nstructo,r. if a class (derived class) inherits pro,perties o,f ano,ther class (base class) and bo,th classes have destructo,r, then the destructo,r in the derived class is called first.

A destructo,r has the same name as the class and the tilde (~) o,perato,r precedes it.

**~** class name

{// class bo,dy

};

Definitio,n and declaratio,n o,f a co,nstructo,r

A co,nstructo,r definitio,n is just like the o,ther member functio,ns in a class. the definitio,n is either inside the class o,r o,utside the class using the class name fo,llo,wed by the sco,pe reso,lutio,n :: o,perato,r.

Syntax

class base

{

do,uble a, b;

pro,tected:

base (do,uble, do,uble); // co,nstructo,r

vo,id print ()

};

The class base has a member functio,n co,nstructo,r base () which has the same name as the class base. this member functio,n is the co,nstructo,r o,f the class and it can be utilized in o,rder to, create values fo,r the o,bject class. when making a call to, the functio,n, yo,u can pass values to, the functio,n by declaring the o,bject.

Base b; // o,bject declaratio,n

B= base (35, 58);

In this case, an o,bject b is created fro,m the base class and a co,nstructo,r call is pro,mpted.

See belo,w fo,r an example o,f a co,nstructo,r demo,nstratio,n.

#include <io,stream>

#include <co,nio,.h>

Class triangle

{

Private:

Do,uble length, height;

Public:

length = 15.2;

height = 20.5;

Do,uble area()

{

return (length*height/2);

}

};

int main()

{

clrscr();

triangle tri;

co,ut<<"the area o,f triangle is:" <<tri.area()<<"sq.units\n";

getch();

}

// o,utput

The area o,f triangle is: 155.8 sq.units

Characteristics o,f co,nstructo,rs

1.  They sho,uld always be declared under the public access specifier.
2.  Co,nstructo,rs do,n’t have a return type, no,t even a null (vo,id) return type.
3.  Creating a new o,bject results in an auto,matic call to, the co,nstructo,r functio,n.
4.  A derived class can’t inherit a co,nstructo,r functio,n but it can make a call to, the base class co,nstructo,r.
5.  A co,nstructo,r can have default parameters just like o,ther functio,ns.
6.  Co,nstructo,rs can never wo,rk as virtual functio,ns.
7.  Yo,u can’t refer to, the address o,f a co,nstructo,r.

Types o,f co,nstructo,rs

C++ pro,gramming language has vario,us types o,f co,nstructo,rs which extend its functio,nality. these co,nstructo,rs include: default, parameterized, o,verlo,aded and co,py.

#### Default co,nstructo,rs

A default co,nstructo,r do,esn’t have any arguments o,r parameters. see example belo,w.

Class cube

{

public:

int x;

cube()

{

x= 5;

}

};

Int main ()

{

cube c;

co,ut<< c.x;

}

o,nce the o,bject is created, a call to, the co,nstructo,r is made immediately, thus initializing the data member. the default co,nstructo,r initializes the o,bject members. if yo,u do,n’t define a co,nstructo,r, the co,mpiler implicitly assigns a default co,nstructo,r to, the class.

If a co,mpiler returns a default co,nstructo,r, it will initialize the o,bject data members with a default value which is initially 0 o,r any rando,m integer value.

Parameterized co,nstructo,rs

This is a co,nstructo,r which has arguments. yo,u can supply different parameters o,r values to, the data members o,f different o,bjects.

The initial values to, the co,nstructo,r are passed as arguments when the co,nstructo,r is declared. this is do,ne by:

●  calling the co,nstructo,r explicitly.

●  calling the co,nstructo,r implicitly.

See example belo,w.

Class cube

{

public:

int val;

cube( int x)

{

val= x;

}

};

Int main ()

{

cube c (5);

cube c1 (10);

cube c2 (15);

co,ut<< c.val;

co,ut<< c1.val;

co,ut<< c2.val;

}

o,verlo,aded co,nstructo,r

Co,nstructo,rs no,t o,nly initialize data members, they’re no,t different fro,m o,ther member functio,ns. they also, perfo,rm functio,n o,verlo,ading just like in po,lymo,rphism. the default and parameterized co,nstructo,rs can act as an o,verlo,aded co,nstructo,r where o,ne o,f them has no, parameters while the o,ther o,ne has parameters.

o,verlo,aded co,nstructo,r allo,ws yo,u to, have multiple co,nstructo,rs in a class with each having different parameter list.

See example belo,w.

#include <io,stream>

Using namespace std;

Class o,verlo,ad

{

public:

Do,uble area;

o,verlo,ad()

{

area = 0;

}

o,verlo,ad(flo,at num1, flo,at num2)

{

area = num1 * num2;

}

Vo,id display()

{

co,ut<< area<< endl;

}

};

Int main()

{

// co,nstructo,r o,verlo,ading with same class name and different arguments

o,verlo,ad c1;

o,verlo,ad c2(8.6, 6.2);

c1.display();

c2.display();

}

// o,utput

0

53.32

Co,py co,nstructo,rs

C++ o,ffers a special type o,f co,nstructo,r which passes an o,bject as a parameter to, the functio,n and co,py data member values fro,m o,ne o,bject to, ano,ther. co,py co,nstructo,r declares and initializes o,bject values fro,m ano,ther o,bject.

co,py co,nstructo,r creates new o,bjects with exact features as the existing o,bject, hence the name co,py co,nstructo,r. a co,py co,nstructo,r acts as o,verlo,aded co,nstructo,r because it declares and initializes an o,bject fro,m ano,ther o,bject.

There are two, types o,f co,py co,nstructo,rs:

●  default co,py co,nstructo,r: the co,mpiler auto,matically defines this type o,f co,py co,nstructo,r if the user o,r pro,grammer do,esn’t define the co,py co,nstructo,r.

●  user defined co,nstructo,r: it is a co,py co,nstructo,r defined by the pro,grammer.

![00230.jpeg](images/00230.jpeg)

Syntax

Class_name (co,nst class_name & o,bject_name);

Example 1:

Class co,py

{

Co,py (co,py &y) // co,py co,nstructo,r

{ // functio,n bo,dy o,f co,py co,nstructo,r }

};

To, call the co,py co,nstructo,r in the abo,ve example, yo,u have to, initialize the o,bject. this can be do,ne in any o,f the fo,llo,wing ways:

co,py c2 (c1);

o,r

co,py c2=c1

Where,

C1 initializes the c2 o,bject.

Example 2:

#include <io,stream>

Using namespace std;

Class co,py

{

Public:

Flo,at i;

Co,py(flo,at x) //parameterized co,nstructo,r.

{

I=x;

}

Co,py(co,py &y) // co,py co,nstructo,r definitio,n

{

I = y.i;

}

};

Int main()

{

Co,py c1(35); // call to, parameterized co,nstructo,r.

Co,py c2(c1); // call to, co,py co,nstructo,r.

Co,ut<<c2.i;

Return 0;

}

// o,utput

35

When a call is made to, the co,nstructo,r, two, co,pies are pro,duced:

●  shallo,w co,py

●  deep co,py

Shallo,w co,py

The default co,py co,nstructo,r created by the co,mpiler can o,nly pro,duce a shallo,w co,py. it is a shallo,w co,py since the o,bjects are created by co,pying all data variables o,f an o,bject to, ano,ther o,bject.

See the example belo,w:

Class example

{

Int num1;

Int num2;

Int *ptr;

Public:

Example()

{

ptr=new int;

}

Vo,id setdata(int a,int b,int c)

{

num1=a;

num2=b;

*ptr=c;

}

Vo,id printdata()

{

std::co,ut << "num1 value is : " <<num1<< std::endl;

std::co,ut << "num2 value is : " <<num2<< std::endl;

std::co,ut << "*ptr value is : " <<*ptr<< std::endl;

}

};

Int main()

{

example e1;

e1.setdata (8, 9, 12);

example e2 = e1;

e2.printdata();

Return 0;

}

// o,utput

Num1 value is: 8

Num2 value is: 9

*ptr value is: 12

In the abo,ve example, the co,nstructo,r is no,t defined, therefo,re the co,mpiler assigns example e2= e1 by calling the default co,py co,nstructo,r. in this case, the co,mpiler creates a similar co,py o,f the existing o,bject. the po,inter ptr po,ints to, the same memo,ry lo,catio,n o,n bo,th o,bjects.

If the memo,ry o,f o,ne o,f the o,bjects is freed, the o,ther memo,ry is auto,matically freed since bo,th fields po,int to, the same memo,ry. to, avo,id this pro,blem, yo,u can define the co,py co,nstructo,r (user-defined co,nstructo,r) that uses deep co,py technique.

#### Deep co,py

Deep co,py is a technique where memo,ry is dynamically allo,cated to, a co,py and then it co,pies the actual values. the so,urce and the co,py have distinct characteristics and wo,n’t share the same memo,ry lo,catio,n.

In deep co,py, the pro,grammer has to, write a user-defined co,nstructo,r.

Syntax

Class example

{

Public:

Int num1;

Int num2;

Int *ptr;

Example()

{

Ptr=new int;

}

Example (example &y)

{

Num1=y.num1;

Num2=y.num2;

Ptr=new int;

*ptr=*(y.ptr);

}

Vo,id setdata(int a,int b,int c)

{

Num1=a;

Num2=b;

*ptr=c;

}

Vo,id printdata()

{

Std::co,ut << "num1 value is : " <<num1<< std::endl;

Std::co,ut << "num2 value is : " <<num2<< std::endl;

Std::co,ut << "*ptr value is : " <<*ptr<< std::endl;

}

};

Int main()

{

Example e1;

E1.setdata (5, 7, 9);

Example e2 = e1;

E2.printdata();

Return 0;

}

// o,utput

Num1 value is: 5

Num2 value is: 7

*ptr value is: 9

Since the pro,grammer defined the co,nstructo,r, then e2=e1 calls fo,r an already user-defined co,py co,nstructo,r. this result to, an exact co,py o,f the o,bject which is po,inted by *ptr and all the values o,n the type data members.

Class destructo,r

A destructo,r has a special member functio,n which executes when the delete o,peratio,n is invo,ked in the o,bject o,f that class o,r when an o,bject in the class gets o,ut o,f sco,pe.

A destructo,r will have the same name as the class with a prefix o,f the tilde o,perato,r. it has no, return values, and yo,u can’t pass any parameters to, it. destructo,r is an impo,rtant c++ feature which frees memo,ry space when it’s no, lo,nger needed.

Example: the fo,llo,wing example explains ho,w to, use co,nstructo,rs and destructo,rs in a pro,gram.

Syntax

// co,nstructo,r & destructo,r

Class crectangle

{

Int *len, *wid;

Public:

Crectangle (int, int)// co,nstructo,r

~crectangle ()//destructo,r

Int area()

{

return (len*wid);

}

};

Crectangle:: crectangle (int c, int d)

{

*len=c;

*wid=d;

};

//destructo,r to, free the memo,ry

Crectangle :: crectangle ()

{

Delete len;

Delete wid;

};

int main()

{

crectangle.rect a (c,d);

crectangle.rect b (c,d);

co,ut << area o,f a rectangle is: <<rect a.area();

co,ut << area o,f a rectangle is: <<rect b.area();

co,ut << endl;

}

Special characteristics o,f destructo,rs

1.  When an o,bject is destro,yed, a co,nstructo,r is called auto,matic.
2.  Just like o,ther member functio,ns, destructo,rs fo,llo,w the same access rules.
3.  A destructo,r de-initializes an o,bject befo,re it gets o,ut o,f sco,pe.
4.  Destructo,rs do,n't have a return type and do, no,t even suppo,rt vo,id.
5.  Destructo,r functio,ns can never be inherited.
6.  A destructo,r do,esn't allo,w the use o,f static destructo,rs.
7.  A destructo,r can make calls to, member functio,ns o,f it's class.
8.  If an o,bject in a class has a destructo,r, then that o,bject can't be a member o,f the unio,n.

**Chapter summary**

In this chapter, yo,u have learned abo,ut co,nstructo,r, destructo,r and functio,ns o,verlo,ad. co,nstructo,rs are very essential in c++ language since they help build values in o,bjects thro,ugh auto,matic initializatio,n. specifically, yo,u learned:

●  ho,w to, declare and initialize co,nstructo,rs.

●  ho,w a co,nstructo,r initializes an o,bject o,f the class type.

●  ho,w a destructo,r de-initializes the o,bject after executio,n. a destructo,r helps free the memo,ry space by de-initializing the o,bject after it has been destro,yed.

●  abo,ut parameterized co,nstructo,rs with parameters. yo,u will be able to, pass different parameters and values to, the data members o,n different o,bjects. yo,u also, learned ho,w to, make calls to, the co,nstructo,r.

●  ho,w to, use the o,verlo,aded co,nstructo,r and co,py co,nstructo,r.

●  to, understand the two, types o,f co,py co,nstructo,rs: shallo,w and deep.

●  ho,w to, create a pro,ject with bo,th types o,f co,py co,nstructo,rs and ho,w to, make calls to, the o,bjects created.

In the next chapter yo,u will learn ho,w to, use templates. at the end o,f the chapter yo,u will be able to, create class templates, functio,n temples and ho,w to, create templates with multiple parameters.

## **Chapter seven: templates**

Intro,ductio,n to, templates

Templates are an impo,rtant feature in c++ pro,gramming language, as it allo,ws functio,ns and classes to, use generic types. they play an essential ro,le o,n ho,w functio,ns and classes wo,rk by allo,wing them to, define different data types witho,ut rewriting each o,ther.

Using templates, yo,u can write a generic co,de that can be used with any data type. all yo,u need is to, pass the data types as parameters. templates pro,mo,te co,de reusability and impro,ve the flexibility o,f the pro,gram. yo,u can create a simple class o,r a functio,n and pass data types as parameters and implement the co,de to, be used by any data type. whenever yo,u want to, use the functio,n, yo,u make a call to, the functio,n and specify the return type.

Fo,r example, if yo,u use so,rt() functio,n to, so,rt data in a wareho,use, yo,u can pass different data types as parameters to, the functio,n. yo,u do,n't have to, write and maintain multiple file co,des to, so,rt data. based o,n the data type passed to, the so,rting algo,rithm, yo,ur data in the wareho,use is so,rted irrespective o,f that particular data type. therefo,re, templates are used in situatio,ns where yo,u need a co,de to, be reusable with mo,re than o,ne data type.

Templates are o,f great impo,rtance when dealing with multiple inheritance and o,perato,r o,verlo,ading. it is widely applied where co,de reusability is o,f prime impo,rtance.

Types o,f templates

Templates are implemented in two, ways:

●  using functio,n templates

●  using class templates

A template can be defined as a macro,. that is, when yo,u define an o,bject o,f a specific type, the template definitio,n o,f that type o,f class substitutes it with the appro,priate data type. templates are o,ften referred to, as parameterized class o,r functio,ns since a specified data type will replace the defined parameter during executio,n time.

Class templates

Class templates o,ffer the specificatio,ns fo,r creating a class based o,n the parameters. a class template accepts members with parameter type. that is, yo,u can instantiate a class template by passing a given set o,f data type to, its parameter list. class templates are mo,stly used in implementing co,ntainers.

Syntax

Template <class identifier>

Class class-name

{

…

//class member specificatio,ns

…

};

Example:

![00231.jpeg](images/00231.jpeg)

A class template definitio,n is similar to, no,rmal class definitio,n except that in templates, yo,u add a prefix template <class m> where, m is the type. the template prefix tells the co,mpiler that a class template is declared which uses m as the type name in the declaratio,n. in this case, the class vecto,r is a parameterized class that uses type m as its arguments. type m can be replaced by any data type o,r by using a user-defined data type.

If a class is derived fro,m a class template, then it’s called a template class. the o,bjects o,f the template class are defined as fo,llo,ws:

Classname<type> o,bjectname (arglist);

Creating a derived class fro,m class template is kno,wn as instantiatio,n pro,cess. befo,re creating a template class, yo,u have to, debug the class template befo,re co,nverting it to, a template class. the co,mpiler checks fo,r erro,rs in a template class after instantiatio,n has taken place.

Example: class template

Template <class tt>

Class rectangle

{

tt width;

tt height;

Public:

vo,id setvalues(tt num1,tt num2)

tt area()

{

tt a;

a=width*height;

return a;

}

};

Vo,id rectangle <tt> ::setvalues (tt num1,tt num2)

{

width=num1;

height=num2;

}

Int main()

{

rectangle o,bj1;

rectangle <int> o,bj1(5,6);

rectangle o,bj2;

rectangle <flo,at> o,bj2(5.6,4);

co,ut<< o,bj1.setvalues()

co,ut<<o,bj2.setvalues()

return 0;

}

//o,utput

o,bj1=30

o,bj2=22.4

The abo,ve pro,gram creates a class o,f type tt. the <tt> in the (vo,id rectangle <tt> ::setvalues (tt num1,tt num2)) statement specifies that the functio,n parameter is also, a class template parameter and sho,uld always be included when calling a class.

Class templates with multiple parameters

Yo,u can also, have mo,re than o,ne generic data type in a class. yo,u can declare the generic type class with a co,mma-separated list inside the template specificatio,n.

Syntax

Template <class xy, class xyz, …>

Class class-name

{

//functio,n bo,dy;

};

Example: class with two, generic types

Template<class f1,class f2>

Class numbers

{

f1 j; f2 k;

Public:

numbers (f1 x, f2 y)

{ j=x; k=y;

}

vo,id print()

{

co,ut<<j<<”and”<<k<<”\n”;

}

};

Int main()

{

Numbers <flo,at, int> numbers1 (2.53, 253);

Numbers <int, char> numbers2 (50,’z’);

Numbers1.print();

Numbers2.print();

Return 0;

};

// o,utput

1.53 and 253

50 and z

Functio,n templates

Functio,n templates wo,rk like a no,rmal functio,n except that the no,rmal functio,n wo,rks with o,nly a single data type, while templates acco,mmo,date multiple data types. with templates, yo,u can o,verlo,ad a no,rmal functio,n so, as to, wo,rk with different data types.

This makes functio,n templates mo,re useful since yo,u o,nly have to, write a single pro,gram that wo,rks o,n all data types.

Templates are always expanded during co,mpile time.

Just like class template, yo,u can create a functio,n template with different argument types.

Syntax

Template <class type>

Return-type functio,n-name (arguments)

{

Functio,n bo,dy;

};

When defining functio,n templates, yo,u must include the template type in bo,th the functio,n bo,dy and parameter list when necessary.

Example1: functio,n to, swap values

Template <class t1>

Vo,id swap (t1&num1, t1&num2)

{t1 val= num1; num1=num2; num2=val;};

Calling a template functio,n wo,rks the same way as the no,rmal functio,n call.

Example 2: implementatio,n o,f functio,n template

Template <class test>

Test max (test x, test y);

{

test results;

results=x>y? x:y;

return results;

};

Int main()

{

int a=5, b=6, c;

do,uble l=4, m=6, n;

c= max <int> (a,b);

n=max <do,uble> (l,m);

co,ut<< c<<endl;

co,ut<<n<<endl;

return 0;

}

In this example, test is the template parameter. the functio,n max is called twice with different argument types (int and do,uble). when the co,mpiler instantiates, it calls the functio,n each time by its type.

The o,utput o,bject pro,duced (after instantiatio,n o,f the template with specific type) will be o,f the same type with the parameters x and y.

The abo,ve pro,gram will so,rt values based o,n which is higher. if using an array o,f numbers, the so,rting algo,rithm will be applied to, so,rt the numbers fro,m the smallest to, highest.

Functio,n template with multiple parameters

Just like in class templates, yo,u can have mo,re than o,ne generic data type separated by co,mmas.

![00232.jpeg](images/00232.jpeg)

Example: temple class with multiple parameters

Template<class temp1,class temp2>

Vo,id display( temp1 j, temp2 k)

{

Co,ut<<j<<” “<<k<<”\n”;

}

Int main()

{

J=display1(2019, “edge”);

K=display2(18.54, “1854);

return 0;

}

// o,utput

2019edge

18.541854

o,verlo,ading template functio,ns

Yo,u can o,verlo,ad a template functio,n using its template functio,n o,r using the o,rdinary functio,n fro,m its name. o,verlo,ading can be do,ne thro,ugh:

1.  Calling an o,rdinary functio,n that matches the template functio,n.
2.  Calling a template functio,n which is built with the exact functio,n.
3.  Use no,rmal o,verlo,ading functio,n o,n an o,rdinary functio,n and make a functio,n call to, the o,ne that matches the template functio,n.

If there is no, match fo,und, an erro,r message is generated by the system.

Example: o,verlo,aded template using an explicit functio,n

Template <class m>

vo,id display(m n)

{

Co,ut<<”display template functio,n:” << n<< “\n”;

}

Vo,id display ( int n)

{

Co,ut<<”explicit template display: “<< n<<”\n”;

}

Int main()

{

display (80); display (15.20);

return 0;

}

//o,utput

Explicit template display: 80 display template functio,n: 15.20

The functio,n call display (80) calls the o,rdinary versio,n o,f a display () functio,n and no,t its template versio,n.

Member functio,n templates

When creating class templates, all member functio,ns can be defined o,utside the class since the member functio,ns in a template class are parameterized using type argument. therefo,re, the functio,n template sho,uld define the member functio,ns.

Member functio,ns (whether inline o,r no,n-inline) declared inside a class template are implicitly a functio,n template. if a template class is declared, it inherits all the template functio,ns defined in a class template.

Member functio,n templates are defined in three ways:

1.  Explicit definitio,n in a file sco,pe fo,r each return-type used to, instantiate a template class.
2.  During file sco,pe within the template parameters.
3.  Inclined within the class.

A member functio,n template can instantiate functio,ns no,t explicitly generated. if a class has bo,th a member functio,n and an explicit functio,n, then the explicit definitio,n is given mo,re prio,rity.

Syntax

![00233.jpeg](images/00233.jpeg)

Example: class vecto,r with member functio,n template

![00234.jpeg](images/00234.jpeg)

No,n-type template arguments

Templates can have single o,r multiple type arguments. yo,u can also, use a no,n-type argument template in additio,n to, the type t argument. yo,u can create a template argument using strings, co,nstants, built-in types and functio,n names.

![00235.jpeg](images/00235.jpeg)

The abo,ve template passes the size o,f an array as an argument. the co,mpiler will o,nly kno,w the size o,f the array during the executio,n time. the arguments are specified during the creatio,n o,f template class.

**Chapter summary**

C++ pro,gramming language suppo,rts the use o,f templates co,ncept in o,rder to, suppo,rt generic pro,gramming. in this chapter, we are able to, learn ho,w templates allo,w us to, create a family o,f classes o,r functio,ns which can handle different data types. o,ther functio,ns o,f templates yo,u have learned include:

●  use o,f templates to, avo,id duplicatio,n o,f co,des by just making a call to, the template functio,n argument return-type. this also, makes it easy to, manage the pro,gram as well as make the pro,gram develo,pment pro,cess easier.

●  creating templates by use o,f multiple parameters fo,r bo,th class templates and functio,n templates.

●  ho,w to, create a derived class fro,m a class template which is called a template class. the pro,cess used in the creatio,n o,f the template class is kno,wn as instantiatio,n.

●  template functio,ns and ho,w yo,u can o,verlo,ad the template functio,n by either calling the o,rdinary functio,n that matches the template name o,r by calling the template functio,n which has an exact match to, the functio,n template.

●  ho,w to, use arguments in class templates. all member functio,ns o,f the class sho,uld be defined as a functio,n template by using the arguments in a class template.

●  ho,w to, instantiate member functio,ns which are explicitly generated.

●  ho,w to, use no,n-type arguments to, define and declare functio,n templates.

In the next chapter yo,u will learn abo,ut the input and o,utput streams and vario,us file o,peratio,n metho,ds. at the end o,f the chapter, yo,u will be able to, use io,s fo,rmatting functio,ns, manage o,utput with manipulato,rs, design yo,ur o,wn manipulato,rs, carry o,ut file o,peratio,ns, determine end o,f file, file o,pening mo,des, use put (), get () functio,ns and using file stream classes.

## Chapter eight: c++ input and o,utput streams

Intro,ductio,n

C++ pro,gramming language co,mes with a lo,t o,f libraries which helps in perfo,rming input o,utput functio,ns. the input o,utput co,ncept is perfo,rmed thro,ugh a series o,f bytes which are co,mmo,nly kno,wn as streams. it suppo,rts two, types o,f input/o,utput streams with o,ne stream inherited fro,m the c pro,gramming language and the o,ther fro,m the o,bject o,riented input/o,utput system. just like the i/o, streams in the c pro,gramming language, the i/o, system in c++ language are fully integrated.

Every develo,ped pro,gram takes in data as input, the data is pro,cessed then displayed o,ut as an o,utput. this is based o,n the input o,utput pro,cessing cycle o,r fetch and execute cycle. c++ suppo,rts all the i/o, functio,n fo,und in c language. the i/o, metho,ds in c++ suppo,rts o,bject o,riented pro,gramming co,ncept and user defined data types.

Implementatio,n o,f i/o, o,peratio,ns in c++ is by use o,f streams co,ncept and stream classes are achieved thro,ugh the co,nso,le and disk files.

Bo,th input stream and o,utput streams are used in class definitio,n.

**C++ streams**

A stream acts as a lo,gical device which accepts input data and generates info,rmatio,n. it is linked to, a physical device via the i/o, system. even tho,ugh the devices co,nnected to, the streams wo,rk the same, the devices may differ fro,m o,ne ano,ther.

Since streams behave in the same manner, their i/o, functio,ns can o,perate in any device. fo,r example, yo,u can use the same functio,n to, write to, a file, printer, scanner, and display unit.

The stream is bo,th the so,urce and the destinatio,n. the so,urce stream supplies data to, the pro,gram and is co,mmo,nly kno,wn as the input stream. o,n the o,ther hand, a destinatio,n stream receives info,rmatio,n as o,utput and it is called an o,utput stream.

Input stream: this invo,lves flo,w o,f bytes fro,m an input device like keywo,rd into, the main memo,ry fo,r pro,cessing.

o,utput stream: this is the flo,w o,f bytes o,r pro,cessed data fro,m the main memo,ry into, an o,utput device like the display screen.

C++ has bo,th cin and co,ut as the predefined streams in its standard library. these streams are auto,matically triggered when a pro,gram begins to, execute. cin stream is an input stream that is co,nnected to, the standard input device and allo,ws the user to, enter new data into, the system memo,ry, while the co,ut represents the o,utput stream which is co,nnected to, an o,utput device to, display info,rmatio,n.

**C++ stream classes**

I/o, system in c++ co,nsists o,f a hierarchy o,f classes which define streams fo,r handling the system co,nso,le unit and disk files. stream class hierarchy perfo,rms bo,th input and o,utput o,peratio,ns within the co,nso,le unit. the i/o, stream classes are declared in the header file o,f io,stream. the header file sho,uld be inserted in every pro,gram that co,mmunicates with the co,nso,le.

The io,s acts as the base class fo,r input stream (istream) and o,stream (o,utput stream) acts as the base class fo,r io,stream (input/o,utput stream). the io,s class is declared as a virtual base class and as a result, o,nly a single co,py o,f its data members will be inherited by the io,stream (input/o,utput stream.)

The io,s class o,ffers basic suppo,rt fo,r i/o, o,peratio,ns o,n bo,th fo,rmatted and unfo,rmatted streams. it suppo,rts handling o,f bo,th input and o,utput stream. the istream class is respo,nsible fo,r fo,rmatted and unfo,rmatted input while the o,stream class is respo,nsible fo,r fo,rmatted o,utput thro,ugh inheritance co,ncept.

Co,nso,le o,peratio,n using stream classes

**Class name**

Pro,perties

Io,s (basic input/o,utput stream)

Has basic pro,perties that can be used by o,ther input and o,utput classes.

Has po,inters fo,r buffering o,bjects.

Declare functio,ns and co,nstants essential fo,r perfo,rming fo,rmatted input and o,utput o,peratio,ns.

Istream (input stream)

It inherits io,s pro,perties.

Used to, declare get (), getline(), and read () input functio,ns.

Co,nsists o,f o,verlo,aded extractio,n o,perato,r >>

o,stream (o,utput stream)

It inherits io,s pro,perties.

Allo,ws yo,u to, declare o,utput functio,ns like put() and write().

Uses o,verlo,aded insertio,n o,perato,r <<

Io,stream (input/o,utput stream)

Inherits all characteristics o,f io,s stream and o,stream thro,ugh the use o,f multiple inheritance.

It has bo,th input and o,utput functio,ns o,f bo,th classes.

Streambuf

Pro,vides interface to, all physical devices via the buffer.

It wo,rks as the base class o,f filebuf available in io,s files.

Unfo,rmatted input/o,utput o,peratio,ns

o,verlo,aded o,perato,rs >> and <<

C++ cin and co,ut standard library functio,ns fo,r input and o,utput uses o,verlo,aded o,perato,rs >> and << respectively. the >> o,perato,r is o,verlo,aded in the istream class while << o,perato,r is o,verlo,aded in the o,stream class.

To, read input data fro,m the keywo,rd, yo,u use the >> o,perato,r.

Cin>> variable 1….>>variable n;

The input variable 1 up to, variable n is a variable name which has already been declared inside the class. the cin standard tells the co,mputer to, search fo,r the input data fro,m the input devices like keybo,ard.

The data is read character by character and assigned to, the indicated lo,catio,n by the >> o,perato,r. data inputs are separated by white spaces and if the co,mpiler enco,unters the white spaces when reading a variable o,r enco,unters a character that do,esn’t match the destinatio,n data type, it terminates.

Suppo,se yo,u have a class with a variable declared as an integer, yo,u can use the input data device to, input the data.

Int num;

Cin>> num;

The cin statement fo,llo,wed by >> o,perato,r will pro,mpt yo,u to, enter any value o,f integer type fro,m the keybo,ard like 520. when yo,u enter the input data, the o,perato,r reads the value 520 assigned to, the num variable.

To, display the data o,n the screen, yo,u use the co,ut statement.

Co,ut<< data1<< data 2…. <<data n;

The data1 all the way to, data n can be a variable o,r a co,nstant o,f any data type.

Put () and get () functio,ns

The istream and o,stream classes defines two, types o,f member functio,ns get(), and put() to, handle input/ o,utput o,peratio,ns o,f a single character.

The get() functio,ns is represented into, two, fo,rms o,f functio,n pro,to,type. that is, the get(char*) and the get(vo,id). these functio,n pro,to,types fetch a new character, a blank space, newline and even a tab in the input data. the get(char*) pro,to,type assigns input character to, the functio,n arguments while get(vo,id) o,nly returns the input character.

The functio,n pro,to,types represent member functio,ns o,f input/o,utput stream and they sho,uld be invo,ked using an appro,priate o,bject.

Example:

Char i;

Cin.get(i) // this allo,ws yo,u to, get a character fro,m the keybo,ard and assign to, variable i.

{

Co,ut<<i // display the variable o,n the screen

}

The abo,ve co,de reads and displays a line o,f text statements. the >> o,perato,r in the co,ut statement reads a character by character and skips any white spaces o,r new line character in the statement.

Cin>>i; can be used instead o,f cin.get(i)

Where,

I=cin.get();

In this, the value o,f the member functio,n get() is assigned to, the variable i.

Put() is a member functio,n o,f o,stream class and it o,utputs a single line o,f statements o,r a character by character. fo,r example:

Co,ut.put(i);

This co,de displays a single character i while co,ut.put(ch) displays the value to, the ch variable. yo,u pass any number variable as argument to, the put() member functio,n.

Example:

Char x; cin.get (x); while(x!=\n)

{

co,ut.put(x);

cin.get(x);

}

A pro,gram using get() and put () to, represent i/o, data.

# include<io,stream>

Using namespace std;

Int main()

{

int m=0;

char n;

co,ut<<"enter input text"

cin.get(n);

while (n1=\n)

{

co,ut.put(n);

m++;cin.get(n);

}

co,ut<<\n number o,f characters="<m<< "\n";

return 0;

}

Input

C++ pro,gramming language.

o,utput

C++ pro,gramming language.

Number o,f characters = 22

Getline() and write() functio,n

The getline() and write() functio,ns are respo,nsible fo,r reading o,r displaying a line o,f text in an effective manner. the getline() reads a who,le line o,f text which has a new line character “\n”. when the co,mpiler enco,unters the new line character, the pro,gram is executed. a call to, the functio,n is made thro,ugh:

Cin.getline (line, size);

The functio,n call invo,kes getline() functio,n which reads the characters entered to, the system via the keybo,ard. o,nce the size-1 o,r \n character is enco,untered, the reading is terminated.

Example:

Char empname [30];

Cin.getline(empname, 30);

Example:

#include <io,stream>

Using namespace std;

Int main()

{

int size=30;

char co,untry[30];

co,ut<<”enter the name o,f the co,untry:\n “;

cin>>co,untry;

co,ut<<”co,untry name is:”<<co,untry<<”\n\n”; co,ut<<”enter ano,ther co,untry name again: \n”;

cin.getline(co,untry,size);

co,ut<<”the current co,untry name is:”<<co,untry<<”\n\n”;

return 0;

}

//o,utput

Enter the name o,f the co,untry: kenya

Enter ano,ther co,untry name again: uganda

The current co,untry name is: uganda

The write() functio,n display the who,le line and uses the fo,llo,wing fo,rm:

Co,ut.write(line, size)

The line argument indicates the string’s name displayed and the size argument sho,ws the number o,f characters. if the variable size is greater than the pro,gram line, then beyo,nd the bo,und o,f the line is displayed.

Fo,rmatted co,nso,le i/o, o,peratio,ns

There are vario,us features suppo,rted by c++ to, help fo,rmat the o,utput. these features include:

●  io,s class functio,n and flags.

●  user-defined o,utput functio,ns.

●  manipulato,rs.

Io,s fo,rmat functio,ns

The io,s class has a large number o,f functio,ns fo,r fo,rmatting the o,utput in a number o,f ways. these member functio,ns include:

Member functio,n

Manipulato,rs

Actio,n

Width()

Setw()

This functio,n indicates the required field size needed to, display an o,utput value.

Fill()

Setfill()

It specifies the characters essential fo,r filling unused po,rtio,n o,f the field.

Precisio,n()

Setprecisio,n()

Indicates the number o,f digits which are to, be displayed after the decimal po,int o,f flo,at value.

Setf()

Setio,flags()

It specifies the fo,rmat flag used to, co,ntro,l what fo,rm o,f o,utput is to, be displayed.

Unsetf()

Resetio,sflags()

It clears any specified flag

When included in the i/o, statements, these manipulato,rs change the parameter fo,rmat o,f a stream. to, access manipulato,r functio,ns in a pro,gram, yo,u have to, include io,manip file.

Defining field width

The width() functio,n determines the width field needed fo,r the o,utput o,f an o,bject. yo,u can invo,ke the functio,n thro,ugh:

Co,ut.width(w);

Where,

W is the width field and it is printed in a field o,f w characters wide. the functio,n specifies the field width fo,r a single o,bject. after printing the o,utput details o,f the single o,bject, it reverts back to, default settings.

Fo,r example, co,ut.width(7);

Co,ut<<6543<<12<<”\n”; // printing in the fo,rmat o,f 6, 5, 4, 3 and 1, 2

This will pro,duce the fo,llo,wing o,utput:

6

5

4

3

1

2

Setting precisio,n (precisio,n ())

When wo,rking with flo,ating po,int numbers, they’re printed six digits after the decimal po,int. to, avo,id printing all these six digits, yo,u can specify the number o,f digits to, be printed after the decimal po,int. this can easily be achieved by the use o,f precisio,n () member functio,n.

Co,ut.precisio,n (d);

Where,

D is the number o,f digits after the decimal po,int are to, be printed. the functio,n retains its setting until they’re reset, unlike the width ().

Example:

Co,ut.precisio,n (3)

Filling and padding

The unused part o,f field width is always filled up with white spaces. the fill() functio,n is used to, fill these unused white spaces with any desired character.

Co,ut.fill (ch);

Where,

Ch is the character used in filling up the unused white spaces.

Example:

Co,unt.fill (‘*’)

In this case, the white spaces will be filled with ‘*’ o,perato,r. fo,r example, so,me institutio,ns like banks use this fo,rm o,f filling blank spaces, especially when printing a cheque.

Fo,rmatting flags, bit fields and setf()

The setf () is io,s class member functio,n fo,r justifying answers.

Co,ut.setf (arg1, arg2)

Where,

Arg 1 is the already fo,rmatting flag in io,s class. the flag indicates the fo,rmatting requirements o,f an o,utput. arg2 is an io,s co,nstant which specifies the fo,rmatting gro,up to, which the fo,rmatting flag belo,ngs to,.

Example:

Co,ut.setf (io,s::left, io,s::adjustfield);

Co,ut.setf (io,s::scientific, io,s::flo,atfield);

The first statement in the abo,ve example sho,uld have a gro,up member to, the seco,nd statement.

Example:

Co,ut.fill (*);

Co,ut.setf (io,s::left, io,s::adjustified);

Co,ut.width (8);

Co,ut<<”flag”<<”\n”;

// o,utput

F

L

A

G

*

*

*

Using manipulato,r to, manage o,utput

The io,manip header file has a set o,f manipulato,r functio,ns which manipulates the o,utput fo,rmat. these manipulato,rs wo,rk the same way as io,s member functio,ns and flags. yo,u can use mo,re than o,ne manipulato,r in a single statement.

Example:

Co,ut<<manip a<< manip b<< manip c<<item;

Co,ut<<manip a <<item1 <<manip b <<item2;

The abo,ve co,ncatenatio,n is great when yo,u want to, display data in co,lumn fo,rms.

There are different types o,f manipulato,rs yo,u can use to, alter fields. these manipulato,rs include:

Manipulato,r

Set o,f actio,ns perfo,rmed

Alternative member functio,n

Setw (int w)

Functio,n fo,r setting field with to, w

Width()

Setprecisio,n (int d)

Essential fo,r setting the flo,ating po,int numbers precisio,n to, d

Precisio,n()

Setfill (int c)

Used to, set the fill element with character c

Fill()

Setio,sflags (lo,ng f)

Used fo,r setting the fo,rmat flag

Setf()

Resetio,sflags (lo,ng f)

Used to, clear any fo,rmat flag specified by f

Unserf()

Helps yo,u insert a new line o,r to, flush a stream.

“\n”

Example:

Co,ut<<setw(8)<< 1234;

The abo,ve statement will print values 1, 2, 3,4 in a right justified field o,f 8 characters. the o,utput o,f this  statement can be altered to, be left-justified. yo,u can do, this in the fo,llo,wing way:

Co,ut<<setw (8) <<setio,sflags (io,s::left) <<1234;

File o,peratio,ns

The i/o, system handles file o,peratio,ns similar to, the i/o, o,peratio,ns. in this case, file streams are used as an interface between the specific files and the pro,grams. files have bo,th input and o,utput streams.

An input stream is a stream in which data is supplied to, the pro,gram while an o,utput stream is a stream that receives data fro,m the pro,gram. the input stream extracts data fro,m the file while the o,utput stream enters data into, the file. any input o,peratio,n used o,n the data acts as a link between the pro,gram and the input file. similarly, o,utput file o,peratio,ns co,nsists o,f an o,utput stream that links the pro,gram with the o,utput file.

**File stream classes**

The input/o,utput system in c++ pro,gramming language pro,vides a set o,f stream classes essential fo,r handling file metho,ds and o,peratio,ns. so,me o,f these metho,ds include the use o,f ifstream, o,fstream, and fstream.

File stream classes are derived fro,m fstream base class which co,rrespo,nds to, the io,stream class. the class fo,r managing disk files sho,uld be declared in the fstream and the file sho,uld be included in every pro,gram that needs the use o,f the file.

Steps to, file o,peratio,n

When using disk files yo,u have to,:

1.  Select a suitable name fo,r the file.
2.  Define the data type and structure o,f the files.
3.  Define the file purpo,se.
4.  Define metho,d fo,r o,pening the files.

**File stream classes**

**Class**

Class co,ntents

Filebuf

This class sets the file buffers fo,r read and write o,peratio,n. the class has o,penpro,t co,nstant used in o,pening the file thro,ugh the o,pen() functio,n. it also, has bo,th o,pen () and clo,se () member functio,ns.

Fstreambase

Fstreambase class o,ffers vario,us file o,peratio,ns co,mmo,n to, the file streams.

The fstreambase act as the base o,r super class fo,r fstream, ifstream, and o,fstream file o,peratio,ns.

It also, co,ntains bo,th o,pen() and clo,se() functio,ns.

Ifstream

It is respo,nsible fo,r input o,peratio,ns and has o,pen () as the default input mo,de.

Ifstream inherits get(), getline(),read(), tellg(),and seekg() functio,ns fro,m the istream i/o, system.

o,fstream

o,fstream is respo,nsible fo,r o,utput o,peratio,n and it uses the o,pen() with the default o,utput mo,de.

The class inherits functio,n pro,perties like put(),write(), seekp(), and tellp() fro,m the o,stream.

Fstream

It is respo,nsible fo,r o,ffering suppo,rt fo,r simultaneo,us i/o, o,peratio,ns. it uses o,pen() with its default input mo,de.

Fstream inherits pro,perties fro,m istream and o,stream classes via the io,stream.

A filename co,nsists o,f a string o,f characters making it a valid file name. a filename is divided into, two, parts: the primary name and an extensio,n. fo,r example, file.do,c, test.txt, and input.cpp amo,ng o,ther extensio,ns.

To, o,pen any file, yo,u have to, create a file stream first and then link it to, the filename. the file stream is declared using the ifstream, o,fstream and fstream classes which are included in the fstream header file.

The file class created depends o,n the purpo,se fo,r creatio,n. that is, whether to, read data o,r write data into, the file.

After creatio,n o,f the file, yo,u can o,pen it using:

1.  The co,nstructo,r functio,n in the class.
2.  The member functio,n o,pen() in the class.

o,pening a file using co,nstructo,r functio,n is o,nly applied when o,ne file is being used in the stream, while the o,pen() functio,n metho,d is used when o,pening multiple files using a single stream.

o,pening files using co,nstructo,r

If a co,nstructo,r is used to, o,pen a file, the filename initializes the file stream o,bject. this can be achieved thro,ugh:

1.  Creating a file stream o,bject in o,rder to, manage the stream using an appro,priate class. in this case, yo,u can use o,fstream class to, create o,utput stream while the ifstream class creates an input stream.
2.  Using a desired filename so, as to, initialize the file o,bject. fo,r example, the fo,llo,wing co,de is used to, o,pen a file named perfo,rmance as an o,utput:

o,fstream o,utfile(“perfo,rmance”); // to, display an o,utput.

The o,utfile is created as an o,fstream o,bject who,se main purpo,se is to, manage the o,utput stream.

Yo,u can also, create an infile as an ifstream o,bject and asso,ciate it with the file data fo,r reading file inputs.

**Ifstream infile (“data”);** // an input file

Yo,u can use the same file name to, read o,r write data into, a file.

When an o,bject terminates, it auto,matically clo,ses the co,nnectio,n to, that file. in the abo,ve example o,n perfo,rmance file, when the pro,gram is terminated, the perfo,rmance file will be disco,nnected fro,m the o,utfile stream. this also, happens to, the infile stream.

A filename co,nsists o,f a string o,f characters making it a valid file name. a filename is divided into, two, parts: the primary name and an extensio,n. fo,r example, file.do,c, test.txt, and input.cpp amo,ng o,ther extensio,ns.

To, o,pen any file, yo,u have to, create a file stream first and then link it to, the filename. the file stream is declared using the ifstream, o,fstream and fstream classes which are included in the fstream header file.

The file class created depends o,n the purpo,se fo,r creatio,n. that is, whether to, read data o,r write data into, the file.

After creatio,n o,f the file, yo,u can o,pen it using:

1.  The co,nstructo,r functio,n in the class.
2.  The member functio,n o,pen() in the class.

o,pening a file using co,nstructo,r functio,n is o,nly applied when o,ne file is being used in the stream while the o,pen() functio,n metho,d is used when o,pening multiple file using a single stream.

Example: a pro,gram to, write and read data fro,m a file

#include <io,stream.h>

#include <fstream.h>

Int main()

{

Char pro,dname[20];

Flo,at price;

o,fstream o,utfile(“pro,duct”);

Co,ut <<”enter pro,duct's name:”

Cin >>pro,dname; o,utfile <<pro,dname<<”\n”;

Co,ut <<”enter the pro,duct's price:”;

Cin >>price; o,utfile <<price <<”\n”;

o,utfile.clo,se();

Ifstream infile(“pro,duct”);

Infile >>pro,dname;

Infile >>price;

Co,ut <<”\n”;

Co,ut <<”pro,duct name is : “ << pro,dname <<”\n”;

Co,ut <<”pro,duct price: “ << price <<”\n”;

Infile.clo,se();

Return 0;

}

// o,utput

Pro,duct name is: mango,

Pro,duct price: 25

This pro,gram gets data via the input device like keywo,rd and writes it to, a file. after co,mpletio,n o,f the writing pro,cess, the file is clo,sed. the file is then o,pened to, read the info,rmatio,n already written in the file and later displayed o,n the screen fo,r the user to, view.

Example 2: writing to, a file.

#include <io,stream>

#include <fstream>

Using namespace std;

Int main () {

o,fstream samplefile;

samplefile.o,pen ("sample.do,c");

samplefile << "writing data to, the sample.do,c file.\n";

samplefile.clo,se();

return 0;

}

o,pening files using o,pen() functio,n

The o,pen() functio,n o,pens multiple files that use the same o,bject stream. if a set o,f files are to, be pro,cessed sequentially, then a single o,bject stream is created to, enable o,pening o,f each file.

Syntax

Vo,id o,pen (co,nst char* filename, io,s:: o,penmo,de mo,de);

o,r

o,pen (filename, mo,de);

The first argument indicates the name o,f the file and file fo,rmat to,gether with its address, while the seco,nd part o,f the argument indicates the access mo,de o,f the file.

There are different access mo,des fo,r o,pening a file, and they include:

File mo,de

Descriptio,n

In

It is the default mo,de fo,r ifstream files. it o,pens the file fo,r reading purpo,ses.

o,ut

This mo,de is respo,nsible fo,r writing into, a file.

It is the default mo,de fo,r o,fstream.

Binary

It is used to, o,pen a file in a binary fo,rm o,r mo,de.

App

The app mo,de is suitable fo,r o,pening the file and appends the file o,utputs at the end.

Ate

This mo,de is respo,nsible fo,r o,pening the file and transferring the co,ntro,l to, the end o,f the file.

Trunc

It is used to, delete data fro,m an existing file.

No,create

It tests the existence o,f a file and o,pens it if it exists.

No,replace

If a file do,esn’t exist, no,replace o,pens a new file.

Example:

Fstream example_file;

Example_file.o,pen(example.txt”, io,s::o,ut);

In o,rder to, access the member functio,n o,f fstream class, yo,u have to, create that class. example_file is an o,bject o,f type fstream. calling the o,pen() functio,n allo,ws yo,u to, o,pen the file and write data into, it.

The default o,pen mo,de fo,r the files are:

●  ifstream io,s::in

●  o,fstream io,s::o,ut

●  fstream io,s::in | io,s::o,ut

The symbo,l | is used to, co,mbine different mo,des. fo,r example:

Example_file.o,pen(example.txt”, io,s::o,ut | io,s::ate);

The input mo,de and co,ntro,l mo,de are co,mbined to, ensure the file is o,pened fo,r writing then transfers the co,ntro,l to, the end o,f the file.

When a pro,gram terminates, the allo,cated memo,ry is freed up and all o,pened files are clo,sed. using the clo,se() functio,n ensures all the files are clo,sed as so,o,n as executio,n is co,mplete.

With the stream insertio,n o,perato,r <<, yo,u can write info,rmatio,n into, a file and use the stream extractio,n o,perato,r >> to, read the info,rmatio,n fro,m the file.

Example: o,pening a file using the o,pen () and writing to, the file

#include<io,stream>

#include <fstream>

Using namespace std;

Int main()

{

Fstream example_file;

Example_file.o,pen("example.do,c", io,s::o,ut);

If(!Example_file)

{

Co,ut<<" file creatio,n has failed";

}

Else

{

Co,ut<<"the new file was successfully created";

Example_file<< “this is a new file created”; // writing to, the file

Example_file.clo,se(); // clo,se the file to, free memo,ry

}

Return 0;

}

//o,utput

C:\users\faith\do,cuments>no,tepad++ example.cpp –o, example.exe

C:\users\faith\do,cuments\example.do,c

The new file was successfully created

C:\users\faith\do,cuments>

![00236.jpeg](images/00236.jpeg)

In the abo,ve pro,gram, we have created an o,bject example_file to, be used in the fstream class. then we o,pen the o,bject using the o,pen() functio,n and create a new file named example where to, write data into,. the file is assigned to, o,ut mo,de which allo,ws writing into, the file. if statement test whether the file exists o,r no,t if the file is unavailable “file creatio,n has failed” statement is displayed, o,therwise “the new file was successfully created” message will be displayed o,n the screen.

Example 2: reading info,rmatio,n fro,m file

#include<io,stream>

#include <fstream>

Using namespace std;

Int main()

{

Fstream example_file;

Example_file.o,pen("example.do,c", io,s::in);

If(!Example_file)

{

Co,ut<<" the file do,esn’t exist";

}

Else

{

Char ch;

While (!Example.eo,f())

{example-file>>ch;

Co,ut<<ch;}

Example_file.clo,se(); // clo,se the file to, free memo,ry

}

Return 0;

}

The abo,ve pro,gram reads the example.do,c file we had already created in the previo,us example. to, read a file, the ‘in’ mo,de is used (io,s::in). the extractio,n o,perato,r >> is used to, print the file co,ntent o,f the file.

Finding end o,f file

When reading a file, it’s impo,rtant to, determine the end o,f file, o,therwise the pro,gram will be in an infinite lo,o,p if it do,esn’t detect the end o,f file. the pro,grammer sho,uld pro,vide appro,priate instructio,ns to, the pro,gram so, as to, be able to, detect the end o,f file.

When the end o,f file is determined, the reading data pro,cess can easily be terminated after all the data has been read. if the end-o,f-file is determined, the fin ifstream o,bject will return a zero, value if an erro,r o,ccurs in the file o,peratio,n.

When the fin returns 0 after reaching the end-o,f-the-file, the while lo,o,p will terminate. yo,u can also, detect the end o,f file using the eo,f() functio,n.

if(example.eo,f()!=0)

{exit file}

If the end-o,f-file is detected, a no,n-zero, value is returned, o,therwise if the end-o,f-file is no,t detected, a 0 value is returned. the pro,gram will auto,matically terminate after reaching the end-o,f-file.

File po,inters and manipulato,rs

Each c++ file has two, po,inters: input po,inter and o,utput po,inter. the input po,inter reads the co,ntent o,f a particular file lo,catio,n while the o,utput po,inter writes data to, a given file lo,catio,n. whenever an input o,r o,utput file o,peratio,n takes place, an appro,priate po,inter is updated auto,matically.

Default file actio,ns

When yo,u o,pen a file in a read-o,nly mo,de, the input po,inter is set at the start o,f the file so, as to, enable reading fro,m the start o,f that file. if the file is o,pened in a write-o,nly mo,de, all the file co,ntent is deleted and the o,utput po,inter is placed at the start o,f the file. this ensures that yo,u write the file fro,m the beginning po,int.

To, add mo,re data to, an existing file, the file sho,uld be o,pened in an ‘append’ mo,de. this auto,matically mo,ves the po,inter to, the end o,f the file.

Functio,ns and manipulatio,ns o,f file po,inter

All the actio,ns and file o,peratio,ns using po,inters take place by default. in o,rder to, co,ntro,l file po,inter mo,vement o,peratio,ns, there are vario,us file stream classes yo,u can use. so,me o,f these file stream class member functio,ns include:

●  seekg() this functio,n mo,ves the (input) get po,inter to, a specific lo,catio,n.

●  seekp() the functio,n mo,ves the (o,utput) put po,inter to, a specific lo,catio,n.

●  tellg() this functio,n indicates the get po,inter current po,sitio,n.

●  tellp() it indicates the put po,inter current po,sitio,n.

Example:

Infile.seekg(5);

This functio,n will mo,ve the po,inter to, a number byte labelled 5 since the file bytes are numbered fro,m 0. the po,inter then po,ints to, the 6^(th) byte which is the current lo,catio,n o,f the file.

Example 2:

o,fstream myfile;

Myfile.o,pen(“welco,me”, io,s::app);

Int ppt=myfile.tellp();

When the abo,ve statements are executed, the o,utput po,inter mo,ves up to, the end o,f file “welco,me” and the ppt value indicates the number o,f bytes in the file.

Specifying o,ffset functio,ns

The seek functio,ns (seekg() and seekp()) take two, arguments:

●  seekg (o,ffset, refpo,sitio,n)

●  seekp (o,ffset,refpo,sitio,n)

The o,ffset argument indicates the number o,f bytes to, mo,ve the file po,inter fro,m the specified lo,catio,n by the refpo,sitio,n argument.

The refpo,sitio,n takes the fo,rm o,f:

●  io,s::beg this indicates the start o,f file.

●  io,s::cur indicates the current po,sitio,n o,f the po,inter.

●  io,s::end this indicates the end o,f a file.

The seekg() functio,n mo,ves all the asso,ciated files with the get po,inter. the seekp() mo,ves the file and its asso,ciated files using the put po,inter.

Po,inter o,ffset calls

![00237.jpeg](images/00237.jpeg)

Sequential input and o,utput o,peratio,ns

There are a number o,f member functio,ns fo,r perfo,rming input and o,utput file o,peratio,ns suppo,rted by file stream classes. the member functio,ns put() and get() handle single character o,peratio,ns at a time. the write() and read() functio,ns write into, and read to, a blo,ck o,f binary data.

Put() and get() functio,ns

Yo,u can write a single character into, an asso,ciated stream using the put() functio,n. the get () functio,n reads a single character fro,m the asso,ciated stream. let’s write a pro,gram to, illustrate ho,w the functio,ns wo,rks o,n a pro,gram.

![00238.jpeg](images/00238.jpeg)

The abo,ve pro,gram requests fo,r a string and o,nce it receives the string, it writes o,n the file a character by character using the put () functio,n with fo,r lo,o,p. when the string length ends, the fo,r lo,o,p is terminated.

After the executio,n, the pro,gram is displayed o,n the screen using the get() functio,n. the get() functio,n fetches a character by character data fro,m the file until it reaches the end o,f file co,nditio,n. the data read fro,m the file is displayed o,n the screen fo,r users to, view using the << o,perato,r.

Write() and read() functio,ns

The write () and read() functio,n can handle binary fo,rms o,f data. the data values are sto,red in the disk file using the same fo,rmat used when they’re being sto,red in an internal memo,ry. fo,r example, and int character can sto,re 2 bytes o,f its data value into, a binary fo,rm regardless o,f its size, while a 4 digit integer value can sto,re 4 bytes in character fo,rm.

Binary input and o,utput takes the fo,rm o,f:

![00239.jpeg](images/00239.jpeg)

The functio,n receives two, arguments: the address o,f the variable var, and the length o,f the variable in the fo,rm o,f bytes. the address o,f the variable is represented with type char* (a po,inter to, a character data type).

Example:

![00240.jpeg](images/00240.jpeg)

Erro,r handling during file o,peratio,n

When carrying o,ut vario,us file o,peratio,ns, there are vario,us erro,rs enco,untered. so,me o,f these pro,blems enco,untered include:

●  no,n-existence o,f the file yo,u are trying to, access.

●  the file name being used to, create a new file already exists.

●  attempting an invalid file o,peratio,n like trying to, read data past the end o,f file co,nditio,n.

●  no,t eno,ugh memo,ry in the disk drive to, sto,re mo,re data.

●  dealing with an invalid file name.

These are so,me o,f the co,mmo,n file o,peratio,n pro,blems yo,u may face when handling and manipulating files. file o,peratio,n stream in c++ language inherits the ‘stream-state’ member fro,m the io,s class.

The stream-state member keeps info,rmatio,n o,n the status o,f the current o,pened file. the io,s class suppo,rt a number o,f member functio,ns fo,r reading the file status reco,rded o,n the stream.

Erro,r handling functio,ns

Functio,n

Meaning and its return value

Eo,f()

Eo,f() returns a true value o,r a no,n-zero, value if the end o,f file is successfully detected while reading the file, o,therwise, it will return a zero, value.

Fail()

This functio,ns returns true after the failure o,f bo,th input and o,utput o,peratio,ns.

Bad()

If an attempt o,f an invalid o,peratio,n is enco,untered o,r unreco,verable erro,r, it returns true. if the erro,r can be reco,vered and file o,peratio,n co,ntinues, then it returns false value

Go,o,d()

If no, erro,r has been enco,untered, it will return true. if the file.go,o,d() functio,n returns true, then yo,u can co,ntinue with o,ther i/o, o,peratio,ns.

If it returns false, there are no, further o,peratio,ns are carried o,ut.

**Chapter summary**

Input/o,utput streams are an impo,rtant feature in c++ pro,gramming language. the streams help in class definitio,n and pro,vide a set o,f library functio,ns that perfo,rm a series o,f functio,ns. in this chapter, yo,u learned abo,ut the c++ streams co,ncept and ho,w to, use input and o,utput stream to, execute pro,grams. yo,u also, learned the vario,us devices yo,u can use when wo,rking with vario,us stream input and o,utputs. c++ stream classes will enable yo,u to,:

●  define a hierarchy o,f classes that defines the use o,f streams co,nso,le unit and the disk files.

●  learn ho,w to, declare the i/o, stream classes in the header file as well as learn the vario,us co,nso,le o,peratio,ns using the stream classes.

●  learn different types o,f class names and their pro,perties and functio,nalities.

●  learn ho,w io,s class pro,vide basic suppo,rt fo,r i/o, o,peratio,ns o,n bo,th unfo,rmatted i/o, o,peratio,n and fo,rmatted i/o, o,peratio,ns.

●  use the o,verlo,aded o,perato,rs (>>&<<) used fo,r data inputs and o,utputs. the cin standard library functio,ns use the o,verlo,aded o,perato,rs >> to, read data fro,m an input device. while co,ut standard library functio,n o,perato,r << is used to, display data o,n the screen o,r o,utput device.

●  use unfo,rmatted i/o, o,peratio,ns like put() and get() functio,ns. the put() functio,n is a member o,f o,stream class which is used to, o,utput data character by character, while the get() functio,n wo,rks as input stream.

●  learn ho,w to, use getline () and write() functio,ns.

●  learn vario,us fo,rmatted co,nso,le i/o, o,peratio,ns suppo,rted by c++ language to, fo,rmat the o,utput.

●  use io,s class functio,ns and flags to, fo,rmat data inputs.

●  ho,w to, use user-defined o,utput functio,ns o,r the use o,f o,utput manipulato,rs and o,ther fo,rmatting features o,f io,s class functio,ns to, fo,rmat the o,utput.

●  learn ho,w to, use user-defined functio,ns to, fo,rmat o,utput.

●  learn ho,w to, manage o,utput with manipulato,rs.

●  perfo,rm vario,us file o,peratio,ns and kno,w ho,w to, handle stream classes.

●  kno,w ho,w to, o,pen files using co,nstructo,rs and using o,pen () functio,n, create new files and ho,w to, write into, a file.

●  use c++ to, write a co,de o,n ho,w to, o,pen a file, write a co,de o,f ho,w to, write into, an existing file o,r creating a new file, as well as write a co,de o,f reading info,rmatio,n fro,m a file.

●  use the clo,se () member functio,n which is added in every file co,de to, clo,se the file.

●  learn ho,w to, co,ntro,l input o,utput streams thro,ugh the use o,f classes. bo,th istream and o,stream co,ntro,l the input and o,utput functio,ns.

●  using wo,rking examples, derive an io,stream class fro,m the istream and o,stream classes. o,ther classes derived in i/o, streams include: istream_withassigh.o,stream_withassign and io,stream_withassign. these classes are derived fro,m the pro,perties o,f istream, o,stream, and io,stream classes respectively.

●  use eo,f () functio,n to, test whether the end o,f file is reached and it returns value 1 if it’s detected. yo,u’re able to, write a co,de that determines the end-o,f-file, ho,w to, use the clo,se() functio,n to, terminate a pro,gram, and use o,f po,inters to, manipulate files.

●  use seekg() functio,n links to, the asso,ciated file po,inter (bo,th input and o,utput file po,inter).

●  write co,des using the put() and get() functio,ns which reads and writes a single character in a file while the write() and read() are used fo,r writing and reading a blo,ck o,f binary data.

●  kno,w ho,w to, ho,w to, handle erro,rs during file o,peratio,ns.

In the next chapter yo,u will learn abo,ut exceptio,n handling. by the end o,f the chapter, yo,u will understand the co,ncept and principles o,f exceptio,n handling, mechanisms o,f exceptio,n handling, and the use o,f thro,w and catch exceptio,ns mechanisms.

## Chapter nine: exceptio,n handling

Intro,ductio,n

Exceptio,n handling pro,vides yo,u with a way to, create and deal with the erro,rs that o,ccur during the pro,gram develo,pment pro,cess, such as run time erro,rs. this is achieved by transferring the co,ntro,l o,f the pro,gram to, a special functio,n called handlers.

During the pro,gram develo,pment pro,cess, there are cases where the pro,grammer is uncertain whether a piece o,f co,de will run successfully o,r no,t due to, run time erro,rs like limited reso,urce allo,catio,n o,r o,ut o,f range erro,rs.

To, so,lve this pro,blem, yo,u have to, place the piece o,f co,de under the exceptio,n inspectio,n. this is achieved by enclo,sing the piece o,f co,de in a try blo,ck. when an exceptio,nal circumstance arises within that blo,ck o,f co,de, then an exceptio,n is thro,wn that transfers the co,ntro,l to, the exceptio,n handler.

If there are no, exceptio,n detected o,r thro,wn, then the pro,gram co,de co,ntinues to, execute no,rmally and the handlers created are igno,red.

When the pro,gram co,de enco,unters an exceptio,nal co,nditio,n, it’s impo,rtant to, identify the exceptio,n and deal with it effectively. an exceptio,n is that part o,f an o,bject that o,ccurs whenever an erro,r is enco,untered o,n that part o,f the pro,gram.

Principles o,f exceptio,n handling

Exceptio,n handling is a mechanism fo,r detecting and repo,rting exceptio,nal circumstances in a pro,gram to, ensure an appro,priate actio,n is implemented. exceptio,n handling mechanism invo,lves:

1.  Detecting the exceptio,ns (pro,blem).
2.  Thro,wing the exceptio,n (ackno,wledge the erro,r has o,ccurred).
3.  Catching the exceptio,n (receive detail info,rmatio,n o,n the erro,r).
4.  Handling the exceptio,ns (taking co,rrective actio,ns to, so,lve the pro,blem).

An exceptio,n handling mechanism sho,uld have two, segments: o,ne segment to, detect the erro,r and thro,w exceptio,ns while the o,ther segment will catch the exceptio,ns and take up appro,priate measures to, handle the erro,rs.

There are two, types o,f exceptio,ns; synchro,no,us and asynchro,no,us exceptio,ns. synchro,no,us exceptio,ns are enco,untered during pro,gram run-time due to, pro,gram ano,malies, and they include o,ut o,f range index erro,r and o,verflo,w erro,r. o,ccurrence o,f events beyo,nd the pro,gram co,ntro,l results in asynchro,no,us exceptio,ns. an example o,f asynchro,no,us exceptio,ns is keybo,ard interrupts.

Exceptio,n handling mechanisms

Exceptio,n handling is built o,n three keywo,rd o,perato,rs:

1.  Try.
2.  Thro,w.
3.  Catch.

The try keywo,rd prefaces a blo,ck o,f statements in o,rder to, generate exceptio,ns. the blo,ck o,f statements is kno,wn as the try blo,ck. o,nce an exceptio,n is detected it is thro,wn using the thro,w keywo,rd inside the try blo,ck statements. exceptio,n handlers are defined by the use o,f the catch keywo,rd that catches an exceptio,n thro,wn using the thro,w statement in the try blo,ck. the catch blo,ck statements must appear immediately after the try blo,ck.

Syntax

Try

{

//blo,ck o,f statements to, be tried

Thro,w exceptio,n

}

Catch (type arguments)

{

Co,de to, be executed in case o,f exceptio,n

}

When an exceptio,n is thro,wn in the try blo,ck, the pro,gram co,ntro,l is transferred fro,m the try blo,ck into, the catch statement. if the thro,wn o,bject type matches the arguments type in the catch blo,ck, then the catch statements to, handle exceptio,ns is executed.

If the o,bject arguments do,n’t match, the pro,gram is abo,rted using abo,rt () functio,n. if no, exceptio,n is detected o,r thro,wn, then the co,ntro,l is taken back immediately using the catch blo,ck.

Example:

#include <io,stream.h>

Using namespace std;

Int main()

{

try

{

thro,w 15;

}

catch(int a)

{

co,ut<< "an exceptio,n has o,ccurred"; <<endl;

}

return 0;

}

If there is no, exceptio,n thro,wn, the catch statements will no,t be executed.

Example:

![00241.jpeg](images/00241.jpeg)

// o,utput

![00242.jpeg](images/00242.jpeg)

Thro,w mechanism

When an exceptio,n is detected, it is thro,wn using the fo,llo,wing co,mmand:

![00243.jpeg](images/00243.jpeg)

The exceptio,n o,bject thro,wn may be o,f any fo,rm, even co,nstants. o,ther o,bjects no,t intended fo,r erro,r handling can also, be thro,wn. if an exceptio,n is thro,wn, a catch statement will be able to, catch it. the pro,gram co,ntro,l will be transferred fro,m the try blo,ck into, the catch blo,ck.

Catching mechanisms

The exceptio,n handler will have a co,de in the catch blo,ck. the catch blo,ck is a functio,n o,n its o,wn and it’s  used to, manage exceptio,ns.

![00244.jpeg](images/00244.jpeg)

The type is used to, indicate the type o,f exceptio,n handled by the catch blo,ck. the arguments are o,ptio,nal. the catch statement catches exceptio,ns with type that matches the catch parameter. after the exceptio,n is caught, the blo,ck co,de inside the catch blo,ck is executed. when the handler is executed, the co,ntro,l is passed immediately. if the catch statements do,esn’t catch the exceptio,n then the catch blo,ck statements will be skipped.

**Chapter summary**

Exceptio,ns are vario,us erro,rs a pro,gram may enco,unter during its running time. c++ pro,gramming language has a built-in language functio,n fo,r trapping all pro,gram erro,rs and co,ntro,l exceptio,ns. the latest c++ co,mpiler suppo,rts this feature making it easy fo,r the user to, debug a pro,gram.

●  an exceptio,n acts as an o,bject which is sent fro,m the part o,f the pro,gram where an erro,r has o,ccurred to, the part o,f the pro,gram where the erro,r will be co,ntro,lled.

●  exceptio,n metho,d is do,ne via the use o,f three keywo,rds: try, thro,w and catch. the try keywo,rd is fo,r detecting an exceptio,n in the file and the exceptio,n statements kno,wn as try blo,ck is enclo,sed within curly braces.

●  the catch blo,ck receives the exceptio,n sent by the thro,wing blo,ck inside the try blo,ck.

●  yo,u can create multiple catch blo,cks within a pro,gram o,r even pass the exceptio,n to, ano,ther exceptio,n handler.

●  specified exceptio,ns are great fo,r binding functio,ns to, thro,w o,nly co,nditio,n fo,r a specified exceptio,n.

## Final wo,rds

C++ pro,gramming language is a co,mpetitive general purpo,se pro,gram which bo,rro,ws so,me features o,f imperative pro,gramming paradigm and can run o,n any platfo,rm. it is referred to, as an imperative pro,gramming language because it uses step by step pro,cesses in o,rder to, achieve its go,als. the pro,gram uses the co,ncept o,f o,bject o,riented pro,gram to, design and implement co,mplex pro,grams.

The pro,gram revo,lves aro,und data which is created using o,bjects. these o,bjects co,mmunicate with each o,ther by passing messages. the o,bjects do,n’t have to, kno,w the detail info,rmatio,n o,f ano,ther o,bject so, as to, exchange data between them. they o,nly need to, establish a co,nnectio,n between themselves and exchange info,rmatio,n.

C++ pro,gramming language utilizes the features o,f o,o,p paradigms to, develo,p and execute a pro,gram. so,me o,f these features include: use o,f o,bjects, classes, data abstractio,ns and encapsulatio,n, inheritance and po,lymo,rphism.

The pro,gram fo,cuses o,n the use o,f data rather than pro,cedures to, so,lve real wo,rld pro,blems. the pro,gram tries to, eliminate the sho,rtco,mings o,f o,ther co,nventio,nal pro,gramming languages by impro,ving the data security o,f pro,grams, pro,mo,ting co,de reusability and its ability to, use inheritance feature to, make an effective pro,gram.

Just like many o,ther o,o,p languages, c++ suppo,rts vario,us building blo,cks. in this tuto,rial, yo,u have learned ho,w to, use vario,us built-in data types when handling simple to, co,mplex pro,grams. the data types are divided into, primitive data types, derived data types, and abstract data types. yo,u no,t o,nly learned ho,w to, use the primitive o,r standard data types, but also, ho,w to, declare yo,ur o,wn user-defined datatypes.

Yo,u learned ho,w to, create arrays fo,r sto,ring values, and ho,w yo,u can access variables created using arrays. yo,u also, learned ho,w to, initialize arrays and ho,w to, wo,rk with different types o,f arrays.

Po,inters play an impo,rtant ro,le in the allo,catio,n o,f memo,ry space to, the user pro,grams. when declaring variables, a memo,ry space is allo,cated fo,r the variable. each variable has a defined memo,ry address fo,r accessing the variable. therefo,re, in this tuto,rial, yo,u learned ho,w to, create pro,grams that assign the memo,ry address to, the po,inter variable. yo,u also, learned ho,w to, use dynamic free sto,re o,perato,rs like new and delete o,perato,r to, allo,cate and deallo,cate memo,ry space. the co,mputer memo,ry is a limited reso,urce, therefo,re, yo,u have to, free the memo,ry when a pro,gram no, lo,nger needs it and allo,cate that memo,ry space to, ano,ther pro,gram that needs it.

Yo,u also, learned ho,w to, use library functio,ns and user-defined functio,ns in develo,ping pro,grams. the library functio,ns are pre-defined o,r built-in c++ functio,ns which perfo,rm a number o,f tasks. c++ also, allo,w users to, define their o,wn functio,ns and write a blo,ck o,f statements to, be executed o,nce the functio,n is invo,ked. in this tuto,rial, yo,u learned ho,w to, create yo,ur o,wn functio,n, functio,n definitio,n and declaratio,n. yo,u are also, able to, learn ho,w to, call functio,ns and pass parameters to, a functio,n. yo,u’re able to, kno,w ho,w to, use functio,n pro,to,type, and use inline functio,ns in a pro,gram.

Ano,ther impo,rtant feature yo,u learned abo,ut is ho,w to, o,rganize different data elements and variables into, a single unit using structures. yo,u learned ho,w to, initialize a structure element, ho,w to, access the structure memo,ry and ho,w to, use references.

In chapters two, and three, yo,u learned the basic co,ncepts in o,o,p and ho,w to, wo,rk with classes and o,bjects. yo,u’re no,w able to, define a class and declare class members either private, public, o,r pro,tected. defining the class header files will allo,w yo,u to, reuse the co,de in vario,us files. the class definitio,n is put in a header file with the same name as the class. the member functio,ns are sto,red o,utside the class and sto,red with the same name as the class.

Yo,u are no,w able to, create class o,bjects and define bo,th private and public access specifiers, define data members and member functio,ns, and use pro,tected data members. c++ presents different types o,f class member functio,ns which can be utilized to, manipulate data. learning ho,w to, use each o,f the data members will make it easy to, mo,dify data files and make calls to, the member functio,ns.

Classes can be created in two, fo,rms in c++ pro,gramming language: using a base class o,r using a derived class. the base class allo,ws yo,u to, build o,ther classes fro,m it while a derived class inherits the pro,perties and characteristics o,f the base class. yo,u’re no,w able to, create a base class and derived class and extend the class functio,nality using o,verriding members.

In chapter 4, we discussed inheritance. that is, ho,w to, derive a new class fro,m an existing class. in inheritance, a class bo,rro,ws the members o,f o,ther classes so, as to, avo,id any repetitio,ns. when inheriting members, the public members o,f the base class will remain public while the pro,tected members will remain pro,tected, while the private members will remain private in the derived class.

There are different types o,f inheritance users can define and these include: single inheritance, multiple inheritance, hierarchical inheritance, multi-level inheritance, and hybrid inheritance.

Yo,u are no,w able to, create o,bjects using co,nstructo,rs and destructo,rs o,f derived o,bjects. the co,nstructo,rs will help in initializing member variables while the destructo,r will destro,y the o,bject and free up memo,ry space.

During a pro,gram executio,n, the co,mpiler auto,matically calls fo,r the co,nstructo,r and destructo,r variables. co,nstructo,rs and destructo,rs can be used in the base class and also, in the derived class. when the co,nstructo,r is used in the derived class, the arguments will be passed to, the base class.

Upcasting is ano,ther feature which utilizes the use o,f base class reference o,r a po,inter to, po,int directly to, a subclass. in this chapter, yo,u are able to, learn ho,w to, use upcasting and do,wncasting features to, create a base class.

C++ allo,ws yo,u to, dynamically allo,cate memo,ry space to, pro,grams. yo,u can allo,cate the memo,ry space to, a pro,gram by initially defining the pro,gram variables befo,re the pro,gram executes. in such a case, the memo,ry is determined during run-time o,r based o,n the user inputs. dynamically, allo,catio,n is achieved thro,ugh the use o,f new and delete o,perato,rs.

The new o,perato,r fo,llo,wed by the data type specifier auto,matically allo,cates memo,ry space to, the file. it allo,ws yo,u to, allo,cate memo,ry to, an array o,f elements using the new[] o,perato,r. the delete o,perato,r deallo,cates the memo,ry thus making the memo,ry available fo,r o,ther pro,grams when dealing with multiple elements the delete [] o,perato,r is used to, deallo,cate memo,ry space. if yo,u create a memo,ry and fo,rget to, delete it, it creates a memo,ry leak. therefo,re, any memo,ry created o,n the heap sho,uld be freed when no, lo,nger in use to, avo,id creating a memo,ry leak.

Po,lymo,rphism is an o,o,p feature that enables yo,u to, have an o,bject with mo,re than o,ne fo,rm. creating multiple inheritance in a class results in po,lymo,rphism. po,lymo,rphism is divided into, two,: run-time po,lymo,rphism and co,mpile time po,lymo,rphism. run-time po,lymo,rphism is achieved by use o,f o,verlo,ading functio,ns and virtual functio,ns, while co,mpile time po,lymo,rphism is achieved via o,verriding functio,n and o,perato,r o,verlo,ading. yo,u no,w have practical kno,wledge abo,ut ho,w to, create virtual functio,ns, o,verlo,ading functio,ns, and o,verriding functio,ns. yo,u also, learned ho,w to, access the private member functio,n in a derived class using virtual keywo,rd and ho,w to, create abstract classes and pure virtual functio,ns.

In chapter six, we discussed ho,w co,nstructo,rs and destructo,rs wo,rk, characteristics o,f co,nstructo,rs, ho,w to, define and declare a co,nstructo,r class, and wo,rking with different types o,f co,nstructo,rs. we also, discussed in class destructo,r and ho,w to, declare a class destructo,r.

Templates allo,ws functio,ns and classes to, use generic type. this plays an impo,rtant ro,le o,n ho,w functio,ns and classes wo,rk by allo,wing users to, define different data types witho,ut the need o,f rewriting the co,de. a template allo,ws yo,u to, create a generic class which suppo,rts any data type. there are two, main types o,f templates: functio,n templates and class templates.

A class template wo,rks like a no,rmal class with a prefix ‘template’ fo,llo,wed by the class identifier. class templates accept members with any type o,f arguments. these templates are mo,stly used in implementing co,ntainers.

Yo,u can also, create a derived class fro,m the class template thro,ugh a pro,cess kno,wn as instantiatio,n. the derived class is kno,wn as template class. yo,u can also, pass multiple parameters to, a class template. a multiple parameter class template suppo,rts mo,re than o,ne generic data type. the generic type classes are separated by co,mmas.

Functio,n templates acco,mmo,date multiple data types co,mpared to, the no,rmal functio,n which o,nly acco,mmo,dates a single data type. templates allo,w yo,u to, o,verlo,ad a no,rmal functio,n with different data types. this makes them mo,re useful since yo,u o,nly have to, write a single pro,gram that can wo,rk with all data types. in this tuto,rial, yo,u learned to, create templates with multiple parameters, ho,w to, use o,verlo,ading template functio,ns and ho,w to, create member functio,n templates.

This pro,gramming language suppo,rts a lo,t o,f libraries which are used in perfo,rming the input and o,utput functio,ns. the input o,utput o,peratio,ns are perfo,rmed using a series o,f bytes kno,wn as streams. this chapter discusses the input o,utput streams used in running the pro,gram effectively. a stream acts as a sequence o,f bytes fo,rming the so,urce and destinatio,n o,f input o,utput data. the so,urce stream supplies data to, a pro,gram thro,ugh the use o,f an input device while the destinatio,n stream is used to, receive an o,utput fro,m the pro,gram.

Input/o,utput o,peratio,ns are implemented thro,ugh the use o,f streams co,ncepts and stream classes. these stream classes are declared in the header file o,f the io,stream. c++ stream classes act as a lo,gical device that accepts data inputs and displays o,utput. streams are i/o, o,peratio,ns which can wo,rk in any device. the streams acts as bo,th the so,urce and the destinatio,n.

Stream classes co,nsists o,f a hierarchy o,f classes which define streams fo,r handling the system co,nso,le unit and the disk files. stream classes perfo,rm bo,th input and o,utput o,peratio,ns. the io,s class is the base class fo,r the input stream while o,stream acts as the o,utput stream. there are different class streams yo,u can use to, manipulate yo,ur files.

o,verlo,aded o,perato,rs >> and << are used fo,r bo,th input and o,utput o,peratio,ns. the input o,perato,r >> uses the standard cin library to, access input data. the o,utput o,perato,r << is used to,gether with co,ut to, display the co,ntent. the >> o,perato,r is o,verlo,aded in an istream while << is o,verlo,aded in an o,stream.

Yo,u can define the put () and get() functio,ns to, handle input/o,utput o,peratio,ns o,n a single character. o,ther functio,ns which can be used to, handle class streams include the use o,f getline() and write () functio,ns. line o,riented i/o, functio,ns like getline() and write() helps yo,u to, easily read and write into, a line o,f text.

The header file io,manip pro,vides a wide set o,f standard functio,n manipulato,rs which manipulate an o,utput fo,rmat. there are also, vario,us fo,rmat co,nso,les yo,u can use to, fo,rmat data o,utput. these fo,rmatted co,nso,les include the use o,f io,s class functio,n and flags o,r the use o,f user-defined functio,ns. yo,u also, learned abo,ut vario,us file o,peratio,ns and using file stream classes.

The file o,peratio,ns wo,rk similarly to, the co,nso,le i/o, o,peratio,ns. so,me o,f the file o,peratio,ns yo,u no,w understand are ho,w to, o,pen files, write files, read fro,m files, and clo,se a file. when o,pening files, yo,u can use co,nstructo,rs o,r use o,pen () functio,n. the file o,pen() functio,n wo,rks within a set o,f file stream classes like fstreambase, ifstream, and o,fstream. the eo,f() functio,n is used to, detect the end o,f the file. when the end o,f file is detected the pro,gram is terminated.

Each file created has two, types o,f po,inters: the input po,inter and the o,utput po,inter. the input file po,inter reads the co,ntents o,f the file while the o,utput po,inter is used to, write into, the file. whenever an i/o, o,peratio,n takes places, the specific file po,inter is activated auto,matically. there are also, vario,us functio,ns yo,u can use to, manipulate file po,inters like the seekg() functio,n. o,ther functio,ns used to, manipulate files include write() and read() functio,n which write and read a blo,ck o,f binary data while put() and get() functio,ns are used to, read and write a single character.

Lastly, yo,u learned ho,w to, handle erro,rs during file o,peratio,ns and ho,w to, handle exceptio,ns in a pro,gram. the exceptio,n handling mechanism invo,lves use o,f three keywo,rds: try, thro,w and catch exceptio,ns to, allo,w to, detect ano,malies, thro,w exceptio,ns, and co,me up with appro,priate measures to, handle the exceptio,ns.

## **references**

[Http://www.cplusplus.co,m/do,c/tuto,rial/dynamic/](http://www.cplusplus.com/doc/tutorial/dynamic/)

[Https://co,descracker.co,m/cpp/cpp-data-structures.htm](https://codescracker.com/cpp/cpp-data-structures.htm)

[Https://www.edureka.co,/blo,g/dynamic-memo,ry-allo,catio,n-cpp/](https://www.edureka.co/blog/dynamic-memory-allocation-cpp/)

[Https://www.edureka.co,/blo,g/inline-functio,n-in-cpp/](https://www.edureka.co/blog/inline-function-in-cpp/)

[Https://www.geeksfo,rgeeks.o,rg/c-classes-and-o,bjects/](https://www.geeksforgeeks.org/c-classes-and-objects/)

[Https://www.geeksfo,rgeeks.o,rg/o,bject-o,riented-pro,gramming-in-cpp/](https://www.geeksforgeeks.org/object-oriented-programming-in-cpp/)

[Https://www.pro,gramiz.co,m/cpp-pro,gramming/functio,n](https://www.programiz.com/cpp-programming/function)

[Https://www.so,ftwaretestinghelp.co,m/data-structures-in-cpp/](https://www.softwaretestinghelp.com/data-structures-in-cpp/)

[Https://www.studyto,night.co,m/cpp/functio,n-o,verriding.php](https://www.studytonight.com/cpp/function-overriding.php)

[Https://www.studyto,night.co,m/cpp/o,rder-o,f-co,nstructo,r-call.php](https://www.studytonight.com/cpp/order-of-constructor-call.php)

[Https://www.studyto,night.co,m/cpp/types-o,f-member-functio,n.php](https://www.studytonight.com/cpp/types-of-member-function.php)

[Https://www.tuto,rialspo,int.co,m/cplusplus/cpp_arrays.htm](https://www.tutorialspoint.com/cplusplus/cpp_arrays.htm)

[Https://www.w3scho,o,ls.in/cplusplus-tuto,rial/co,nstructo,rs-destructo,rs/](https://www.w3schools.in/cplusplus-tutorial/constructors-destructors/)

Image credit: geeksfo,rgeeks.co,m

Image credit: studyto,night.co,m