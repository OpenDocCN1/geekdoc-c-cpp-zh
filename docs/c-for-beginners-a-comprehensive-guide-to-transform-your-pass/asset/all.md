C++ for beginners

A comprehensive guide to transform your passion into programming proficiency

Vera poe

Copyright © [2024] by [vera poe] all rights reserved.

No portion of this book may be reproduced in any form without written permission from the publisher or author, except as permitted by u.s. Copyright law.

This publication is designed to provide accurate and authoritative information in regard to the subject matter covered. It is sold with the understanding that neither the author nor the publisher is engaged in rendering legal, investment, accounting or other professional services. While the publisher and author have used their best efforts in preparing this book, they make no representations or warranties with respect to the accuracy or completeness of the contents of this book and specifically disclaim any implied warranties of merchantability or fitness for a particular purpose. No warranty may be created or extended by sales representatives or written sales materials. The advice and strategies contained herein may not be suitable for your situation. You should consult with a professional when appropriate. Neither the publisher nor the author shall be liable for any loss of profit or any other commercial damages, including but not limited to special, incidental, consequential, personal, or other damages.

Table of contents

[Introduction](#index_split_003.html_id_Toc158309533)

[Chapter 1: anatomy of c++](#index_split_004.html_id_Toc158309534)

[Chapter 2: declaring constants](#index_split_006.html_id_Toc158309535)

[Chapter 5: operator type and overloading](#index_split_009.html_id_Toc158309536)

[Chapter 6: macros and template](#index_split_010.html_id_Toc158309537)

[Chapter 7: classes](#index_split_012.html_id_Toc158309538)

[Chapter 8: library](#index_split_014.html_id_Toc158309539)

[Chapter 9: stl](#index_split_016.html_id_Toc158309540)

[Conclusion](#index_split_017.html_id_Toc158309541)

## Introduction

Welcomea  btoa  bthea  bwonderfula  bworlda  bofa  bprogramming,a  bthea  bchaptersa  bcontaineda  bina  bthisa  bbooka  bwilla  bgivea  byoua  baa  bbasica  bunderstandinga  bofa  bprogramminga  bina  bc++.a  bbya  bitsa  bfinala  bchapter,a  byoua  bwilla  bbea  bablea  btoa  bcreatea  baa  bcompletea  bprograma  bona  byoura  bown,a  businga  bc++.

Thisa  bguidea  bisa  baimeda  bata  bnewcomersa  btoa  bc++.a  bif,a  bhowever,a  byoua  barea  bentirelya  bnewa  btoa  bprogramming,a  bia  brecommenda  bfirsta  breadinga  boura  bprimera  btoa  bprogramming.a  bita  bcoversa  balla  bthea  bconcepts,a  bterms,a  bprogramminga  bparadigms,a  banda  bcodinga  btechniquesa  bthata  baa  bcompletea  bnovicea  bneedsa  btoa  bknow.

Thisa  bguidebooka  bisa  bgoinga  btoa  btakea  bsomea  btimea  btoa  blooka  bovera  balla  bofa  bthea  bthingsa  bthata  bwea  bcana  bdoa  bwitha  bthea  bc++a  blanguage,a  banda  bhowa  bbeneficiala  blearninga  bthisa  blanguagea  bcana  bbe.

Thisa  bobject-orienteda  bprogramminga  bcoursea  bina  bc++a  blanguagea  bpresentsa  blearnersa  bwitha  bthea  bconceptsa  banda  btechniquesa  bnecessarya  btoa  bdesign,a  bdevelopa  banda  bimplementa  baa  brobusta  bprograma  bmodela  beffectively.a  basa  baa  blearner,a  byoua  bwilla  bbea  bablea  btoa  bgraspa  bpracticala  bknowledgea  bona  bhowa  btoa  bapplya  bthea  bfundamentala  bconceptsa  bofa  bobject-orienteda  banalysisa  banda  bdesigna  banda  bsolvea  bvariousa  bproblemsa  bina  byoura  bdaya  btoa  bdaya  bactivities.

C++a  bisa  baa  bcomputera  bprogramminga  blanguagea  bwidelya  buseda  bfora  bgeneral-purposea  bprogramming.a  bita  bisa  bana  bextensiona  bofa  bc-language.a  bthea  bbasica  bunderstandinga  bofa  bc++a  bcana  bbea  bacquireda  bfroma  bc.a  bthat’sa  bwhya  bbotha  bcomputera  blanguagesa  barea  brepresenteda  basa  bc/c++.a  bbjarnea  bstroustrupa  bdevelopeda  bthisa  bmulti-paradigma  blanguagea  bina  b1979.

Ina  btoday’sa  bworld,a  bmanya  boperatinga  bsystemsa  busea  bc++a  basa  btheira  bbasica  blanguage.a  bsomea  bsystema  bdrivers,a  bbrowsers,a  banda  bgamesa  barea  bbaseda  bona  bc++a  bprograms.a  bita  bisa  baa  bfreea  bform,a  bcompiled,a  banda  bstaticallya  btypeda  bprogramminga  blanguage.a  bmanya  bprofessionalsa  bbelievea  bthata  bc++a  bisa  bthea  bmosta  befficienta  blanguagea  btoa  bachievea  bthea  bdesireda  bresults.

Learninga  bcodea  bisa  bultimatelya  bthea  blanguagea  bofa  bthea  bfuture.a  bwea  bhavea  balla  bhearda  bsomethinga  bclosea  btoa  bthata  bata  bsomea  bpointa  bina  boura  blives.

Bya  bthea  btimea  byoua  breacha  bthea  bend,a  byoua  bshoulda  bhavea  bnoa  bproblema  breadinga  bc++a  bcodea  banda  bwritinga  bprogramsa  bthata  barea  bbotha  binterestinga  banda  buseful.a  bso,a  blet’sa  bdivea  bina  banda  blearna  bc++.

## Chaptera  b1:a  banatomya  bofa  bc++

Introductiona  btoa  bprogramminga  blanguages

Asa  byoua  balreadya  bknow,a  bthea  bprograma  bisa  bnothinga  bbuta  baa  bseta  bofa  binstructions.a  bthesea  binstructionsa  barea  bexecuteda  bbya  bthea  bhardware,a  bwhicha  bisa  bthea  bphysicala  bcomputera  bmachinery.a  bthougha  bmoderna  bcomputersa  barea  bfast,a  btheya  bhavea  btheira  blimitations.a  bcomputersa  bcana  bonlya  bunderstanda  baa  bseta  bofa  binstructionsa  bgivena  bina  btheira  bnativea  blanguage.a  bfora  bthis,a  byoua  bshoulda  bunderstanda  bthea  bconceptsa  bofa  bmachinea  blanguage,a  bassemblya  blanguage,a  banda  bhigh-levela  blanguages.

Machinea  blanguage

Thougha  bcomputersa  barea  bverya  badvanceda  bmachines,a  btheya  bcannota  bunderstanda  blanguagesa  blikea  bc++a  bdirectly.a  baa  bcomputera  bonlya  bunderstandsa  b0sa  banda  b1s.a  btheya  barea  bcalleda  bbits.a  banda  btheya  bcana  bonlya  bunderstanda  binstructionsa  bgivena  bina  bthea  bbinarya  bformat.a  beverya  bseta  bofa  binstructionsa  bthata  bwea  bgivea  btoa  bsleepa  byoua  barea  btranslateda  bintoa  baa  bseta  bofa  binstructionsa  bthata  btella  bthea  bprocessora  btoa  bdoa  baa  bparticulara  bjob.a  byoua  bshoulda  bunderstanda  bthata  bdifferenta  btypesa  bofa  bprocessorsa  bhavea  bdifferenta  btypesa  bofa  binstructiona  bsets.a  bfora  bexample,a  bthea  bpentiuma  bprocessorsa  bwilla  bonlya  bunderstanda  btheira  binstructionsa  bset.a  bita  bisa  baa  bsimilara  bcasea  bwitha  bmacintosh.a  bina  bthea  bverya  bbeginning,a  bprogrammersa  bhada  btoa  bwritea  btheira  binstructionsa  bina  bthea  bbinarya  blanguage.a  bita  bwasa  bverya  btime-consuminga  banda  bchallenging.a  bluckily,a  bwea  bdon’ta  bhavea  btoa  bgoa  bthrougha  balla  bofa  bthat.

Assemblya  blanguage

Asa  bthea  bmachinea  blanguagea  bisa  btougha  btoa  bdeala  bwith,a  baa  bnewa  blanguagea  bcalleda  bthea  bassemblya  blanguagea  bwasa  binvented.a  bherea  beverya  binstructiona  bisa  bgivena  baa  bshorta  bname,a  banda  bthea  bvariablesa  barea  breplaceda  bbya  bnamesa  banda  bnota  bbya  bbinarya  bdigits,a  bmakinga  bita  beasya  bfora  baa  bprogrammera  btoa  bwritea  bcode.a  byoua  bmaya  baska  bhowa  byoua  bcana  bunderstanda  banda  bassemblya  blanguage.a  bita  bcannot.a  bthea  bassemblya  blanguagea  bwilla  bbea  bconverteda  bintoa  bmachinea  blanguagea  bwitha  bthea  bhelpa  bofa  bana  bassembler.a  byoua  bshoulda  bremembera  bthata  beacha  bcpua  bhasa  bitsa  bassemblya  blanguage.a  bso,a  bthea  bassemblya  blanguagea  bofa  baa  bcpua  bcannota  bbea  bruna  bona  baa  bdifferenta  bcpu.a  bevena  bassemblya  blanguagea  bhasa  bgota  bitsa  bdrawbacks.a  btheya  brequirea  blargea  bsetsa  bofa  binstructions,a  bevena  bfora  bsimplea  btasks.

High-levela  blanguage

Thea  bhigh-levela  bprogramminga  blanguagesa  bcamea  bintoa  bexistencea  btoa  bsolvea  bthosea  bproblemsa  bthata  bthea  bassemblya  banda  bmachinea  blanguagesa  bwerea  bcausing.a  bthesea  bcana  bruna  bona  banya  bcomputer.a  bhigh-levela  blanguagesa  bcomea  bwitha  baa  bprograma  bcalleda  baa  bcompiler.a  bthea  brolea  bofa  baa  bcompilera  bisa  btoa  bgeneratea  bana  bexecutablea  bfilea  bora  baa  bprograma  bthata  baa  bcpua  bcana  bdirectlya  bunderstand.a  bthesea  bprogramsa  barea  bstandalonea  bprograms.a  bthea  bmoderna  bcompilersa  bthata  barea  bavailablea  btodaya  barea  bverya  befficienta  banda  bfasta  banda  bconvertinga  bthea  bcodea  bintoa  bana  bexecutablea  bformat.a  bsomea  bofa  bthea  bprogramminga  blanguagesa  busea  bthea  binterpreter.a  bthea  bjoba  bofa  bana  binterpretera  bisa  btoa  bexecutea  bthea  bcodea  bbuta  bwithouta  bcompilinga  bita  btoa  bthea  bmachinea  bcode.a  bbuta  bherea  bwea  bwon’ta  blearna  babouta  bana  binterpreter.a  banya  bgivena  bprogramminga  blanguagea  bcana  bbea  binterpreteda  bora  bcompiled.a  blanguagesa  blikea  bc,a  bc++,a  banda  bpascala  barea  bcompileda  bwhilea  bscriptinga  blanguagesa  blikea  bjavascripta  banda  bperla  barea  binterpreted.

Aska  bthisa  bquestion,a  banda  byoua  bwilla  bgeta  baa  bdozena  bdifferenta  banswers,a  bbut,a  bputa  bsimply,a  bc++a  bisa  baa  bcompiled,a  bobject-orientateda  bcomputer-programminga  blanguage.a  bifa  byoua  barea  bnewa  btoa  bprogramming,a  bevena  bthata  bhasa  bprobablya  blefta  byoua  bsomewhata  bconfused,a  bsoa  blet’sa  bbreaka  bita  bdowna  baa  bbita  bmore.

Therea  barea  btwoa  btypesa  bofa  bprogramminga  blanguagea  b–a  bonea  bisa  binterpreted,a  banda  bthea  bothera  bisa  bcompiled.a  binterpreteda  blanguagesa  barea  bruna  bona  bana  binterpretera  b–a  bthisa  breadsa  bthea  bcodea  banda  bexecutesa  bthea  bcommandsa  binsidea  bonea  bata  baa  btime.a  bthea  bcpua  breadsa  bcompileda  blanguagesa  bona  byoura  bcomputera  binsteada  bofa  baa  bprogram.a  bcomputersa  bcannota  breada  bletters;a  btheya  bcana  bonlya  breada  bbinarya  bnumbersa  bso,a  bwhena  byoua  bwritea  byoura  bcode,a  bita  bhasa  btoa  bbea  btranslateda  bintoa  bbinarya  bfirst.a  bthisa  bisa  bcalleda  bcompiling.

Thea  bobject-orientateda  bparta  bofa  bthea  bexplanationa  bjusta  bdescribesa  bhowa  bthea  bcodea  bisa  bstructured,a  bbuta  bia  bwilla  bbea  bgoinga  bintoa  bmorea  bdetaila  bona  bthata  blatera  bon.

Whata  bdoesa  bthisa  balla  bmeana  btoa  bme?

Toa  bbea  bsuccessfula  bata  blearninga  bc++,a  byoua  bneeda  btoa  busea  bbotha  baa  btexta  beditora  banda  baa  bcompiler.a  bifa  byoua  barea  businga  baa  bwindowsa  bpca  btoa  bdoa  bthisa  bon,a  byoua  bcana  busea  bnotepad,a  bwhicha  bisa  balreadya  binstalled,a  bona  byoura  bcomputera  basa  byoura  btexta  beditora  band,a  basa  byoura  bcompiler,a  bwhicha  bisa  bgoinga  btoa  bconverta  byoura  bcodea  bintoa  bana  bexecutablea  bformat,a  byoua  bshoulda  busea  bgnua  bc/c++.

Linux/unix

Aa  bsimplea  bwaya  btoa  bchecka  bwhethera  bgcca  bisa  binstalleda  bona  byoura  blinux/unixa  bcomputera  bisa  btoa  bbringa  bupa  bthea  bcommanda  blinea  banda  btypea  bin:

$a  bg++a  b-v

Ifa  bgcca  bisa  binstalleda  byoua  bwilla  bgeta  bthea  bfollowinga  bmessage,a  bora  bsomethinga  bverya  blikea  bit:

Usinga  bbuiltina  bspecs

Target:a  bi386-redhat-linux

Configureda  bwith:a  b../configurea  b—prefix=/usra  b…….

Threada  bmodel:a  bposix

Gcca  bversiona  b4.1.2a  b20080704a  b(reda  bhata  b4.1.2-46)

Ifa  bgcca  bisa  bnota  binstalled,a  byoua  bcana  bfollowa  bthea  binstructionsa  bona  b[http://gcc.gnu.org/install/](http://gcc.gnu.org/install)a  btoa  bdoa  bso.

Maca  bosa  bx

Thea  bbesta  bwaya  btoa  bgeta  bgcca  bfora  bmaca  bosa  bxa  bisa  btoa  bgoa  btoa  b[http://developer.apple.com/technologies/tools](http://developer.apple.com/technologies/tools)a  b,a  bdownloada  bxcode,a  banda  bfollowa  bthea  binstallationa  binstructions.

Windows

Toa  bgeta  bgcca  bona  byoura  bwindowsa  bpc,a  byoua  bmusta  bfirsta  bdownloada  bmingwa  bfroma  b[http://www.mingw.org](http://www.mingw.org)a  b.a  bmakea  bsurea  byoua  bdownloada  bthea  blatesta  bversiona  bofa  bmingw,a  basa  bwella  basa  binstallinga  bgcc-core,a  bbinutils,a  bgcc-g++,a  banda  bmingwa  bruntimea  b–a  bthesea  barea  bminimuma  brequirements.

Onea  bmorea  bthinga  byoua  bcoulda  bconsidera  bisa  bana  bidea  b–a  bintegrateda  bdevelopmentsa  benvironment.a  bthisa  btexta  beditora  bfeaturesa  bana  bintegrateda  bcompilera  banda  bsyntaxa  bhighlighting.a  bthea  bbesta  bonea  btoa  busea  bisa  bcode:a  bblocks.

Isa  btherea  banythinga  belsea  bia  bshoulda  bknow?

Yes.a  bc++a  bisa  bverya  brigida  bina  bitsa  bsyntax,a  banda  beverythinga  bisa  bcasea  bsensitive,a  bsoa  bbea  bcarefula  bwhata  byoua  barea  btyping.a  bina  bc++,a  bthea  bworda  b“hello”a  bmeansa  bsomethinga  bdifferenta  btoa  b“hello”a  bbuta  bthisa  bisa  bsomethinga  byoua  bwilla  blearna  bmorea  babouta  blatera  bona  bina  bthea  bbook.a  bfora  bnow,a  blet’sa  bgeta  bstraighta  bona  bwitha  bthea  bprogramming.

Beforea  bwea  bgoa  bintoa  btooa  bmucha  bdetail,a  blet’sa  bgeta  byoua  bstarteda  bina  bwritinga  bsimplea  bcode.a  bthisa  bisa  baa  btypicala  bexamplea  bfora  balla  btypesa  bofa  bcomputera  bprogramminga  btutorials,a  bso,a  bwithouta  bfurthera  bado,a  blet’sa  bbreaka  bita  bdown.a  bfirsta  bofa  ball,a  bthea  bcodea  bisa  bwrittena  basa  bsuch:

![Image00059.jpg](images/Image00059.jpeg)a  b

Linea  b1a  bisa  btellinga  byoura  bcomputera  bthata  byoua  bwanta  btoa  blinka  biostreama  blibrarya  btoa  byoura  bprogram.a  bthea  blibrarya  bisa  baa  brepositorya  bwherea  blittlea  bbitsa  bofa  bcodea  barea  bstored,a  balonga  bwitha  bvariablesa  banda  boperatorsa  bona  boccasion.a  bthea  biostreama  blibrarya  bhasa  bcodea  bina  bita  bthata  bletsa  busa  bmovea  bcharactersa  btoa  baa  btexta  bstream,a  bwhicha  bthena  bappearsa  bona  bthea  bscreen.

Linea  b2a  btellsa  bthea  bcomputera  bthata  bwea  bwanta  btoa  busea  bthea  bstandarda  bnamespacea  b–a  bthisa  bisa  bwherea  byoura  bcodea  bwilla  bbea  bstored,a  busefula  bifa  byoua  bwritea  btwoa  bbitsa  bofa  bcodea  bwitha  bthea  bsamea  bname,a  blinea  b4a  bisa  bthea  bstarta  bofa  bthea  bcode.a  beverythinga  bthata  bgoesa  binsidea  bthea  bbracesa  bisa  bwhata  bthea  bcompilera  breadsa  banda  btranslatesa  b–a  bthisa  blinea  bmusta  bgoa  bina  beverya  bsinglea  bprograma  byoua  bwrite;a  botherwise,a  bnothinga  bisa  bgoinga  btoa  bhappen.

Thea  bnexta  bstagea  bisa  bthea  bprintinga  bofa  bthea  bprogram,a  bwhich,a  bina  bthisa  bcase,a  bisa  b“hello,a  bworld!”A  bthisa  bisa  bwherea  bwea  busea  bsomea  bofa  bthea  bcodea  bstoreda  bina  biostreama  b–a  baa  bpiecea  bofa  bcodea  bcalleda  bcout.a  bthea  b<<a  bthata  bcomesa  baftera  bthea  bcodea  bisa  bana  boperator,a  banda  bthisa  bonea  btranslatesa  btoa  b“output”a  bwhicha  bmeansa  bwea  barea  btellinga  bthea  bcomputera  btoa  bsenda  bthea  bcodea  btoa  baa  bspecifieda  bstream.a  bthea  bprintinga  b“hello,a  bworld!”A  bisa  bcalleda  baa  bstring,a  bwhicha  bisa  bnothinga  bmorea  bthana  baa  bcharactera  bsequencea  bencloseda  bina  bdoublea  bquotations.a  bnoticea  bthata  bthea  blinea  bendsa  bwitha  baa  bsemicolona  b–a  bthisa  bisa  btellinga  bthea  bcomputera  bthata  bthea  bcodea  bisa  bfinished,a  banda  bifa  bita  bisa  bnota  bused,a  bthea  bprograma  bcannota  bbea  bcompiled.

Linea  b8a  bisa  balwaysa  bplaceda  bata  bthea  benda  bofa  bmain,a  banda  bita  bisa  btoa  binforma  bthea  bcomputera  bthata  bthea  bblocka  bisa  bcompleted

Nowa  bthata  byoua  bhavea  bthea  bsourcea  bcodea  bfora  bthea  bprogram,a  bita  bhasa  btoa  bbea  bcompileda  businga  byoura  bcompiler.a  bmorea  bdetaila  blater,a  bfirst,a  bia  bwanta  btoa  bstarta  bgoinga  bovera  bwhata  bmakesa  bupa  byoura  bcode.a  bthea  bnexta  bchaptera  bdetailsa  balla  bthata  byoua  bwilla  bneeda  btoa  blearna  btoa  bbecomea  baa  bsuccessfula  bc++a  bprogrammer.

Structurea  bofa  bthea  bc++a  bprogram

Asa  bwea  bhavea  balreadya  bdiscussed,a  baa  bcomputera  bprograma  bisa  bnothinga  bbuta  baa  bseta  bofa  binstructionsa  bina  baa  bsequencea  bthata  btella  bthea  bcpua  bwhata  btoa  bdo.

Statementsa  banda  bexpressions

Ina  bc++,a  bthea  bstatementa  bisa  bnothinga  bbuta  bthea  bsmallesta  banda  bana  bindependenta  bunita  bina  bthea  bprogram.a  bita  bisa  balsoa  bthea  bmosta  bcommona  bforma  bofa  binstructiona  bina  baa  bprogramminga  blanguage.a  bina  bc++,a  bstatementsa  barea  baa  bwaya  btoa  bconveya  byoura  binstructionsa  btoa  bthea  bcompilersa  btoa  bcarrya  bouta  baa  bspecifica  btask.a  bwea  busea  b‘;’a  btoa  bterminatea  baa  bstatement.a  bina  bc++,a  btherea  barea  bmanya  bkindsa  bofa  bstatements,a  banda  bsomea  bofa  bthea  bmosta  bcommona  btypesa  bofa  bstatementsa  barea  bgivena  bbelow.

Inta  bx;

Xa  b=a  b5;

Std::couta  b<<a  bx;

Wea  bwilla  bdiscussa  bthea  bfunctionsa  bofa  bthea  babovea  bstatementsa  bina  bthea  blatera  bchapters.

Functions

Functionsa  barea  bnothinga  bbuta  bstatementsa  bina  baa  bsequence,a  bwhicha  barea  bexecuteda  bina  bsequentiala  border.a  btherea  bisa  baa  bfunctiona  bcalleda  bthea  bmaina  bfunction,a  banda  bita  bisa  baa  bmusta  bina  beverya  bc++a  bprogram.a  bwhena  banya  bgivena  bc++a  bprograma  bisa  brun,a  bthea  bexecutiona  bofa  bthea  bprograma  bstartsa  bwithina  bthea  bmaina  bfunction.a  bfunctionsa  bhavea  bverya  bspecifica  bjobsa  btoa  bperform.a  banda  btheya  bcana  bperforma  bonlya  bthosea  bjobs.a  bfora  byoua  btoa  bbecomea  baa  bgooda  bc++a  bprogrammer,a  byoua  bneeda  btoa  bknowa  bhowa  btoa  busea  bfunctionsa  befficiently.a  bina  bthea  bnexta  bchapter,a  byou’lla  blearna  bmorea  babouta  bfunctions.

Librariesa  banda  bthea  bc++a  bstandarda  blibrary

Librariesa  barea  bnothinga  bbuta  baa  bcollectiona  bofa  bcode,a  bwhicha  bisa  bpre-compiled.a  btheya  bcana  bbea  buseda  bwithina  bdifferenta  bprograms.a  bifa  byoua  bwisha  btoa  bextenda  bthea  bcapabilitiesa  bofa  byoura  bprogram,a  byoua  bcana  badda  blibraries.

Thea  bcorea  bc++a  blanguagea  bisa  bminimalistica  banda  bstraightforward,a  bbuta  bita  balsoa  bcomesa  bwitha  baa  bbuilt-ina  blibrarya  bcalleda  bthea  bc++a  bstandarda  blibrary.a  bthea  bc++a  bstandarda  blibrarya  bprovidesa  bthea  busera  bwitha  badditionala  bfunctionalities.

Syntaxa  banda  bsyntaxa  berrors

Wea  balla  bknowa  bthata  bina  banya  blanguage,a  bsentencesa  barea  bconstructeda  bfollowinga  bthea  bgrammaticala  brulesa  bofa  bthata  bparticulara  blanguage.a  btakea  bthea  bexamplea  bofa  bthea  benglisha  blanguagea  bwherea  byoua  bnormallya  benda  bofa  bsentencesa  bina  baa  bperiod.a  balla  bthea  brules,a  bwhicha  bgoverna  bthea  bconstructiona  bofa  bsentencesa  bina  baa  blanguage,a  bisa  bcalleda  bsyntax.a  bsimilarly,a  bc++a  balsoa  bhasa  bsyntax.a  bnota  bfollowinga  bthea  bsyntaxa  bwilla  bsimplya  bleavea  byoura  bcodea  binvalid.a  bita  bisa  bthea  bresponsibilitya  bofa  bthea  bcompilera  btoa  bseea  bthata  bthea  bbasica  bsyntaxa  bofa  bthea  bc++a  blanguagea  bisa  bfollowed.a  bifa  byoua  bviolatea  bthea  bbasica  bsyntax,a  bthea  bcompilera  bwilla  bcompilea  bthea  bcodea  banda  bwilla  bcomplaina  babouta  bthea  bsyntaxa  bviolation.a  bthata  bissuea  bisa  bcalleda  baa  bsyntaxa  berror.a  bthea  bc++a  bcompilersa  bonlya  bcompilea  bthea  bprograma  bifa  btherea  barea  bnoa  bsyntaxa  berrorsa  bfound.a  bita  bwilla  bdisplaya  balla  bthea  berrorsa  bthata  barea  bfounda  banda  bsuggesta  bfora  byoua  btoa  bmakea  bthema  bvalida  bsoa  bthata  bita  bcoulda  bexecutea  bthea  bcodea  bwithouta  banya  berrors.

Compilinga  byoura  bfirsta  bprogram

Therea  barea  btwoa  bimportanta  bthingsa  bthata  byoua  bshoulda  bknowa  bbeforea  byoua  bcana  bgoa  btoa  byoura  bfirsta  bprogram.

Youra  bprogramsa  bwilla  bbea  bwrittena  bina  bthea  b.cppa  bfiles,a  bwhicha  bwilla  bbea  baddeda  btoa  byoura  bprojecta  blater.a  bprojectsa  barea  balsoa  bcalleda  basa  bworkspacesa  bora  bsolutions.a  bthea  bcodea  bfilesa  banda  bthea  bidea  bsettingsa  bwilla  bbea  bsaveda  btoa  byoura  bproject.

Youa  bshoulda  bstarta  baa  bnewa  bprojecta  bbya  bcreatinga  bonea  basa  btherea  barea  bmanya  bkindsa  bofa  bprojects.a  bbeforea  bstarting,a  byoua  bneeda  btoa  bspecifya  bthea  btypea  bofa  bprojecta  byoua  bwisha  btoa  bworka  bon.

Whata  bmakesa  bthea  bc++a  bcode?

Aa  bvariablea  bisa  bsomethinga  bthata  bstoresa  baa  bvalue.a  bit’sa  blikea  baa  bbox,a  beacha  bboxa  bhasa  baa  bnamea  banda  bcategorya  bona  bit,a  banda  bthea  bcategorya  bisa  bthea  btypea  bofa  bitema  bstoreda  bina  bita  b–a  bthea  bnamea  bisa  bthea  bspecifica  bvariable.a  beacha  bvariablea  bhasa  baa  bspecifica  btype,a  bname,a  banda  bsize,a  banda  bthesea  bgoverna  bexactlya  bwhata  bcana  bbea  bstoreda  binsidea  bofa  bit.

Linea  b7a  bisa  bcalleda  bana  bassignment.a  bthisa  bassignsa  baa  bvaluea  btoa  bthea  bvariable,a  banda  bthea  b=a  bisa  bthea  boperatora  b–a  bthisa  bisa  bwhata  bdoesa  bthea  bassigning.a  bthea  bvaluea  baftera  bthea  b=a  bisa  bcalleda  baa  bbinarya  boperator.

Notea  bthata  btherea  barea  bnoa  bquotationa  bmarksa  barounda  bthea  bcouta  bstatementa  bthisa  btime.a  bthisa  bisa  bbecause,a  brathera  bthana  bdisplayinga  bthea  bstring,a  bwea  barea  boutputtinga  bthea  bvalue.a  bcompilinga  bthea  bprograma  bnowa  bwoulda  bprinta  b“42”a  bona  bthea  bscreen.

Asa  bwella  basa  bhavinga  baa  btypea  baa  bvariablea  bcana  balsoa  bhavea  baa  bprefixa  baddeda  btoa  bthea  bdeclarationa  banda  bthesea  bchangesa  bhowa  bthea  bvariablea  bbehaves.a  bsomea  bwilla  bchangea  bthea  bsizea  bofa  bthea  bvariablea  bwhilea  bothersa  bleta  byoua  busea  bora  bblocka  byoua  bfroma  businga  bnegativea  bnumbers,a  bwhilea  bothersa  bdoa  baa  bcompletelya  bdifferenta  bjob.a  balmosta  balla  bofa  bthema  bwilla  bbea  btalkeda  babouta  bhere.

Sizea  bchangers

Twoa  bspecifica  bprefixesa  bchangea  bthea  bbytea  bsizea  bofa  bthea  bvariablea  b–a  bshorta  banda  blong.a  bthea  bideaa  bbehinda  bthisa  bisa  btoa  ballowa  bthea  bvariablea  btoa  bstorea  bmorea  bvalesa  banda  bbiggera  bnumbers.a  bhowa  bbiga  bdependsa  bona  bthea  barchitecturea  bofa  bthea  bcomputera  bthata  byoua  barea  busing:

Ona  baa  b32-bita  bcomputera  binta  banda  blonga  binta  barea  bbotha  b4a  bbytes

Ona  baa  b64-bita  bcomputera  binta  bisa  b4a  bbytesa  banda  blonga  binta  bisa  b8a  bbytes

Ona  bbotha  barchitectures,a  bshorta  binta  bisa  b2a  bbytes

Therea  bisa  bnothinga  bthata  bdictatesa  bthea  bsizea  bofa  bthea  bmodifiera  bfora  bthosea  bparticulara  bkeywords,a  bexcept:

Shorta  bmusta  bbea  bequala  btoa  bora  bsmallera  bthana  baa  bnormala  bvariable

Thea  bnormala  bvariablea  bmust,a  bina  bturn,a  bbea  bequala  btoa  bora  bsmallera  bthana  baa  blong.

Thea  bonlya  bvariablea  bthata  bcana  btakea  baa  bprefixa  bisa  bint

Evena  bmorea  bconfusing,a  byoua  bcana  bomita  binta  banda  bjusta  busea  blonga  bora  bshort,a  bfora  bexample:

Shorta  binta  bsa  b=a  b0;

Inta  bia  b=a  b0;

Longa  binta  bla  b=a  b0;

Shorta  bs2a  b=a  b0;

Longa  bl2a  b=a  b0;

Signa  bchangers

Twoa  bothera  bprefixesa  bcana  brestricta  bthea  bvaluesa  bthata  barea  bstoreda  bbya  baa  btypea  b–a  bsigneda  banda  bunsigned.a  baa  bsigneda  bvariablea  bcana  bstorea  bnegativea  banda  bpositivea  bvalues,a  bwhilea  bana  bunsigneda  bvariablea  bcana  bonlya  btakea  bpositives.

Othera  bprefixes

Therea  barea  bsomea  bothera  bprefixesa  bthata  byoua  bcana  busea  bina  bc++,a  bnota  bsoa  bcommon,a  banda  bmosta  bofa  bwhicha  bwea  barea  bnota  bgoinga  btoa  busea  banda  bwilla  bnota  bcovera  bina  bthisa  bbook.a  btherea  barea  btwoa  bverya  busefula  bones,a  bthougha  b–a  bconsta  banda  bstatic.a  bthea  bformera  bisa  bconstant,a  bnevera  bchanginga  btheira  bvalue,a  banda  bthea  blattera  bkeepsa  bthea  bvaluea  bofa  bthea  bvariablea  bthea  bsamea  bbuta  bonlya  bina  bbetweena  bfunctiona  bcalls;a  bthat’sa  baa  btopica  bfora  blatera  bon.

Ata  bthea  bcorea  bofa  bthea  blanguage:a  bunderstandinga  bc++

Computersa  bruna  bvirtuallya  beverythinga  barounda  busa  btoday;a  bata  bthea  bcorea  bofa  bcomputera  bora  byoura  bpreferreda  bcellphonea  bbrand,a  barea  bprograms.a  bfora  boura  blearninga  bprocess,a  bia  bassumea  byoua  barea  bawarea  bofa  bwhata  baa  bcomputera  bprograma  bisa  banda  bstructuresa  bbehinda  bit.a  bata  bthea  bcorea  bofa  balla  bprogramsa  bisa  baa  bcomputinga  blanguage.a  bthisa  bquestiona  bthena  bcomesa  bup.a  bwhata  bexactlya  bisa  bc++?

C++a  b(pronunciationa  bseea  bplusa  bplus)a  bisa  bata  bitsa  bcorea  baa  bgenerala  ball-purposea  bprogramminga  blanguage.a  bwhata  bmakesa  bthea  blanguagea  bdifferenta  bisa  bthea  bfacta  bthata  bita  bintegratesa  bcruciala  bobject-orienteda  bcoupleda  bwitha  bgenerica  bprogramminga  bina  badditiona  btoa  bprovidinga  blow-levela  bmemorya  bmanagement.

Thea  blanguagea  banda  bitsa  bdesigna  bhavea  baa  bbiasa  btowardsa  bsystemsa  bprogramming,a  bfora  bexample,a  bembeddeda  bsystems,a  banda  boperatinga  bsystema  bkernelsa  bjusta  btoa  bpointa  bouta  baa  bfew.

Thea  blanguagea  bisa  baa  bfavoritea  bofa  bmanya  bprogrammersa  bduea  btoa  bitsa  bperformance,a  bflexibility,a  banda  befficiency.a  bthea  blanguagea  bhasa  beffectivea  busesa  bina  bmanya  bcontextsa  bsucha  basa  bservers,a  be.g.,a  bweba  bsearcha  bsqla  banda  be-commerce,a  bdesktopa  bapplications,a  bperformance-criticala  bapplicationsa  bsucha  basa  bspacea  bprobea  banda  btelephonea  bswitches,a  banda  bmorea  bthana  banythinga  belse,a  bentertainmenta  bsoftware,a  bwhicha  bisa  bwherea  byoura  bfavoritea  bvideoa  bgamea  bfalls.

Thea  blanguagea  bisa  btermeda  basa  baa  bcompileda  blanguagea  bwitha  bitsa  bimplementationsa  bavailablea  bona  bmanya  bplatformsa  bacrossa  bthea  bglobea  banda  bina  busea  bina  bmanya  bmultinationalsa  bsucha  basa  bintel,a  bfsf,a  bmicrosoft,a  banda  bllvma  bjusta  btoa  bpointa  bouta  baa  bfew.

Ifa  byoua  bsearcha  bthea  bisoa  b(internationala  borganizationa  bfora  bstandardization),a  byoua  bwilla  blearna  bthata  bc++a  bisa  bstandardized.a  bisoa  bapproveda  banda  bpublisheda  bthea  bcurrenta  bversiona  bofa  bc++a  bina  bseptembera  bofa  b2011a  basa  biso/ieca  b14882:2011,a  bwhicha  bisa  binformallya  bknowna  basa  bc++11.a  bc++a  bfirsta  bwasa  bstandardizeda  bina  b1998a  basa  biso/ieca  b14882:1198,a  bthena  bamendeda  btoa  bc++03,a  banda  bthena  bagaina  bina  b2003a  basa  biso/ieca  b14882:2003.a  bthea  babovea  binformationa  bthougha  busefula  bholdsa  bnoa  bimportancea  btoa  byou.

Whata  bisa  bmorea  bimportanta  bisa  bthea  bcurrenta  bstandarda  bc++11,a  bwhicha  bsupersedesa  balla  bthea  bothersa  bbecausea  bofa  bthea  bintegrationa  bofa  bnewa  bfeaturesa  banda  baa  bbiggera  bstandarda  blibrary.

Everythinga  brelateda  btoa  bcomputers,a  banda  bina  bfact,a  beverythinga  belsea  bina  bthea  bworlda  bhasa  bana  borigin.a  bc++a  bisa  bthea  bbrainchilda  bofa  bbjarnea  bstroustrupa  bata  bbella  blabsa  basa  bearlya  basa  b1979a  b(c).a  beverya  bgreata  binnovationa  bhasa  baa  bcausea  bora  bpurpose.a  bbjarnea  bwanteda  baa  bmorea  bflexiblea  banda  befficienta  blanguagea  bsucha  basa  bca  bbuta  balsoa  baa  blanguagea  bthata  bprovideda  bhigher-levela  bfeaturesa  bofa  borganizinga  bprograms.

Herea  bisa  baa  bkicker;a  bremembera  bwhena  bia  bsaida  bthata  blearninga  bc++a  bwoulda  bpreparea  byoua  btoa  blearna  bothera  blanguages?A  bherea  bisa  bwhy.a  bc++a  bhasa  binfluenceda  bmanya  blanguages,a  bincludinga  bjavaa  bc#,a  banda  balla  blatera  bversionsa  bofa  bca  bdevelopeda  baftera  b1998.

Beforea  bclosinga  bthisa  bfirsta  bchapter,a  bia  bshoulda  bperhapsa  bmentiona  bthata  bca  bisa  bthea  bprecursora  btoa  bc++,a  banda  btherefore,a  bworkinga  bwitha  bc++a  bwilla  bdemanda  bsomea  bknowledgea  bofa  bthea  blatter.

Gettinga  bstarted-workinga  bwitha  bc++a  bfora  bthea  bfirsta  btime

Whilea  bstudyinga  banda  blearninga  bc++a  bisa  bexciting,a  btherea  barea  bsomea  bprerequisitesa  bbeforea  bwea  bembarka  bona  bwritinga  bcode.a  bbeforea  byoua  bcana  bundertakea  banya  bprogramming,a  byoua  bneeda  bana  bintegrateda  bdevelopmenta  benvironmenta  b(ide).a  bana  bidea  bisa  baa  bcompilera  bthata  btranslatesa  byoura  bcodea  bintoa  baa  bbuncha  bofa  bonesa  banda  bzeroesa  bthata  barea  bthea  blanguagea  bora  bcodea  byoura  bmachinea  bcana  bcomprehend.

Ifa  byoua  bdoa  bnota  balreadya  bhavea  baa  bcompilera  binstalled,a  byoua  bcana  bdownloada  baa  bbuncha  bofa  bfreea  banda  bpaida  bcompilers.

Installinga  bana  bide

Ana  bidea  bformsa  baa  bverya  bcentrala  bparta  bofa  byoura  bprogramming.a  btherefore,a  btherea  bisa  bsomea  bimportancea  bina  busa  blookinga  bata  bsomea  bofa  bthea  bmorea  bfundamentala  baspectsa  bofa  bana  bide,a  bespeciallya  binstallation.a  basa  bia  bhavea  bmentioned,a  byoua  bcana  busea  baa  bbuncha  bofa  bide’s.a  bmosta  bdevelopersa  bstrugglea  bwitha  bthea  bquestiona  bofa  bwhicha  bone,a  bwhicha  bidea  bbesta  bsuitsa  bme.a  bherea  bisa  bthea  bthing,a  bthough;a  byoua  bcana  binstalla  bmultiplea  bidea  bona  byoura  bsystem,a  bsoa  btherea  bisa  bnoa  bonea  bcorrecta  bora  bwronga  bide.a  bthea  bmosta  bcommona  banda  bintegrateda  bcompilersa  barea  bcode::blocksa  banda  bmicrosoft’sa  bvisuala  bc++a  b2005a  bexpressa  bedition.a  btherefore,a  bia  bcana  brecommenda  byoua  binstalla  beithera  bonea  bofa  bthem,a  bbuta  bifa  byoua  bhavea  baa  bcompilera  bthata  byoua  bdeema  bfriendlier,a  bbetter,a  bora  bsuperiora  btoa  bthesea  btwo,a  bdoa  bnota  bfeela  brestricteda  bbya  bmya  bchoice;a  bindulgea  byourself.

Ifa  byoua  barea  bprogramminga  bona  bwindows,a  bi.e.,a  baa  bwindowsa  bmachine,a  bchancesa  bare,a  bthea  bbesta  boptiona  bfora  byoua  bisa  bmicrosoft’sa  bvisuala  bc++a  b2010a  bexpressa  beditiona  bthata  bisa  bdownloadablea  bfroma  bmicrosoft’sa  bwebsite.a  bperhapsa  bita  bisa  balsoa  bwella  btoa  bpointa  bouta  bthata  bthea  bfilea  byoua  bd0wnloada  bfroma  bthea  bwebsitea  bisa  bsimplya  baa  bdownloader;a  bthea  bactuala  bidea  bdownloada  bcommencesa  bwhena  byoua  bruna  bthea  bdownloader.

However,a  bifa  byoua  barea  bworkinga  bina  bana  benvironmenta  bthata  bhasa  blimiteda  binterneta  bconnectivity,a  banda  bwoulda  blikea  bthea  bdownloada  bfilea  bfora  blatera  buse,a  bwitha  baa  blittlea  bhelpa  bfroma  bgooglea  bora  byoura  bfavoritea  bsearcha  bengine,a  byoua  bcana  bfinda  bana  bofflinea  binstaller.

P.s.a  bia  bdoa  bnota  brecommenda  bdownloadinga  bfilesa  bfroma  bthirda  bparties

Ita  bisa  balsoa  bimportanta  btoa  bnotea  bthata  bmosta  bofa  bthea  bfunctionsa  bofa  bca  banda  bc++a  bwea  bshalla  blooka  bata  barea  bcontaineda  bina  bthea  bdocumentationa  bfilea  bthata  bcomesa  bwitha  bthea  binstallationa  bofa  bmsdna  bexpress.a  bhowever,a  bifa  byoua  bdoa  bnota  binstalla  bmsdna  bona  byoura  bdrive,a  bvisuala  bc++a  bwilla  busea  bana  bonlinea  bversiona  bavailablea  b[here](http://msdn.microsoft.com)a  b.a  bdependinga  bona  byoura  binterneta  bbandwidth,a  bthea  bfilesa  bmaya  btakea  bsomea  btimea  btoa  bdownload,a  banda  boncea  bthea  bdownloada  banda  binstallera  barea  bdone,a  bwindowsa  bwilla  bprompta  bfora  baa  breboot,a  bsoa  breboota  bthea  bsystem.

Youa  bwilla  bprobablya  bnoticea  baa  blaga  bina  byoura  bcomputera  bresponsea  btime,a  baa  bsorta  bofa  b“hang”;a  byoua  bshoulda  bnota  bbea  balarmed,a  bora  bforcea  bshutdowna  bsincea  bthea  blaga  bisa  bbecausea  byoura  bsystema  bisa  binstallinga  balla  bthea  bresourcesa  brequireda  btoa  bruna  bthea  benvironment.a  balso,a  boncea  byoura  bsystema  bbootsa  bupa  banda  bopensa  bthea  bwindowsa  bdesktop,a  byoua  bmaya  bfinda  bita  bnecessarya  btoa  breruna  bthea  binstallera  bsimilarlya  btoa  bthea  binstallationa  bbita  bwea  bjusta  bcompleted.

However,a  bthisa  btime,a  bthea  binstallera  bwilla  bnota  bdownloada  bthea  bfiles;a  bita  bwilla  bsimplya  binstalla  bthea  bprogram.

Ona  bthea  bothera  bhand,a  byoua  bmaya  bbea  bdevelopinga  bona  bwindowsa  bbuta  barea  bwritinga  bprogramsa  bfora  bportinga  bwitha  bthea  blinuxa  bkernela  bora  bvicea  bversa;a  bina  bthisa  bcase,a  byoura  bbesta  boptiona  bisa  btoa  busea  bcode::blocks,a  bthea  bopen-source,a  bcross-platforma  bfreea  bidea  bthata  bwilla  bruna  bona  bbotha  bwindowsa  banda  blinux.

Nevertheless,a  btherea  bisa  baa  bkeya  bpointa  btoa  bnotea  bfora  bwindowsa  busers.a  bifa  byoua  bintenda  btoa  bwritea  bc++a  bcodea  bona  bwindowsa  businga  bcode::blocks,a  byoua  bshoulda  bmakea  baa  bpointa  bofa  bdownloadinga  bthea  bmingwa  bbundleda  bversion.a  bifa  bcode::blocksa  bdoesa  bnota  bticklea  byoura  bfancy,a  byoua  bcana  balsoa  busea  bbloodshed’sa  bdev-c++,a  bwhicha  bisa  balsoa  bcross-platform,a  bi.e.,a  brunsa  bona  bwindowsa  banda  blinux.

Soa  bfar,a  bwea  bhavea  bcovereda  balmosta  balla  bthea  bothera  bplatformsa  bexcepta  bmaca  bosx.a  bifa  byoua  barea  bana  bosxa  buser,a  byoua  bcana  busea  bxcodea  bora  beclipse.a  bc++a  bona  beclipsea  bisa  bnota  bautomaticallya  bset;a  bita  bwilla  brequirea  bdownloadinga  banda  binstallinga  boptionala  bc++a  bcomponents.

Thea  bidea  binstallationa  bparta  bofa  bprogramminga  bisa  bprobablya  bthea  bhardesta  bparta  bofa  banya  bprogramminga  btutorial.a  bnowa  bthata  bwea  bhavea  bcompleteda  bthata  bpart,a  byoua  barea  breadya  btoa  bbegina  bcodinga  byoura  bfirsta  bprogram.

Youra  bfirsta  bc++a  bprogram

Welcomea  btoa  bthea  bmosta  bexcitinga  bpart,a  bperhapsa  bthea  bparta  bthata  bmadea  byoua  bpicka  bupa  bthisa  bbook,a  bwritinga  bprogramsa  businga  bc++.a  blikea  bmosta  bcomputera  blanguagea  btutorials,a  boura  bfirsta  bfocusa  bwilla  bbea  btoa  bcreatea  baa  bhelloa  bworlda  bprogram.

Whilea  bthea  b“helloa  bworld”a  bcodea  bmaya  bsounda  blikea  baa  bcliché,a  bina  boura  bprograma  bcreation,a  bita  bisa  bthea  bbesta  billustrationa  bofa  b“spinala  bcode”a  bofa  bvirtuallya  banya  banda  beverya  bprograma  byoua  bshalla  bcreatea  bwaya  baftera  bia  bama  bthrougha  bteachinga  byoua  bmya  bbit.a  bregardlessa  bofa  bthea  bcomplexitya  bora  bsimplicitya  bofa  byoura  bprograma  bora  bcode,a  bita  bmusta  bhavea  baa  bfewa  bbasica  blinesa  bofa  bcode.

![Image00060.jpg](images/Image00060.jpeg)a  b

Thea  babovea  bcodea  bisa  bwhata  bwea  brefera  btoa  basa  baa  bpre-processora  bdirective.a  bifa  byoua  blooka  bata  bthea  bcode,a  byoua  bwilla  bnoticea  bthata  btherea  bisa  bana  b‘i’a  banda  b‘o’a  b‘iostream’;a  btheya  bstanda  bfora  binputa  banda  boutput,a  brespectively,a  banda  barea  bana  babsolutea  brequirementa  bina  banya  bprograma  byoua  bcreatea  businga  bthea  bc++.a  bona  bthea  bothera  bhand,a  b‘namespacea  bstd’a  binformsa  bthea  bcompilera  bthata  byoua  bintenda  btoa  busea  bthea  bstandarda  blibrary.a  bifa  byoua  bfaila  btoa  busea  bthea  bcodea  blinea  btoa  bspecifya  bthis,a  byoua  bwilla  blimita  byourselfa  banda  bnota  bbea  bablea  btoa  busea  bcin,a  bcout,a  bora  bendl,a  bwhicha  bwea  bshalla  blooka  bata  bina  baa  blittlea  bwhile.

![Image00061.jpg](images/Image00061.jpeg)a  b

Ona  bthea  bothera  bhand,a  bthea  bcodea  babovea  bindicatesa  bwherea  boura  bmaina  bprograma  bbegins,a  bwhicha  bisa  bwherea  bmosta  bofa  bthea  bcodinga  bhappens.a  bifa  byoua  barea  bwondering,a  bthea  binta  bmeansa  binteger.a  bana  bintegera  bisa  bwhata  bwilla  bpassa  bbacka  btoa  bthea  bprogram.

Ita  bisa  balsoa  bimportanta  btoa  bnotea  bthata  byoua  bshoulda  bnota  boverlooka  bthea  bparenthesisa  b();a  btheya  barea  bimportanta  bevena  bifa  btheya  barea  bempty.a  bina  bthea  bsamea  bbreath,a  byoua  bshoulda  balsoa  bnota  boverlooka  bthea  bcurlya  bbracea  b{,a  bbecausea  bita  bisa  bnecessary.a  bnowa  bthata  bwea  bhavea  bunderstooda  bthat,a  businga  bthea  bconsolea  bout,a  bleta  busa  bprinta  bsomethinga  btoa  bthea  bscreen.

![Image00062.jpg](images/Image00062.jpeg)a  b

Ia  bdoa  bnota  bknowa  bifa  byoua  barea  bfamiliara  bwitha  bthea  bca  blanguage,a  bbuta  bthea  bcouta  bina  bthea  bcodea  babovea  bisa  bthea  bprintfa  bstatement.a  bthea  bcodea  b(cout)a  bprintsa  btoa  bthea  bscreena  banything,a  btext,a  bora  botherwise,a  bthata  bisa  bwithina  bthea  bquotation’sa  bmarks.a  bona  bthea  bothera  bhand,a  bendla  bindicatesa  bthea  benda  bofa  bthea  blinea  b(ita  bisa  bsimilara  btoa  bpressinga  bthea  bentera  bbuttona  bwhilea  bworkinga  bona  baa  bworda  bdocumenta  bfile).a  bthea  bsemicolona  bisa  balsoa  brequired,a  bsoa  bdoa  bnota  bforgeta  bit.a  bina  bthea  bcodea  babove,a  breturna  b0a  bactsa  basa  bthea  bintegera  bthata  breturnsa  btoa  bthea  binta  bmain.a  bnota  btoa  bsounda  blikea  baa  bbrokena  brecord,a  bdoa  bnota ![Image00063.jpg](images/Image00063.jpeg)bforgeta  btoa  benda  bina  bwitha  bthea  bcurlya  bbracketa  bbecausea  btheya  bsignifya  bthea  benda  bofa  bthea  bmain.

Ina  bthea  babovea  bcode,a  bherea  bisa  bhowa  boura  bmaina  bprograma  bcodea  bwoulda  bappear.

A  b

Thisa  bmaya  bcomea  basa  baa  bsurprisea  btoa  byoua  bbut,a  bifa  byoua  bhavea  bfolloweda  beverythinga  bwea  bhavea  bdonea  bsoa  bfar,a  byoua  bhavea  bjusta  bcreateda  byoura  bfirsta  bprogram.

Suprise!A  bthea  bcodea  bwea  bjusta  buseda  banda  bcreateda  bisa  bthea  bbasica  bstructurea  bofa  balla  bprograms;a  bthinka  bofa  bita  blikea  blearninga  bthea  balphabeta  bina  bkindergarten.a  byoua  bshoulda  bmakea  beverya  befforta  btoa  bunderstanda  banda  bmemorizea  bit.a  bsecondly,a  byoua  bshoulda  bremembera  bina  bwhicha  bordera  btoa  busea  bcouta  banda  bendl.a  bdoa  bnota  bforgeta  btoa  bdeclarea  businga  bnamespacea  bstd;a  botherwise,a  bthea  bcompilera  bwilla  breturna  bana  berror.

However,a  btherea  bisa  baa  bworkaround.a  bifa  byoua  bdoa  bnota  busea  bnamespacea  bstda  btoa  bdeclare,a  bthena  byoua  bmusta  busea  bstd::a  btoa  bdeclarea  beacha  bcout,a  bcin,a  banda  bendl.

Herea  bisa  bana  bexamplea  bofa  bwhata  bia  bmeana  bbya  bthis.a  bfora  bclarity,a  bwea  bshalla  bhighlighta  bthea  bdifferencea  bina  bthea  bprograma  bina  bblue.

![Image00064.jpg](images/Image00064.jpeg)a  b

Ifa  byoua  barea  bnota  bverya  bconversanta  bwitha  bprogramminga  bina  bgenerala  bora  bc++,a  byoua  bwilla  brealizea  bthata  bcout,a  bcin,a  banda  bendla  bwilla  bcomea  bupa  baa  blota  bina  byoura  bcoding.a  boptinga  btoa  busea  bthea  bmethoda  bia  bhavea  bjusta  bdescribeda  bwilla  bbea  btedious.a  btherefore,a  byoua  bshoulda  bopta  btoa  binstructa  bthea  bcompilera  bbya  businga  bthea  bnamespacea  bstda  btoa  bmakea  byoura  bworka  bfaster.

## Chaptera  b2:a  bdeclaringa  bconstants

C++a  bconstants

Constantsa  barea  bfixeda  bvaluesa  bthata  bprogramsa  bmaya  bnota  bbea  balloweda  btoa  balter,a  banda  btheya  barea  breferreda  btoa  basa  bliterals.a  baa  bconstanta  bcana  bbelonga  btoa  banya  bofa  bthea  bavailablea  bbasica  bdataa  btypes.a  bnotea  bthata  barea  bjusta  bregulara  bvariablesa  bwitha  bthea  bdifferencea  bbeinga  bthata  bthea  bvaluesa  bofa  bconstantsa  bcannota  bbea  bchangeda  baftera  bdefinition.

Toa  bdefinea  baa  bconstanta  businga  bthea  b#definea  bpreprocessor,a  bwea  busea  bthea  bsyntaxa  bgivena  bbelow:

#definea  bidentifiera  bvalue

Thea  bidentifiera  bisa  bthea  bnamea  bofa  bthea  bconstanta  bwhilea  bthea  bvaluea  bdenotesa  bthea  bvaluea  bassigneda  btoa  bthea  bconstant.a  bthea  bfollowinga  bprograma  bdescribesa  bhowa  bthisa  bcana  bbea  bdone:

#includea  b<iostream>usinga  bnamespacea  bstd;

#definea  bwidtha  b7

#definea  blengtha  b11

Inta  bmain(){

Inta  brectangle_area;

Rectangle_areaa  b=a  blengtha  b*a  bwidth;a  bcouta  b<<“thea  bareaa  bofa  bthea  brectanglea  bisa  b“<<rectangle_area;returna  b0;}

Ina  bthea  babovea  bexample,a  bwea  bhavea  bdefineda  btwoa  bconstants,a  bnamelya  bwidth,a  banda  blength.a  bwea  bhavea  bassigneda  bvaluesa  bofa  b7a  banda  b11a  btoa  bthese,a  brespectively.a  bwea  bhavea  balsoa  bdefineda  bthea  bvariablea  brectangle_areaa  banda  bassigneda  bita  bthea  bvaluea  bofa  bthea  bproducta  bofa  bthea  btwoa  bconstants.a  bwea  bhavea  bthena  bprinteda  bouta  bthea  bvaluea  bofa  bthisa  bvariable.

Whena  bexecuted,a  bthea  bcodea  bshoulda  breturna  bthea  bfollowinga  basa  bthea  boutput:

Usinga  bthea  bconsta  bkeyword

Wea  bcana  balsoa  bdefinea  baa  bconstanta  bbya  busea  bofa  bthea  bconsta  bkeyword.a  btoa  bdoa  bthis,a  bwea  bhavea  btoa  busea  bthea  bsyntaxa  bgivena  bbelow:

Consta  bdata_typea  bvariablea  b=a  bvalue;

Notea  bthata  bwea  bhavea  btoa  bdefinea  bthea  bdataa  btypea  bofa  bthea  bconstant.a  bthea  bvaluea  bofa  bthea  bconstanta  bthisa  btimea  bhasa  bbeena  bassigneda  businga  bthea  bassignmenta  b(=)a  boperator.a  bleta  busa  bgivea  bana  bexamplea  bdemonstratinga  bthis:

#includea  b<iostream>usinga  bnamespacea  bstd;

Inta  bmain(){

Consta  binta  blengtha  b=7;constinta  bwidtha  b=11;inta  brectangle_area;

Rectangle_areaa  b=a  blengtha  b*a  bwidth;a  bcouta  b<<“thea  bareaa  bofa  bthea  brectanglea  bisa  b“<<a  brectangle_area;returna  b0;}

Wea  bhavea  bjusta  bcreateda  bthea  bsamea  bexample,a  bbuta  bthisa  btime,a  bthea  bconstantsa  bhavea  bbeena  bdefineda  businga  bthea  bconsta  bkeyword.

Whena  bexecuted,a  bthea  bcodea  bshoulda  breturna  bthea  bfollowinga  bresult:

Notea  bthata  bprogrammatically,a  bita  bisa  balwaysa  bgooda  btoa  bnamea  bconstantsa  bina  bthea  buppera  bcase.

Workinga  bwitha  bc++a  bdataa  btypes

Nowa  bthata  bwea  bhavea  bcreateda  byoura  bverya  bfirsta  bprogram,a  btherea  bisa  bsomethinga  belsea  bofa  bequala  bimportance,a  bifa  bnota  bgreater,a  bthana  bspendinga  beverya  bwakinga  bhoura  bwritinga  bcode;a  bdocumentation.

Everya  bprograma  bneedsa  bdocumentation,a  bifa  bnota  btoa  bhelpa  bothera  bprogrammersa  bunderstanda  byoura  bprogram,a  btoa  bhelpa  byoua  bunderstanda  byoura  bprogram,a  byearsa  baftera  bwritinga  bit.a  bthata  bmaya  bsounda  blikea  brevealinga  byoura  bmagica  b“codea  bwritinga  bskill”a  bbuta  bina  bthea  bprogramminga  bworld,a  byoua  barea  bnevera  baa  bsuccessa  buntila  bothera  bprogrammersa  bpaya  byoua  baccolades.a  bwhena  businga  bthea  bc++a  blanguage,a  byoua  bcana  badda  bdocumentationa  bina  bthea  bforma  bofa  bnotesa  btoa  byoura  bprograma  bbya  businga  btwoa  bslashesa  b“//”thea  bcompilera  bwilla  bignorea  banythinga  byoua  bwritea  bbetweena  bthesea  btwoa  bslashesa  bona  bthea  bsamea  bline.

Throughouta  byoura  bcodinga  blifea  banda  bwork,a  bia  bwoulda  brecommenda  byoua  btoa  bdocumenta  byoura  bworka  basa  boftena  basa  bpossible.a  badditionally,a  byoua  bwilla  balsoa  bnoticea  bthata  bmosta  bofa  bthea  bnotesa  byoua  bwritea  bwilla  bhavea  baa  bdifferenta  bcolora  bfroma  bthea  bcode.a  bifa  byoura  bcompilera  bdoesa  bnota  bdoa  bthisa  bautomatically,a  byoua  bshoulda  bdoa  bita  bmanuallya  btoa  bavoida  bconfusion.

Herea  bisa  banothera  bfuna  bfacta  byoua  barea  bprobablya  bnota  bawarea  bof;a  balmosta  beverya  bprograma  busesa  bvariables.a  btooa  b“mathematical”a  bfora  byou?A  baa  bvariablea  bina  bprogramminga  bisa  bthea  bsamea  basa  baa  bvariablea  bina  bmath,a  baa  blettera  buseda  btoa  bholda  baa  bvalue.a  bina  bprogramming,a  byoua  busea  bvariablesa  btoa  bholda  bdifferenta  bdataa  btypesa  bthata  byoua  bmusta  bdeclarea  bbeforea  byoua  bruna  bthea  bprogram.

Therefore,a  btoa  bfixa  bthis,a  byoua  bmusta  bassigna  bxa  bvaluea  bina  bthea  bfollowinga  bmanner:

X=12;

Ifa  bwea  busea  bthisa  bexamplea  bina  boura  bprogram,a  beacha  btimea  bwea  busea  bthea  bvariablea  bx,a  bita  bwilla  bbea  bsimilara  btoa  businga  bthea  bnumbera  b12a  bunlessa  bwea  bspecifya  botherwise.a  bwitha  bthis,a  bwhena  byoua  bwanta  btoa  bprinta  bsomethinga  btoa  bthea  bscreen,a  bherea  bisa  bhowa  byoua  bdoa  bit.

Note:a  bina  bthisa  bcase,a  bwea  barea  bprintinga  bxa  btoa  bthea  bscreen.

Cout<<x;

Ifa  byoua  bhavea  bpriora  bexperiencea  bwitha  bthea  bca  blanguage,a  bita  bwilla  bnota  bpassa  byoua  bthata  bthisa  bisa  bdifferent.a  bfora  bone,a  btherea  bisa  bnoa  bprintf,a  banda  bsecondly,a  btherea  bisa  bnoa  bplacea  bholder.a  bthisa  bshoulda  bnota  bbea  bcausea  bfora  balarm.a  bina  bthea  bcodea  babove,a  bthea  b‘c’a  bina  bcouta  bisa  baa  bplaceholdera  bfora  b“console”a  banda  btherefore,a  bcouta  bmeansa  bconsolea  bout.a  bleta  busa  bassumea  baa  bscenarioa  bwherebya  byoua  bdoa  bnota  bwanta  btoa  bassigna  baa  bvariablea  btoa  byoura  bprograma  bbuta  bwoulda  blikea  bthea  bprograma  btoa  bassigna  baa  bvariablea  bvaluea  bwhilea  bita  bisa  brunning.a  bwhilea  bthisa  bmaya  bsounda  bverya  bmathematicala  banda  bcomplicated,a  byoua  bcana  beasilya  bachievea  bthisa  bbya  businga  bcin,a  bwhich,a  basa  byoua  bmaya  bhavea  bguessed,a  bstandsa  bfora  bthea  bconsolea  bin.

![Image00065.jpg](images/Image00065.jpeg)A  b

Asa  baa  bprogrammer,a  byoua  bhavea  btoa  bbea  bverya  bkeen.a  blooka  bata  bthea  bcodea  babovea  banda  btella  bmea  bifa  byoua  bnoticea  banythinga  bdifferenta  bfroma  bwhata  bwea  bhavea  blearneda  bsoa  bfar.a  bdida  byoua  bnoticea  banything?A  bthea  barrowsa  bina  bthea  babovea  bcodea  barea  bpointinga  bina  bthea  boppositea  bdirectiona  bfroma  bwhena  byoua  busea  bcout.a  bina  bthea  babove,a  bwea  bdida  bnota  bassigna  baa  bvaluea  btoa  bthea  bintegera  bcalleda  bx.a  bthisa  bisa  bbecausea  bthea  bprograma  bwilla  bprompta  bthea  busera  bfora  baa  bnumbera  bvaluea  bthata  bwilla  bthena  bbea  bstoreda  basa  bthea  bvaluea  bfora  bvariablea  bx.a  bherea  bisa  bhowa  boura  bprograma  bshoulda  bnowa  blooka  blike

![Image00066.jpg](images/Image00066.jpeg)a  b

Thea  bprograma  babovea  bfirsta  bdeclaresa  bana  binteger,a  bintegera  b‘x’,a  bthena  bita  basksa  byoua  btoa  bentera  baa  bvaluea  bthata  boncea  bentered,a  bdisplaysa  bona  bthea  bscreen.a  bina  bana  binstancea  bwherea  byoua  bora  bsomeonea  belsea  bwantsa  btoa  bmanipulatea  bthea  bvariablea  beithera  bthrougha  bmultiplicationa  bora  bthrougha  bdivision,a  byou,a  bthea  bprogrammer,a  bwoulda  bhavea  btoa  bdeclarea  bsomea  bmorea  bvariablesa  banda  bcoina  bsomea  bforma  bofa  bexpression.a  bleta  busa  badda  bsomea  bcodea  btoa  bthea  bprograma  babove.

![Image00067.jpg](images/Image00067.jpeg)a  b

Ina  bthea  babove,a  bthea  bprograma  bdeclaresa  bthreea  bintegersa  banda  bequalsa  bvariablea  b‘z’a  btoa  bthea  bdivisiona  bofa  b‘x’a  banda  b‘y’.a  bwhena  bthea  bprograma  busera  bassignsa  baa  bvaluea  btoa  bxa  banda  by,a  bthea  bprograma  bthena  bdisplaysa  bthea  bdivisiona  bhelda  bina  bvariablea  b‘z’.a  bwhilea  bthea  babovea  bcodea  bmaya  bworka  bok,a  btherea  barea  bflawsa  bbounda  btoa  barisea  bfroma  bza  bbeinga  bequala  btoa  bthea  bdivisiona  bofa  bxa  banda  by.a  bina  bthea  babovea  binstance,a  bifa  bthea  busera  bassignsa  b4a  basa  bxa  banda  b2a  basa  by,a  bthata  bwoulda  bnota  bpresenta  baa  bproblema  bbecausea  b4a  bisa  bdivisiblea  bbya  b2.a  bhowever,a  bwhata  bwoulda  bhappena  bifa  bthea  bvaluesa  bwerea  b6a  banda  b4?A  bleavinga  bthea  bprograma  bcodea  bina  bitsa  bcurrenta  bstatea  bwoulda  bprompta  baa  b0a  banswera  bmainlya  bbecausea  bsoa  bfara  banda  basa  bofa  brighta  bnow,a  bx,a  by,a  banda  bza  bonlya  bholda  bintegera  bnumbersa  bwithouta  bdecimals.a  bina  bthea  babovea  bexamplea  bofa  bthea  busera  bassigninga  b6a  banda  b4,a  bita  bisa  bevidenta  bthata  btheya  barea  bnota  bdivisible,a  banda  bsubdivisiona  bwilla  bplacea  baa  bdecimal.a  bso,a  bhowa  bdoa  bwea  bfixa  bthis?A  bthea  banswera  btoa  bthisa  bisa  brelativelya  bsimple;a  brathera  bthana  bdeclaringa  bz,a  bwhicha  bisa  bana  bintegera  bthata  bcannota  bholda  bvaluesa  bwitha  bdecimals,a  bwea  bcana  bdeclarea  bita  basa  baa  bdouble.a  bia  bwoulda  bbea  btempteda  btoa  bsaya  bthata  bdoublea  bdataa  btypesa  barea  bsuperiora  btoa  bintegersa  bina  bthea  bsensea  bthata  bdoublea  bdataa  btypesa  barea  bcapablea  bofa  bholdinga  bdecimala  bnumbers.a  bherea  bisa  bhowa  boura  bprograma  bwoulda  blooka  blike

![Image00068.jpg](images/Image00068.jpeg)a  b

Whilea  bthea  bprograma  bcodea  blooksa  bsoa  bmucha  bbettera  bsoa  bfar,a  btherea  bisa  balsoa  bsomethinga  bnota  bentirelya  bcorrecta  bwitha  bit,a  banda  bifa  byoua  bruna  bthea  bprogram,a  byoua  bwilla  bstilla  bnota  bgeta  bthea  brighta  banswer.a  bcana  byoua  bguessa  bwhy?A  bbecausea  bofa  bsomethinga  bcalleda  btruncation.a  bthisa  bmighta  bsounda  bcomplicateda  bbuta  bis,a  bina  bfact,a  bnot.a  bina  bthea  babovea  bprograma  bcode,a  bxa  banda  bya  barea  bintegers.a  basa  bwea  bhavea  bseen,a  byoua  bcannota  bgeta  bthea  bcorrecta  banswera  bifa  bthea  btwoa  bintegersa  bresulta  bina  baa  bdecimal.

Simplya  bput,a  bthisa  bisa  bthea  bmeaninga  bofa  btruncation.a  btoa  bfixa  bthis,a  bonea  bofa  bthea  bvariablesa  bhasa  btoa  bbea  bdoublea  btype.a  bdoinga  bthisa  bpromptsa  bthea  bcompilera  btoa  brecognizea  bthisa  banda  bconverta  bthea  bothera  bintegera  bintoa  baa  bdoublea  balbeita  btemporarily.a  balternatively,a  byoua  bcana  bsimplya  bdeclarea  beacha  bvariablea  basa  baa  bdouble;a  bthisa  bisa  bsomethinga  bata  byoura  bdiscretion.a  bherea  bisa  bhowa  bthea  bfulla  bprograma  bcodea  bwoulda  blook.

![Image00069.jpg](images/Image00069.jpeg)a  b

Witha  beverythinga  bwea  bhavea  bseena  bsoa  bfara  bina  boura  bc++a  blearninga  bexperience,a  byoua  barea  bwella  bona  byoura  bwaya  btoa  bbecominga  baa  bmastera  bcoder.a  bnevertheless,a  bpracticea  bisa  bkey.

Typesa  bofa  bconstantsa  bina  bprogramming

Integera  bconstants

Firsta  bthinga  bfirst,a  bintegersa  barea  bstoreda  bina  bbinarya  bformation.a  byou’lla  bcodea  bintegersa  basa  byoua  busea  bthema  bina  byoura  bdailya  broutine;a  bfora  bexample,a  byoua  bwilla  bcodea  beighta  bsimplya  basa  b8.

Thea  bfollowinga  btablea  bwilla  bshowa  byoua  bdifferenta  bintegers,a  btheira  bvaluesa  bina  bprogramminga  banda  btheira  bdataa  btypes

![Image00070.jpg](images/Image00070.jpeg)a  b

Charactera  bconstants

Whenever,a  byou’lla  bfinda  bana  binteger,a  bcloseda  bbetweena  btwoa  bsinglea  bapostrophes,a  bthisa  bwoulda  bbea  bcharactera  bconstant.a  bmoreover,a  btherea  bisa  baa  bchancea  bthata  byou’lla  bfinda  baa  bbackslasha  b“\”a  bbetweena  bthosea  bapostrophes.

Fora  bmosta  bmachines,a  basclla  bcharactera  bseta  bisa  bused,a  bi.e.

![Image00071.jpg](images/Image00071.jpeg)a  b

![Image00072.jpg](images/Image00072.jpeg)a  b

Floata  bconstants

Floata  bconstantsa  barea  bstoreda  basa  btwoa  bpartsa  bina  bmemorya  basa  bfloata  bconstantsa  barea  bnumbersa  bhavinga  bdecimala  bparts.a  bthea  bfirsta  bpart,a  btheya  bobtaina  bina  bmemorya  bisa  bsignificant,a  banda  bthea  bseconda  bisa  bthea  bexponent.

Floata  bconstant’sa  bdefaulta  btypea  bisa  b“double”.a  byoua  bmusta  bwritea  bcodea  btoa  bspecifya  byoura  bdesireda  bdataa  btype,a  bi.e.,a  b“float”a  bora  b“longa  bdouble”.a  bwea  bmaya  bremembera  bthata  b“f”a  bora  b“f”a  bisa  buseda  btoa  brepresenta  bfloat,a  banda  b“l”a  bora  b“l”a  bisa  buseda  btoa  brepresenta  blonga  bdouble.

Ina  bthea  bfollowinga  btable,a  bsomea  bofa  bthea  bexamplesa  bofa  bfloat,a  bdoublea  banda  blonga  bdouble.area  bshown:

![Image00073.jpg](images/Image00073.jpeg)a  b

![Image00074.jpg](images/Image00074.jpeg)a  b

Booleana  bconstants

Thesea  bconstantsa  barea  bpredefineda  bkeywords,a  banda  btheya  bcannota  bbea  bdefineda  bora  bdeclareda  bbya  bthea  bprogrammer.a  bita  bhasa  btwoa  bpredefineda  bconstants,a  b“true”a  banda  b“false”.a  bina  bprogramming,a  bwea  brepresenta  bthisa  bkinda  bofa  bconstanta  basa  b“bool”.

Programminga  bconstants

Ina  bthisa  bpart,a  bwea  barea  bgoinga  btoa  bunderstanda  bdifferenta  bprogramminga  bconstantsa  banda  bwaysa  btoa  bwritea  banda  bdefinea  bconstantsa  bina  baa  bc++a  bprogram.a  busually,a  btherea  barea  bthreea  btypesa  bofa  bprogramminga  bconstants.

Defineda  bconstants

Aa  bwaya  btoa  bdefinea  baa  bconstanta  bina  baa  bc++a  bprograma  bisa  btoa  busea  baa  bprecompilera  bstatementa  b“define”.a  blikea  beverya  bothera  bprecompilera  bdirective,a  bita  bstartsa  bwitha  baa  b“#”.a  bfora  bexample,a  baa  btraditionala  bprecompilera  bdirectivea  bfora  b“define”a  bwoulda  bbe:a  b#definea  btable_sizea  b150

Definea  bdirectivesa  barea  busuallya  bplaceda  bata  bthea  bbeginninga  bofa  bthea  bprograma  bsoa  bthata  banyonea  breadinga  byoura  bprograma  bcana  bfinda  bthema  beasily.

Memorya  bconstants

Anothera  bwaya  btoa  bcodea  bconstantsa  bisa  bbya  businga  baa  bmemorya  bconstant.a  bthesea  bconstantsa  busea  baa  bc++a  btypea  bqualifiera  btoa  bremembera  bthata  bthea  bspecifieda  bdataa  bcannota  bbea  bchanged.

C++a  bprogramminga  bprovidesa  busa  bwitha  bana  babilitya  btoa  bdefinea  bnameda  bconstants.a  bwea  bjusta  bhavea  btoa  badda  btypea  bqualifiera  bina  boura  bcode,a  bbeforea  bconstant.a  bfora  bexample:a  bcode:

#includea  b<iostream>

Usinga  bnamespacea  bstd;

#definea  bvala  b50

#definea  bfloatvala  b9.7

#definea  bcharvala  b‘k’

Inta  bmain()

{

Couta  b<<a  b“integera  bconstanta  bina  boura  bcode:a  b"a  b<<a  bvala  b<<a  b“\n”;a  bcouta  b<<a  b“floatinga  bpointa  bconstanta  bina  boura  bcode:a  b"a  b<<a  bfloatvala  b<<a  b“\n”;a  bcouta  b<<a  b“charactera  bconstanta  bina  boura  bcode:a  b“<<a  bcharvala  b<<a  b“\n”;a  breturna  b0;

}

Output:

Ina  bthea  bcasea  bofa  bthisa  bcode,a  baa  bconsolea  bscreena  bwilla  bpopa  bupa  bwitha  bthea  boutput:

Integera  bconstanta  bina  boura  bcode:a  b50

Floating-pointa  bconstanta  bina  boura  bcode:a  b9.7

Charactera  bconstanta  bina  boura  bcode:a  bk

Literala  bconstants

Aa  bliterala  bconstanta  bisa  baa  bconstanta  bwhicha  bisa  bunnameda  banda  buseda  btoa  bspecifya  byoura  bdesireda  bdata.a  basa  bwea  bknow,a  baa  bconstanta  bcannota  bbea  bchanged,a  bsoa  bwea  bjusta  bhavea  btoa  bcodea  bitsa  bdataa  bvaluea  bina  baa  bstatement.

Aa  bliterala  bconstanta  bisa  bthea  bmosta  bcommona  bforma  bofa  bconstant.a  bherea  bisa  baa  btablea  btoa  bshowa  baa  bdifferenta  bkinda  bofa  bliterala  bconstants.

![Image00075.jpg](images/Image00075.jpeg)a  b

Chaptera  b3:a  bfunctions

Youa  bmaya  bremembera  bfroma  bmatha  bclassa  bata  bsomea  bpointa  bwherea  byoua  bhada  btoa  bdeala  bwitha  bfunctions,a  blikea  bf(x)a  b=a  b2xa  b+a  b5.a  bf(0)a  bwoulda  bhavea  bbeena  b5a  b(2(0)a  b=a  b5),a  bf(1)a  bwoulda  bhavea  bbeena  b7a  b(2(1)a  b+a  b5),a  bf(2)a  bwoulda  bhavea  bbeena  b9a  b(2(2)a  b+a  b5),a  banda  bsoa  bon.

Functionsa  bina  bc++a  bworka  bsimilarly.

Functionsa  boperatea  banda  bthena  boftena  breturna  baa  bvalue.a  btheya  bdon’ta  balwaysa  bhavea  btoa  breturna  baa  bvalue.a  bhowevera  b-a  bfunctionsa  bthata  bdon’ta  breturna  baa  bvaluea  barea  bvoida  bfunctions.

First,a  btakea  baa  blooka  bata  bthisa  bchunka  bofa  bcode.a  bita  bdoesn’ta  bhavea  btoa  bmakea  bsensea  brighta  bnow;a  bwe’rea  bgoinga  btoa  bgoa  bthrougha  bit.a  bcreatea  baa  bnewa  bprojecta  banda  berasea  bthea  bcontentsa  bofa  bmain.cpp,a  banda  btypea  bthisa  bin.

#includea  b<iostream>

Usinga  bnamespacea  bstd;

Inta  bgetarea(inta  bl,a  binta  bw);

Inta  bmain()

{

Inta  blength,a  bwidth;

Couta  b<<a  b“entera  bthea  blength,a  banda  bthena  bentera  bthea  bwidth.\n”;

Cina  b>>a  blengtha  b>>a  bwidth;

Couta  b<<a  b“thea  bareaa  bis:a  b"a  b<<a  bgetarea(length,a  bwidth);

Returna  b0;

}

Inta  bgetarea(inta  bl,a  binta  bw)a  b{

Inta  bareaa  b=a  bla  b*a  bw;

Returna  barea;

}

Soa  blet’sa  bbreaka  bthisa  bdowna  blinea  bbya  bline.

#includea  b<iostream>

Thisa  bincludesa  bthea  bessentiala  bcomponentsa  bfora  binputa  banda  boutput.

Usinga  bnamespacea  bstd;

Thisa  bdenotesa  bthata  bwe’rea  businga  bthea  bstandarda  binput/outputa  bnamespace.

Inta  bgetarea(inta  bl,a  binta  bw);

Thisa  bisa  bwherea  bwea  bdeclarea  boura  bfirsta  bfunction.a  bc++a  bisa  bprocedurallya  bcompiled,a  bsoa  byoua  bcan’ta  bjusta  bthrowa  bfunctionsa  barounda  bwilly-nilly.a  byoua  bhavea  btoa  bdeclarea  bthema  bbeforea  byoua  bwritea  bthema  blater,a  bora  btheya  bhavea  btoa  bwritea  bentirelya  bbeforea  byoura  bmaina  bfunction.a  bfora  bthea  bsakea  bofa  bclarity,a  bia  bprefera  bthea  binitiala  bdeclarationa  banda  bthena  bwritinga  bthea  bfunctiona  baftera  bmya  bmaina  bfunction,a  bbuta  bit’sa  baa  bpersonala  bchoice.a  bregardless,a  bwe’rea  bcreatinga  baa  bfunctiona  bherea  bcalleda  b“getarea”.a  bthea  binta  bbeforea  bthea  bnamea  bdenotesa  bthata  bit’sa  bgoinga  btoa  breturna  bana  bintegera  bvalue.a  blikewise,a  baa  bfloata  bgetarea(…)a  bwoulda  breturna  baa  bfloata  bvalue,a  baa  bchara  bgetchararacter(…)a  bwoulda  breturna  baa  bcharacter,a  banda  bsoa  bon.

Withina  bthea  bdeclaration,a  bwe’vea  bgivena  btwoa  bvariables,a  bcalleda  barguments.a  bmucha  blikea  bhowa  bina  bf(x)a  bequations,a  bxa  bwasa  bthea  bthinga  bthata  bthea  bequationa  bmodified,a  bthea  bargumenta  bvariablesa  barea  bwhata  boura  bc++a  breadsa  bina  banda  butilizes.

Inta  bmain()

{

Thisa  bisa  bthea  bstarta  bofa  boura  bmaina  bfunction.a  bina  bcasea  byoua  bhaven’ta  bfigureda  bita  bout,a  beverya  bprograma  bmusta  bhavea  baa  bmaina  bfunction.a  bit’sa  bthea  bentrya  bpointa  bfora  byoura  bcode,a  banda  bthea  bcompilera  bwilla  bactivelya  bseeka  bita  bout.

Inta  blength,a  bwidth;

Wea  bdeclarea  btwoa  bvariables,a  blength,a  banda  bwidth.

Couta  b<<a  b“entera  bthea  blength,a  banda  bthena  bentera  bthea  bwidth.\n”;

Cina  b>>a  blengtha  b>>a  bwidth;

Wea  baska  bthea  busera  btoa  binputa  bthea  blengtha  banda  bwidth,a  banda  bthena  baccepta  btheira  binput.

Couta  b<<a  b“thea  bareaa  bis:a  b“a  b<<a  bgetarea(length,a  bwidth);

Thisa  bisa  bwherea  baa  bbita  bofa  bfurthera  bexplanationa  bisa  bneeded.a  bthea  boutputa  bstreama  bputsa  bouta  baa  bvaluea  bwea  bgivea  bit,a  bright?A  bsincea  bfunctionsa  bsimplya  breturna  baa  bvalue,a  bwea  bcana  bputa  bthema  bstraighta  bina  bthea  boutputa  bstream.

Also,a  bsincea  bthisa  bfunctiona  breturnsa  bana  bintegera  bvalue,a  byoua  bcoulda  bcreatea  baa  bnewa  bintegera  banda  bthena  bassigna  bitsa  bvaluea  basa  bthea  bvaluea  bofa  bthea  bfunction,a  blikea  bthis:a  binta  bareaa  b=a  bgetarea(length,a  bwidth);

Youa  bcoulda  bthena  bjusta  boutput:

Couta  b<<a  b“thea  bareaa  bis:a  b“a  b<<a  barea;

Thisa  bisa  baa  bwaste,a  bthough,a  bbecausea  bthisa  bvariablea  bdoesn’ta  bneeda  btoa  bbea  bcreateda  bfora  bthisa  bprogram.a  bifa  byoua  bdo,a  bhowever,a  bneeda  btoa  bstorea  baa  bvariablea  bsucha  basa  bthea  bareaa  bofa  baa  brectangle,a  byoua  bcoulda  bdoa  bexactlya  bthat.

Returna  b0;

}

Simple,a  beverya  bmaina  bfunctiona  bmusta  breturna  b0.

Inta  bgetareaa  b(inta  bl,a  binta  bw)a  b{

Thisa  bmirrorsa  bthea  bfunctiona  bdeclarationa  bearliera  banda  bisa  bwherea  bwea  bstarta  bwritinga  bit.

Inta  bareaa  b=a  bla  b*a  bw;

Returna  barea;

Wea  bcreatea  baa  bnewa  bvariablea  bcalleda  barea,a  bwhicha  btakesa  bthea  btwoa  bargumentsa  bfroma  bthea  bfunctiona  bheadera  banda  bmultipliesa  bthema  btoa  bgeta  bitsa  bvalue.a  bwea  bthena  breturna  bthata  bsamea  binteger.

Wea  balsoa  bcoulda  bhavea  bsimplya  bwrittena  bthis:

Returna  bla  b*a  bw;

Botha  barea  bvalida  bwaysa  bofa  breturninga  bthisa  bfunctiona  banda  bwilla  bgivea  byoua  bana  bappropriatea  bresult.

That’sa  baa  bcursorya  bintroductiona  btoa  bfunctions.a  bthey’rea  baa  bvitala  bwaya  bofa  bstructuringa  byoura  bprogram.a  bprograms,a  bwherea  beverythinga  bisa  bonlya  bina  bonea  bfunction,a  barea  btediousa  btoa  breada  banda  bchallenginga  btoa  bmaintain.a  bprograms,a  bwherea  bthingsa  barea  bmorea  bsplita  bup,a  barea  beasiera  btoa  bunderstanda  banda  bmanagea  bbya  bfar.

Chaptera  b4:a  bpolymorphism

Polymorphisma  bmeansa  btoa  bexista  bina  bmanya  bforms.a  bina  bprograming,a  bpolymorphisma  boccursa  bwhena  bwea  bhavea  bmanya  bclassesa  bthata  barea  brelateda  btoa  beacha  bothera  bthrougha  binheritance.

Ina  bc++,a  bpolymorphisma  bmeansa  bthata  baa  bcalla  btoa  baa  bfunctiona  bwilla  bleada  btoa  bthea  bexecutiona  bofa  baa  bdifferenta  bfunctiona  bdependinga  bona  bthea  btypea  bofa  bobjecta  bthata  bhasa  binvokeda  bthea  bfunction.a  bconsidera  bthea  bexamplea  bgivena  bbelowa  bina  bwhicha  bwea  bhavea  baa  bbasea  bclassa  bderiveda  bora  binheriteda  bbya  btwoa  bothera  bclasses:

#includea  b<iostream>usinga  bnamespacea  bstd;

Classa  bfigurea  b{

Protected:a  binta  bbreadth,a  blength;

Public:a  bfigure(inta  bxa  b=0,a  binta  bya  b=a  b0){

Breadtha  b=a  bx;a  blengtha  b=a  by;a  b}

Inta  barea()a  b{

Couta  b<<“areaa  bofa  bparenta  bclassa  bisa  b:”<<endl;a  breturna  b0;a  b}

};classa  brectangle:a  bpublica  bfigurea  b{

Public:a  brectangle(a  binta  bxa  b=a  b0,a  binta  bya  b=a  b0):figure(x,a  by)a  b{}

Inta  bareaa  b(){

Couta  b<<a  b“areaa  bofa  brectanglea  bclassa  bisa  b:”a  b<<endl;returna  b(breadtha  b*a  blength);a  b}

};

Classa  bsquare:a  bpublica  bfigurea  b{

Public:a  bsquare(inta  bxa  b=0,a  binta  bya  b=a  b0):figure(x,a  by)a  b{}

Inta  bareaa  b()a  b{

Couta  b<<“areaa  bofa  bsquarea  bclassa  bisa  b:”<<endl;a  breturna  b(breadtha  b*a  blength);a  b}

};

//a  bmaina  bfunction

Inta  bmain()a  b{

Figurea  b*figure;a  brectanglea  brec(10,7);a  bsquarea  bsq(5,5);

//a  bstorea  baddressa  bofa  brectanglefigurea  b=&rec;

//a  bcalla  brectanglea  barea.

Figure->area();

//a  bstorea  bthea  baddressa  bofa  bsquarefigurea  b=&sq;

//a  bcalla  baquarea  barea.

Figure->area();

Returna  b0;a  b}

Thea  bcodea  bwilla  breturna  bthea  bfollowinga  boutput:

![Image00076.jpg](images/Image00076.jpeg)a  b

Thea  boutputa  bisa  bincorrect.a  bthea  breasona  bfora  bthisa  bisa  bthata  bthea  bcalla  bofa  barea()a  bfunctiona  bhasa  bbeena  bseta  bonlya  boncea  bbya  bthea  bcompilera  basa  bthea  bversiona  bthata  bhasa  bbeena  bdefineda  bina  bthea  bbasea  bclass.a  b|thisa  bisa  breferreda  btoa  basa  bstatica  bresolutiona  bora  bstatica  blinkagea  bofa  bthea  bfunctiona  bcall.a  bthea  bfunctiona  bcalla  bisa  bfixeda  bbeforea  bthea  bexecutiona  bofa  bthea  bprogram.a  bsometimes,a  bthisa  bisa  breferreda  btoa  basa  bearlya  bbindinga  bsincea  boura  bareaa  bhasa  bbeena  bseta  bduringa  bthea  bcompilationa  bofa  bthea  bprogram.

Leta  busa  bmakea  baa  bmodificationa  btoa  bthea  bcodea  bsoa  bthata  bthea  barea()a  bfunctiona  bisa  bdeclareda  bwithina  bthea  bfigurea  bclass.a  bhowever,a  bwea  bwilla  bdeclarea  bita  bwitha  bthea  bvirtuala  bkeyworda  basa  bshowna  bbelow:

Classa  bfigurea  b{

Protected:a  binta  bbreadth,a  blength;

Public:a  bfigure(inta  bxa  b=0,a  binta  bya  b=a  b0){

Breadtha  b=a  bx;a  blengtha  b=a  by;a  b}

Virtuala  binta  barea()a  b{

Couta  b<<“areaa  bofa  bparenta  bclassa  bisa  b:”<<endl;a  breturna  b0;a  b}

};

Thisa  bmeansa  byoua  bshoulda  bnowa  bhavea  bthea  bfollowinga  bcode:

#includea  b<iostream>usinga  bnamespacea  bstd;

Classa  bfigurea  b{

Protected:a  binta  bbreadth,a  blength;

Public:a  bfigure(inta  bxa  b=0,a  binta  bya  b=a  b0){

Breadtha  b=a  bx;a  blengtha  b=a  by;a  b}

Virtuala  binta  barea()a  b{

Couta  b<<“areaa  bofa  bparenta  bclassa  bisa  b:”<<endl;a  breturna  b0;a  b}

};classa  brectangle:a  bpublica  bfigurea  b{

Public:a  brectangle(a  binta  bxa  b=a  b0,a  binta  bya  b=a  b0):figure(x,a  by)a  b{}

Inta  bareaa  b()a  b{

Couta  b<<“areaa  bofa  brectanglea  bclassa  bisa  b:”<<endl;a  breturna  b(breadtha  b*a  blength);a  b}

};

Classa  bsquare:a  bpublica  bfigurea  b{

Public:a  bsquare(inta  bxa  b=0,a  binta  bya  b=a  b0):figure(x,a  by)a  b{}

Inta  bareaa  b()a  b{

Couta  b<<“areaa  bofa  bsquarea  bclassa  bisa  b:”<<endl;a  breturna  b(breadtha  b*a  blength);a  b}

};

//a  bmaina  bfunction

Inta  bmain()a  b{

Figurea  b*figure;a  brectanglea  brec(10,7);a  bsquarea  bsq(5,5);a  b//a  bstorea  baddressa  bofa  brectanglea  bfigurea  b=a  b&rec;

//a  bcalla  brectanglea  barea.

Figure->area();

//a  bstorea  bthea  baddressa  bofa  bsquarefigurea  b=a  b&sq;

//a  bcalla  baquarea  barea.

Figure->area();

Returna  b0;a  b}

Thea  bcodea  bshoulda  bnowa  breturna  bthea  bfollowinga  bresult:

![Image00077.jpg](images/Image00077.jpeg)a  b

Thea  bcompilera  bhasa  bconsidereda  bthea  belementsa  bofa  bthea  bpointera  brathera  bthana  bitsa  btype.a  bthea  bobjectsa  bofa  breca  banda  bsqa  bclassesa  bhavea  bbeena  bstoreda  bina  bthea  b*figure;a  btheira  brespectivea  bdefinitiona  bofa  bthea  barea()a  bfunctiona  bhasa  bbeena  bcalled.

Thisa  bshowsa  bthata  beacha  bofa  bthea  bderiveda  bclassesa  bhasa  baa  bdifferenta  bimplementationa  bofa  bthea  bfunctiona  bnameda  barea().a  bthisa  bisa  bknowna  basa  bpolymorphism.a  byoua  bhavea  bmorea  bthana  bonea  bclassa  bwitha  bthea  bsamea  bfunctiona  bnamea  banda  bthea  bsamea  bparameters,a  bbuta  bthea  bimplementationa  bisa  bdifferent.

Noticea  bthata  bwea  buseda  bthea  bvirtuala  bkeyworda  btoa  bmakea  bthea  bfunctiona  bvirtual.a  bwhena  baa  bvirtuala  bfunctiona  bisa  bdefineda  bina  bthea  bbasea  bclass,a  banda  banothera  bversiona  bina  bthea  bderiveda  bclass,a  bthisa  bwilla  bacta  basa  baa  bsignala  btoa  bthea  bcompilera  bthata  baa  bstatica  blinkagea  btoa  bthea  bfunctiona  bisa  bnota  bneeded.a  bwea  bonlya  bneeda  baa  bselectiona  bofa  bthea  bfunctiona  btoa  bbea  bcalleda  bata  banya  bpointa  bina  bthea  bprograma  bbaseda  bona  bthea  btypea  bofa  bobjecta  bfora  bwhicha  bthea  bfunctiona  bisa  bbeinga  bcalled.a  bthisa  boperationa  bisa  bknowna  basa  blatea  bbindinga  bora  bdynamica  blinkage.

Sometimes,a  byoua  bmaya  bneeda  bincludinga  baa  bvirtuala  bfunctiona  bina  bthea  bbasea  bclassa  bfora  bita  btoa  bbea  bredefineda  bina  baa  bderiveda  bclassa  btoa  bsuita  bthea  bclassa  bobjects,a  bbuta  byoua  bhavea  bnoa  bmeaningfula  bdefinitiona  btoa  bgivea  btoa  bthea  bfunctiona  bina  bthea  bbasea  bclass.

Ina  bsucha  baa  bcase,a  boura  bvirtuala  bfunctiona  barea()a  bina  bthea  bbasea  bclassa  bcana  bbea  bchangeda  btoa  bthea  bfollowing:

Classa  bfigurea  b{

Protected:a  binta  bbreadth,a  blength;

Public:a  bfigure(inta  bxa  b=0,a  binta  bya  b=a  b0){

Breadtha  b=a  bx;a  blengtha  b=a  by;a  b}

Virtuala  binta  barea()a  b=a  b0;a  b};

Noticea  bthea  busea  bofa  bthea  b=a  b0;a  bina  bthea  bfunction.a  bthisa  btellsa  bthea  bc++a  bcompilera  bthata  bthea  bfunctiona  bdoesn’ta  bhavea  baa  bbody.a  bsucha  baa  bfunctiona  bisa  bknowna  basa  baa  bpurea  bvirtuala  bfunction.

Objecta  bdestructiona  banda  bpolymorphism

Objecta  bdestructiona  bisa  btricky,a  bespeciallya  bwhena  bita  bcomesa  btoa  bthea  bobjecta  bbeinga  bdestroyeda  bthrougha  bana  binterface.a  byoua  bcoulda  bhavea  bcodea  blikea  bthis,a  bfora  bexample:

Classa  bdrawable

{

Public:

Virtuala  bvoida  bdrawa  b()a  b=a  b0;

};

Classa  bmydrawablea  b:a  bpublica  bdrawable

{

Public:

Virtuala  bvoida  bdrawa  b();

Mydrawablea  b();

~mydrawablea  b();

Private:

Inta  b*mydata;

};

Mydrawable::mydrawablea  b()

{

Mydataa  b=a  bnewa  bint;

}

Mydrawable::~mydrawablea  b()

{

Deletea  bmydata;

}

Voida  bdeletedrawablea  b(drawablea  b*drawable)

{

Deletea  bdrawable;

}

Inta  bmaina  b()

{

Deletedrawable(a  bnewa  bmydrawable()a  b);

}

What’sa  bgoinga  bona  binsidea  bdeletedrawable?A  bremember,a  bwhena  bdeletea  bgetsa  bused,a  bthea  bdestructora  bisa  bcalled,a  bsoa  bthea  blinea  bthata  breads

Deletea  bdrawable;

Makesa  baa  bfunctiona  bcalla  bona  bthea  bobject.a  bbuta  bhowa  bdoesa  bthea  bcompilera  bknowa  bwherea  bthea  bmydrawablea  bdestructora  bis?A  bthea  bcompilera  bdoesn’ta  bknowa  bwhata  bthea  bexacta  btypea  bofa  bthea  bdrawablea  bvariablea  bis,a  bbuta  bita  bdoesa  bknowa  bthata  bit’sa  baa  bdrawable,a  bsomethinga  bthata  bhasa  baa  bdraw()a  bmethod.a  balla  bita  bknowsa  bisa  bhowa  bthea  bmydrawablea  bdestructora  bitselfa  bcana  bfounda  bthea  bdestructora  bassociateda  bdrawable.a  basa  bmydrawablea  ballocatesa  bmemorya  bina  bitsa  bconstructor,a  btoa  bfreea  bthea  bmemory,a  bthea  bmydrawablea  bdestructora  bmusta  brun.

Okay,a  bsoa  byoua  bcoulda  bbea  bthinkinga  bthata  bthisa  bisa  bwhata  bvirtuala  bfunctionsa  barea  bdesigneda  btoa  bfix.a  bthat’sa  bcorrect.a  bwhata  bwea  bshoulda  bbea  bdoinga  bisa  bdeclaringa  bthea  bdestructora  bvirtuala  bina  bdrawable;a  bthata  bwaya  bthea  bcompilera  bwilla  bknowa  bthata  bita  bhasa  btoa  blooka  bfora  baa  bdestructora  bthata  bhasa  bbeena  boverriddena  bwhena  bdeletea  bhasa  bbeena  bcalleda  bona  baa  bpointera  btoa  baa  bdrawable:a  bclassa  bdrawable

{

Public:

Virtuala  bvoida  bdrawa  b();

Virtuala  b~drawablea  b();

};

Classa  bmydrawablea  b:a  bpublica  bdrawable

{

Public:

Virtuala  bvoida  bdrawa  b();

Mydrawablea  b();

Virtuala  b~mydrawablea  b();

Private:

Inta  b*mydata;

};

Whena  bwea  bmakea  bthea  bstructurea  bina  bthea  bsuperclassa  bvirtual,a  banda  bwhena  bdeletea  bfreesa  bupa  baa  bdrawablea  binterface,a  bthea  boverriddena  bdestructora  bgetsa  bcalled.

Asa  baa  brule,a  bwhena  byoua  bmakea  banya  bsuperclassa  bmethoda  bvirtual,a  bthea  bsuperclassa  bdestructora  bshoulda  bbea  bmadea  bvirtuala  basa  bwell.a  boncea  bonea  bmethoda  bhasa  bbeena  bmadea  bvirtual,a  byoua  barea  bsayinga  bthata  bthea  bclassa  bcana  bbea  bpasseda  barounda  btoa  bmethodsa  bthata  bwilla  btakea  bana  binterface.a  bthea  bmethodsa  bcana  bthena  bdoa  bwhatevera  btheya  bwant,a  banda  bthata  bincludesa  bdeletinga  bthea  bobject,a  bsoa  bmakinga  bthea  bdestructora  bvirtuala  bmakesa  bsurea  bthata  bthea  bobjecta  bisa  bcleaneda  bupa  bproperly.

## Chaptera  b5:a  boperatora  btypea  banda  boverloading

Operatorsa  bina  bc++

C++a  bprovidesa  baa  bricha  bseta  bofa  boperatorsa  bthata  bperforma  baa  bnumbera  bfora  bdifferenta  bfunctionsa  bona  bconstantsa  banda  bvariables.

C++a  bhasa  bmainlya  bfollowinga  btypesa  bofa  boperators:

Arithmetica  boperatorsa  basa  baddition,a  bmultiplication,a  betc.

Relationala  boperatorsa  basa  blessa  bthan,a  bgreatera  bthan,a  betc.

Logicala  boperatorsa  basa  band,a  bor,a  betc.

Bitwisea  boperators

Assignmenta  boperators

Arithmetica  boperators

C++a  bmainlya  bprovidesa  b7a  barithmetica  boperators.a  bwea  bwilla  bdiscussa  beacha  boperatora  bwitha  btwoa  bvariablesa  bxa  banda  bya  bwherea  bxa  bhasa  bvaluea  basa  b45a  banda  bya  bhasa  bvaluea  bhasa  b25.

![Image00078.jpg](images/Image00078.jpeg)a  b

Relationala  boperators

C++a  bmainlya  bprovidesa  b7a  brelationala  boperators.a  bthesea  boperatorsa  bprovidea  baa  bresultanta  bvaluea  basa  btruea  bora  bfalsea  banda  bgenerallya  buseda  bina  bconditiona  bchecks.a  bwea  bwilla  bunderstanda  bthea  bmeaninga  bofa  beacha  boperatora  bwitha  btwoa  bvariablesa  bxa  banda  bya  bwherea  bxa  bhasa  bvaluea  basa  b45a  banda  bya  bhasa  bvaluea  bhasa  b25.

![Image00079.jpg](images/Image00079.jpeg)a  b

![Image00081.jpg](images/Image00081.jpeg)![Image00080.jpg](images/Image00080.jpeg)a  b

Logicala  boperators

C++a  bsupportsa  bthea  bfollowinga  b3a  blogicala  boperators,a  bwhicha  bwea  bwilla  bexplaina  businga  btwoa  bvariablesa  bxa  banda  bya  bwherea  bxa  bhavinga  bvaluea  basa  b0a  banda  bya  bhavinga  bvaluea  basa  b1.

A  b

Bitwisea  boperators

Bitwisea  boperatorsa  bperforma  btheira  bfunctionalitya  bbita  bbya  bbit.a  bbitwisea  banda  boperatora  bperformsa  banda  boperatora  bona  beverya  btwoa  bcorrespondinga  bbitsa  bofa  btwoa  boperandsa  banda  bbitwisea  bora  bperformsa  bora  boperatora  bona  beverya  btwoa  bcorrespondinga  bbitsa  bofa  btwoa  boperands

![Image00082.jpg](images/Image00082.jpeg)a  b

Assumea  bifa  bxa  b=a  b13;a  banda  bya  b=a  b60;

Xa  b=a  b0000a  b1101

Ya  b=a  b0011a  b1100

X|ya  b=a  b0011a  b1101

X&ya  b=a  b0000a  b1100

Tablea  bshowinga  bbitwisea  boperatora  bwitha  bp=a  b60a  banda  bqa  b=a  b13

![Image00083.jpg](images/Image00083.jpeg)a  b

![Image00084.jpg](images/Image00084.jpeg)a  b

Assignmenta  boperators

![Image00085.jpg](images/Image00085.jpeg)a  b

![Image00086.jpg](images/Image00086.jpeg)a  b

Operatorsa  bprecedencea  banda  bassociativity

Everya  boperatora  bhasa  bprecedencea  banda  bassociativitya  bassociateda  bwitha  bit.a  bprecedencea  bofa  boperatorsa  bisa  buseda  bina  bdetermininga  bthea  bsequencea  bofa  boperatorsa  bfora  bevaluatinga  bana  bexpressiona  bina  bcasea  bexpressiona  bhasa  bseverala  boperators.a  bina  bana  bexpression,a  bthea  boperatorsa  bhavinga  bhighera  bprecedencea  barea  bevaluateda  bfirst.

Associativitya  bisa  bthea  bconcepta  bfora  bdetermininga  bthea  bevaluationa  bordera  bofa  boperatorsa  bwhena  btherea  barea  bmultiplea  boperatorsa  bwitha  bthea  bsamea  bprecedence,a  bthena  bassociativea  bdeterminesa  beithera  btoa  bbea  bevaluateda  bfroma  blefta  btoa  brighta  bora  brighta  btoa  bleft.

![Image00087.jpg](images/Image00087.jpeg)a  b

Overloading

Ina  bc++,a  bwea  bcana  bspecifya  bmorea  bthana  bonea  bdefinitiona  bfora  baa  bfunctiona  bora  boperatora  bwithina  bthea  bsamea  bscope.a  bthesea  barea  bprocessesa  bknowna  basa  bfunctiona  boverloadinga  banda  boperatora  boverloading,a  brespectively.

Ana  boverloadeda  bdeclarationa  bisa  bdonea  bwithina  bthea  bsamea  bscopea  basa  bthea  bpreviousa  bdeclaration,a  bbuta  bbotha  bdefinitionsa  bhavea  bdifferenta  bargumentsa  banda  baa  bdifferenta  bimplementation/definition.

Aftera  bcallinga  bana  boverloadeda  bfunctiona  bora  boperator,a  bthea  bcompilera  bwilla  bdeterminea  bthea  bmosta  bappropriatea  bdefinitiona  btoa  busea  bbya  bcomparinga  bthea  btypesa  bofa  bargumentsa  bthata  byoua  bhavea  buseda  btoa  bcalla  bthea  bfunctiona  bora  boperatora  bwitha  bthea  btypesa  bofa  bparametersa  bthata  bhavea  bbeena  bspecifieda  bina  bthea  bdefinition.a  bthea  bprocessa  bofa  bdetermininga  bthea  bmosta  bappropriatea  bdefinitiona  btoa  busea  bisa  breferreda  btoa  basa  boverloada  bresolution.

Operatorsa  boverloading

C++a  ballowsa  byoua  btoa  bredefinea  bora  boverloada  bthea  bmajoritya  bofa  bitsa  bin-builta  boperators.a  bthisa  bmeansa  bthata  bprogrammersa  bcana  busea  boperatorsa  bwitha  buser-defineda  btypes.

Overloadeda  boperatorsa  barea  bsimplea  bfunctionsa  bwitha  bspeciala  bnames,a  bthata  bis,a  bthea  boperatora  bkeyworda  banda  bthena  bsymbola  bofa  bthea  boperatora  bthata  bisa  bundera  bthea  bdefinition.a  bjusta  blikea  baa  bfunctiona  bdefinition,a  bana  boverloadeda  boperatora  bwilla  bhavea  baa  breturna  btypea  banda  baa  blista  bofa  bparameters.a  bthea  bdefinitiona  bofa  bana  boverloadeda  boperatora  bisa  bdemonstrateda  bbelow:

Rectanglea  boperator+(consta  brectangle&);

Ina  bthea  bexamplea  bgivena  bbelow,a  bwea  barea  bdemonstratinga  bthea  bprocessa  bofa  boperatora  boverloadinga  bbya  bthea  busea  bofa  baa  bmembera  bfunction.a  bwea  bwilla  bpassa  bana  bobjecta  basa  bana  bargument,a  banda  bthea  bpropertiesa  bofa  bthea  bobjecta  bwilla  bbea  baccesseda  businga  bthea  bobject.a  bthea  bobjecta  bthata  bwilla  bcalla  bthea  boperatora  bwilla  bbea  baccessiblea  bbya  busea  bofa  bthisa  boperatora  basa  bdemonstrateda  bbelow:

#includea  b<iostream>usinga  bnamespacea  bstd;

Classa  brectanglea  b{

Public:a  bdoublea  bgetarea(void){

Returna  blengtha  b*a  bbreadth;}

Voida  bsetlength(a  bdoublea  blena  b)a  b{

Lengtha  b=a  blen;a  b}

Voida  bsetbreadth(a  bdoublea  bbrea  b)a  b{

Breadtha  b=a  bbre;a  b}

//a  boverloada  bthea  b+a  boperatora  btoa  badda  btwoa  brectanglea  bobjects.

Rectanglea  boperator+(consta  brectangle&a  br)a  b{

Rectanglea  brect;rect.lengtha  b=this->lengtha  b+a  br.length;rect.breadtha  b=this->breadtha  b+a  br.breadth;returna  brect;a  b}

Private:a  bdoublea  blength;a  b//a  blengtha  bofa  baa  brectanglea  bdoublea  bbreadth;a  b//a  bbreadtha  bofa  baa  brectanglea  b};

//a  bmaina  bfunction

Inta  bmain()a  b{

Rectanglea  brectangle1;a  b//a  bdeclarea  brectangle1a  bofa  btypea  brectanglea  brectanglea  brectangle2;a  b//a  bdeclarea  brectangle2a  bofa  btypea  brectanglea  brectanglea  brectangle3;a  b//a  bdeclarea  brectangle3a  bofa  btypea  brectanglea  bdoublea  bareaa  b=a  b0.0;a  b//a  bstorea  bthea  bareaa  bofa  baa  brectanglea  bhere

//a  brectanglea  b1a  bspecificationrectangle1.setlength(6.0);rectangle1.setbreadth(7.0);

//a  brectanglea  b2a  bspecificationrectangle2.setlength(12.0);rectangle2.setbreadth(13.0);

//a  bareaa  bofa  brectanglea  b1

Areaa  b=a  brectangle1.getarea();a  bcouta  b<<“areaa  bofa  brectangle1a  b:a  b“<<a  bareaa  b<<endl;

//a  bareaa  bofa  brectanglea  b2

Areaa  b=a  brectangle2.getarea();a  bcouta  b<<“areaa  bofa  brectangle2a  b:a  b“<<a  bareaa  b<<endl;

//a  baddinga  btwoa  bobjects:a  brectangle3a  b=a  brectangle1a  b+a  brectangle2;

//a  bareaa  bofa  brectanglea  b3

Areaa  b=a  brectangle3.getarea();a  bcouta  b<<“areaa  bofa  brectangle3a  b:a  b“<<a  bareaa  b<<endl;

Returna  b0;a  b}

Whena  bexecuted,a  bthea  bcodea  bwilla  breturna  bthea  bfollowing:

![Image00088.jpg](images/Image00088.jpeg)a  b

Considera  bthea  bfollowinga  bsectiona  bextracteda  bfroma  bthea  babovea  bcode:

Rectanglea  boperator+(consta  brectangle&a  br)a  b{

Rectanglea  brect;a  brect.lengtha  b=this->lengtha  b+a  br.length;a  brect.breadtha  b=this->breadtha  b+a  br.breadth;a  breturna  brect;a  b}

Thisa  bisa  bwherea  bthea  bmechanisma  bofa  boperatora  boverloadinga  bhasa  bbeena  bimplemented.a  bwea  bhavea  boverloadeda  bthea  b+a  boperatora  bsoa  bthata  bita  baddsa  bthea  bmeasurementsa  bofa  btwoa  brectanglea  bobjects.a  bherea  bisa  banothera  blinea  bextracteda  bfroma  bthea  bcode:

Rectangle3a  b=a  brectangle1a  b+a  brectangle2;

Ina  bthea  babovea  bline,a  brectangle1willa  bbea  baddeda  btoa  brectangle2.a  bthisa  bmeansa  bthata  bthea  blengtha  bofa  brectangle1a  bwilla  bbea  baddeda  btoa  bthea  blengtha  bofa  brectangle2a  btoa  bgeta  bthea  blengtha  bofa  brectangle3a  bwhilea  bthea  bbreadtha  bofa  brectangle1a  bwilla  bbea  baddeda  btoa  bthea  bbreadtha  bofa  brectangle2a  btoa  bgeta  bthea  bbreadtha  bofa  brectangle3.a  bthesea  btwoa  bwilla  bthena  bbea  bmultiplieda  btoa  bgivea  bthea  bareaa  bofa  brectangle3.

Thea  bmeaninga  bofa  b+a  boperatora  bhasa  bbeena  boverloaded!

## Chaptera  b6:a  bmacrosa  banda  btemplate

Introductiona  btoa  btemplates

Templatesa  barea  bana  bimportanta  bfeaturea  bina  bc++a  bprogramminga  blanguage,a  basa  bita  ballowsa  bfunctionsa  banda  bclassesa  btoa  busea  bgenerica  btypes.a  btheya  bplaya  bana  bessentiala  brolea  bina  bhowa  bfunctionsa  banda  bclassesa  bworka  bbya  ballowinga  bthema  btoa  bdefinea  bdifferenta  bdataa  btypesa  bwithouta  brewritinga  beacha  bother.

Usinga  btemplates,a  byoua  bcana  bwritea  baa  bgenerica  bcodea  bthata  bcana  bbea  buseda  bwitha  banya  bdataa  btype.a  balla  byoua  bneeda  bisa  btoa  bpassa  bthea  bdataa  btypesa  basa  bparameters.a  btemplatesa  bpromotea  bcodea  breusabilitya  banda  bimprovea  bthea  bflexibilitya  bofa  bthea  bprogram.a  byoua  bcana  bcreatea  baa  bsimplea  bclassa  bora  baa  bfunctiona  banda  bpassa  bdataa  btypesa  basa  bparametersa  banda  bimplementa  bthea  bcodea  btoa  bbea  buseda  bbya  banya  bdataa  btype.a  bwhenevera  byoua  bwanta  btoa  busea  bthea  bfunction,a  byoua  bmakea  baa  bcalla  btoa  bthea  bfunctiona  banda  bspecifya  bthea  breturna  btype.

Fora  bexample,a  bifa  byoua  busea  bsort()a  bfunctiona  btoa  bsorta  bdataa  bina  baa  bwarehouse,a  byoua  bcana  bpassa  bdifferenta  bdataa  btypesa  basa  bparametersa  btoa  bthea  bfunction.a  byoua  bdon’ta  bhavea  btoa  bwritea  banda  bmaintaina  bmultiplea  bfilea  bcodesa  btoa  bsorta  bdata.a  bbaseda  bona  bthea  bdataa  btypea  bpasseda  btoa  bthea  bsortinga  balgorithm,a  byoura  bdataa  bina  bthea  bwarehousea  bisa  bsorteda  birrespectivea  bofa  bthata  bparticulara  bdataa  btype.a  btherefore,a  btemplatesa  barea  buseda  bina  bsituationsa  bwherea  byoua  bneeda  baa  bcodea  btoa  bbea  breusablea  bwitha  bmorea  bthana  bonea  bdataa  btype.

Templatesa  barea  bofa  bgreata  bimportancea  bwhena  bdealinga  bwitha  bmultiplea  binheritancea  banda  boperatora  boverloading.a  bita  bisa  bwidelya  bapplieda  bwherea  bcodea  breusabilitya  bisa  bofa  bprimea  bimportance.

Typesa  bofa  btemplates

Templatesa  barea  bimplementeda  bina  btwoa  bways:

●a  businga  bfunctiona  btemplates

●a  businga  bclassa  btemplates

Aa  btemplatea  bcana  bbea  bdefineda  basa  baa  bmacro.a  bthata  bisa  bwhena  byoua  bdefinea  bana  bobjecta  bofa  baa  bspecifica  btype,a  bthea  btemplatea  bdefinitiona  bofa  bthata  btypea  bofa  bclassa  bsubstitutesa  bita  bwitha  bthea  bappropriatea  bdataa  btype.a  btemplatesa  barea  boftena  breferreda  btoa  basa  bparameterizeda  bclassa  bora  bfunctionsa  bsincea  baa  bspecifieda  bdataa  btypea  bwilla  breplacea  bthea  bdefineda  bparametera  bduringa  bexecutiona  btime.

Classa  btemplates

Classa  btemplatesa  boffera  bthea  bspecificationsa  bfora  bcreatinga  baa  bclassa  bbaseda  bona  bthea  bparameters.a  baa  bclassa  btemplatea  bacceptsa  bmembersa  bwitha  bparametera  btype.a  bthata  bis,a  byoua  bcana  binstantiatea  baa  bclassa  btemplatea  bbya  bpassinga  baa  bgivena  bseta  bofa  bdataa  btypea  btoa  bitsa  bparametera  blist.a  bclassa  btemplatesa  barea  bmostlya  buseda  bina  bimplementinga  bcontainers.

Syntax

Templatea  b<classa  bidentifier>

Classa  bclass-name

{

…

//classa  bmembera  bspecifications

…

};

Example:

![Image00089.jpg](images/Image00089.jpeg)a  b

Aa  bclassa  btemplatea  bdefinitiona  bisa  bsimilara  btoa  bnormala  bclassa  bdefinitiona  bexcepta  bthata  bina  btemplates,a  byoua  badda  baa  bprefixa  btemplatea  b<classa  bm>a  bwherea  bma  bisa  bthea  btype.a  bthea  btemplatea  bprefixa  btellsa  bthea  bcompilera  bthata  baa  bclassa  btemplatea  bisa  bdeclared,a  bwhicha  busesa  bma  basa  bthea  btypea  bnamea  bina  bthea  bdeclaration.a  bina  bthisa  bcase,a  bthea  bclassa  bvectora  bisa  baa  bparameterizeda  bclassa  bthata  busesa  btypea  bma  basa  bitsa  barguments.a  btypea  bma  bcana  bbea  breplaceda  bbya  banya  bdataa  btypea  bora  bbya  businga  baa  buser-defineda  bdataa  btype.

Ifa  baa  bclassa  bisa  bderiveda  bfroma  baa  bclassa  btemplate,a  bthena  bit’sa  bcalleda  baa  btemplatea  bclass.a  bthea  bobjectsa  bofa  bthea  btemplatea  bclassa  barea  bdefineda  basa  bfollows:a  bclassname<type>a  bobjectnamea  b(arglist);

Creatinga  baa  bderiveda  bclassa  bfroma  bclassa  btemplatea  bisa  bknowna  basa  binstantiationa  bprocess.a  bbeforea  bcreatinga  baa  btemplatea  bclass,a  byoua  bhavea  btoa  bdebuga  bthea  bclassa  btemplatea  bbeforea  bconvertinga  bita  btoa  baa  btemplatea  bclass.a  bthea  bcompilera  bchecksa  bfora  berrorsa  bina  baa  btemplatea  bclassa  baftera  binstantiationa  bhasa  btakena  bplace.

Example:a  bclassa  btemplate

Templatea  b<classa  btt>

Classa  brectangle

{

Tta  bwidth;

Tta  bheight;

Public:

Voida  bsetvalues(tta  bnum1,tta  bnum2)

Tta  barea()

{

Tta  ba;

A=width*height;

Returna  ba;

}

};

Voida  brectanglea  b<tt>a  b::setvaluesa  b(tta  bnum1,tta  bnum2)

{

Width=num1;

Height=num2;

}

Inta  bmain()

{

Rectanglea  bobj1;

Rectanglea  b<int>a  bobj1(5,6);

Rectanglea  bobj2;

Rectanglea  b<float>a  bobj2(5.6,4);

Cout<<a  bobj1.setvalues()

Cout<<obj2.setvalues()

Returna  b0;

}

//output

Obj1=30

Obj2=22.4

Thea  babovea  bprograma  bcreatesa  baa  bclassa  bofa  btypea  btt.a  bthea  b<tt>a  bina  bthea  b(voida  brectanglea  b<tt>a  b::setvaluesa  b(tta  bnum1,tta  bnum2))a  bstatementa  bspecifiesa  bthata  bthea  bfunctiona  bparametera  bisa  balsoa  baa  bclassa  btemplatea  bparametera  banda  bshoulda  balwaysa  bbea  bincludeda  bwhena  bcallinga  baa  bclass.

Classa  btemplatesa  bwitha  bmultiplea  bparameters

Youa  bcana  balsoa  bhavea  bmorea  bthana  bonea  bgenerica  bdataa  btypea  bina  baa  bclass.a  byoua  bcana  bdeclarea  bthea  bgenerica  btypea  bclassa  bwitha  baa  bcomma-separateda  blista  binsidea  bthea  btemplatea  bspecification.

Syntax

Templatea  b<classa  bxy,a  bclassa  bxyz,a  b…>

Classa  bclass-name

{

//functiona  bbody;

};

Example:a  bclassa  bwitha  btwoa  bgenerica  btypes

Template<classa  bf1,classa  bf2>

Classa  bnumbers

{

F1a  bj;a  bf2a  bk;

Public:

Numbersa  b(f1a  bx,a  bf2a  by)

{a  bj=x;a  bk=y;

}

Voida  bprint()

{

Cout<<j<<”and”<<k<<”\n”;

}

};

Inta  bmain()

{

Numbersa  b<float,a  bint>a  bnumbers1a  b(2.53,a  b253);

Numbersa  b<int,a  bchar>a  bnumbers2a  b(50,’z’);

Numbers1.print();

Numbers2.print();

Returna  b0;

};

//a  boutput

1.53a  banda  b253

50a  banda  bz

Functiona  btemplates

Functiona  btemplatesa  bworka  blikea  baa  bnormala  bfunctiona  bexcepta  bthata  bthea  bnormala  bfunctiona  bworksa  bwitha  bonlya  baa  bsinglea  bdataa  btype,a  bwhilea  btemplatesa  baccommodatea  bmultiplea  bdataa  btypes.a  bwitha  btemplates,a  byoua  bcana  boverloada  baa  bnormala  bfunctiona  btoa  bworka  bwitha  bdifferenta  bdataa  btypes.

Thisa  bmakesa  bfunctiona  btemplatesa  bmorea  busefula  bsincea  byoua  bonlya  bhavea  btoa  bwritea  baa  bsinglea  bprograma  bthata  bworksa  bona  balla  bdataa  btypes.

Templatesa  barea  balwaysa  bexpandeda  bduringa  bcompilea  btime.

Justa  blikea  baa  bclassa  btemplate,a  byoua  bcana  bcreatea  baa  bfunctiona  btemplatea  bwitha  bdifferenta  bargumenta  btypes.

Syntax

Templatea  b<classa  btype>

Return-typea  bfunction-namea  b(arguments)

{

Functiona  bbody;

};

Whena  bdefininga  bfunctiona  btemplates,a  byoua  bmusta  bincludea  bthea  btemplatea  btypea  bina  bbotha  bthea  bfunctiona  bbodya  banda  bparametera  blista  bwhena  bnecessary.

Example1:a  bfunctiona  btoa  bswapa  bvalues

Templatea  b<classa  bt1>

Voida  bswapa  b(t1&num1,a  bt1&num2)

{t1a  bval=a  bnum1;a  bnum1=num2;a  bnum2=val;};

Callinga  baa  btemplatea  bfunctiona  bworksa  bthea  bsamea  bwaya  basa  bthea  bnormala  bfunctiona  bcall.

Examplea  b2:a  bimplementationa  bofa  bfunctiona  btemplate

Templatea  b<classa  btest>

Testa  bmaxa  b(testa  bx,a  btesta  by);

{

Testa  bresults;

Results=x>y?A  bx:y;

Returna  bresults;

};

Inta  bmain()

{

Inta  ba=5,a  bb=6,a  bc;

Doublea  bl=4,a  bm=6,a  bn;

C=a  bmaxa  b<int>a  b(a,b);

N=maxa  b<double>a  b(l,m);

Cout<<a  bc<<endl;

Cout<<n<<endl;

Returna  b0;

}

Ina  bthisa  bexample,a  bthea  btesta  bisa  bthea  btemplatea  bparameter.a  bthea  bfunctiona  bmaxa  bisa  bcalleda  btwicea  bwitha  bdifferenta  bargumenta  btypesa  b(inta  banda  bdouble).a  bwhena  bthea  bcompilera  binstantiates,a  bita  bcallsa  bthea  bfunctiona  beacha  btimea  bbya  bitsa  btype.

Thea  boutputa  bobjecta  bproduceda  b(aftera  binstantiationa  bofa  bthea  btemplatea  bwitha  bspecifica  btype)a  bwilla  bbea  bofa  bthea  bsamea  btypea  bwitha  bthea  bparametersa  bxa  banda  by.

Thea  babovea  bprograma  bwilla  bsorta  bvaluesa  bbaseda  bona  bwhicha  bisa  bhigher.a  bifa  businga  bana  barraya  bofa  bnumbers,a  bthea  bsortinga  balgorithma  bwilla  bbea  bapplieda  btoa  bsorta  bthea  bnumbersa  bfroma  bthea  bsmallesta  btoa  bhighest.

Functiona  btemplatea  bwitha  bmultiplea  bparameters

![Image00090.jpg](images/Image00090.jpeg)justa  blikea  bina  bclassa  btemplates,a  byoua  bcana  bhavea  bmorea  bthana  bonea  bgenerica  bdataa  btypea  bseparateda  bbya  bcommas.

A  b

Example:a  btemplea  bclassa  bwitha  bmultiplea  bparameters

Template<classa  btemp1,classa  btemp2>

Voida  bdisplay(a  btemp1a  bj,a  btemp2a  bk)

{

Cout<<j<<”a  b“<<k<<”\n”;

}

Inta  bmain()

{

J=display1(2019,a  b“edge”);

K=display2(18.54,a  b“1854);

Returna  b0;

}

//a  boutput

2019a  bedge

18.54a  b1854

Overloadinga  btemplatea  bfunctions

Youa  bcana  boverloada  baa  btemplatea  bfunctiona  businga  bitsa  btemplatea  bfunctiona  bora  businga  bthea  bordinarya  bfunctiona  bfroma  bitsa  bname.a  boverloadinga  bcana  bbea  bdonea  bthrough:

Callinga  bana  bordinarya  bfunctiona  bthata  bmatchesa  bthea  btemplatea  bfunction.

Callinga  baa  btemplatea  bfunctiona  bthata  bisa  bbuilta  bwitha  bthea  bexacta  bfunction.

Usea  bnormala  boverloadinga  bfunctiona  bona  bana  bordinarya  bfunctiona  banda  bmakea  baa  bfunctiona  bcalla  btoa  bthea  bonea  bthata  bmatchesa  bthea  btemplatea  bfunction.

Ifa  btherea  bisa  bnoa  bmatcha  bfound,a  bana  berrora  bmessagea  bisa  bgenerateda  bbya  bthea  bsystem.

Example:a  boverloadeda  btemplatea  businga  bana  bexplicita  bfunction

Templatea  b<classa  bm>

Voida  bdisplay(ma  bn)

{

Cout<<”displaya  btemplatea  bfunction:”a  b<<a  bn<<a  b“\n”;

}

Voida  bdisplaya  b(a  binta  bn)

{

Cout<<”explicita  btemplatea  bdisplay:a  b“<<a  bn<<”\n”;

}

Inta  bmain()

{

Displaya  b(80);a  bdisplaya  b(15.20);

Returna  b0;

}

//output

Explicita  btemplatea  bdisplay:a  b80a  bdisplaya  btemplatea  bfunction:a  b15.20

Thea  bfunctiona  bcalla  bdisplaya  b(80)a  bcallsa  bthea  bordinarya  bversiona  bofa  baa  bdisplaya  b()a  bfunctiona  banda  bnota  bitsa  btemplatea  bversion.

Membera  bfunctiona  btemplates

Whena  bcreatinga  bclassa  btemplates,a  balla  bmembera  bfunctionsa  bcana  bbea  bdefineda  boutsidea  bthea  bclassa  bsincea  bthea  bmembera  bfunctionsa  bina  baa  btemplatea  bclassa  barea  bparameterizeda  businga  btypea  bargument.a  btherefore,a  bthea  bfunctiona  btemplatea  bshoulda  bdefinea  bthea  bmembera  bfunctions.

Membera  bfunctionsa  b(whethera  binlinea  bora  bnon-inline)a  bdeclareda  binsidea  baa  bclassa  btemplatea  barea  bimplicitlya  baa  bfunctiona  btemplate.a  bifa  baa  btemplatea  bclassa  bisa  bdeclared,a  bita  binheritsa  balla  bthea  btemplatea  bfunctionsa  bdefineda  bina  baa  bclassa  btemplate.

Membera  bfunctiona  btemplatesa  barea  bdefineda  bina  bthreea  bways:

Explicita  bdefinitiona  bina  baa  bfilea  bscopea  bfora  beacha  breturn-typea  buseda  btoa  binstantiatea  baa  btemplatea  bclass.

Duringa  bfilea  bscopea  bwithina  bthea  btemplatea  bparameters.

Inclineda  bwithina  bthea  bclass.

Aa  bmembera  bfunctiona  btemplatea  bcana  binstantiatea  bfunctionsa  bnota  bexplicitlya  bgenerated.a  bifa  baa  bclassa  bhasa  bbotha  baa  bmembera  bfunctiona  banda  bana  bexplicita  bfunction,a  bthena  bthea  bexplicita  bdefinitiona  bisa  bgivena  bmorea  bpriority.

Syntax

![Image00091.jpg](images/Image00091.jpeg)a  b

Example:a  bclassa  bvectora  bwitha  baa  bmembera  bfunctiona  btemplate

![Image00092.jpg](images/Image00092.jpeg)a  b

Non-typea  btemplatea  barguments

Templatesa  bcana  bhavea  bsinglea  bora  bmultiplea  btypea  barguments.a  byoua  bcana  balsoa  busea  baa  bnon-typea  bargumenta  btemplatea  bina  badditiona  btoa  bthea  btypea  bta  bargument.a  byoua  bcana  bcreatea  baa  btemplatea  bargumenta  businga  bstrings,a  bconstants,a  bbuilt-ina  btypes,a  banda  bfunctiona  bnames.

![Image00093.jpg](images/Image00093.jpeg)a  b

Thea  babovea  btemplatea  bpassesa  bthea  bsizea  bofa  bana  barraya  basa  bana  bargument.a  bthea  bcompilera  bwilla  bonlya  bknowa  bthea  bsizea  bofa  bthea  barraya  bduringa  bthea  bexecutiona  btime.a  bthea  bargumentsa  barea  bspecifieda  bduringa  bthea  bcreationa  bofa  btemplatea  bclass.

Templatea  bclasses

Whilea  btemplatea  bclassesa  btenda  btoa  bbea  blimiteda  btoa  blibrarya  bwritersa  bwhoa  bwanta  bclassesa  bsucha  basa  bmapa  banda  bvector,a  beverydaya  bprogrammersa  bcana  balsoa  bbenefita  bfroma  bbeinga  bablea  btoa  bmakea  btheira  bcodea  bmorea  bgeneric.a  byoua  bshouldn’ta  busea  baa  btemplatea  bjusta  bbecausea  byoua  bcan;a  binstead,a  byoua  bshoulda  bbea  blookinga  bfora  bopportunitiesa  btoa  bgeta  brida  bofa  bclassesa  bthata  bonlya  bdiffera  bbya  bthea  btype.

Yes,a  byoua  barea  blikelya  btoa  bfinda  byourselfa  bwritinga  bmorea  btemplatea  bmethodsa  bthana  bclasses,a  bbuta  byoua  bstilla  bneeda  btoa  bhavea  bsomea  bideaa  bofa  bhowa  btoa  busea  bthem,a  bespeciallya  bifa  byoua  bhavea  baa  bdataa  bstructurea  bofa  byoura  bowna  bthata  byoua  bwanta  btoa  bimplement.

Declaringa  baa  btemplatea  bclassa  bisn’ta  bverya  bdifferenta  bfroma  baa  btemplatea  bfunction.a  blet’sa  bsaya  bthata  bwea  bwanta  btoa  bbuilda  baa  bsmalla  bclassa  bthata  bwilla  bwrapa  bana  barray:

Templatea  b<typenamea  bt>a  bclassa  barraywrapper

{

Private:

Ta  b*pmem;

};

Asa  bwitha  bthea  btemplatea  bfunction,a  bwea  bbegina  bwitha  bthea  bdeclarationa  bthata  baa  btemplatea  bisa  bbeinga  bintroduced.a  bwea  busea  bthea  btemplatea  bkeyword,a  banda  bthena  bthea  btemplatea  bparametersa  barea  badded.a  bwea  bonlya  bhavea  bonea  bparametera  bhere,a  bt.

Typea  bta  bcana  bbea  buseda  bwhenevera  bwea  bwanta  bthea  btypea  bthata  bwoulda  bbea  bspecifieda  bbya  baa  buser,a  bjusta  blikea  bwitha  bthea  btemplatea  bfunctions.a  bwhena  baa  bfunctiona  bisa  bdefineda  bfora  baa  btemplatea  bclass,a  bthea  btemplatea  bsyntaxa  balsoa  bhasa  btoa  bbea  bused.a  bsoa  blet’sa  badda  baa  bconstructora  bcalleda  barraywrappera  btoa  boura  bclass:a  btemplatea  b<typenamea  bt>a  bclassa  barraywrapper

{

Public:

Arraywrappera  b(inta  bsize);

Private:

Ta  b*pmem;

};

//a  bsoa  bthata  bthea  bconstructora  bcana  bbea  bdefineda  boutsidea  bthea  bclass,a  bwea  bstarta  bby

//a  bindicatinga  bthata  bthea  bfunctiona  bisa  baa  btemplate

Templatea  b<typenamea  bt>

Arraywrapper<t>::arraywrappera  b(inta  bsize)

:a  bpmem(a  bnewa  bt[a  bsizea  b]a  b)

{a  b}

Wea  bstarta  bwitha  bthea  bbasica  btemplatea  bintroductiona  banda  bredeclarea  bthea  bparametera  bfora  bthea  btemplate.a  bthea  bdifferencea  bis,a  bthea  bclassa  bnamea  bnowa  bhasa  bthea  barraywrappera  btemplatea  bina  bit,a  bwhicha  btellsa  beveryonea  bthata  bthisa  bbelongsa  btoa  baa  btemplatea  bclassa  banda  bisn’ta  baa  btemplatea  bfunctiona  bona  baa  bstandarda  bclassa  bcalleda  barraywrapper.

Ina  bthisa  bimplementation,a  bthea  btemplatea  bparametera  bcana  bbea  buseda  btoa  bstanda  bina  bfora  bthea  bprovideda  btype,a  bjusta  basa  bwitha  bthea  btemplatea  bfunctions.a  bhowever,a  bthea  bfunctiona  bcallera  bwilla  bnevera  bneeda  btoa  bprovidea  bthea  bparameter—ita  bgetsa  btakena  bfroma  bthea  bfirsta  btemplatea  btypea  bdeclaration.a  bfora  bexample,a  binsteada  bofa  bwritinga  bvec.size<int>()

Or

Vec<int>.size();

Toa  bgeta  bthea  bsizea  bofa  baa  bvectora  bofa  bintegers,a  balla  byoua  bneeda  btoa  bwritea  bis

Vec.size().

Templatesa  banda  bheadera  bfiles

Upa  btoa  bnow,a  bthea  btemplatesa  bwea  bhavea  blookeda  bata  bhavea  bbeena  bdirectlya  bwrittena  bintoa  b.cppa  bfiles.a  bwhata  bifa  bwea  bwanteda  btoa  bplacea  boura  btemplatea  bdeclarationa  bintoa  bthea  bheadera  bfile?A  bcoulda  bwe?A  bthea  bproblema  bherea  bisa  bthata  bcodea  bthata  bmakesa  busea  bofa  btemplatea  bclassesa  bora  btemplatea  bfunctionsa  bneedsa  btoa  bbea  bablea  btoa  baccessa  bthea  bwholea  btemplatea  bdefinitiona  bfora  beverya  bsinglea  bfunctiona  bcalla  btoa  bthea  btemplatea  basa  bwella  basa  btoa  beverya  bmembera  bfunctiona  bthata  bisa  bcalleda  bona  btemplatea  bclasses.

Thisa  bisa  bnota  bthea  bsamea  bwaya  bthata  baa  bstandarda  bfunctiona  bworks;a  bthesea  bonlya  brequirea  bthea  bcallera  btoa  bknowa  babouta  bthea  bdeclaration.a  bif,a  bfora  bexample,a  byoua  bplaceda  bthea  bcalca  bclassa  binsidea  bitsa  bheadera  bfile,a  byoua  bwoulda  balsoa  bneeda  btoa  badda  bthea  bfulla  bconstructora  bdefinitiona  balonga  bwitha  bthea  badd()a  bmethoda  binsteada  bofa  bputtinga  bthema  balla  bintoa  bonea  b.cppa  bfilea  basa  byoua  bwoulda  bnormally.a  bifa  byoua  bdidn’ta  bdoa  bthis,a  byoua  bwoulda  bnota  bbea  bablea  btoa  busea  bcalc.

Thisa  bisa  baa  brathera  bunfortunatea  bthinga  babouta  btemplates,a  banda  bit’sa  balla  babouta  bhowa  btemplatesa  bhavea  bbeena  bcompiled.a  bmosta  bofa  bthea  btime,a  bwhena  bthea  bcompilera  bparsesa  bthema  bthea  bfirsta  btime,a  bita  bprettya  bmucha  bignoresa  btemplates.a  bit’sa  bonlya  bwhena  baa  btemplatea  bisa  buseda  bthata  bhasa  baa  bconcretea  btypea  battacheda  bthata  bthea  bcompilera  bgeneratesa  bthea  bcodea  bfora  bthata  btype.a  btoa  bdoa  bthat,a  bthea  btemplatea  bhasa  btoa  bbea  bavailablea  btoa  bthea  bcompilera  bsoa  bthea  bcodea  bcana  bbea  bgenerated.a  baa  bresulta  bofa  bthisa  bisa  bthata  balla  btemplatea  bcodea  bhasa  btoa  bbea  bincludeda  bina  balla  bofa  bthea  bfilesa  bthata  bwilla  busea  bthata  btemplate.a  band,a  bwhena  baa  bfilea  bthata  bhasa  baa  btemplatea  bisa  bcompiled,a  byoua  bmaya  bnota  blearna  bofa  banya  bsyntaxa  berrorsa  bina  bthata  btemplatea  buntila  bthea  btemplatea  bisa  buseda  bfora  bthea  bfirsta  btime.

Thea  beasiesta  bthinga  btoa  bdo,a  bwhena  bcreatinga  btemplatea  bclasses,a  bisa  btoa  bplacea  balla  btemplatea  bdefinitionsa  bintoa  bthea  bheadera  bfile.a  bit’sa  balsoa  bhelpfula  bifa  byoua  busea  bana  bextensiona  bothera  bthana  b.h,a  bjusta  btoa  bindicatea  bthata  bthea  bfilea  bisa  baa  btemplate—.hxx,a  bfora  bexample.

Analyzinga  btemplatea  berrora  bmessages

Ifa  btherea  bisa  bonea  bsignificanta  bdownsidea  btoa  businga  btemplates,a  bit’sa  bthata  bmanya  bcompilersa  bwilla  bthrowa  bouta  berrora  bmessagesa  bthata  barea  bnota  beasya  btoa  bunderstanda  bwhena  baa  btemplatea  bisa  bmisused,a  bwhethera  byoua  bwritea  bita  bora  bnot.a  byoua  bcoulda  benda  bupa  bwitha  bpagesa  bofa  berrora  bmessagesa  bjusta  bfora  bonea  bmistake.

Templatea  berrora  bmessagesa  barea  bnota  beasya  btoa  breada  bsimplya  bbecausea  bthea  btemplatea  bparametersa  barea  bexpandeda  btoa  btheira  bfullest,a  bevena  bthosea  bthata  byoua  bdon’ta  bnormallya  buse,a  bsucha  basa  bthea  bdefaulta  bparameters.

Therea  bisa  baa  bsimilara  bconstrainta  bona  bthea  bseconda  bparametera  bfora  bthea  bvectora  btemplate—a  bthisa  bonea  brequiresa  baa  btypea  bthata  bhasa  bsupporta  bfora  bmorea  bfunctionalitya  bthana  bthea  bhumblea  bbasica  bintegera  bgivesa  bus.a  bthea  berrorsa  barea  balla  bcomplaininga  babouta  bthea  bmultitudea  bofa  bwaysa  bthata  binta  bjusta  bisn’ta  baa  bvalida  btypea  bfora  bthea  bparameter.

Findinga  bthea  bcodea  blinea  bwherea  bthea  berrora  bisa  bwilla  balwaysa  bbea  bthea  bfirsta  bstepa  btoa  bworkinga  bouta  bwherea  bita  balla  bwenta  bwrong.a  bmorea  boftena  bthana  bnot,a  banda  bevena  bmorea  bsoa  basa  byoua  bgaina  bexperiencea  banda  bconfidence,a  baa  bsimplea  blooka  bata  byoura  bcodea  bwilla  btella  byoua  bwhata  bthea  berrora  bis.a  bifa  bita  bisn’ta  bthata  bobvious,a  byoua  bjusta  bkeepa  bgoinga  bthrougha  bthea  binstantiationa  blista  buntila  bthea  bpropera  berrora  bmessagea  bappears:a  b“error:a  binta  bisa  bnota  baa  bclass,a  bstructa  bora  buniona  btype.”A  bthea  bcompilera  bexpecteda  baa  bstructurea  bora  baa  bclass,a  bnota  banya  bofa  bthea  bbuilt-ina  btypesa  bsucha  basa  bint.a  baa  bvectora  bshoulda  bholda  banya  btype,a  bsoa  bthea  berrora  bliesa  bina  bthea  bparametera  bgivena  btoa  bthea  bvector.

Youa  bshoulda  bmakea  bsurea  byoua  bknowa  bhowa  baa  bvectora  bisa  bdeclareda  banda  bthata  bita  bonlya  bneedsa  bonea  btemplatea  bparameter.

Nowa  bthata  bthea  bproblema  bhasa  bbeena  bfound,a  bwea  bcana  bfixa  bita  banda  bthena  brecompilea  bthea  bcode.a  bsometimesa  byoua  bwilla  bbea  bablea  btoa  bworka  bouta  banda  bfixa  baa  bfewa  berrorsa  bata  bthea  bsamea  btime,a  bbuta  bwherea  btemplatesa  barea  bconcerned,a  bthea  bfirsta  berrora  bisa  busuallya  bthea  broota  bofa  bthea  bproblema  bfora  balla  bothers.a  bfixa  bthingsa  bonea  bata  baa  btime,a  banda  byoua  bwilla  bfinda  bthata  banya  bothera  berrorsa  bfixa  bthemselves.

Ina  boura  bfinala  bexamplea  babove,a  balla  bthosea  berrora  bmessagesa  bresulteda  bfroma  bonea  bsimplea  bmistake:a  bgivinga  baa  bseconda  btemplatea  bparametera  bofa  bana  bint.

## Chaptera  b7:a  bclasses

Introductiona  btoa  bclasses

Ata  bthea  bhearta  bofa  balla  bobject-orienteda  bprogramminga  bliesa  bthea  bnotiona  bofa  bclasses,a  bobjectsa  bthata  byoua  bcreate,a  banda  butilizea  bthroughouta  byoura  bcode.a  bthisa  bhelpsa  bwitha  bmodularity,a  bwitha  beasea  bofa  buse,a  bwitha  befficiency,a  banda  bwitha  bhigher-levela  bprogramminga  bthata  bisa  bfara  bmorea  blogicala  banda  bcoherent.

Ina  bthea  bearlya  biterationsa  bofa  bc,a  btherea  bwasa  baa  bprimitivea  bsorta  bofa  bclassa  bcalleda  baa  bstruct.a  bstructsa  bstilla  bexista  bina  bc++a  bbuta  barea  bmainlya  bdeprecateda  banda  bshirkeda  bina  bfavora  bofa  businga  bclassesa  binstead.a  bnevertheless,a  bstructsa  barea  bimportanta  btoa  bcover.a  bc++a  bstructsa  barea  balsoa  bdifferenta  bfroma  bca  bstructs.a  bca  bstructsa  bdidn’ta  bhavea  bmucha  bofa  bthea  bfunctionalitya  bwhicha  bc++a  bstructsa  bdo.

Beforea  bwea  bjumpa  bintoa  bthat,a  blet’sa  btalka  bbrieflya  babouta  bthea  bnotiona  bofa  baccessa  bmodifiers.

We’vea  btalkeda  babouta  bthingsa  blikea  bint,a  bstring,a  bbool,a  banda  bfloata  bcalleda  btypes.a  bwea  bcreateda  bwhata  bcoulda  bbea  bconsidereda  bsomewhata  bofa  baa  btypea  businga  benumerators.a  bhowever,a  byoua  bcana  bcreatea  bana  bentirea  btypea  bthata  bisa  bmadea  bupa  bofa  bsmallera  bpiecesa  bofa  bdataa  banda  binnatea  bfunctions.a  bthisa  bisa  bcalleda  bana  bobject.

Accessa  bmodifiersa  bdescribea  bwhata  bcana  bchangea  bwhata  bwithina  byoura  bcode.a  btherea  barea  bthreea  bdifferenta  baccessa  bmodifiers.

Publica  baccessa  bmeansa  bthata  bthea  bobjecta  band/ora  bitsa  binternala  bdataa  banda  bfunctionsa  bcana  bbea  baccesseda  banda  bmodifieda  bbya  banya  bothera  bcodea  bina  bthea  bprogram.

Protecteda  bmeansa  bthata  bthea  bobjecta  band/ora  bitsa  binternala  bdataa  banda  bfunctionsa  bcana  bbea  baccessa  banda  bmodifieda  bbya  bonlya  bitsa  bderivatives.a  b(thisa  bwilla  bmakea  bsensea  bwhena  bwea  bgeta  bintoa  binheritancea  banda  bpolymorphism.)

Privatea  bmeansa  bthata  bonlya  bthea  bobjecta  bitselfa  bcana  baccessa  banda  bmodifya  bitsa  bdata.

Thisa  bisa  bimportanta  bfora  bpurposesa  bofa  bsecurity,a  bclarity,a  banda  bcodea  bsafety.

Structsa  banda  bclassesa  barea  bbotha  bwaysa  btoa  bcreatea  bnewa  bobjects.a  bthea  bprimarya  bdifferencea  bbetweena  bstructsa  bisa  bthata  bstructsa  barea  bpublica  bbya  bdefault,a  banda  bclassesa  barea  bprivatea  bbya  bdefault.a  bothera  bthana  bthat,a  bthea  bdifferencesa  barea  bverya  bnegligible.

However,a  bina  bthea  btecha  bindustry,a  bstructsa  bhavea  baa  bfaira  bbita  bofa  baa  bnegativea  bconnotation.a  bdevelopersa  btenda  btoa  bseea  bthema  basa  bunprotecteda  bobjectsa  bwitha  blimiteda  bfunctionality,a  bwhilea  btheya  btenda  btoa  bseea  bclassesa  basa  bverya  bfunctionala  bobjectsa  bwitha  bchilda  bclassesa  bthata  barea  bwella  bmadea  banda  bwella  bstructured.

Asa  bsuch,a  bit’sa  bgenerallya  bbettera  btoa  bcreatea  bclassesa  bunlessa  byoura  bobjecta  bhasa  bverya  blittlea  bina  bthea  bwaya  bofa  bfunctionalitya  banda  bsimplya  bcontainsa  bverya  blittlea  bdataa  banda  binnatea  bfunction.

Looka  bata  bthisa  bstructa  banda  bdeclaration.

Structa  banimala  b{

Enuma  bdieta  b{a  bherbivore,a  bomnivore,a  bcarnivorea  b};

Inta  blegs;

Stringa  bname;

Dieta  bnaturaldiet;

};

Inta  bmain()a  b{

Animala  bdog;

Dog.legsa  b=a  b4;

Dog.namea  b=a  b“dog”;

Dog.naturaldieta  b=a  bdog.carnivore;

}

Thisa  bisa  bthea  bsimplesta  bwaya  btoa  bdeclarea  baa  bnewa  bobject.a  byoua  bshoulda  bnota  bdeclarea  bthema  bwithina  bana  bexistenta  bfunction.

Let’sa  bgoa  baheada  banda  breplacea  bthata  bstructa  bwitha  baa  bclassa  bbecausea  bwe’rea  bgoinga  btoa  bbea  businga  bclassesa  bgoinga  bforwarda  basa  bthey’rea  bgenerallya  baa  bsafera  banda  bbettera  boptiona  bthana  bstructsa  bare.

Createa  baa  bnewa  bprojecta  bina  bcodeblocksa  bcalleda  b“animalsimulator”.a  bnota  bthea  bmosta  bcreativea  btitle,a  bbuta  bit’lla  bworka  bfora  bwhata  bwe’vea  bgota  btoa  bdo.a  bredacta  bthea  bcontentsa  bofa  bmain.cppa  banda  bimporta  biostreama  banda  bcreatea  byoura  bmaina  bmethod.

Abovea  bthea  bmaina  bmethod,a  blet’sa  bdeclarea  baa  bclassa  bcalleda  banimal.a  byoua  bwoulda  bdoa  bthata  bverya  bsimilara  btoa  bhowa  byou’da  bdeclarea  baa  bstruct.a  bfora  bthea  bsakea  bofa  billustration,a  bmakea  bita  blooka  blikea  bthis:

Classa  banimala  b{

Stringa  bname;

};

Thena  bwithina  byoura  bmaina  bmethod,a  bdeclarea  bana  binstancea  banda  bseta  bitsa  binstancea  bofa  bnamea  btoa  bthea  bnamea  bofa  byoura  bfavoritea  banimal.a  bafterward,a  btrya  btoa  bbuild.

Youa  bshoulda  bhavea  bgottena  bana  berrora  bthata  bsaida  b“error:a  bstringa  banimal::namea  bisa  bprivate”.

Perfect.a  bthisa  bisa  bsupposeda  btoa  bhappena  bbecausea  bnowa  bwea  bhavea  btoa  bfixa  bthis.a  bthisa  bisa  bwherea  bthata  bwholea  bnotiona  bofa  baccessa  bdescriptiona  bcomesa  bin.

Modifya  byoura  bclassa  bsoa  bthata  bita  blooksa  blikea  bthis:

Classa  banimala  b{

Public:

Stringa  bname;

}

Thena  btrya  btoa  bbuild.a  bita  bshoulda  bworka  bfinea  bthisa  btime.a  bthat’sa  bbecausea  bwea  bmadea  bthea  bstringa  b“name”a  bpublic,a  bwhicha  bmeansa  bothera  bmethods/functionsa  boutsidea  bofa  bthea  bclassa  bitselfa  bcana  baccessa  bit.

Thisa  bisa  bgenerallya  bconsidereda  bbada  bpracticea  bthough,a  bsoa  bwe’rea  bgoinga  btoa  brewritea  bthea  bclassa  blikea  bso:

Classa  banimala  b{

Private:

Stringa  bname;

}

Thea  bbest-practicea  bwaya  btoa  bmodifya  bvaluesa  bwithina  baa  bclassa  bisa  btoa  busea  bget/seta  bmethods.a  bhere’sa  bthea  bwaya  bthea  bclassa  bwoulda  blooka  bifa  byoua  bimplementeda  bget/seta  bmethods.

Classa  banimala  b{

Private:

Stringa  bname;

Public:

Stringa  bgetname()a  b{

Returna  bthis->name;

}

Voida  bsetname(stringa  bname)a  b{

This->namea  b=a  bname;

}

}

Now,a  bina  byoura  bmaina  bmethod,a  baftera  bdeclaringa  bwhatevera  banimala  bita  bis,a  binsteada  bofa  bdirectlya  bmodifyinga  bitsa  bname,a  byoua  bshoulda  binsteada  busea  bthea  bget/seta  bmethoda  blikea  bsoa  b(assuminga  byoura  binstancea  banimala  bisa  bcalleda  b“dog”):

Dog.setname(“dog”);

Thena  byoua  bcana  btesta  bthisa  bbya  bprintinga  bouta  bthea  bnamea  bina  byoura  bmaina  bmethod:

Couta  b<<a  b“thea  bnamea  bofa  bmya  bfavoritea  banimala  bis:a  b“a  b<<a  bdog.getname()a  b<<a  b“\n”;

Thea  bwaya  bthesea  bworksa  bisa  bbya  breturninga  bora  bsettinga  bthea  bvaluea  bofa  bthea  bvariablea  bviaa  baa  bmethoda  bfroma  bwithina  bthea  bclass.a  b“this->”a  bisa  bcalleda  bthea  bthisa  bpointer,a  banda  bita  brefersa  btoa  bthea  bvariablea  bofa  baa  bgivena  binstancea  bofa  baa  bclass.a  beverya  bobjecta  bhasa  baccessa  btoa  bitsa  bvariablesa  banda  bcana  bmodifya  bthema  bdirectlya  bviaa  bthea  b‘thisa  bpointer’.

Anyway,a  byoura  bcodea  bshoulda  bworka  bstunningly.a  bbuta  bwhata  bifa  byoua  bdon’ta  bwanta  btoa  bgoa  bthrougha  bget/seta  bfora  beverya  binstancea  bofa  beverya  bclass?A  bwell,a  byoua  busea  bwhat’sa  bcalleda  bana  binitializera  bfunction.

Modifya  byoura  bclassa  bsoa  bita  blooksa  blikea  bthis:

Classa  banimala  b{

Private:

Stringa  bname;

Public:

Animal(stringa  bname)a  b{

This->namea  b=a  bname;

}

Stringa  bgetname()a  b{

Returna  bthis->name;

}

Voida  bsetname(stringa  bname)a  b{

This->namea  b=a  bname;

}

}

Now,a  bina  byoura  bmaina  bfunction,a  btakea  bouta  bthea  bchunka  bofa  bcodea  bthata  bsaysa  banimala  bxa  bfolloweda  bbya  bthea  bx.setname(“name”)a  bfunction.a  bwhena  byoua  bcreatea  bana  binitializera  bfunction,a  byoua  bcana  bseta  bcertaina  bvariablesa  bfroma  bthea  bget-go.

Fora  bexample,a  bsincea  byoura  binitializera  bfunctiona  btakesa  bthea  bargumenta  bofa  bname,a  byoua  bcana  bdeclarea  bthata  bwhena  byoua  bdeclarea  bthea  bvariablea  banda  bcircumventa  bthea  bwholea  bsetnamea  boperation.a  blooka  bata  bthisa  bcodea  bfora  bana  bexample:

Animala  bdog(“dog”);

Animala  belephant(“elephant”);

Animala  bbird(“bird”);

Thesea  barea  balla  bseparatea  binstancesa  bofa  bthea  bclassa  banimal,a  banda  btheira  bnamesa  bhavea  bbeena  bseta  bwithouta  bthea  busea  bofa  baa  bseta  bfunctiona  bthanksa  btoa  bthea  bfunctiona  binitializer.

Thisa  bcana  btakea  basa  bmanya  bargumentsa  basa  byou’da  blikea  bita  bto.a  bthisa  bmakesa  bita  bincrediblya  beasya  btoa  bcreatea  bnewa  bobjectsa  banda  bprettya  bstreamlineda  bofa  baa  bprocessa  btoo.

Nowa  bthata  bwe’vea  bspokena  bfora  baa  bmomenta  babouta  bdeclaringa  bobjectsa  banda  bthingsa  bofa  bthata  bnaturea  blet’sa  btalka  bmorea  babouta  bthea  bspecificsa  bofa  bwhata  byoua  bcana  bdoa  bwitha  bthem.a  bthea  bobjecta  banimala  bhere,a  brepresents,a  bofa  bcourse,a  banimals.a  bwea  bcana  bgivea  bthea  bentirea  bclassa  baa  bseta  bofa  bmethodsa  bthata  btheya  bcana  bperform.

Let’sa  bthinka  bfora  baa  bseconda  babouta  bwhata  beverya  banimala  bdoes.a  beverya  banimala  bsleeps,a  beats,a  banda  bdrinks,a  bright?A  bsoa  bita  bwouldn’ta  bbea  bverya  boutlandisha  btoa  bincludea  bthesea  bwithina  boura  bclassa  bsoa  bthata  beverya  bmembera  bobjecta  bofa  bthea  bclassa  banimala  bcana  bperforma  bthesea  bmethods.

Let’sa  bsaya  bwea  bhada  btwoa  bspecifica  bkindsa  bofa  bfood:a  bmeata  banda  bplants,a  bbotha  bofa  bwhicha  balsoa  brepresenteda  bbya  btheira  brespectivea  bobjects.

Wea  bcoulda  bcreatea  btwoa  bdifferenta  bfunctionsa  bfora  bthis:

Voida  beat(planta  bp)a  b{

//a  bcodea  bhere

}

Voida  beat(meata  bm)a  b{

//a  bcodea  bhere

}

Evena  bthougha  bthesea  bsharea  baa  bname,a  byoua  bcana  bcalla  beithera  bdependinga  bupona  bthea  btypea  bofa  bobjecta  bwhicha  byoua  bputa  bincludea  bina  bthea  bfunctiona  bcall,a  banda  bbotha  bwilla  bperforma  btheira  brespectivea  bcodea  bina  bresponsea  btoa  bthea  bargumenta  bwhicha  byoua  bincluded.a  bthisa  bisa  bcalleda  bfunctiona  boverloading.a  bit’sa  bana  bessentiala  btechniquea  bina  bobject-orienteda  bprogramminga  bthata  bwilla  bhelpa  byoua  btoa  bcreatea  bfunctionala  banda  bcleara  bsetsa  bofa  bcodea  bthata  barea  beasya  bfora  bpeoplea  btoa  busea  banda  bunderstand.a  bina  bthea  bnexta  bchapter,a  bwe’rea  bgoinga  btoa  bstarta  bexploringa  bsomea  bofa  bthea  bdeepera  bthingsa  bthata  byoua  bcana  bdoa  bwitha  bclasses,a  bincludinga  bthea  binherenta  bqualitiesa  bwhicha  bmakea  bthema  bbotha  bincrediblya  busefula  banda  bincrediblya  bpracticala  bina  bobject-orienteda  bprogramming.

Becausea  bit’sa  bunwieldya  btoa  bcreatea  baa  blargea  bnumbera  bofa  btypesa  bwhilea  bwe’rea  blearninga  babouta  bclassesa  bina  bthea  bfirsta  bplace,a  blet’sa  bjusta  bleavea  b“eat”a  basa  baa  bvoida  bfunctiona  bthata  bdoesn’ta  btakea  barguments.a  byoura  bcodea  bshoulda  blooka  blikea  bthis:

Classa  banimala  b{

Private:

Stringa  bname;

Public:

Animal(stringa  bname)a  b{

This->namea  b=a  bname;

}

Stringa  bgetname()a  b{

Returna  bthis->name;

}

Voida  bsetname(stringa  bname)a  b{

This->namea  b=a  bname;

}

Voida  beat()a  b{

//a  beata  bfood

}

}

Ina  bthea  bnexta  bchapter,a  bwe’rea  bgoinga  btoa  bcovera  bfara  bmorea  bin-deptha  bconceptsa  bregardinga  bclasses.

Objectsa  banda  bclasses

Classesa  barea  bthea  bspeciala  bfeaturea  bofa  bc++,a  bwhicha  bcastsa  bc++a  bintoa  bobject-orienteda  bprogramming.a  bremember,a  bc++a  bisa  bnota  baa  bpurea  bobject-orienteda  blanguagea  bbecause,a  bina  baa  bpurea  bobject-oriented,a  bwea  bcana  bperforma  bnoa  bfunctionalitya  bwithouta  bclasses,a  bbuta  bina  bc++,a  bita  bisa  bpossible.

Class

Ita  bisa  baa  buser-defineda  bdataa  btypea  bhavinga  bdataa  bmembersa  banda  bmembera  bfunctionsa  bthata  bcana  bonlya  bbea  baccesseda  baftera  bana  binstancea  bisa  bcreateda  bfora  bthata  bclass.a  bina  bgenerala  bterms,a  baa  bclassa  bisa  baa  bblueprinta  bthata  brepresentsa  bthea  bstatesa  banda  bbehaviorsa  bfora  bclass’sa  binstancesa  bknowna  basa  bobjects.

Dataa  bmembersa  barea  bdefineda  bina  bclassa  bdefinitiona  basa  bvariablesa  banda  bmembera  bfunctionsa  basa  bfunctions.

Fora  bexample,a  baa  bclassa  bofa  bhumans,a  balla  bhumansa  bcana  bwalk,a  brun,a  beat,a  banda  btheya  balla  bhavea  btheira  bspecifica  bcolor,a  bweight,a  bage.a  bhere,a  bwalk,a  beat,a  banda  bruna  barea  bbehaviorsa  bfora  bhumansa  banda  bcolor,a  bage,a  bweighta  bisa  btheira  bcharacteristics.a  btherea  barea  bseverala  bdifferenta  bhumana  bbeingsa  bina  bthisa  bclass,a  balla  bhavinga  bdifferenta  bnames,a  bbuta  balla  bofa  bthema  bhavea  bthesea  bcharacteristicsa  banda  bbehavior.

So,a  bthea  bclassa  bisa  baa  bblueprinta  bthata  bdeclaresa  bcharacteristicsa  basa  bdataa  bmembersa  banda  bbehaviorsa  basa  bmembera  bfunctions,a  banda  balla  bthea  binstancesa  bknowna  basa  bobjectsa  bsharea  balla  bthesea  bcharacteristicsa  banda  bbehavior.

Importanta  bpointsa  babouta  bclasses

Aa  bclassa  bnamea  bisa  bconventionallya  bstarteda  bwitha  bana  buppercasea  bletter.

Classa  bhuman

A-classa  bhasa  bdataa  bmembersa  basa  bvariablesa  banda  bmembera  bfunctionsa  basa  bsimplea  bfunctions,a  banda  bthea  baccessa  bscopea  bofa  bthesea  bvariablesa  banda  bdataa  bmembersa  bisa  bdependenta  bona  bthea  baccessa  bspecifiersa  basa  bprivate,a  bpublic,a  bora  bprotected,a  bwhicha  bwea  bwilla  bdiscussa  blater.

Wea  bcana  bdefinea  bthea  bmembera  bfunctiona  bofa  baa  bclassa  binsidea  bthea  bdefinitiona  bofa  bthata  bclassa  bora  boutsidea  bthea  bdefinitiona  bofa  bclass.

Classa  bina  bc++a  bisa  bsimilara  btoa  bstructuresa  bina  bca  bwitha  bthea  bonlya  bdifferencea  bthata  bbya  bdefault,a  baccessa  bcontrola  bfora  bclassesa  bisa  bprivatea  bwhilea  bthea  bstructurea  bhasa  bpublic.

C++a  bprovidesa  balla  bimportanta  bfeaturesa  bofa  bobject-orienteda  bprogramminga  basa  bencapsulation,a  babstraction,a  banda  binheritance,a  betc.a  bwitha  bclasses.

Eacha  bobjecta  bofa  baa  bclassa  bhasa  bitsa  bseparatea  bcopya  bofa  bdataa  bmembers,a  banda  bwea  bcana  bcreatea  basa  bmanya  bnumbersa  bofa  bobjectsa  bfora  baa  bclassa  basa  bneeded.

Objects

Classa  bisa  bjusta  baa  bblueprint.a  bjusta  bwitha  bdefininga  baa  bclass,a  bnoa  bmemorya  bisa  ballocateda  btoa  bit.a  bmemorya  bisa  ballocateda  bonlya  baftera  bobjectsa  barea  bcreateda  bfora  bthata  bclass.a  bthesea  bobjectsa  barea  binstancesa  bhavinga  bthea  bdataa  bvariablesa  bdeclareda  bina  bthata  bclassa  banda  bthea  bmembera  bfunctionsa  bofa  bthata  bclassworka  bona  bthesea  binstances.

Objectsa  barea  binitializeda  bwitha  bspeciala  bconstructorsa  b–a  bspeciala  bmethodsa  bwhicha  bwea  bwilla  bstudya  blater.a  bdestructorsa  barea  bothera  bspeciala  bfunctionsa  bthata  bdestroya  bthea  bobjecta  bwhena  bita  bgoesa  bouta  bofa  bscope.

Classa  bmobiles{

Inta  bprice;

Voida  bcallinga  b(){}

Voida  bmessaginga  b(){}

};

Voida  bmain(){

Mobilesa  bm1;a  b//a  bana  bobjecta  bcreateda  bfora  bclassa  bmobilesa  b}

Constructors

Constructorsa  barea  bspeciala  bfunctionsa  bsimilara  btoa  bclassa  bmembera  bfunctionsa  banda  bhavinga  bana  bimportanta  btaska  bofa  bobjecta  binitialization.a  basa  bana  bobjecta  bisa  bcreated,a  bcompilera  bmakesa  baa  bcalla  btoa  bthea  bconstructor.a  bthea  bconstructora  binitializesa  bthea  bcreateda  bobjecta  bbya  binitializinga  bitsa  bmembersa  baftera  bthea  bstoragea  bisa  bprovideda  btoa  bthata  bparticulara  bobject.a  btherea  bisa  bata  bleasta  bonea  bconstructora  bfora  baa  bclass.a  bifa  btherea  bisa  bnoa  bexplicitlya  bdefineda  bconstructora  bina  baa  bclass,a  baa  bbya  bdefaulta  bconstructora  bwitha  bnoa  bparametera  bcomesa  bintoa  bexistence.

Classa  btest

{

Chara  bc;

Public:

Test();a  b//a  baa  bconstructor

};

Classa  btest

{

Inta  ba;

Public:

Test();a  b//declarationa  bfora  bconstructor

Test::test()a  b//a  bdefininga  bconstructor

{

A=1;

}

};

Destructors

Destructorsa  barea  bthea  bspeciala  bclassa  bfunctionsa  bhavinga  baa  bspeciala  bresponsibilitya  bofa  bdestroyinga  bthea  bobjecta  basa  bthata  bobjecta  bgoesa  bouta  bofa  bitsa  bscope.a  bcompilera  bautomaticallya  bcallsa  bthea  bconstructora  basa  bana  bobjecta  bgoesa  bouta  bofa  bthea  bscope.

Destructora  bhasa  bthea  bsamea  bsyntaxa  basa  bthata  bofa  bconstructora  bwitha  baa  bsinglea  bdifferencea  bthata  btildea  bsigna  bsymbola  basa  b~a  bisa  buseda  bora  bdestructora  bdeclaration.a  balsoa  baa  bdestructora  bhasa  bnoa  bargument.

Classa  btest

{

Public:

~test();a  b//a  bdestructora  bfora  bclassa  btest

};

Examplea  bfora  bdemonstrationa  bofa  bcallinga  bofa  bconstructorsa  banda  bdestructors

Classa  btest{

Test()

{

Couta  b<<a  b“aa  bconstructora  bhasa  bbeena  bcalled”;a  b}

~test()

{

Couta  b<<a  b“aa  bdestructora  bhasa  bbeena  bcalled”;a  b}

};

Inta  bmain()

{

Testa  btest1;a  b//a  bconstructora  bisa  bcalled

Inta  ba=18;

If(a)

{

Testa  btest2;a  b//a  bagaina  bconstructora  bisa  bcalleda  b}//a  bobj2a  bisa  bouta  bofa  bscopea  banda  bdestructora  bisa  bcalleda  bfora  bthata  bobj2

}a  b//a  bdestructora  bisa  bcalleda  bfora  bthea  bobjecta  bobj1

Thea  blifea  bcyclea  bofa  baa  bclass

Whena  bcreatinga  bclasses,a  byoua  bwanta  bthema  btoa  bbea  basa  beasya  basa  bpossiblea  btoa  buse.a  btherea  barea  baa  bcouplea  bofa  bbasica  boperationsa  bthata  banya  bclassa  bwilla  blikelya  bneeda  btoa  bprovidea  bsupporta  bfor:

Ita  bneedsa  btoa  binitializea  bitself

Ita  bneedsa  btoa  bcleana  bupa  bmemorya  band/ora  bothera  bresources

Ita  bneedsa  btoa  bcopya  bitself

Alla  bofa  bthesea  barea  bverya  bimportanta  bfora  bthea  bcreationa  bofa  bgooda  bdataa  btypes.a  bwe’lla  busea  bthea  bstringa  btoa  bdemonstratea  bthis.a  bstringsa  bmusta  bbea  bablea  btoa  binitializea  bthemselves,a  bevena  bifa  bthey’rea  bempty.a  btheya  bshoulda  bneeda  btoa  brelya  bona  bexternala  bcodea  bfora  bthat.a  boncea  bthea  bstringa  bisa  bdeclared,a  bit’sa  bimmediatelya  bavailablea  bfora  buse.a  bwhena  byou’rea  bfinisheda  bwitha  bthea  bstring,a  bita  bmusta  bbea  bablea  btoa  bcleana  bupa  bbecausea  balla  bstringsa  ballocatea  bmemory.a  bwhena  bthea  bstringa  bclassa  bisa  bused,a  btherea  bisa  bnoa  bneeda  bfora  banothera  bmethoda  btoa  bbea  bcalleda  bfora  bthat;a  bthea  bstringa  bdoesa  bita  bautomatically.

Lastly,a  bita  bmusta  bbea  bablea  btoa  bcopya  bfroma  bonea  bvariablea  btoa  banother,a  bthea  bsamea  bwaya  bthata  bintegersa  bcana  bbea  bcopieda  bbetweena  bvariables.a  bputa  btogether,a  balla  bofa  bthisa  bfunctionalitya  bshoulda  bbea  bmadea  baa  bparta  bofa  balla  bclassesa  bsoa  bthata  btheya  bcana  beasilya  bbea  bused.

We’lla  btakea  bthesea  bthreea  bfeatures,a  bonea  bata  baa  btime,a  banda  blooka  bata  bhowa  beasya  bc++a  bmakesa  balla  bofa  bthis.

Objecta  bconstruction

Youa  bmighta  bhavea  bspotteda  bthata  bwea  bdidn’ta  bhavea  banya  bcodea  bfora  binitializinga  bthea  bboarda  bina  boura  bchessboarda  binterface,a  bwhicha  bwasa  bthea  bpublica  bsectiona  bofa  bthea  bcode.a  bwea  bcana  bfixa  bthata  bnow.

Whena  baa  bclassa  bvariablea  bisa  bdeclared,a  bthea  bvariablea  bneedsa  btoa  bbea  bablea  btoa  bbea  binitialized:

Chessboarda  bboard;

Whena  bana  bobjecta  bisa  bdeclared,a  bthea  bcodea  bthata  brunsa  bita  bisa  bcalleda  bthea  bconstructor,a  banda  bthisa  bshoulda  bseta  bthea  bobjecta  bupa  bsoa  bthata  bita  bneedsa  bnoa  bmorea  binitialization.a  bconstructorsa  bcana  btakea  bargumentsa  btoo—youa  bsawa  bthisa  bwitha  bthea  bvectora  bdeclarationa  bofa  baa  bparticulara  bsize:a  bvector<int>a  bv(a  b10a  b);

Thea  bvectora  bconstructora  bisa  bcalleda  bwitha  baa  bvaluea  bofa  b10;a  bthea  bnewa  bvectora  bisa  binitializeda  bbya  bthea  bconstructora  bsoa  bthata  bita  bcana  bholda  b10a  bintegersa  bimmediately.

Creatinga  baa  bconstructora  bisa  bnothinga  bmorea  bthana  bdeclaringa  baa  bfunctiona  bwitha  bthea  bsamea  bnamea  basa  bthea  bclass,a  bwitha  bnoa  bargumentsa  banda  bnoa  breturna  bvalue.a  byoua  bdon’ta  bevena  bgivea  bita  baa  bvoida  bvalue;a  bnoa  btypea  bisa  bprovideda  bfora  bthea  breturna  bvalue:a  benuma  bchesspiecea  b{a  bempty_square,a  bwhite_pawna  b/*a  banda  bothersa  b*/a  b};

Enuma  bplayercolora  b{a  bpc_white,a  bpc_blacka  b};

Classa  bchessboard

{

Public:

Chessboarda  b();a  b//a  b<—a  bnoa  breturna  bvaluea  bata  ball!

Playercolora  bgetmovea  b();

Chesspiecea  bgetpiecea  b(inta  bx,a  binta  by);

Voida  bmakemovea  b(inta  bfrom_x,a  binta  bfrom_y,a  binta  bto_x,a  binta  bto_y);

Private:

Chesspiecea  b_board[a  b8a  b][a  b8a  b];

Playercolora  bwhosemove;

};

Chessboard::chessboarda  b()a  b//a  b<—a  bnoa  breturna  bvalue

{

Whosemovea  b=a  bpc_white;

//a  bemptya  bthea  bentirea  bboarda  btoa  bstarta  bwitha  banda  bthena  badda  bina  bthea  bpieces

Fora  b(a  binta  bia  b=a  b0;a  bia  b<a  b8;a  bi++a  b)

{

Fora  b(inta  bja  b=a  b0;a  bja  b<a  b8;a  bj++a  b)

{

Board[a  bia  b][a  bja  b]a  b=a  bemptysquare;

}

}

//a  bothera  bcodea  bneededa  bfora  bboarda  binitialization

}

Ia  bwon’ta  bkeepa  bshowinga  byoua  bthea  bmethoda  bdeclarations,a  bbuta  bia  bwilla  bcontinuea  btoa  bshowa  byoua  bthea  bclassa  bdeclaration,a  bsoa  bthata  byoua  bcana  bseea  bhowa  bita  balla  bfitsa  btogether.

Now,a  bnotea  bthata  bthea  bconstructora  babovea  bisa  bina  bthea  bpublica  bparta  bofa  bthea  bclass.a  bifa  bwea  bdidn’ta  bmakea  bthea  bchessboarda  bconstructora  bpublic,a  bwea  bcouldn’ta  bcreatea  banya  bobjecta  binstances.a  bwhya  bnot?A  bbecause,a  bwhenevera  bana  bobjecta  bisa  bcreated,a  bthea  bconstructora  bhasa  btoa  bbea  bcalled;a  bifa  bwea  bmakea  bita  bprivate,a  bita  bcan’ta  bbea  bcalleda  bfroma  boutsidea  bthea  bclass.a  bobjectsa  bcana  bonlya  bbea  binitializeda  bbya  bcallinga  bthea  bconstructora  band,a  bifa  byoua  bmakea  bita  bprivate,a  byoua  bwon’ta  bbea  bablea  btoa  bdeclarea  bthea  bobject.

Thea  bconstructora  bgetsa  bcalleda  bona  bthea  bsamea  blinea  bthea  bobjecta  bisa  bcreateda  bon:

Chessboarda  bboard;a  b//a  bcallsa  bchessboarda  bconstructor

Ora  bwhena  bmemorya  bisa  ballocated:

Chessboarda  b*boarda  b=a  bnewa  bboard;a  b//a  bthisa  bcallsa  bthea  bchessboarda  bconstructora  basa  bparta  bofa  bthea  bmemorya  ballocation

Whena  bmultiplea  bobjectsa  barea  bdeclared:

Chessboarda  ba;

Chessboarda  bb;

Constructorsa  barea  balwaysa  bruna  bina  bthea  bordera  bofa  bobjecta  bdeclaration—aa  banda  bthena  bb.a  basa  bwitha  baa  bnormala  bfunction,a  bconstructorsa  bcana  btakea  bonea  bora  bmorea  barguments,a  banda  bseverala  bconstructorsa  bcana  bbea  boverloadeda  bbya  bthea  btypea  bofa  bargumenta  bifa  btherea  bisa  baa  bdifferenta  bwaya  bofa  binitializinga  bthea  bobject.a  bfora  bexample,a  baa  bseconda  bconstructora  bcoulda  bbea  bcreateda  bfora  bchessboarda  btoa  btakea  bthea  bboarda  bsize:a  bclassa  bchessboard

{

Chessboarda  b();

Chessboarda  b(inta  bboard_size);

};

Thea  bfunctiona  bdefinitiona  bisa  bthea  bsamea  basa  banya  bclassa  bmethod:

Chessboard::chessboarda  b(inta  bsize)

{

//a  b…a  bcode

}

Thea  bargumenta  bisa  bpasseda  btoa  bthea  bconstructora  blikea  bthis:

Chessboarda  bboard(a  b8a  b);a  b//a  b8a  bisa  bana  bargumenta  btoa  bthea  bchessboarda  bconstructor

Whena  byoua  busea  bthea  bnewa  bkeyword,a  bpassinga  bana  bargumenta  blooksa  blikea  byou’rea  bcallinga  bthea  bconstructora  bdirectly:

Chessboarda  b*p_boarda  b=a  bnewa  bchessboard(a  b8a  b);

Aa  bnotea  bona  bthea  bsyntax:a  balthougha  bparenthesesa  barea  buseda  bfora  bpassinga  barguments,a  byoua  bcan’ta  busea  bthema  btoa  bdeclarea  bobjectsa  bthata  bhavea  bno-argumenta  bconstructors.

Youa  bcan’ta  bdoa  bthis:

Chessboarda  bboard();

Thea  bcorrecta  bforma  bis:

Chessboarda  bboard;

However,a  byoua  bcana  busea  bparenthesesa  bwhena  bthea  bnewa  bkeyworda  bisa  bused:

Chessboarda  b*boarda  b=a  bnewa  bboard();

Thisa  bisa  bonea  bofa  bthea  bunfortunatea  blittlea  bfoiblesa  bofa  bc++a  bparsinga  bbecausea  bthea  bdetailsa  barea  bkepta  bverya  bobscure.a  bjusta  bdon’ta  busea  bparenthesesa  bwhena  byoua  bdeclarea  bobjectsa  bwitha  baa  bno-argumenta  bconstructor.

So,a  bwhata  bhappensa  bifa  baa  bconstructora  bisn’ta  bdeclared?

Ifa  baa  bconstructora  bisn’ta  bdeclared,a  bc++a  bcreatesa  bone.a  bita  bwon’ta  btakea  bargumentsa  bora  binitializea  bints,a  bchars,a  bora  banya  bothera  bprimitivea  btype,a  bbuta  bita  bwilla  binitializea  beverya  bclassa  bfielda  bbya  bcallinga  bthea  bdefaulta  bconstructora  bfora  beacha  bone.

Generally,a  byoua  bshoulda  bcreatea  bconstructorsa  bjusta  btoa  bmakea  bsurea  beverythinga  bgetsa  bproperlya  binitialized.a  basa  bsoona  basa  bthea  bcalla  bconstructora  bisa  bdeclared,a  bc++a  bwon’ta  bgeneratea  bthea  bdefaulta  bfora  byou.a  bthea  bcompilera  bassumesa  bthata  byoua  bknowa  bexactlya  bwhata  byou’rea  bdoinga  banda  bthata  byou’rea  bgoinga  btoa  bcreatea  bthea  bconstructora  byoua  bneed.a  bina  bparticular,a  bifa  byoua  bcreatea  bconstructorsa  bthata  btakea  barguments,a  bthea  bcodea  bnoa  blongera  bhasa  bthea  bdefaulta  bconstructora  bunlessa  byoua  bdeclarea  bonea  bspecifically.

Thisa  bcana  bhavea  bunexpecteda  bconsequences.a  bifa  bthea  bautomaticallya  bgenerateda  bconstructora  bisa  buseda  banda  bthena  byoua  badda  baa  bnon-defaulta  bonea  bthata  btakesa  barguments,a  bthea  bcodea  bthata  bdependsa  bona  bthea  bautomatica  bconstructora  bwon’ta  bcompile.a  bit’sa  bupa  btoa  byoua  btoa  bprovidea  baa  bdefaulta  bconstructora  bbecausea  bthea  bcompilera  bwon’ta  bdoa  bita  bfora  byou.

Initializationa  blista  banda  bconsta  bfields

Ifa  bthea  bclassa  bfieldsa  barea  bdeclareda  basa  bconsts,a  bthea  bfilea  bhasa  btoa  bbea  binitializeda  bina  bthea  blist:

Classa  bconstholder

{

Public:

Constholdera  b(inta  bval);

Private:

Consta  binta  b_val;

};

Constholder::constholdera  b()

:a  b_val(a  bvala  b)

{}

Consta  bfieldsa  bcan’ta  bbea  binitializeda  bbya  bassigninga  btoa  bthema  bbecausea  bthea  bfieldsa  barea  bseta  banda  bcan’ta  bbea  bchanged.a  bthea  bonlya  bplacea  bwherea  bthea  bclassa  bhasa  bnota  bbeena  bformeda  bfullya  bisa  bina  bthea  binitializationa  blist,a  bsoa  bimmutablea  bobjectsa  bcana  bsafelya  bbea  bset.a  bfora  bthea  bsamea  breason,a  bifa  baa  bfielda  bisa  baa  breference,a  bita  bhasa  btoa  bbea  binitializeda  bina  bthea  blist.

## Chaptera  b8:a  blibrary

Thea  bstandarda  btemplatea  blibrary

It’sa  bgooda  btoa  bbea  bablea  btoa  bwritea  byoura  bowna  bdataa  bstructures.a  bhowever,a  basa  byoua  bmighta  bhavea  bpickeda  bup,a  bita  bisn’ta  balla  bthata  bcommon.a  bbuta  byoua  bdidn’ta  bworka  bthrougha  balla  bthea  bpreviousa  bcontenta  bfora  bnoa  breason.a  byou’vea  bnowa  blearneda  bquitea  baa  bbita  babouta  bbuildinga  bdataa  bstructuresa  basa  bnecessary,a  balonga  bwitha  bsomea  bofa  bthea  bmorea  bcommona  bstructuresa  bthata  byoua  bmighta  bneeda  bwhena  bwritinga  baa  bdataa  bstructure.

However,a  bc++a  bhasa  baa  bcoola  bfeature,a  baa  bhugea  blibrarya  bofa  bcodea  bthata  bcana  bbea  breused.a  bit’sa  bcalleda  bthea  bstandarda  btemplatea  blibrarya  b(stl)a  banda  bcontainsa  bthea  bmosta  bcommona  bdataa  bstructures,a  bincludinga  bthosea  bbuilta  bona  bthea  bbinarya  btreesa  banda  blinkeda  blists.a  bthesea  bstructuresa  bleta  byoua  bspecifya  bwhata  bdataa  btypea  btheya  bwilla  bstorea  bata  bthea  btimea  byoua  bcreatea  bthema  bsoa  bthata  btheya  bcana  bbea  buseda  bfora  banything—structureda  bdata,a  bstrings,a  bints,a  banda  bsoa  bon.

Becausea  byoua  bhavea  bthisa  bflexibility,a  bthea  bstla  bwill,a  bina  bmanya  bcases,a  beliminatea  bthea  bneeda  bfora  byoua  btoa  bbuilda  bstructuresa  bofa  byoura  bown.a  businga  bita  bcana  braisea  byoura  bcodea  blevela  bina  bthesea  bways:

Youa  bcana  bstarta  bthinkinga  bofa  byoura  bcodea  bina  btermsa  bofa  bthea  bstructuresa  brequireda  brathera  bthana  bhavinga  btoa  bthinka  babouta  bbuildinga  banda  bimplementinga  bthema  byourself

Youa  bhavea  bfreea  banda  beasya  baccessa  btoa  bthea  bbesta  bdataa  bstructurea  bimplementations,a  bwitha  bspacea  busea  banda  bperformancea  boptimizeda  bfora  bmosta  bproblems

Youa  bnoa  blongera  bhavea  btoa  bconcerna  byourselfa  bwitha  bthea  ballocationa  banda  bdeallocationa  bofa  bmemorya  bfora  byoura  bdataa  bstructures.

However,a  basa  bwitha  beverything,a  businga  bthea  blibrarya  bcomesa  bwitha  bitsa  btrade-offs:

Youa  bneeda  btoa  blearna  bthea  bstla  binterfacesa  banda  bhowa  btheya  bshoulda  bbea  bused

Whena  byoua  bgeta  bcompilera  berrorsa  bfroma  businga  bthea  bstl,a  btheya  barea  bincrediblya  bdifficulta  btoa  breada  banda  bunderstand

Youa  bwon’ta  bfinda  balla  bdataa  bstructuresa  bina  bthea  blibrary

Thoroughlya  bdiscussinga  bthea  bstla  bwoulda  brequirea  bana  bentirea  bbook,a  bsoa  bia  bwilla  bonlya  bgivea  byoua  bana  boverviewa  bofa  bthea  bmosta  bcommona  bdataa  bstructuresa  bthata  byoua  bwilla  busea  bfroma  bthea  bstl.

Vectors

Containeda  bina  bthea  bstla  bisa  bana  barraya  breplacement—thea  bvector.a  bthisa  bisa  bmucha  blikea  bana  barraya  bbuta  bisa  bresizablea  bautomatically;a  byoua  bnoa  blongera  bhavea  btoa  bworrya  babouta  ballocatinga  bmemorya  banda  bmovinga  bthea  bothera  belementsa  baround.a  bhowever,a  bthea  bvectora  bsyntaxa  bisa  bdifferenta  bfroma  bthata  bofa  baa  bstandarda  barray.

Thea  barraya  bsyntaxa  bis:

Inta  ban_array[a  b10a  b];

Whereasa  bthea  bvectora  bsyntaxa  bis:

#includea  b<vector>

Usinga  bnamespacea  bstd;

Vector<int>a  ba_vector(a  b10a  b);

Thea  bvectora  bheadera  bfilea  bmusta  bbea  bincludeda  balonga  bwitha  bthea  bnamespacea  bstd.a  bthisa  bisa  bbecause,a  blikea  bcouta  banda  bcin,a  bthea  bvectora  bisa  baa  bparta  bofa  bthea  bstandarda  blibrary.

Furthermore,a  bwhena  baa  bvectora  bisa  bdeclared,a  byoua  bmusta  bprovidea  bthea  bdataa  btypea  bbeinga  bstoreda  bina  bthea  bvector.a  bthisa  bisa  bdonea  businga  bangleda  bbrackets<>:

Vector<int>

Thisa  bmakesa  busea  bofa  baa  bc++a  bfeaturea  bknowna  basa  btemplates.a  bvectora  bcodea  bisa  bwrittena  bina  bsucha  baa  bwaya  bthata  banya  bdataa  btypea  bcana  bbea  bstored.a  balla  byoua  bhavea  btoa  bdoa  bisa  btella  bthea  bcompilera  bwhata  btypea  baa  bvectora  bisa  bstoring.a  bwhata  bthisa  breallya  bmeansa  bisa  bthata  bwea  bhavea  btwoa  btypesa  bhere:a  bthea  bdataa  bstructurea  btype,a  bwhicha  bdictatesa  bthea  bwaya  bdataa  bisa  borganized,a  banda  bthea  bdataa  btypea  bhelda  bina  bthea  bdataa  bstructure.a  businga  baa  btemplatea  bletsa  byoua  bcombinea  bdifferenta  bdataa  bstructurea  btypesa  bwitha  bdifferenta  bdataa  btypesa  bwithina  bthea  bdataa  bstructure.

Finally,a  bwhena  bthea  bvectora  bsizea  bisa  bprovided,a  bita  bmusta  bbea  bplaceda  bina  baa  bseta  bofa  bparentheses,a  brathera  bthana  bbrackets:

Vector<int>a  ba_vector(a  b10a  b);

Thisa  bisa  bthea  bsyntaxa  buseda  bfora  bthea  binitializationa  bofa  bcertaina  bvariablea  btypes.a  bfora  bthis,a  bthea  bvaluea  bofa  b10a  bisa  bpasseda  btoa  bthea  binitialization,a  bcalleda  bthea  bconstructor,a  banda  bthata  bsetsa  bthea  bvectora  bwitha  bthea  bsizea  bten.a  basa  bwea  bgoa  bthrougha  bthea  bguide,a  byoua  bwilla  blearna  babouta  bconstructorsa  banda  bobjectsa  bthata  bhavea  bconstructors.

Oncea  bthea  bvectora  bisa  bcreated,a  bindividuala  belementsa  bcana  bbea  baccesseda  bina  bthea  bsamea  bwaya  basa  bana  barray:

Fora  b(a  binta  bia  b=a  b0;a  bia  b<a  b10;a  bi++a  b)

{

A_vector[a  bia  b]a  b=a  b0;

An_array[a  bia  b]a  b=a  b0;

}

Callinga  baa  bmethoda  bona  baa  bvector

Aa  bvectora  bprovidesa  byoua  bwitha  bmucha  bmorea  bthana  bthea  bfunctionalitya  bfora  bana  barray.a  byoua  bcana  bdoa  balla  bsortsa  bofa  bthings,a  bsucha  basa  baddinga  belementsa  bbeyonda  bthea  bvectora  bend.a  bthea  bvectora  bprovidesa  bfunctionsa  btoa  bhelpa  bwitha  bthisa  bsorta  bofa  bthing,a  bbuta  bthea  bfunctiona  bsyntaxa  bisn’ta  bthea  bsamea  basa  bthea  bsyntaxa  bwea  buseda  bbefore.

Aa  bvectora  busesa  baa  bc++a  bfeaturea  bknowna  basa  baa  bmethod.a  bthisa  bisa  baa  bfunctiona  bthata  byoua  bdeclarea  bwitha  bthea  bdataa  btype.a  bcallinga  bmethodsa  brequiresa  bnewa  bsyntax,a  basa  bina  bthisa  bexample:

A_vector.size();

Thisa  bisa  bcallinga  baa  bmethoda  bsizea  bona  ba_vector,a  banda  bita  breturnsa  bthata  bsize.a  bit’sa  bmucha  blikea  baccessinga  baa  bstructurea  bfielda  bbut,a  binstead,a  byou’rea  bcallinga  baa  bmethoda  bthata  bgoesa  bwitha  bthea  bstructure.a  balthougha  bsomethinga  bisa  bbeinga  bdonea  btoa  ba_vectora  bbya  bthea  bmethod,a  ba_vectora  bdoesn’ta  bneeda  btoa  bbea  bpasseda  basa  bana  bargumenta  btoa  bthea  bmethod.a  bthea  bsyntaxa  balreadya  bknowsa  bthata  ba_vectora  bisa  btoa  bbea  bpasseda  basa  bana  bimplicita  bargumenta  bintoa  bthea  bsizea  bmethod.

Thea  bsyntaxa  bbelow

<variable>.<functiona  bcall>(a  b<args>a  b);

Cana  bbea  bthoughta  bofa  basa  bcallinga  baa  bfunctiona  bthata  bgoesa  bwitha  bthea  btypea  bfora  bthea  bvariable.a  bina  bothera  bwords,a  bit’sa  baa  bbita  blikea  bwriting:

<functiona  bcall>(a  b<variable>,a  b<args>a  b);

Ina  bthea  bexample:

A_vector.size();

Ita  bwoulda  bbea  blike:

Size(a  ba_vectora  b);

Overa  bthea  bnexta  bfewa  bsections,a  bwea  bwilla  bdiscussa  bmorea  bmethods,a  bincludinga  bwaysa  btoa  bdeclarea  banda  busea  bthem.a  bfora  bnow,a  bit’sa  benougha  bfora  byoua  btoa  bunderstanda  bthata  bseverala  bmethodsa  bcana  bbea  bcalleda  bona  baa  bvector,a  businga  bthea  brighta  bsyntax.a  bthea  bspeciala  bmethoda  bsyntaxa  bisa  bthea  bonlya  bwaya  bofa  bmakinga  bthata  btypea  bofa  bfunctiona  bcall.a  byoua  bcouldn’t,a  bfora  bexample,a  bwritea  bthis:a  bsize(

A_vectora  b).

Othera  bvectora  bfeatures

Aa  bvectora  balsoa  bmakesa  bita  bverya  beasya  btoa  bupa  bthea  bnumbera  bofa  bitemsa  bhelda  bwithouta  bneedinga  btoa  ballocatea  bmemory.a  bfora  bexample,a  baddinga  bextraa  bitemsa  btoa  bthea  bvectora  bwoulda  bbea  bwrittena  blikea  bthis:

A_vector.push_back(a  b10a  b);

Thisa  baddsa  banothera  bitema  bofa  b10a  bata  bthea  benda  bofa  bthea  bvector.a  bthea  bvectora  bwilla  btakea  bcarea  bofa  bthea  bresizing.a  bifa  byoua  bwanteda  btoa  bdoa  bthisa  bwitha  bana  barray,a  bthea  bmemorya  bwoulda  bhavea  btoa  bbea  ballocated,a  bthea  bvaluesa  bcopieda  bover,a  banda  bthea  bnewa  bitema  baddeda  bin.a  bwhilea  baa  bvectora  bdoesa  bdoa  bmemorya  ballocationa  banda  bcopying,a  bita  bdoesa  bita  bintelligently,a  bina  baa  bmannera  bina  bwhicha  bita  bdoesn’ta  bhavea  btoa  bresizea  bitselfa  beverya  btimea  baa  bnewa  bitema  bisa  badded.

However,a  balthougha  byoua  bcana  busea  bpush_backa  btoa  badda  bitemsa  btoa  bthea  benda  bofa  bthea  bvector,a  businga  bthea  bbracketsa  bona  btheira  bowna  bwouldn’ta  bbea  bthea  bsame.a  bbracketsa  bleta  byoua  bworka  bonlya  bwitha  bdataa  bthata  bhasa  balreadya  bbeena  ballocated,a  bmainly,a  bsoa  bthata  bmemorya  ballocationa  bisn’ta  bdonea  bwithouta  byoua  bbeinga  baware.

So,a  baa  bcodea  blikea  bthis:

Vector<int>a  ba_vector(a  b10a  b);

A_vector[a  b10a  b]a  b=a  b10;a  b//a  bthea  blasta  bvalida  belementa  bisa  b9

Wouldn’ta  bworka  banda  bwoulda  blikelya  bresulta  bina  bthea  bprograma  bcrashing.a  bnota  btoa  bmention,a  bit’sa  bdangerous.a  bwritinga  bita  blikea  bthis:

Vector<int>a  ba_vector(a  b10a  b);

A_vector.push_back(a  b10a  b);a  b//a  badda  baa  bnewa  belementa  btoa  bthea  bvector

Worksa  btoa  bresizea  bthea  bvector.

Maps

Wea  bmentioneda  bmapsa  baa  blittlea  bwhilea  bagoa  businga  baa  bvaluea  btoa  blooka  bupa  banothera  bvalue.a  bthisa  bisa  bcommona  bina  bprogramminga  bsucha  basa  bwhena  byoua  bwanta  btoa  bimplementa  bana  baddressa  bbooka  bfora  bemailsa  bwherea  baddressesa  barea  blookeda  bupa  bbya  bnamea  bora  baa  bprograma  bwherea  byoua  blooka  bupa  bana  baccounta  businga  bana  baccounta  bnumbera  bora  blettinga  buser’sa  blogina  btoa  btheira  bgames.

Thea  bstla  bgivesa  busa  baa  bmapa  btypea  bthata  bletsa  busa  bspecifya  bthea  bkeya  btypea  banda  bvalue.a  bana  bexamplea  bwoulda  bbea  baa  bdataa  bstructurea  bthata  bholdsa  bana  bemaila  baddressa  bbook;a  bthisa  bcoulda  bbea  bimplementeda  basa  bfollows:

#includea  b<map>

#includea  b<string>

Usinga  bnamespacea  bstd;

Map<string,a  bstring>a  bname_to_email;

Wea  bhavea  btoa  btella  bthea  bstructurea  bthata  btherea  barea  btwoa  btypes:a  bstring,a  bfora  bthea  bkey,a  banda  banothera  bstringa  bfora  bthea  bvalue,a  bana  bemaila  baddressa  bina  bthisa  bcase.

Onea  bofa  bthesea  bmaps’a  bhelpfula  bfeaturesa  bisa  bthata  bwhena  baa  bmapa  bisa  bused,a  bthea  bsyntaxa  bcana  balsoa  bbea  buseda  basa  bana  barray.a  bifa  byoua  bwanta  btoa  badda  bvalue,a  bit’sa  bmucha  blikea  bana  barray,a  bexcepta  bthea  bkeya  btypea  bisa  buseda  binsteada  bofa  bana  binteger:

Name_to_email[a  b“billya  bbunter”a  b]a  b=a  b“billybunterathisemailaddress.com”;

Anda  bgettinga  bvaluea  bfroma  baa  bmapa  bisa  bmucha  bthea  bsame:

Couta  b<<a  bname_to_email[a  b“billya  bbunter”a  b];

Youa  bgeta  bthea  bsimplicitya  bthata  bgoesa  bwitha  bana  barray,a  bbuta  bwitha  bthea  babilitya  btoa  bstorea  bwhatevera  btypea  byoua  bwant.a  banda  bwhat’sa  bevena  bbettera  bisa  bthat,a  bunlikea  bthea  bvector,a  bthea  bmapa  bsizea  bdoesn’ta  bhavea  btoa  bbea  bseta  bbeforea  bthea  b[]a  boperatora  bisa  buseda  btoa  badda  bana  belement.

Removinga  bitemsa  bfroma  bmapsa  bisa  bjusta  basa  beasy.a  blet’sa  bsaya  bthata  byoua  bfella  bouta  bwitha  bbillya  bbuntera  banda  bwanta  bhima  bremoveda  bfroma  byoura  baddressa  bbook.a  byoua  bcana  bdoa  bthata  businga  bthea  berasea  bmethod:

Name_to_email.erase(a  b“billya  bbunter”a  b);

Anda  byoua  bcana  busea  bthea  bsize()a  bmethoda  btoa  bchecka  bwhata  bsizea  baa  bmapa  bis:

Name_to_address.size();

Anda  bthea  bempty()a  bmethoda  btoa  bseea  bifa  baa  bmapa  bisa  bempty:

Ifa  b(a  bname_to_address.empty()a  b)

{

Couta  b<<a  b“thea  baddressa  bbooka  bisa  bempty.a  bia  bbeta  byoua  bwisha  byoua  bhadn’ta  bdeleteda  bbilly.”;

}

Doa  bnota  bconfusea  bthisa  bwitha  bhowa  byoua  bmakea  baa  bmapa  bempty.a  bthat’sa  bdonea  businga  bthea  bclear()a  bmethod:

Name_to_address.clear();

Becausea  bofa  bthea  bconsistencya  bina  bthea  bnaminga  bconventionsa  bina  bthea  bstl,a  bthea  bsamea  bmethodsa  bcana  bbea  buseda  bona  bvectors.

Iterators

Asa  bwella  basa  bdataa  bstoragea  banda  bthea  babilitya  btoa  baccessa  belementsa  bindividually,a  byoua  bcana  balsoa  bgoa  bthrougha  balla  bthea  bitemsa  bina  baa  bdataa  bstructure.a  bwitha  barraysa  bora  bvectors,a  bthisa  bisa  bjusta  baa  bcasea  bofa  breadinga  beacha  belementa  businga  bthea  barraya  blength.a  bbuta  bwitha  bmaps,a  bbecausea  btheya  bhavea  bbotha  bnumerica  banda  bnon-numerica  bkeys,a  byoua  bcan’ta  balwaysa  biteratea  bthrougha  businga  baa  bcountera  bvariable.

Toa  bgeta  barounda  bthis,a  bthea  bstla  bprovidesa  busa  bwitha  bana  biterator,a  bwhicha  bisa  baa  bvariablea  bthata  bletsa  byoua  baccessa  bthea  belementsa  bofa  baa  bdataa  bstructurea  bsequentially,a  bevena  bifa  bthea  bdataa  bstructurea  bdoesn’ta  busuallya  bhavea  baa  bgooda  bwaya  bofa  bdoinga  bthat.a  bwe’lla  bstarta  bbya  blookinga  bata  businga  biteratorsa  bwitha  bvectorsa  banda  bthena  bmovea  bona  btoa  businga  bonea  bwitha  bthea  bmapa  belements.a  bthea  bideaa  bisa  bthata  bthea  biteratora  bwilla  bstorea  bthea  bpositiona  bina  baa  bstructurea  bsoa  bthata  byoua  bcana  busea  bthata  bpositiona  btoa  baccessa  bthea  belement.a  bthena  byoua  bcalla  baa  bmethoda  bona  bthea  biteratora  btoa  bmovea  bona  btoa  bthea  bnexta  belement.

Somea  bunusuala  bsyntaxa  bisa  brequireda  bfora  bdeclaringa  bana  biterator.a  bfora  baa  bvectora  bofa  bintegers,a  bita  bwoulda  blooka  blikea  bthis:

Vector<int>::iterator

Whata  bthisa  bsaysa  bisa  bthata  byoua  bhavea  bthea  bvectora  banda  bwanta  bana  biteratora  bthata  bwilla  bworka  bfora  bthea  bspecifica  btype,a  bwhicha  bisa  bwhya  bwea  buseda  bthea  b::iterator.a  bbecausea  bthea  biteratora  bmarksa  bthea  bpositiona  bina  bthea  bstructure,a  bthea  biteratora  bisa  brequesteda  bfroma  bthea  bdataa  bstructure:a  bvectora  bvec;

Vector<int>a  bvec;

Vec.push_back(a  b1a  b);

Vec.push_back(a  b2a  b);

Vector<int>::iteratora  bitra  b=a  bvec.begin();

Thea  bbegina  bmethoda  bcalla  bwilla  breturna  bana  biteratora  bthata  ballowsa  byoua  btoa  baccessa  bthea  bvector’sa  bfirsta  belement.

Iteratorsa  bcana  bbea  bconsidereda  bsimilara  btoa  bpointers—youa  bspeaka  bofa  belementa  blocationsa  bina  bthea  bstructurea  bora  busea  bita  bfora  bgettinga  bthea  belement.a  bina  boura  bcase,a  bwea  breada  bthea  bvector’sa  bfirsta  belementa  businga  bthisa  bsyntax:

Couta  b<<a  b*itr;a  b//a  bprinta  bouta  bthea  bvector’sa  bfirsta  belement

Wea  busea  bthea  b*a  boperatora  bina  bthea  bsamea  bwaya  bwea  bdoa  bwitha  baa  bpointer;a  bita  bmakesa  bsensea  bwhena  byoua  bconsidera  bthata  bbotha  bstorea  blocations.

Ifa  byoua  bwanta  bthea  bnexta  belement,a  bthea  biteratora  bisa  bincremented:

Itr++;

Thisa  bletsa  bthea  biteratora  bknowa  bita  bneedsa  btoa  bmovea  bona  btoa  bthea  bnexta  belement.

Thea  bprefixa  boperatora  bcana  balsoa  bbea  bused:

++itr;

Youa  bcana  bseea  bifa  byoua  bhavea  breacheda  bthea  benda  bbya  bmakinga  baa  bcomparisona  bwitha  bthea  biteratora  banda  bthea  benda  biterator;a  btoa  bdoa  bthis,a  bcall:

Vec.end();

Ifa  byoua  bwanta  bcodea  bthata  bwilla  bloopa  bovera  baa  bwholea  bvector,a  bita  bwilla  blooka  blikea  bthis:

Fora  b(a  bvector<int>::iteratora  bitra  b=a  bvec.begin();a  bitra  b!=a  bvec.end();a  b++itra  b)

{

Couta  b<<a  b*itra  b<<a  bendl;

}

Wea  bcana  bloopa  bovera  baa  bmapa  businga  baa  bsimilara  bapproach,a  bbuta  bremembera  bthata  bthea  bmapa  bdoesn’ta  bstorea  bsinglea  bvalues;a  bita  bstoresa  bkey/valuea  bpairs.a  bwhena  byoua  bdereferencea  bana  biterator,a  bita  bhasa  btwoa  bfields—onea  bfora  bkeya  banda  bonea  bfora  bvalue:

Inta  bkeya  b=a  bitr->first;a  b//a  bgeta  bthea  bkeya  bfroma  biterator

Inta  bvaluea  b=a  bitr->second;a  b//a  bgeta  bthea  bvaluea  bfroma  biterator

Belowa  bisa  bsomea  bcodea  bthata  bwilla  bdisplaya  baa  bmap’sa  bcontenta  bina  bana  beasy-to-reada  bformat:

Voida  bdisplaymapa  b(map<string,a  bstring>a  bmap_to_print)

{

Fora  b(a  bmap<string,a  bstring>::iteratora  bitra  b=a  bmap_to_print.begin(),a  benda  b=

Map_to_print.end();

Itra  b!=a  bend;

++itra  b)

{

Couta  b<<a  bitr->firsta  b<<a  b"a  b—>a  b"a  b<<a  bitr->seconda  b<<a  bendl;

}

}

Thisa  bcodea  bisa  bverya  bsimilara  btoa  bwhata  bisa  buseda  bfora  biteratinga  bovera  baa  bvector;a  bthea  bonlya  bdifferencea  bisa  bthata  bthea  bmapa  bdataa  bstructurea  bisa  buseda  balonga  bwitha  bthea  bfirsta  banda  bseconda  bfieldsa  bona  bthea  biterator.

Checkinga  baa  bmapa  bfora  baa  bvalue

Sometimesa  byoua  bwanta  btoa  bbea  bablea  btoa  bseea  bifa  baa  bgivena  bkeya  bhasa  bbeena  bstoreda  bina  baa  bmap.a  blet’sa  bsaya  byou’rea  blookinga  bfora  bsomeonea  bina  byoura  baddressa  bbook.a  byoua  busea  bthea  bfind()a  bmethoda  btoa  bseea  bifa  bthea  bspecifieda  bvaluea  bisa  btherea  band,a  bifa  bita  bis,a  bretrievea  bit.a  bana  biteratora  bisa  breturneda  banda  bwilla  beithera  bhavea  bthea  bobjecta  blocationa  bwitha  bthea  bspecifieda  bkeya  bora  bwilla  bbea  bana  benda  biteratora  bifa  bthea  bobjecta  bwasn’ta  bfound.

Map<string,a  bstring>::iteratora  bitra  b=a  bname_to_email.find(a  b“billya  bbunter”a  b);

Ifa  b(a  bitra  b!=a  bname_to_email.end()a  b)

{

Couta  b<<a  b“howa  bita  bisa  btoa  bseea  bbillya  bagain.a  bhisa  bemaila  bis:a  b"a  b<<a  bitr->second;

}

Ifa  byoua  bjusta  bwanta  btoa  baccessa  bana  belementa  bthata  bisn’ta  bina  bthea  blist,a  busea  bthea  bstandarda  bbrackets:

Name_to_email[a  b“johna  bdoe”a  b];

Thea  bmapa  bwilla  binserta  bana  bemptya  belementa  bifa  bthea  bvaluea  bisn’ta  btherea  balready.

Takinga  bstock

Ia  bhavea  bonlya  btoucheda  bona  bthea  bbasicsa  bofa  bthea  bstl,a  bbuta  byoua  bnowa  bhavea  benougha  binformationa  btoa  busea  bsomea  bofa  bthea  bfoundationala  btypesa  bina  bthea  blibrary.a  bthea  bvectora  bcana  bbea  buseda  btoa  breplacea  barraysa  baltogethera  band,a  bifa  byoua  bdon’ta  bwanta  btoa  btakea  bthea  btimea  btoa  binserta  banda  bmodify,a  bvectorsa  bcana  balsoa  bbea  buseda  bina  bplacea  bofa  blinkeda  blists.a  bwitha  bthea  bvectora  btypea  bata  byoura  bfingertips,a  btherea  barea  bverya  bfewa  breasonsa  bwhya  byoua  bwoulda  bwanta  btoa  busea  bana  barray,a  banda  bmosta  bofa  bthosea  breasonsa  barea  badvanced,a  bsucha  basa  bwhena  byoua  bworka  bwitha  bthea  bfilea  bi/o,a  bwhicha  bwea  bwilla  bdiscussa  bata  bthea  benda  bofa  bthea  bguide.

Thea  bsinglea  bmosta  busefula  bdataa  btypea  bisa  bthea  bmap.a  businga  bmapsa  bmakesa  bita  beasya  btoa  bwritea  bsophisticateda  bprogramsa  bwithouta  bhavinga  btoa  bworrya  btooa  bmucha  babouta  bdataa  bstructurea  bcreation.a  binstead,a  byoura  battentiona  bcana  bbea  bfocuseda  bona  bsolvinga  bproblems.a  bina  bsomea  bways,a  bthea  bmapa  bcana  breplacea  baa  bbasica  bbinarya  btree.a  bmosta  bofa  bthea  btime,a  byou’lla  bwanta  btoa  bgoa  bintoa  bbinarya  btreea  bimplementationa  bunlessa  bit’sa  bfora  bcertaina  bperformancea  brequirements,a  bora  byoua  bspecificallya  bneeda  baa  btreea  bstructure.

That’sa  bwherea  bthea  bstl’sa  btruea  bpowera  blies:a  barounda  b80a  bpercenta  bofa  bthea  btime,a  bita  bgivesa  byoua  bthea  bcorea  bstructuresa  byoua  bneed,a  bleavinga  byoua  bfreea  btoa  bwritea  bthea  bcodea  bthata  bsolvesa  bthea  bproblems.a  bthea  bresta  bofa  bthea  btime,a  byoua  bwilla  bneeda  bthea  bknowledgea  btoa  bbuilda  banda  bimplementa  byoura  bowna  bdataa  bstructures.

Somea  bprogrammersa  bprefera  businga  btheira  bcodea  binsteada  bofa  bready-builta  bcode.a  bmosta  bofa  bthea  btime,a  byoua  bshoulda  bnota  busea  byoura  bowna  bdataa  bstructures;a  bthea  bbuilt-ina  bonesa  barea  bfaster,a  bbetter,a  banda  bmorea  bcomplete.a  bhowever,a  bknowinga  bhowa  btoa  bbuilda  bdoesa  bgivea  byoua  bmucha  bbettera  binsighta  bintoa  businga  bthem.

So,a  bwhena  bmighta  byoua  bwanta  btoa  busea  byoura  bowna  bstructures?A  blet’sa  bsaya  byoua  bwanta  baa  bcalculatora  bthata  ballowsa  barithmetica  bexpressionsa  btoa  bbea  binputa  bbya  busersa  banda  bthena  bevaluatesa  bthea  binputsa  bwitha  bthea  bcorrecta  bordera  bofa  boperations.a  bana  bexamplea  bwoulda  bbea  bsomethinga  blikea  b4*9+8/3,a  bevaluateda  bina  baa  bwaya  bthata  bthea  bdivisiona  banda  bmultiplicationa  barea  bdonea  bbeforea  bthea  baddition.

Thisa  bkinda  bofa  bstructurea  bcana  beasilya  bbea  bthoughta  bofa  bina  btermsa  bofa  baa  btree.a  byoua  bcoulda  bexpressa  b4*9+8/3a  blikea  bthis:

+

/

4a  b*8a  b3

Eacha  bnodea  bisa  bevaluateda  bina  bonea  bofa  btwoa  bways:

Ifa  bthea  bnodea  bisa  baa  bnumber,a  bthea  bvaluea  bisa  breturned

Ifa  bthea  bnodea  bisa  bana  boperator,a  bthea  bvaluesa  bofa  bthea  btwoa  bsubtreesa  barea  bcomputed,a  banda  bthea  boperationa  bisa  bperformed.

Toa  bbuilda  baa  btreea  blikea  bthisa  bwilla  brequirea  baa  brawa  bdataa  bstructure;a  byoua  bcan’ta  bjusta  busea  baa  bmap.a  bifa  byoua  bonlya  bhavea  bthea  bstl,a  byoua  bwilla  bstrugglea  bwitha  bthis.a  bhowever,a  boncea  byoua  bunderstanda  brecursiona  banda  bbinarya  btrees,a  bita  bbecomesa  baa  blota  beasier.

## Chaptera  b9:a  bstl

Stl/c++a  bstandarda  blibrary:a  bcontainers,a  balgorithms,a  biterators

Aa  bcommona  bmisnomera  bisa  btoa  brefera  btoa  bthea  bc++a  bstandarda  blibrarya  basa  bthea  bstl.a  bthea  bstl,a  bora  bstandarda  btemplatea  blibrary,a  bwasa  baa  bstandarda  bdevelopeda  bsometimea  bina  bthea  bpast.a  bthea  bc++a  bstandarda  blibrarya  bisa  baa  bseta  bofa  btemplates,a  bmanya  bofa  bwhicha  bwerea  badopteda  bfroma  bthea  bstl.a  bthea  bstla  bisa  bnowa  bdeprecated,a  bbuta  bsomea  bextremelya  busefula  btemplatesa  bremain.

Thea  bstandarda  blibrarya  boffersa  baa  bsolutiona  btoa  bthisa  bproblema  bina  bthea  bforma  bofa  bcontainers.a  bcontainersa  bmanagea  bsetsa  bofa  bdataa  bofa  bthea  bsamea  btype.a  btheya  bincludea  bvectors,a  bsets,a  banda  blists,a  bamonga  bothers.

Vectorsa  barea  bmucha  blikea  barrays,a  bexcepta  btheya  bhandlea  btheira  bowna  bstoragea  banda  bsize.

Mucha  blikea  bwitha  bstrings,a  byoua  bneeda  btoa  bimporta  bthea  bvectora  blibrarya  bina  bordera  btoa  busea  bthea  btemplate:

#includea  b<vector>

Nowa  byou’rea  bablea  btoa  baccessa  beverythinga  bregardinga  bvectors.

Youa  bdeclarea  baa  btemplatea  blikea  bso:

Template<type>a  bvariablename;

Let’sa  bsaya  bwea  bwanteda  btoa  bgoa  bbacka  btoa  bthea  bearliera  bexamplea  bofa  bgrades,a  bcreatinga  baa  bself-sizinga  barraya  bofa  bgrades.a  bwe’da  bdeclarea  bita  blikea  bthis:

Vector<int>a  bgrades;

Addinga  bvaluesa  btoa  baa  btemplatea  bisa  bsimple.a  byoua  bhada  bana  belementa  bbya  businga  bthea  bconcepta  bofa  bpushinga  banda  bpopping.a  byoua  bpusha  baa  bnewa  bvaluea  bontoa  bthea  bvector,a  bora  byoua  bpopa  baa  bvaluea  boff.

Let’sa  bsaya  bthea  bfirsta  bgradea  byoua  bwanteda  btoa  badda  bwasa  baa  b55a  b(poora  bguy.)A  bwea  bcoulda  bdoa  bthisa  bbya  btyping:

Grades.push_back(55);

You’vea  bnowa  baddeda  byoura  bfirsta  bvaluea  btoa  bthea  bvector.

Whata  bifa  byoua  bwanta  btoa  badda  baa  bseta  bofa  bvalues?A  bwell,a  bluckily,a  bina  bc++11,a  byoua  bcana  balsoa  binserta  baa  bseta  bofa  bvectorsa  bina  baa  bsimilara  bmannera  btoa  bwhicha  byoua  binitializea  baa  bseta  bofa  bvaluesa  bina  bana  barray,a  businga  bthea  bvector.insert()a  bfunction.a  bthisa  btakesa  btwoa  barguments:a  bthea  bindexa  bata  bwhicha  byoua  bstarta  binserting,a  banda  bthea  bvaluesa  byou’da  blikea  btoa  binsert.a  bifa  byoua  bhavea  bmultiplea  bvaluesa  bina  byoura  bvector,a  byoua  bcana  bjusta  busea  bvector.end()a  btoa  bfinda  bthea  bpointa  bofa  binsertion.

Grades.insert(grades.end(),a  b{a  b96,a  b64,a  b75,a  b83a  b});

Ina  bearliera  bversions,a  byoua  bwoulda  bneeda  btoa  bcreatea  baa  btemporarya  barraya  btoa  binserta  bthea  bdata.

Int[]a  btmpa  b=a  b{a  b96,a  b64,a  b75,a  b83a  b};

Grades.insert(grades.end(),a  btmp,a  btmpa  b+a  b4);

Toa  bgoa  bthrougha  beverya  bitema  bina  bthea  blist,a  byoua  bcana  busea  bsomethinga  bcalleda  baa  bfora  beacha  bloopa  bina  bothera  blanguages.a  bifa  bwea  bwanteda  btoa  bprinta  bouta  beverya  bitema  bona  bthea  blist,a  bwea  bwoulda  bdoa  bthea  bfollowing:

Fora  b(inta  bia  b:a  bgrades)a  b{

Couta  b<<a  bia  b<<a  b“\n”;

}

Whata  bifa  bwea  bweren’ta  businga  baa  bprimitivea  bdataa  btypea  bbuta  binsteada  bana  bobject?A  bthere’sa  bsupporta  bfora  bthata  basa  bwell,a  businga  bsomethinga  bcalleda  biterators.a  bbya  bthea  busagea  bofa  biterators,a  byoua  bcana  baccessa  bmethodsa  bofa  bthea  bobjecta  b(sucha  basa  b.length()a  bora  b.substr()a  bfora  baa  bstring).

Ifa  bwea  bhada  baa  bvectora  bofa  bstrings,a  bfora  bexample,a  bcalleda  bja  banda  bwea  bwanteda  btoa  bprinta  bthea  blengtha  bofa  beverya  bstringa  btherein:

Fora  b(stringa  bia  b:a  bj)a  b{

Couta  b<<a  bia  b<<a  b"a  b-a  bstringa  blength:a  b"a  b<<a  bi.length()a  b<<a  b“\n”;a  b}

Youa  bcana  bdoa  bthisa  bfora  banya  bobjecta  byoua  bcreate,a  bbuta  bwe’lla  btalka  bmorea  bexplicitlya  babouta  bthata  bwhena  bwea  bactuallya  bstarta  bcreatinga  bobjectsa  bina  bthea  bnexta  bchapter.

Anothera  btypea  bofa  bcontainer,a  blists,a  bfunctionsa  bverya  bsimilarlya  btoa  bvectors.a  bthea  bspecifica  bdifferencesa  bbetweena  bthesea  btwoa  barea  bbeyonda  bthea  bgraspa  bofa  baa  brelativea  bbeginner.a  bstill,a  bthea  bgenerala  brulea  bconcerninga  bthesea  btwoa  btypesa  bofa  bcontainersa  bisa  bthata  bvectora  bisa  bgenerallya  bthea  bonea  bthata  bshoulda  bbea  buseda  bunlessa  byoua  bhavea  btoa  bcontinuallya  badda  bora  berasea  belementsa  bfroma  banywherea  bothera  bthana  bthea  benda  bofa  bthea  bcontainer.

There’sa  banothera  btypea  bofa  bcontainera  bcalleda  bana  bassociativea  bcontainer,a  bwhicha  bisa  bformatteda  bwitha  baa  bkeya  bvaluea  banda  baa  bmappeda  bvalue.a  bit’sa  bgenerallya  bordereda  baccordinga  btoa  bthea  bkeys.a  bthea  bmosta  bprominenta  btypea  bofa  bassociativea  bcontainera  bisa  bcalleda  baa  bmap.a  bthisa  bisa  bgreata  bwhena  byoua  bneeda  btoa  bassociatea  baa  bseta  bofa  bdataa  bwitha  baa  bcertaina  btrait.a  bfora  baa  breal-worlda  bexample,a  baa  bstore’sa  binventorya  bsystema  bcoulda  bbea  bkepta  bwitha  baa  bmapa  bofa  bskua  bcodesa  b(integersa  b-a  bthea  bkey)a  banda  bitema  bnamesa  b(stringsa  b-a  bthea  bmappeda  bdata).

Fora  bthis,a  byou’da  bimporta  b<map>,a  banda  bdeclarea  baa  bmapa  bby:

Map<int,a  bstring>a  binventory;

Inventory[00400030]a  b=a  b“tamagotchi,a  bblue”;

Inventory[00400031]a  b=a  b“tamagotchi,a  bwhite”;

Inventory[00324359]a  b=a  b“twilight,a  bdvd”;

Inventory[44539294]a  b=a  b“darka  bsouls,a  bxboxa  b360”;

Ifa  byoua  bwanteda  btoa  brecalla  baa  bspecifica  belementa  blatera  bina  byoura  bcode,a  byoua  bcoulda  bdoa  bsomethinga  balonga  bthea  blinesa  bof:

Couta  b<<a  b“inventory[00400030]a  bis:a  b“a  b<<a  binventory[00400030]a  b<<a  b“\n”;

Callinga  binventory[00400030]a  bwoulda  bprinta  bouta  bthea  bmappeda  bvalue,a  bherea  bbeinga  b“tamagotchi,a  bblue”.

There’sa  banothera  btypea  bofa  bassociativea  bcontainera  bcalleda  baa  bset.a  bsetsa  bfunctiona  bverya  bsimilara  btoa  bmaps,a  bexcepta  bthata  btheya  bdon’ta  ballowa  bduplicates.a  bmapsa  ballowa  bduplicatea  bvalues,a  bbuta  bnota  bduplicatea  bkeys.

Alsoa  bincludeda  bina  bthea  bstla  bisa  baa  blibrarya  bcalleda  b“algorithms”.a  bthisa  blibrarya  bcana  bbea  buseda  btoa  bsearch,a  bsort,a  banda  bmanipulatea  belementa  branges.

Includeda  bina  bthesea  barea  bfunctionsa  bsucha  basa  bequal(),a  bwhicha  bdeterminesa  bifa  btwoa  bsetsa  bofa  belementsa  barea  bequala  btoa  beacha  bother.a  bthere’sa  balsoa  btransform(),a  bwhicha  bappliesa  baa  bgivena  bfunctiona  btoa  baa  bgivena  brange.

## Conclusion

We’vea  bcomea  btoa  bthea  benda  bofa  bthisa  bbook,a  bbuta  bthisa  bisa  bjusta  bthea  bstarta  bofa  baa  blonga  banda  bfruitfula  bjourneya  bfora  byou,a  baa  blifea  bofa  bprogramming.a  bwitha  bthea  bbasicsa  bofa  bc++a  bundera  byoura  bbelt,a  bit’sa  btimea  btoa  bstarta  byoura  breala  blearning.a  bstarta  bwritinga  bthosea  bprograms!A  bstarta  bimplementinga  bdataa  bstructuresa  banda  balgorithms.

Ifa  byoua  benjoyeda  bgettinga  bstarteda  bwitha  bc++,a  btherea  bisa  bsoa  bmucha  bmorea  btoa  blearna  banda  bdoa  bwitha  bthisa  bwonderfula  blanguage.a  bbea  bsurea  btoa  bcontinuea  byoura  bjourneya  bwitha  bthea  bseconda  bbooka  bina  bthea  bseries,a  bwhicha  blooksa  bata  bslightlya  bmorea  bcomplexa  btopicsa  bwhilea  bstilla  bbeinga  bbeginner-friendly.

C++a  bprogramminga  blanguagea  bisa  baa  bcompetitivea  bgeneral-purposea  bplatforma  bwhicha  bborrowsa  bsomea  bfeaturesa  bofa  bana  bimperativea  bprogramminga  bparadigma  banda  bcana  bruna  bona  banya  bplatform.a  bita  bisa  breferreda  btoa  basa  bana  bimperativea  bprogramminga  blanguagea  bbecausea  bita  busesa  bstepa  bbya  bstepa  bprocessesa  btoa  bachievea  bitsa  bgoals.a  bthea  blanguagea  busesa  bthea  bconcepta  bofa  bobject-orienteda  bprogramminga  btoa  bdesigna  banda  bimplementa  bcomplexa  bprograms.

Thea  bnexta  bstepa  bisa  btoa  bstarta  bwritinga  bouta  bsomea  bofa  bthea  bdifferenta  bprogramsa  banda  bcodesa  bthata  byoua  bwanta  bwitha  bthea  bc++a  blanguage.

Evena  bifa  byoua  barea  bjusta  bstartinga  banda  byoua  bjusta  bwanta  btoa  bspenda  byoura  btimea  bpracticinga  bwitha  bsomea  bofa  bthea  bcodesa  bthata  barea  bina  bthisa  bguidebook,a  byoua  barea  bstilla  bona  bthea  brighta  bpatha  btoa  bseeinga  bsomea  bgreata  bresultsa  bwitha  bthisa  blanguage.

Thea  bmorea  bpracticea  byoua  bcana  bgeta  balonga  bthea  bwaya  bwitha  byoura  bowna  bcoding,a  bthea  beasiera  bita  bwilla  bbecomea  btoa  bwritea  banda  bcreatea  byoura  bowna  bcodesa  balonga  bthea  bway.

Thea  bc++a  blanguagea  bisa  baa  buniquea  boptiona  btoa  bworka  bwith,a  bonea  bthata  bwilla  bhelpa  busa  btoa  bcreatea  bsomea  breallya  bpowerfula  banda  bstronga  bcodes,a  banda  bthea  bfunctionalitya  bthata  bisa  bfounda  bwitha  bthisa  blanguagea  bisa  bunlikea  banya  bothera  bthata  bwea  barea  bablea  btoa  bworka  bwith.

Alla  bofa  bthesea  bcana  bbea  bimportanta  bina  bsomea  bofa  bthea  bcodesa  bthata  byoua  bwanta  btoa  bwritea  balonga  bthea  bway,a  banda  bwhena  bwea  barea  bdonea  bwitha  bthisa  bguidebook,a  byoua  bshoulda  bfeela  breadya  btoa  bhandlea  bthesea  banda  badda  bthema  btoa  byoura  bowna  bcodesa  basa  bwell.

Asa  bwea  bcana  bsee,a  btherea  bisa  bsoa  bmucha  bthata  bwea  barea  bablea  btoa  bdoa  bwhena  bita  bcomesa  btoa  bworkinga  bwitha  bthea  bc++a  blanguage.

Ita  bisa  bonea  bofa  bthea  bbesta  bcodinga  blanguagesa  bouta  bthere,a  bwhethera  byoua  barea  baa  bbeginner,a  bora  byoua  barea  bsomeonea  bwhoa  bhasa  bworkeda  bwitha  bprogramminga  banda  bcodinga  bfora  baa  blonga  btime.

Whena  byoua  barea  breadya  btoa  bstarta  byoura  bowna  bcodinga  bjourney,a  banda  byoua  bwanta  btoa  bbea  bablea  btoa  bcreatea  bsomea  bofa  byoura  bowna  bprogramsa  bina  bnoa  btime.

C++a  bprogramminga  blanguagea  butilizesa  bthea  bfeaturesa  bofa  boopa  bparadigmsa  btoa  bdevelopa  banda  bexecutea  baa  bprogram.a  bsomea  bofa  bthesea  bfeaturesa  bincludea  bthea  busea  bofa  bobjects,a  bclasses,a  bdataa  babstractionsa  banda  bencapsulation,a  binheritance,a  banda  bpolymorphism.

Thea  bprograma  bfocusesa  bona  bthea  busea  bofa  bdataa  brathera  bthana  bproceduresa  btoa  bsolvea  breal-worlda  bproblems.a  bthea  bprograma  btriesa  btoa  beliminatea  bthea  bshortcomingsa  bofa  bothera  bconventionala  bprogramminga  blanguagesa  bbya  bimprovinga  bthea  bdataa  bsecuritya  bofa  bprograms,a  bpromotinga  bcodea  breusability,a  banda  bitsa  babilitya  btoa  busea  binheritancea  bfeaturea  btoa  bmakea  bana  beffectivea  bprogram.

Justa  blikea  bmanya  bothera  boopa  blanguages,a  bc++a  bsupportsa  bvariousa  bbuildinga  bblocks.a  bina  bthisa  btutorial,a  byoua  bhavea  blearneda  bhowa  btoa  busea  bvariousa  bbuilt-ina  bdataa  btypesa  bwhena  bhandlinga  bsimplea  btoa  bcomplexa  bprograms.a  bthea  bdataa  btypesa  barea  bdivideda  bintoa  bprimitivea  bdataa  btypes,a  bderiveda  bdataa  btypes,a  banda  babstracta  bdataa  btypes.a  byoua  bnota  bonlya  blearneda  bhowa  btoa  busea  bthea  bprimitivea  bora  bstandarda  bdataa  btypesa  bbuta  balsoa  bhowa  btoa  bdeclarea  byoura  bowna  buser-defineda  bdatatypes.

Enjoya  byoura  bjourney.a  bifa  byoua  bdon’ta  bhavea  bfuna  bwhilea  byoua  bprogram,a  bita  bisn’ta  bfora  byou.a  bmakea  bita  bfun,a  bmakea  bita  bexciting,a  banda  bmakea  bita  bthea  breasona  byoua  bwanta  btoa  bgeta  bupa  bina  bthea  bmornings.

Gooda  blucka  bwitha  byoura  bjourney.