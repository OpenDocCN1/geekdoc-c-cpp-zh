C# for Beginners

A Comprehensive Guide to Crafting Real Projects and Applications

Vera Poe

Copyright © [2024] by [vera poe] all rights reserved.

No portion of this book may be reproduced in any form without written permission from the publisher or author, except as permitted by u.s. Copyright law.

This publication is designed to provide accurate and authoritative information in regard to the subject matter covered. It is sold with the understanding that neither the author nor the publisher is engaged in rendering legal, investment, accounting or other professional services. While the publisher and author have used their best efforts in preparing this book, they make no representations or warranties with respect to the accuracy or completeness of the contents of this book and specifically disclaim any implied warranties of merchantability or fitness for a particular purpose. No warranty may be created or extended by sales representatives or written sales materials. The advice and strategies contained herein may not be suitable for your situation. You should consult with a professional when appropriate. Neither the publisher nor the author shall be liable for any loss of profit or any other commercial damages, including but not limited to special, incidental, consequential, personal, or other damages.

Table of contents

[introduction](#index_split_003.html_id_Toc158305567)

[chapter 1: anatomy of c#](#index_split_004.html_id_Toc158305568)

[chapter 2: data type](#index_split_007.html_id_Toc158305569)

[chapter 3: operators variable](#index_split_008.html_id_Toc158305570)

[chapter 4: string and list](#index_split_009.html_id_Toc158305571)

[chapter 5: syntax](#index_split_010.html_id_Toc158305572)

[chapter 6: classes](#index_split_011.html_id_Toc158305573)

[chapter 7: linq, queries, operators – xaml](#index_split_012.html_id_Toc158305574)

[chapter 8: program to make decision](#index_split_013.html_id_Toc158305575)

[chapter 9: net](#index_split_014.html_id_Toc158305576)

[chapter 10: enum and struct](#index_split_015.html_id_Toc158305577)

[conclusion](#index_split_018.html_id_Toc158305578)

## Introduction

Welcomea  btoa  bc#a  bprogramminga  banda  bthanka  byoua  bsoa  bmucha  bfora  bpickinga  bupa  bthisa  bbook!

Whethera  byoua  barea  baa  bseasoneda  bprogrammera  bora  baa  bcompletea  bnovice,a  bthisa  bbooka  bisa  bwrittena  btoa  bhelpa  byoua  blearna  bc#a  bprogramminga  bfast.

Bya  bthea  benda  bofa  bthea  bbook,a  byoua  bshoulda  bhavea  bnoa  bproblema  bwritinga  byoura  bowna  bc#a  bprograms.a  bina  bfact,a  bwea  bwilla  bbea  bcodinga  baa  bsimplea  bpayrolla  bsoftwarea  btogethera  basa  bparta  bofa  bthea  bprojecta  bata  bthea  benda  bofa  bthea  bbook.a  breadya  btoa  bstart?

Mosta  bpeoplea  barea  bscareda  bofa  blearninga  baa  bnewa  bcodinga  blanguage.a  btheya  bknowa  bthata  bita  bwoulda  bopena  baa  blota  bofa  bdoorsa  bfora  bwhata  btheya  bwoulda  bbea  bablea  btoa  bdoa  bwitha  btheira  bcomputers,a  bbuta  btheya  bworrya  bthata  bcodinga  bitselfa  bisa  btooa  bharda  bfora  bthema  btoa  blearna  bhowa  btoa  bworka  bwith.a  bifa  byoua  bdoa  bnota  btakea  bthea  bpropera  btimea  btoa  blearna  baa  bnewa  bprogramminga  blanguage,a  bthea  bwholea  bprocessa  bofa  bprogramminga  bcoulda  bbea  bdifficult.a  bbuta  bwhena  bita  bcomesa  btoa  bfindinga  baa  bgooda  blanguagea  bthata  bwilla  bhelpa  byoua  bwritea  balmosta  banya  bcodea  bthata  byoua  bwoulda  blike,a  bthena  bita  bisa  btimea  btoa  btakea  baa  blooka  bata  bthea  bc#a  bprogramminga  blanguage.a  bthisa  bbooka  bwilla  btakea  byoua  bthrougha  bsomea  bofa  bthea  bbasicsa  bthata  bcomea  bwitha  businga  bthea  bc#a  bcodinga  blanguagea  bsoa  bthata  byoua  bcana  bstarta  businga  bita  byourself.

Whata  bisa  bspeciala  babouta  bc#?

Thea  bfirsta  bthinga  bthata  byoua  bmighta  bwanta  btoa  blooka  bintoa  bwhena  bita  bcomesa  btoa  baa  bcodinga  blanguagea  bisa  btoa  bunderstanda  bwhya  bc#a  bisa  bsoa  bspeciala  banda  bwhya  byoua  bwoulda  bevena  bwanta  btoa  blearna  bhowa  btoa  busea  bthisa  bparticulara  bprogramminga  blanguage.

Therea  barea  bmanya  bdifferenta  bcodinga  blanguagesa  bouta  btherea  btoa  bchoosea  bfrom,a  banda  btheya  balla  bworka  bdifferently,a  bbuta  byoua  bwilla  bfinda  bthata  btherea  barea  baa  btona  bofa  bbenefitsa  bthata  bcomea  bwitha  businga  bthea  bc#a  bprogram,a  banda  bwea  bwilla  bexplorea  bsomea  bofa  bthema  binsidea  bthisa  bguidebook.a  bevena  bthougha  byoua  barea  bjusta  baa  bbeginner,a  bthisa  bisa  baa  bgreata  bcodinga  blanguagea  btoa  bworka  bwitha  banda  bwilla  ballowa  byoua  btoa  bdesigna  bsoa  bmanya  bprogramsa  bofa  byoura  bown.

Whilea  btherea  barea  bmanya  bdifferenta  boptionsa  bavailablea  bifa  byoua  bwanta  btoa  bgeta  bstarteda  bwitha  bcoding,a  bnonea  barea  basa  bgreata  btoa  bworka  bwitha  blikea  bc#.a  bsomea  bofa  bthea  bbenefitsa  bofa  bgoinga  bwitha  bc#a  brathera  bthana  bsomea  bofa  bthea  bothera  bprogramminga  blanguagesa  binclude:

Ita  bcana  butilizea  baa  bbiga  blibrary

Asa  baa  bbeginner,a  btherea  barea  baa  blota  bofa  bpartsa  bofa  bthea  bcodea  bthata  bwon’ta  bbea  beasya  bfora  byoua  btoa  blearn.a  byoua  bwilla  blearna  bthema  basa  byoua  bgo,a  bbuta  bthea  blibrarya  bthata  byoua  bcana  busea  bwitha  bc#a  bisa  baa  bgreata  bresourcea  bthata  bwilla  bbea  bofa  bgreata  bhelpa  btoa  byou.a  byoua  bcana  bplacea  bthesea  bfunctionsa  bintoa  bthea  bcodea  bwithouta  baa  blota  bofa  bhasslea  bbeinga  binvolved.a  byoua  bcana  bevena  busea  bthema  btoa  bmakea  bsomea  bchangesa  btoa  bthea  bcode,a  bsoa  bita  bworksa  bthea  bwaya  bthata  byoua  bwant.

Automaticallya  bdisposesa  bofa  bthea  bfunctions

Whena  byoua  barea  bworkinga  bwitha  bsomea  bofa  bthea  bothera  bprogramminga  blanguages,a  byoua  bwilla  bhavea  btoa  bgoa  bthrougha  banda  bremovea  bthea  bitemsa  bthata  byoua  bown.a  bthisa  bwilla  btakea  bupa  byoura  btimea  banda  bcana  bbea  baa  bhasslea  bifa  byoua  benda  bupa  bmissinga  bsomea  bofa  bthem.a  businga  bc#a  bwilla  bdoa  balla  bofa  bthisa  bworka  bfora  byoua  btoa  bmakea  bthingsa  bfastera  banda  beasier.

Easya  btoa  blearn

C#a  bisa  bwidelya  bconsidereda  basa  bonea  bofa  bthea  beasiesta  bprogramminga  blanguagesa  byoua  bcana  blearna  bhowa  btoa  bworka  bwith.a  bwhilea  btherea  barea  baa  bfewa  bpartsa  bthata  barea  bmorea  bcomplicateda  bthana  bsomea  bothera  bcodinga  blanguages,a  bthisa  bisa  bnota  baa  bdifficulta  bone,a  banda  byou’lla  bstarta  brecognizinga  bdifferenta  bpartsa  bofa  bthea  bcodea  bprettya  bquicklya  basa  byoua  bcontinuea  btoa  busea  bit.

Compatiblea  bwitha  bwindowsa  bcomputersa  basa  bwella  basa  bothers

Thisa  bprogramminga  blanguagea  bwasa  boriginallya  bcreateda  btoa  bworka  bona  bwindowsa  bcomputersa  banda  bhelpa  byoua  bdesigna  baa  bprograma  bfora  bthem.a  bbuta  bita  balsoa  bworksa  bwella  bwitha  bsomea  bothera  boperatinga  bsystemsa  bsucha  basa  bmac,a  blinux,a  banda  bmorea  basa  blonga  basa  byoua  bdownloada  b.neta  bona  bit.a  bwindowsa  bhasa  bsomea  bgreata  bproductsa  bthata  barea  beasya  btoa  buse,a  bespeciallya  bfora  bbeginners,a  bsoa  byoua  bwilla  bsurelya  bgeta  bgreata  bresultsa  boncea  byoua  bgeta  bstarted.

Worksa  bwitha  b.neta  bwhicha  bhelpsa  bmakea  bita  beasy

Thisa  bisa  baa  bprograma  bthata  balreadya  bcomesa  bwitha  bthea  bwindowsa  bcomputers,a  bbuta  byoua  bcana  badda  bita  btoa  bsomea  bofa  bthea  bothera  bsystemsa  btoa  bmakea  bc#a  baccessiblea  bona  bthesea  bothera  bcomputersa  basa  bwell.

Similara  btoa  bca  banda  bc++

Thisa  bmakesa  bita  breallya  beasya  btoa  bworka  bwitha  bthisa  bprograma  banda  blearna  bthea  bbasicsa  bbeforea  bgoinga  bona  btoa  bthesea  bothera  bprograms.a  bevena  bifa  byoua  bchoosea  btoa  bsticka  bwitha  bthisa  bprogramminga  blanguage,a  byoua  bwilla  bfinda  bthata  bita  bisa  bpowerfula  benougha  btoa  bdoa  bmosta  bofa  bthea  bcodinga  bthata  byoua  bwanta  banda  bwithouta  balla  bthea  bhasslea  byoua  bmighta  bexperiencea  bwitha  bsomea  bofa  bthea  bothera  bprograms.

Readya  btoa  bdipa  byoura  btoesa  bintoa  bthea  bworlda  bofa  bc#a  bprogramming?a  blet’sa  bgeta  bstarted.

## Chaptera  b1:a  banatomya  bofa  bc#

Ana  bintroductiona  btoa  bc#

Learninga  bhowa  btoa  bcodea  bisa  bgoinga  btoa  bprovidea  byoua  bwitha  baa  btona  bofa  bbenefitsa  balonga  bthea  bway.a  bita  bisa  bgoinga  btoa  bmakea  bita  beasiera  btoa  bcreatea  bsomea  bofa  bthea  bprogramsa  banda  bapplicationsa  bthata  byoua  bwoulda  blike.a  bita  bisa  bgoinga  btoa  bbea  bablea  btoa  bhelpa  byoua  bfurthera  byoura  bcareera  bwitha  baa  blota  bofa  boptionsa  bthata  barea  bsimplea  btoa  bworka  bwitha  banda  bcana  ballowa  busa  btoa  bgeta  bthea  bbesta  bouta  bofa  bthesea  bnewa  bskillsa  banda  bmorea  bmoneya  basa  bwell.a  banda  bthena  btherea  barea  btimesa  bwhena  blearninga  bhowa  btoa  bworka  bwitha  bc#a  bisa  bgoinga  btoa  bbea  bvitala  bbecausea  bita  bwilla  ballowa  busa  btoa  blearna  bmorea  babouta  boura  bcomputersa  banda  bhowa  btheya  bwork.

Therea  barea  baa  blota  bofa  bgreata  boptionsa  bwhena  bita  bisa  btimea  btoa  bworka  bwitha  bprogramming.a  bmanya  blanguagesa  bhavea  bbeena  bdevelopeda  btoa  bworka  bona  bdifferenta  bprojects,a  banda  bsometimesa  btheya  bwilla  bworka  bona  bdifferenta  btypesa  bofa  bprocessesa  banda  bapplicationsa  basa  bwell.a  bwhilea  bmanya  bofa  bthesea  bcana  bbea  busefula  bbaseda  bona  bwhata  byoua  bwoulda  blikea  btoa  baccomplisha  bwitha  bthea  blanguagea  bina  bthea  bfirsta  bplace,a  bwea  barea  bgoinga  btoa  btakea  baa  blooka  bata  bhowa  btoa  bworka  bwitha  bthea  bc#a  blanguagea  banda  bhowa  bgreata  bthisa  bonea  bcana  bbea  bfora  boura  bneedsa  basa  bwell.a  blet’sa  bdivea  bintoa  bthea  bc#a  blanguagea  banda  bhowa  btoa  bmakea  bthisa  bworka  bfora  boura  bprogramminga  bneedsa  basa  bwell.

Thea  bfirsta  bthinga  bthata  bwea  bneeda  btoa  btakea  baa  blooka  bata  bherea  bisa  bthea  bc#a  blanguage.a  bc#a  bisa  bgoinga  btoa  bbea  bana  beleganta  banda  bobject-orienteda  blanguagea  bthata  bisa  bgoinga  btoa  bbea  bhelpfula  bbecausea  bita  ballowsa  bprogrammersa  btoa  bgoa  bthrougha  banda  bbuilta  bupa  baa  bvarietya  bofa  brobusta  banda  bsecurea  bapplications,a  balla  bofa  bwhicha  barea  bgoinga  btoa  bruna  bwitha  bthea  b.neta  bframework.a  bita  bisa  bpossiblea  btoa  bworka  bwitha  bc#a  bona  baa  bvarietya  bofa  bprojects,a  bincludinga  bwitha  bwindowsa  bclienta  bapplications,a  bweba  bservices,a  bclient-servera  bapplications,a  bxmla  bdatabasea  bapplications,a  banda  bsoa  bmucha  bmore.

Whena  bwea  barea  bworkinga  bwitha  bthea  bc#,a  bwea  bwilla  bfinda  bthata  bvisuallya  bita  bisa  bgoinga  btoa  bprovidea  busa  bwitha  bana  badvanceda  bcodea  beditora  balonga  bwitha  bsomea  busera  binterfacea  bdesignersa  bthata  barea  bmorea  bconvenienta  btoa  buse,a  baa  bdebuggera  bthata  bisa  bintegrated,a  banda  bsomea  bothera  btoolsa  bthata  bwilla  bensurea  bthata  bita  bisa  beasiera  btoa  bdevelopa  bsomea  bofa  boura  bapplicationsa  bbaseda  bona  bthisa  blanguage.

Thea  bneata  bthinga  babouta  bthea  bc#a  blanguagea  bisa  bthata  bita  bisa  bnota  bonlya  bgoinga  btoa  bbea  bhighlya  bexpressivea  banda  bablea  btoa  bhelpa  busa  bouta  bwitha  baa  blota  bofa  bthea  bmorea  bcomplicateda  bcodesa  bthata  bwea  bwanta  btoa  bhandle,a  bbuta  bita  bisa  balsoa  bgoinga  btoa  bbea  beasya  btoa  blearna  banda  bsimple.a  bthea  bcurlya  bbracesa  bthata  barea  bparta  bofa  bthea  bsyntaxa  bofa  bc#a  barea  bsomethinga  bthata  bisa  bgoinga  btoa  blooka  bfamiliar,a  bprimarilya  bifa  byoua  bhavea  bworkeda  bwitha  bjava,a  bc++,a  banda  bca  bina  bthea  bpast.a  bdevelopersa  bwhoa  barea  bgooda  bwitha  bthesea  blanguagesa  bwilla  bfinda  bthata  bita  bdoesa  bnota  btakea  bthata  blonga  btoa  blearna  bc#a  bbecausea  bofa  bthea  bsimilarities.

C#a  bisa  busefula  bbecausea  bita  bisa  bgoinga  btoa  bbea  bablea  btoa  bsimplifya  bsomea  bofa  bthea  bissuesa  bthata  bhappena  bwitha  bthea  bc++a  blanguage,a  banda  bita  bisa  bgoinga  btoa  bprovidea  busa  bwitha  bsomea  bpowerfula  bfeatures,a  bincludinga  bvaluea  btypesa  bthata  bcana  bbea  bnull,a  bdelegates,a  benumerations,a  blambdaa  bexpressions,a  banda  bdirecta  bmemorya  baccess.a  bnonea  bofa  bthesea  barea  bgoinga  btoa  bbea  bfeatureda  bavailablea  bwitha  blanguagesa  blikea  bjava.

Ina  badditiona  btoa  bthis,a  byoua  bwilla  bfinda  bthata  bthea  bc#a  blanguagea  bisa  bgoinga  btoa  bbea  bablea  btoa  bsupporta  bsomea  bofa  bthea  bgenerica  bmethodsa  banda  btypes,a  bwhicha  bisa  bgoinga  btoa  bhelpa  busa  bprovidea  bincreaseda  btypea  bsafetya  banda  bperformance.a  bita  bcomesa  bwitha  bsomea  biterators,a  bwhicha  benablea  bthea  bimplementersa  bofa  bcollectiona  bclassesa  btoa  bhelpa  bdefinea  bcustoma  biterationa  bbehaviorsa  bthata  bwilla  bbea  beasya  btoa  busea  bbya  bthea  bclienta  bcode.

Becausea  bthisa  blanguagea  bisa  bgoinga  btoa  bfita  bintoa  bthea  bcategorya  bofa  bobject-a  boriented,a  bita  bisa  bgoinga  btoa  bbea  bablea  btoa  bsupporta  baa  blota  bofa  btopicsa  banda  boptionsa  bthata  bfita  bintoa  bthisa  bcategory,a  banda  bthata  bwea  bwilla  bbea  bablea  btoa  bexplorea  bina  bmorea  bdetaila  blatera  bon,a  bincludinga  bpolymorphisma  binheritances,a  banda  bencapsulation.a  balla  bmethodsa  banda  bvariablesa  bthata  bwea  busea  barea  bgoinga  btoa  bbea  bencapsulateda  bwithina  bthesea  bdefinitionsa  bofa  bclasses.a  banda  baa  bclassa  bcana  binherita  bdirectlya  bfroma  bonea  bparenta  bclass,a  bbuta  bita  bcana  bbea  bseta  bupa  btoa  bimplementa  banya  bnumbera  bofa  binterfaces.

Methodsa  bina  bthisa  blanguagea  bwilla  bbea  bablea  btoa  boverridea  baccidentala  bredefinition.a  bwhena  bwea  bworka  bwitha  bc#,a  baa  bstructa  bisa  bgoinga  btoa  bbea  bsimilara  btoa  baa  blightweighta  bclass.a  bthisa  bmeansa  bthata  bita  bisa  bgoinga  btoa  bbea  baa  bstack-allocateda  btypea  bthata  bwilla  bbea  bablea  btoa  bcomea  bona  bboarda  banda  bimplementa  binterfaces,a  bbuta  bita  bisa  bnota  bgoinga  btoa  bbea  bablea  btoa  bhelpa  busa  bwhena  bsupportinga  binheritances.

Ina  badditiona  btoa  bsomea  bofa  bthea  bbasica  bprinciplesa  bthata  bwea  bjusta  btooka  baa  blooka  bat,a  byoua  bwilla  bfinda  bthata  bc#a  bisa  bgoinga  btoa  bmakea  bita  beasiera  btoa  bdevelopa  bsomea  bofa  bthea  bcomponentsa  bofa  bsoftwarea  bthrougha  baa  bfewa  bconstructs,a  banda  bthesea  barea  bgoinga  btoa  bincludea  bthea  bfollowing:

Ita  bcana  bgoa  bthrougha  banda  bencapsulatea  bsomea  bofa  boura  bmethoda  bsignaturesa  bthrougha  bthea  busea  bofa  bdelegates.a  bthesea  barea  bgoinga  btoa  benablea  bsomea  bofa  bthea  btype-safea  beventa  bnotificationsa  bthata  bwea  bneed.

Propertiesa  bthata  barea  bgoinga  btoa  bbea  btherea  btoa  bworka  basa  bthea  baccessorsa  bfora  bsomea  bprivatea  bmembera  bvariables.

Attributes,a  bwhicha  barea  bgoinga  btoa  bhelpa  bprovidea  bdeclarativea  bmetadataa  babouta  bsomea  bofa  bthea  bdifferenta  btypesa  bwhena  bthea  bprograma  bruns.

Linq,a  bwhicha  bisa  bgoinga  btoa  bstanda  bfora  baa  blanguagea  bintegrateda  bquery.a  bthisa  bisa  busefula  bbecausea  bita  bisa  bgoinga  btoa  bprovidea  busa  bwitha  bsomea  bbuilt-ina  bquerya  bcapabilitiesa  bnoa  bmattera  bwhicha  bsourcesa  bofa  bdataa  bthata  bwea  barea  bgoinga  btoa  bworka  bwith.

Therea  barea  baa  blota  bofa  bbenefitsa  bthata  bwea  bcana  bseea  bwhena  bita  bisa  btimea  btoa  bworka  bwitha  bthea  bc#a  blanguagea  banda  bmakea  bita  bworka  bfora  bsomea  bofa  boura  bneeds.a  bita  bisa  bana  bobject-orienteda  blanguagea  bthata  bmakesa  bita  beasiera  btoa  borganizea  banda  bkeepa  bthingsa  btogether,a  banda  bwhena  bwea  bcana  butilizea  bthea  brighta  bide,a  banda  bthea  b.neta  bplatforma  bthata  bwea  bwilla  btalka  babouta  bina  baa  bmoment,a  bwea  bwilla  bbea  bablea  btoa  butilizea  bita  btoa  bmakea  bthea  brobusta  bprogramsa  bthata  bwea  bwant,a  bwithouta  balla  bthea  bcomplexitiesa  bofa  bthea  bmissinga  bfeaturesa  bthata  bhappena  bwitha  bothera  bsimilara  blanguages.

Thea  bc#a  bide

Beforea  bwea  bcana  bgeta  bintoa  bdetailsa  babouta  bhowa  bwea  bcana  bcode,a  banda  bwhata  balla  bwea  bcana  bdoa  bwitha  bthea  bc#a  blanguage,a  bwea  bneeda  btoa  bgeta  baa  bbettera  bideaa  bofa  bwhata  bana  bidea  bisa  babout,a  banda  bwhya  bthisa  bisa  bsucha  bana  bimportanta  bparta  bofa  banya  bcodinga  bthata  bwea  bwanta  btoa  bdo.a  btoa  bstart,a  bana  bidea  bisa  bgoinga  btoa  bbea  bana  bintegrateda  bdevelopmenta  benvironment,a  bwhicha  bisa  bana  bapplicationa  bwea  bcana  busea  btoa  bhelpa  bwitha  bapplicationa  bdevelopment.a  bina  bgeneral,a  bthisa  bisa  bgoinga  btoa  bbea  baa  bguia  bora  bgraphicala  busera  binterfacea  bthata  bisa  bdesigneda  btoa  bmakea  bita  beasiera  bfora  banya  bdevelopera  btoa  bbuilda  bsoftwarea  bapplications.a  bmanya  btimes,a  bthesea  barea  bgoinga  btoa  bhavea  bmorea  bofa  bthea  btoolsa  bthata  byoua  bneed.

Mosta  bofa  bthea  bcommona  bfeatures,a  bsucha  basa  bdataa  bstructurea  bbrowsing,a  bversiona  bcontrol,a  banda  bevena  bdebugging,a  barea  bgoinga  btoa  bbea  btherea  btoa  bhelpa  bthea  bdevelopera  bexecutea  bactionsa  bwithouta  bneedinga  btoa  bswitcha  bbacka  banda  bfortha  bbetweena  bthea  bdifferenta  bapplicationsa  bthata  btheya  barea  bworkinga  bwith.a  bthisa  bmakesa  bita  beasiera  btoa  bmaximizea  bthea  bproductivitya  bbecausea  bwea  bcana  bprovidea  bsimilara  busera  binterfacesa  bfora  bthea  bcomponentsa  bthata  barea  brelated,a  banda  bita  bisa  bgoinga  btoa  breducea  bthea  bamounta  bofa  btimea  bthata  bita  btakesa  btoa  blearna  baa  bnewa  blanguage.a  balso,a  bdependinga  bona  bthea  bkinda  bofa  bidea  bthata  byoua  bchoosea  btoa  bgoa  bwith,a  bita  bcana  bsometimesa  bjusta  bsupporta  bonea  blanguage,a  banda  bothera  btimesa  bita  bwilla  bsupporta  bmanya  blanguages.

Thea  bconcepta  bthata  bisa  bbehinda  bthea  bidea  bisa  bsomethinga  bthata  bevolveda  bfroma  bsomea  bsimplea  bcommand-baseda  bsoftware,a  bwhicha  bata  bthea  btimea  bwasa  bnota  basa  busefula  basa  bthea  bmenu-drivena  bsoftware.a  bsomea  bofa  bthea  bmoderna  bide’sa  barea  bgoinga  btoa  bbea  buseda  bmorea  bina  bthea  bcontexta  bofa  boura  bvisuala  bprogramming,a  bwhilea  bthea  bapplicationsa  bina  bthesea  barea  bgoinga  btoa  bbea  bcreateda  bquicklya  banda  befficientlya  bbya  bmovinga  bthea  bcodea  bnodesa  bora  bthea  bbuildinga  bblocksa  bofa  bprogramminga  bthata  bwilla  bgeneratea  bthea  bflowcharta  banda  bstructureda  bdiagrams.a  bthesea  bcana  bthena  bbea  beithera  bcompileda  bora  binterpreteda  bbaseda  bona  bwhata  byoua  bhopea  btoa  bgeta  bouta  bofa  bthea  bprocess.

Ita  bisa  bimportanta  bthata  bwea  btakea  bthea  btimea  btoa  bpicka  bouta  baa  bgooda  bide,a  banda  btherea  barea  bseverala  bfactorsa  bthata  bwea  bneeda  btoa  bconsidera  basa  bwea  bworka  bthrougha  bthis.a  bfora  bexample,a  bwea  bneeda  btoa  bspenda  btimea  blookinga  bata  bthea  blanguagea  bsupport,a  boperatinga  bsystema  bneeds,a  banda  bsomea  bofa  bthea  bcosts.a  bsometimesa  bthea  bidea  bthata  bwea  bwanta  btoa  bworka  bwitha  bwilla  bbea  bfree,a  bbuta  bsometimesa  bthesea  barea  bgoinga  btoa  bhavea  blimiteda  bfeatures.a  bita  boftena  bdependsa  bona  bwhata  byoua  bwoulda  blikea  btoa  bdesigna  bwitha  bthata  blanguage,a  banda  bwhata  bfeaturesa  barea  bimportanta  btoa  byoura  bcodinga  bneeds.

Therea  barea  bseverala  bgooda  bide’sa  bouta  btherea  bthata  barea  bavailablea  bwitha  bthea  bc#a  blanguage.a  bita  bisa  bimportanta  btoa  bdoa  bsomea  bresearcha  banda  blearna  bmorea  babouta  bhowa  bthesea  bwork,a  banda  bwhicha  bonesa  barea  bgoinga  btoa  bhavea  bthea  bfeaturesa  bthata  byoua  bwoulda  blikea  btoa  bgeta  bthea  bbesta  bresults.a  bwhena  byoua  bcana  bdoa  bthis,a  bita  bisa  binfinitelya  beasiera  btoa  bgeta  bthea  bcodesa  bwrittena  bthata  byoua  bwoulda  blike.

Howa  btoa  bworka  bwitha  bc#a  bona  blinuxa  banda  bmaca  bcomputers

Whilea  bc#a  bisa  bconsidereda  baa  bwindowsa  blanguage,a  bwea  bcana  bgoa  bthrougha  banda  bworka  bwitha  bita  bona  baa  blinuxa  banda  bmaca  bcomputera  basa  bwell.a  bwea  bmaya  bneeda  btoa  bgoa  bthrougha  baa  bfewa  bextraa  bsteps,a  banda  bsometimesa  baa  bfewa  bofa  bthea  bfunctionalitiesa  bthata  bwea  barea  buseda  btoa  bseeinga  bwitha  bwindowsa  bwilla  bbea  bgone,a  bbuta  btherea  barea  bstilla  baa  blota  bofa  bbenefitsa  bthata  bwea  bwilla  bseea  bwitha  businga  bthisa  boptiona  bona  bothera  boperatinga  bsystems.

Fora  bthea  blinuxa  bsystem,a  bthea  bmonodevelopa  bide,a  bwhicha  bisa  bparta  bofa  bthea  bmonoa  bproject,a  bshoulda  bbea  bjusta  bwhata  byoua  bneeda  btoa  bdevelopa  bsomea  bc#a  bcodinga  bona  baa  blinuxa  bcomputer.a  bthea  beasiesta  bwaya  bfora  byoua  btoa  binstalla  bthisa  bisa  btoa  bworka  bwitha  bthea  bmonodevelopa  bpackagea  bthata  bwasa  bdevelopeda  btoa  bworka  bwitha  bubuntu.a  bsometimesa  bita  bisa  brecommendeda  btoa  bworka  bwitha  bthea  bwinformsa  btoolkit,a  bbuta  bthisa  bonea  bisa  bnota  bgoinga  btoa  bbea  basa  befficienta  banda  beasya  btoa  bworka  bwith.

Wea  bcana  balsoa  bseta  bthisa  blanguagea  bupa  btoa  bworka  bona  baa  bmaca  bcomputer.a  bthea  bfirsta  bstepa  bisa  btoa  bdownloada  bana  bide,a  banda  bvisuala  bstudioa  bcodea  bisa  busuallya  bthea  bbesta  bonea  bherea  bbecausea  bita  bdoesa  bworka  bwella  bwitha  bmaca  banda  bstilla  bprovidesa  byoua  bwitha  bthea  bfunctionalitya  bthata  byoua  bneeda  bwhilea  bthea  bsimplicitya  bofa  busea  bisa  bstilla  bthere.a  bjusta  bvisita  bthea  bvisuala  bstudioa  bwebsite,a  banda  bthena  bmakea  bsurea  btoa  bclicka  bona  bthea  bbuttona  btoa  bdownloada  btoa  bmac.a  bthisa  bshoulda  bdownloada  bwhata  byoua  bneeda  bina  baa  bzipa  bfile.

Oncea  byoua  bhavea  bbeena  bablea  btoa  bgeta  bthisa  bsetup,a  byoua  bcana  bunzipa  bthea  bfilea  banda  bthena  bdraga  bita  bovera  btoa  bthea  bapplicationsa  bfolder.a  byoua  bshoulda  bbea  bablea  btoa  bdownloada  bita  bfroma  bthere.a  bthea  bnexta  bstepa  bisa  btoa  bgoa  bthrougha  banda  bdownloada  bthea  bc#a  bextension.a  byoua  bcana  bgoa  bintoa  bvisuala  bstudioa  bcodea  banda  bopena  bupa  bthea  bextensionsa  bthata  byoua  bneeda  btoa  bmakea  bthisa  bwork.

Now,a  basa  byoua  barea  bgoinga  bthrougha  bthisa  bprocess,a  byoua  barea  bgoinga  btoa  bnoticea  bthata  btherea  bisa  baa  bsearcha  bbara  bata  bthea  btopa  bofa  bthea  bextensionsa  bview.a  bthisa  bisa  bwherea  byoua  barea  bgoinga  btoa  btypea  bina  b“c#”.a  bthea  bonea  bthata  byoua  bneeda  bisa  bgoinga  btoa  bbea  bbya  bmicrosoft,a  bsoa  bmakea  bsurea  btoa  bclicka  bona  bthisa  bone.a  bclicka  btoa  binstall,a  banda  byoua  barea  breadya  btoa  bgo.

Remembera  bthougha  bthisa  bprocessa  bthata  bthea  bc#a  blanguagea  bisa  bonea  bthata  bhasa  bbeena  bdevelopeda  btoa  bworka  bthea  bbesta  bwitha  baa  bwindowsa  bsystem.a  bso,a  bifa  byoua  barea  bona  baa  bwindowsa  bsystem,a  byoua  barea  bmorea  blikelya  btoa  bfinda  bthisa  blanguagea  beasya  btoa  buse,a  banda  balla  bofa  bthea  bfeaturesa  banda  bfunctionalitiesa  bthata  byoua  barea  blookinga  bfora  bina  bcodinga  barea  bmorea  blikelya  btoa  bbea  bwherea  byoua  bputa  bthem.

Thisa  bdoesa  bnota  bmeana  bthata  byoua  barea  bnota  bablea  btoa  bgeta  bthisa  btoa  bworka  bona  byoura  bmaca  bcomputera  bata  ball.a  bita  bmerelya  bmeansa  bthata  byoua  bneeda  btoa  btakea  baa  bfewa  bextraa  bstepsa  btoa  bgeta  bthisa  bsetup,a  banda  bita  bmaya  bnota  bbea  basa  beasya  btoa  baccomplisha  bsomea  bofa  bthea  bthingsa  bthata  byoua  bwoulda  blike.a  btakinga  bsomea  btimea  btoa  bgeta  bfamiliara  bwitha  bthea  bc#a  blanguagea  bona  baa  blinuxa  bora  bmaca  bcomputera  bwilla  bbea  bimportanta  btoa  bhelpinga  byoua  bgeta  bthea  bbesta  bresultsa  bina  bthea  bprocess.

Howa  btoa  bgeta  baa  bc#a  bcompiler

Therea  barea  bseverala  bcompilera  boptionsa  bfora  bc#a  btoa  bmakea  bthea  blearninga  beasya  banda  bsmootha  bfora  bthea  bbeginners;a  bina  bthisa  bbook,a  bwea  bwilla  busea  bthea  bc#a  b4.0a  bversiona  bthata  bcomesa  bwitha  bvisuala  bstudioa  b2010.a  bstill,a  bita  bisa  balsoa  bpossiblea  btoa  busea  baa  blatera  bora  boldera  bversion.a  bmosta  bofa  bthea  bexamplesa  bshoulda  bbea  bablea  btoa  bbea  bcompileda  banda  bruna  bwithouta  banya  bproblem.

Ina  bcasea  bwea  bcannota  bgeta  bthea  bprofessionala  bversiona  bofa  bvisuala  bstudioa  b2019,a  baa  bbettera  boptiona  bisa  bthea  bcommunitya  bversiona  bformerlya  bknowna  basa  bthea  bexpressa  bversion.a  bthisa  bversiona  bisa  bfreea  banda  bcana  bbea  bdownloadeda  bdirectlya  bfroma  bthea  binternet;a  balla  byoua  bneeda  btoa  bdoa  bisa  bgoa  bthrougha  baa  bsmalla  bsurvey.a  btoa  bdownloada  bthea  bca  b#a  bvisuala  bstudioa  bcompilera  b(communitya  bversion)a  bcompletelya  bfree,a  byoua  bcana  baccessa  bthea  bmicrosofta  bportala  b[here](https://visualstudio.microsoft.com/vs/express)a  b.

Oncea  bwea  bhavea  bdownloadeda  bthea  bcompiler,a  bwea  bcana  bproceeda  btoa  bcarrya  bouta  bthea  binstallation;a  bthisa  btaska  bisa  bverya  bsimilara  btoa  binstallinga  banya  bothera  bwindowsa  bprogram,a  bbuta  bdoa  bnota  bforgeta  btoa  bregistera  bita  bwithina  b30a  bdays.

Thea  bdevelopmenta  benvironment

Oncea  bthea  binstallationa  bisa  bfinished,a  bwea  bcana  bstarta  bthea  bprograma  bbya  bselectinga  bita  bfroma  bthea  bwindowsa  bstarta  bmenu.a  byoua  bwilla  bseea  baa  bwindowa  bthata  bshowsa  bthea  busera  binterfacea  bofa  bthea  bapplication.

Thea  binterfacea  bisa  bdivideda  bintoa  btwoa  bparts:a  bona  bthea  bleft,a  bwea  bhavea  bthea  bsearcha  bbara  bnameda  bopena  brecent,a  bwherea  bwea  bcana  bfinda  blinksa  btoa  boura  bmosta  brecenta  bprojectsa  bora  bsolutionsa  bbya  benteringa  bkeywords.a  banda  bona  bthea  brighta  bsidea  bofa  bthea  bhomea  bpage,a  bwea  bwilla  bseea  bthea  boptionsa  bofa  bcreatea  baa  bnewa  bproject,a  bopena  baa  blocala  bfolder,a  bopena  baa  bprojecta  bora  bsolution,a  banda  baccessa  btoa  bcodea  brepositoriesa  btitleda  bclonea  bora  bchecka  bouta  bcode.a  bwea  bcana  balsoa  breceivea  bannouncementsa  banda  bnewsa  babouta  bsoftwarea  bdevelopmenta  businga  bca  b#a  bina  bthisa  bsamea  bparta  bofa  bthea  binterface,a  bbuta  basa  bwea  bmovea  bthrougha  bdifferenta  bpages,a  bwea  bwilla  bhavea  bthea  beditinga  bzones.a  bthesea  beditinga  bareasa  bwilla  ballowa  busa  btoa  bedita  bthea  bprograma  bcode,a  bedita  bthea  busera  binterface,a  bicons,a  banda  bothera  bresources.

Editinga  bthea  bprograma  bcodea  bisa  baa  bverya  bsimplea  bactivitya  bthata  bshoulda  bnota  bmakea  busa  bworrya  bifa  bwea  bknowa  bhowa  btoa  busea  banya  btypea  bofa  btexta  beditorsa  bsucha  basa  bmicrosofta  bworda  bora  bwindowsa  bnotepad,a  banda  bthena  bwea  bcana  bedita  bthea  bprograma  bcode.a  bthea  bothera  beditorsa  barea  balsoa  bquitea  buser-friendly,a  bbuta  bwea  bwilla  bnota  bneeda  bthema  btoa  bperforma  bthea  bexamplesa  bshowna  bina  bthisa  bbook.

Ona  bthea  brighta  bside,a  bwea  bhavea  baa  bwindowa  bthata  bisa  bknowna  basa  bsolutiona  bexplorer,a  bina  bthisa  bsamea  bareaa  bothera  bwindowsa  bwilla  bappeara  bthata  bgivea  busa  binformationa  babouta  bthea  bprojecta  bwea  barea  bdeveloping.a  bwea  bwilla  bseea  bthea  bdetailsa  bshowna  bbya  bsomea  bofa  bthesea  bwindowsa  baa  blittlea  blatera  bina  bthisa  bbook.

![Image00094.jpg](images/Image00094.jpeg)a  b

Ata  bthea  bbottom,a  bwea  bfinda  banothera  bwindow;a  bina  bthisa  barea,a  btherea  barea  busuallya  bthea  bsectionsa  bthata  bthea  bcompilera  bwilla  busea  btoa  bcommunicatea  bwitha  bus.a  bfora  bexample,a  bwea  bwilla  bseea  bthea  bwindowa  bthata  bindicatesa  bthea  berrorsa  bthata  boura  bprograma  bhas;a  bata  bthea  btopa  bofa  bthea  bwindow,a  bwea  bwilla  bseea  bthea  bmenusa  banda  bthea  btoolbars.

If,a  bfora  banya  breason,a  bwea  bclosea  bthea  bsourcea  bcodea  beditora  bora  bita  bdoesa  bnota  bappeara  bina  boura  busera  binterface,a  bthea  beasiesta  bwaya  btoa  bfinda  bita  bisa  bthrougha  bthea  bsolutiona  bexplorer.a  bsimplya  bgoa  btoa  bthea  bdocumenta  bthata  brepresentsa  byoura  bsourcea  bcodea  banda  bdoublea  bclicka  bona  bit,a  bthea  bwindowa  bwitha  bthea  bsourcea  bcodea  beditora  bwilla  bappear.

Howa  btoa  bcreatea  boura  bfirsta  bapplication

Toa  bbecomea  bmorea  bfamiliara  bwitha  bc#a  bvisuala  bstudioa  bexpress,a  bita  bisa  bbesta  btoa  bcreatea  bthea  bfirsta  bprojecta  banda  bworka  bona  bit.a  bwea  bwilla  bgeneratea  baa  bsmalla  bprograma  bthata  bsendsa  busa  baa  bmessagea  bina  bthea  bconsole,a  banda  bthena  bwea  bwilla  badda  bothera  belementsa  bsoa  bthata  bwea  bcana  bexplorea  bthea  bdifferenta  bwindowsa  bofa  bthea  busera  binterface.

Therea  barea  bmainlya  btwoa  bwaysa  btoa  bcreatea  baa  bnewa  bprojecta  bina  bvisuala  bstudioa  b2019.a  bthea  bfirsta  bonea  bisa  bmerelya  bclickinga  bona  bcreatea  baa  bnewa  bprojecta  bfroma  bthea  bbottoma  brighta  bparta  bofa  bthea  bmaina  bvisuala  bstudioa  binterface.

Thena  btypea  bconsolea  bina  bthea  bsearcha  bboxa  banda  bchoosea  bthea  bconsolea  bappa  b(.neta  bframework)a  boptiona  banda  bclicka  bthea  bnexta  bbuttona  basa  bshowna  bbelow.

![Image00095.jpg](images/Image00095.jpeg)a  b

Thena  bconfigurea  byoura  bnewa  bprojecta  bwitha  bitsa  bnamea  banda  blocation,a  bsavea  banda  bhita  bthea  bcreatea  bbutton.

Alla  bset,a  bthea  bvisuala  bstudioa  bwilla  binstantlya  bcreatea  baa  bnewa  bprojecta  bfora  byou.

Alternatively,a  btoa  bcreatea  baa  bproject,a  bwea  bcana  bselecta  bthea  bfilea  bmenu,a  banda  baftera  bthat,a  bwea  bhavea  btoa  bclicka  bona  bthea  boptiona  bnewa  bprojecta  basa  bshowna  bina  bthea  bimagea  bbelow,a  bthisa  bwaya  bwea  bwilla  bseea  baa  bdialoga  bboxa  bthata  bshowsa  bsomea  brelateda  boptions.

![Image00096.jpg](images/Image00096.jpeg)a  b

Ina  bthea  brighta  bparta  bofa  bthea  bdialoga  bbox,a  bthea  bdifferenta  btypesa  bofa  bprojectsa  bthata  bwea  bcana  bcreatea  barea  blisted;a  bfora  bthisa  bexample,a  bwea  bmusta  bselecta  bthea  bonea  bindicateda  bbya  bthea  bconsolea  bapplicationa  banda  bclicka  bthea  bnexta  bbutton.

Note:a  bif,a  bfora  banya  breason,a  bwea  bclosea  bthea  bsourcea  bcodea  beditora  bora  bita  bdoesa  bnota  bappeara  bina  boura  busera  binterface,a  bthea  beasiesta  bwaya  btoa  bfinda  bita  bisa  bthrougha  bthea  bsolutiona  bexplorer.a  bsimplya  bgoa  btoa  bthea  bdocumenta  bthata  brepresentsa  byoura  bsourcea  bcodea  banda  bdoublea  bclicka  bona  bit,a  bthea  bwindowa  bwitha  bthea  bsourcea  bcodea  beditora  bwilla  bappear.

![Image00097.jpg](images/Image00097.jpeg)a  b

Ona  bthea  blefta  bside,a  bwea  bwilla  bwritea  bthea  bnamea  bofa  boura  bproject,a  bwhicha  bina  bthisa  bcase,a  bwilla  bbea  bmyproject.a  beacha  bnewa  bprojecta  bwea  bwilla  bcreatea  bwilla  bhavea  bitsa  bname;a  bthen,a  bwea  bwilla  bsimplya  bpressa  bthea  bcreatea  bbutton.

![Image00098.jpg](images/Image00098.jpeg)a  b

Ina  baa  bfewa  bseconds,a  bca  b#a  bexpressa  bcreatesa  bthea  bprojecta  bfora  bus.a  bvisuala  bstudioa  banda  bthea  bcommunitya  bversiona  bmakea  busea  bofa  bsolutionsa  banda  bprojects,a  baa  bsolutiona  bcana  bhavea  bseverala  bprojects,a  banda  bfora  bexample,a  bofficea  bhasa  bdifferenta  bproductsa  bsucha  basa  bword,a  bexcel,a  banda  bpowerpoint.a  bthea  bofficea  bisa  baa  bsolution,a  banda  beacha  bproducta  bisa  baa  bproject.a  bthea  bprojecta  bcana  bbea  baa  bstand-alonea  bprograma  bora  baa  blibrarya  banda  bcana  bhavea  bonea  bora  bmorea  bdocuments,a  banda  bthesea  bdocumentsa  bcana  bbea  bthea  bsourcea  bcodea  banda  badditionala  bresources.

![Image00099.jpg](images/Image00099.jpeg)a  b

Wea  bcana  bseea  bthata  boura  busera  binterfacea  bhasa  bchangeda  baa  bbit,a  bthea  bwindowsa  balreadya  bshowa  busa  binformation,a  banda  bwea  bcana  balsoa  bseea  bthata  bthea  bskeletona  bfora  boura  bprograma  bisa  bshowna  bina  bthea  beditinga  barea.

![Image00100.jpg](images/Image00100.jpeg)a  b

Thea  bsolutiona  bexplorera  bshowsa  busa  bthea  binformationa  babouta  bthea  bsolutiona  bina  baa  blogicala  bwaya  bifa  bwea  bobserve,a  bita  bisa  blikea  baa  bsmalla  btree.a  bata  bthea  broot,a  bwea  bfinda  bthea  bsolution;a  beacha  bprojecta  bwea  bhavea  bina  bthata  bsolutiona  bwilla  bbea  baa  bbranch,a  beacha  bproject,a  bina  bturn,a  bwilla  balsoa  bhavea  bitsa  bdivisions.a  bina  boura  bcase,a  bwea  bseea  bthreea  belements;a  btwoa  bofa  bthosea  belementsa  barea  bfolders;a  bina  bone,a  bwea  bkeepa  bthea  bpropertiesa  bofa  bthea  bproject,a  banda  bina  bthea  bother,a  bthea  breferencesa  b(duringa  bthisa  bbook,a  bwea  bwilla  bnota  busea  bthesea  bfolders).a  bthea  bfourtha  belementa  bisa  baa  bdocumenta  bcalleda  bprogram.cs,a  bthisa  brepresentsa  bthea  bdocumenta  bwherea  bwea  bsavea  bthea  bsourcea  bcodea  bofa  boura  bapplication.a  bwea  bseea  bthata  bthea  bextensiona  bofa  bthea  bc#a  bprogramsa  bisa  b.cs.

Ina  bthea  beditinga  barea,a  bwea  bcana  bseea  bthata  bwea  bhavea  baa  bskeletona  bsoa  bthat,a  bfroma  bthere,a  bwea  bcana  bcreatea  boura  bprogram.a  btoa  bunderstanda  bwhata  bwea  bhave,a  btherea  bisa  bnecessarya  btoa  bknowa  baa  bconcept:a  bnamespace.a  bthea  bnamespacea  bisa  baa  blogicala  bgrouping;a  bfora  bexample,a  balla  bthea  bcodea  bthata  bwea  bcana  bhavea  brelateda  btoa  bmathematicsa  bcana  bbea  bgroupeda  binsidea  bthea  bnamespacea  bofa  bmath.a  banothera  busea  bthata  bnamespacea  bhasa  bisa  btoa  bsolvea  bconflictsa  bwitha  bnames,a  bfora  bexample,a  blet’sa  bsupposea  bthata  bwea  bhavea  baa  bmassivea  bprojecta  banda  bseverala  bprogrammersa  bworkinga  bona  bit.a  btwoa  bora  bmorea  bprogrammersa  bcoulda  bhavea  bcreateda  baa  bmethoda  bthata  bhada  bthea  bsamea  bname;a  bthisa  bgeneratesa  baa  bconflicta  bsincea  bthea  bprograma  bcoulda  bnota  bknowa  bwhicha  bversiona  btoa  buse.a  bthea  bwaya  btoa  bsolvea  bthisa  bisa  bthata  beacha  bprogrammera  bhasa  bitsa  bnamespacea  banda  brefersa  btoa  bthea  bcorrespondinga  bnamespacea  baccordinga  btoa  bthea  bversiona  bwea  bwanta  btoa  buse.

Thea  b.neta  bframeworka  bprovidesa  busa  bwitha  bvariousa  bnamespacesa  bwherea  bwea  bhavea  bthousandsa  bofa  bclassesa  banda  bmethodsa  balreadya  bcreateda  bfora  boura  buse.a  bwhena  bwea  bwanta  btoa  busea  bthea  bresourcesa  bfounda  bina  baa  bnamespacea  bprogrammeda  bbya  bothera  bprogrammersa  bora  bbya  bus,a  bwea  bmusta  bmakea  busea  bofa  baa  bca  b#a  bcommanda  bknowna  basa  busing.

Asa  bwea  bcana  bseea  bata  bthea  btopa  bofa  bthea  bcode,a  bwea  bhavea  bseverala  businga  breferencesa  btoa  bthea  bnamespacesa  bthata  boura  bapplicationa  bneeds;a  bifa  bwea  bneededa  btoa  badda  bmorea  bnamespaces,a  bwea  bwoulda  bdoa  bita  bina  bthisa  bsection.

Belowa  bisa  bdefininga  bthea  bpropera  bnamespacea  bofa  boura  bproject;a  bthisa  bisa  bdonea  basa  bfollows:

Namespacea  bmyproject

{

}

Thea  bnamespacea  bwea  barea  bcreatinga  bisa  bcalleda  bmyproject.a  basa  bwea  bcana  bsee,a  bthea  bnamespacea  busesa  b{}a  basa  bdelimiters;a  bthisa  bisa  bknowna  basa  baa  bcodea  bblock,a  banda  beverythinga  bthata  bisa  bplaceda  bbetweena  b{}a  bwilla  bbelonga  btoa  bthea  bnamespace.a  bthisa  bisa  bwherea  bita  bwilla  bbea  bnecessarya  btoa  bwritea  bthea  bcodea  bcorrespondinga  btoa  boura  bapplication.

Insidea  bthea  bcodea  bblock,a  bwea  bfinda  bthea  bdeclarationa  bofa  baa  bclass,a  bc#a  bisa  bana  bobject-orienteda  blanguage,a  banda  bthata  bisa  bwhya  bita  bneedsa  busa  btoa  bdeclarea  baa  bclassa  bfora  boura  bapplication.a  bthea  bclassa  bhasa  bitsa  bblocka  bofa  bcode,a  banda  bina  boura  bapplication,a  bita  bwilla  bbea  bcalleda  bprogram.a  bthea  bconcepta  bofa  bthea  bclassa  bwilla  bbea  bcovereda  bina  bchaptera  b10a  bofa  bthisa  bbook.

Alla  bprogramsa  bneeda  baa  bstartinga  bpoint,a  baa  bplacea  bthata  bindicatesa  bwherea  bthea  bprograma  bexecutiona  bstarts,a  bina  bc#,a  basa  bina  bothera  blanguages,a  bthea  bstartinga  bpointa  bisa  bthea  bmain()a  bfunction;a  bthisa  bfunctiona  balsoa  bhasa  bitsa  bcodea  bblock.a  bwithina  bthisa  bfunction,a  bwea  bwilla  bgenerallya  bplacea  bthea  bmaina  bcodea  bofa  boura  bapplication,a  balthougha  bita  bisa  bpossiblea  btoa  bhavea  bmorea  bfunctionsa  bora  bmethodsa  banda  bclasses.a  bthea  bpartsa  banda  bcharacteristicsa  bofa  bthea  bfunctionsa  barea  bseena  bina  bchaptera  b5a  bofa  bthisa  bbook.

Nowa  bita  bisa  btimea  btoa  bcreatea  boura  bfirsta  bapplication.a  bwea  barea  bgoinga  btoa  bmodifya  bthea  bfunctiona  bcode,a  basa  bshowna  bbelow.a  bwhena  bwea  barea  baddinga  bthea  bstatementa  binsidea  bmain(),a  bwea  bmusta  bnoticea  bthata  bita  bhappensa  bimmediatelya  baftera  bthea  bpointa  bisa  bplaced.

Toa  bcompilea  bthea  bapplication

Oncea  bwea  bfinisha  bwritinga  boura  bprogram,a  bwea  bcana  bcarrya  bouta  bthea  bcompilation,a  basa  bwea  blearneda  bearlier;a  bthisa  bwilla  bgeneratea  bthea  bassemblya  bthata  bwilla  bthena  bbea  buseda  bbya  bthea  bruntimea  bwhena  bexecuted.

Toa  bcompilea  bthea  bapplication,a  bwea  bmusta  bselecta  bthea  bbuilda  bmenua  banda  bthena  bbuilda  bsolutiona  bora  bsimplya  bpressinga  bbya  bthea  bf6a  bbutton.a  bthea  bcompilera  bwilla  bstarta  bworking,a  banda  bina  bthea  bstatusa  bbar,a  bwea  bwilla  bseea  bthata  boura  bsolutiona  bhasa  bbeena  bcompileda  bsuccessfully.

Toa  bruna  bthea  bapplication

Oncea  bthea  bcompilationa  bhasa  bbeena  bsuccessful,a  bwea  bcana  bruna  boura  bprograma  banda  bseea  bhowa  bita  bworks.a  bfora  bthis,a  bwea  bhavea  btwoa  boptions:a  bruna  bwitha  bdebugginga  banda  bexecutea  bwithouta  bdebugging.a  bina  bthea  bexpressa  bversion,a  bonlya  bthea  bexecutiona  bwitha  bdebugginga  bappears,a  bbuta  bwea  bcana  busea  bthea  bexecutiona  bwithouta  bdebugginga  bwitha  bthea  bkeysa  bctrl+f5a  bora  baddinga  bita  businga  bthea  btoolsa  bmenu.

Thea  bdebuggera  bisa  baa  bprograma  bthata  bhelpsa  busa  bcorrecta  berrorsa  bata  bruntimea  banda  balsoa  blogica  berrors.a  bpreferablya  bwea  bshoulda  busea  bthea  bexecutiona  bwithouta  bthea  bdebuggera  banda  bmakea  busea  bofa  bthea  bexecutiona  bwitha  bdebugginga  bonlya  bwhena  bwea  bneeda  bit.a  bnowa  bwea  bwilla  bruna  boura  bapplication;a  bfora  bthis,a  bwea  bpressa  bthea  bctrla  b+a  bf5a  bkeys.

Whena  bthea  bprograma  bisa  bexecuted,a  baa  bwindowa  bappears,a  bwea  bcalla  bita  bconsole,a  banda  bita  bshowsa  bthea  bexecutiona  bofa  bthea  bprogram.a  bina  bthisa  bway,a  bwea  bcana  breada  bthea  bmessagea  bthata  bwea  bhada  bplaceda  bina  boura  bexample.

Sincea  bthisa  bisa  baa  bstartera  bbooka  bfora  bprogramminga  bwitha  bc#,a  bsoa  bwea  bwilla  bruna  balla  bprogramsa  bona  bthea  bconsole.a  boncea  byoua  bunderstanda  bthea  bmaina  bconcepts,a  byoua  bcana  blearna  bhowa  btoa  bprograma  bshapes,a  bforms,a  banda  bgraphicala  binterfacesa  bina  bc#.a  bthisa  btypea  bofa  bprogramminga  bisa  bnota  bdifficult,a  bbuta  bita  brequiresa  bbasica  bknowledgea  bofa  bobject-orienteda  bprogramming.

Howa  btoa  bdetecta  berrorsa  bina  baa  bprogram

Sometimesa  bwea  bmaya  bmiswritea  bthea  bprogram;a  bwhena  bthisa  bhappens,a  bthea  bapplicationa  bcannota  bbea  bcompileda  bora  bexecuted;a  bifa  bthisa  bhappens,a  bwea  bmusta  bchangea  bwhata  bisa  bwrong.

Let’sa  bwritea  bana  berrora  bintentionallya  bsoa  bthata  bwea  bcana  bseea  bhowa  bthea  bcompilera  bbehaves.

Ina  bthea  bprogram,a  bwea  bhavea  bchangeda  b‘console’a  btoa  b‘consoli’a  banda  breordereda  b‘namespace’‘helloworld,’a  bthisa  bwilla  bcausea  bana  berror;a  bnow,a  bwea  bcana  btrya  btoa  bcompilea  bagaina  banda  bseea  bwhata  bhappens.

![Image00101.jpg](images/Image00101.jpeg)a  b

Asa  bwea  balreadya  bknow,a  bthea  bwindowa  bthata  bappearsa  bata  bthea  bbottoma  bofa  boura  busera  binterfacea  bisa  buseda  bbya  bthea  bcompilera  btoa  bcommunicate;a  bwea  bseea  bthata  baa  bwindowa  bappearsa  bthata  bgivesa  busa  baa  blista  bofa  berrors.a  bina  bthea  bnexta  bbook,a  bwea  bwilla  blearna  bhowa  btoa  busea  bit;a  bfora  bnow,a  bwea  bsimplya  bneeda  btoa  bknowa  bthata  bita  bisa  balwaysa  bnecessarya  btoa  bsolvea  bthea  bfirsta  bproblema  bina  bthea  blista  banda  bthata  bwea  bcana  bgoa  bdirectlya  btoa  bthea  berrora  bbya  bdouble-clickinga  bona  bit.

Thea  bclassa  bview

Nowa  bwea  barea  bgoinga  btoa  bchecka  bthea  bclassa  bview.a  bina  bthisa  bview,a  bwea  bcana  bgeta  binformationa  babouta  bthea  bsolutiona  bwea  barea  bcreating,a  bbuta  bunlikea  bsolutiona  bexplorer,a  bthea  binformationa  bisa  barrangeda  blogically.

Witha  bthisa  bview,a  bwea  bcana  bquicklya  bfinda  bthea  bnamespacesa  bofa  boura  bsolutiona  banda  bwithina  bthema  bthea  bclassesa  btheya  bcontain;a  bifa  bwea  bwish,a  bwea  bcana  bseea  bthea  bmethodsa  bthata  barea  bina  beacha  bclass.a  bthisa  bviewa  bnota  bonlya  ballowsa  busa  btoa  bobservea  bthea  blogicala  binformationa  bbuta  balsoa  bgivesa  busa  bthea  bpossibilitya  btoa  bquicklya  bnavigatea  bina  boura  bcode.

Ina  bthea  bcommunitya  bversion,a  btherea  bisa  bnoa  bpreviouslya  bconfigureda  boption,a  bsoa  bita  bisa  bnecessarya  btoa  badda  bthea  bcommanda  btoa  bthea  bviewa  bmenu.

Toa  bshowa  bthea  bclassa  bview,a  bwea  bmusta  bgoa  btoa  bthea  bviewa  bmenua  banda  bthena  bselecta  bclassa  bviewa  bora  bmerelya  bpressinga  bctrla  b+a  bw,a  bca  baa  bwindowa  bwilla  bappeara  bina  boura  busera  binterface.

![Image00102.jpg](images/Image00102.jpeg)a  b

Thea  bclassa  bviewa  bwindowa  bisa  bdivideda  bintoa  btwoa  bsections;a  bthea  buppera  bsectiona  bshowsa  bthea  blogicala  banda  bhierarchicala  brelationshipa  bofa  bthea  belementsa  bwhilea  bthea  blowera  bsectiona  bshowsa  bthea  bmethodsa  bthata  bmakea  bupa  baa  bparticulara  bclass.

![Image00103.jpg](images/Image00103.jpeg)a  b

Ata  bthea  broota  bofa  bthea  btree,a  bwea  bfinda  bthea  bproject;a  bita  bwilla  bcontaina  bthea  bnecessarya  breferencesa  banda  bthea  bnamespacesa  bofa  bhelloworld.a  bifa  bwea  bhada  bmorea  bnamespaces,a  btheya  bwoulda  bappeara  bthere,a  bwhena  bopeninga  bthea  bhelloworlda  bnamespace,a  bwea  bfinda  bthea  bclassesa  bthata  barea  bunclaimeda  bwithina  bit.a  bina  bthisa  bcase,a  bwea  bonlya  bhavea  bthea  bprograma  bclass;a  bifa  bwea  bselecta  bit,a  bwea  bwilla  bseea  bthata  bata  bthea  bbottom,a  bthea  belementsa  bthata  barea  bdeclareda  binsidea  barea  bshown.a  bina  boura  bexample,a  bwea  bhavea  bthea  bmaina  b()a  bmethod.

If,a  bata  bthisa  btime,a  bwea  bdoublea  bclicka  bona  banya  bofa  bthea  bmethods,a  bwea  bwilla  bautomaticallya  bgoa  btoa  bthea  bcodea  bwherea  bita  bisa  bdefined.a  bbecausea  boura  bprograma  bisa  bverya  bsmall,a  bwea  bmaya  bnota  bseea  bthea  badvantagea  bofa  bthis,a  bbuta  bina  bprogramsa  bwitha  bthousandsa  bofa  blinesa  bofa  bcode,a  bbeinga  bablea  btoa  bnavigatea  bquicklya  bisa  baa  bgreata  badvantage.

Configuringa  bcompilera  bmenus

Toa  badda  bthea  boptionsa  bwea  bneeda  bina  bthea  bmenus,a  bwea  bmusta  bfollowa  baa  bseriesa  bofa  bverya  bsimplea  bsteps.a  bfirst,a  bgoa  btoa  bthea  btoolsa  bmenua  banda  bselecta  bthea  bcustomizea  boption.

Aa  bdialoga  bboxa  bappears,a  bina  bwhicha  bwea  bmusta  bselecta  bcommands;a  bina  bthisa  bsection,a  bwea  bcana  bchoosea  bthea  bmenua  btoa  bwhicha  bwea  bwanta  btoa  badda  baa  bcommand,a  bfora  bexample,a  bthea  bviewa  bmenu.

![Image00104.jpg](images/Image00104.jpeg)a  b

Thea  bcurrenta  bmenua  bcommandsa  barea  blisted,a  bwea  bclicka  bona  bthea  bareaa  bwherea  bwea  bwanta  bthea  bnewa  bcommanda  btoa  bbea  binserteda  banda  bpressa  bthea  badda  bcommanda  bbutton.a  bwitha  bthis,a  baa  bnewa  bdialoga  bboxa  bappearsa  bthata  bshowsa  balla  bthea  bpossiblea  bcommandsa  bthata  bwea  bcana  badda  bclassified.

Ina  bthea  bcategoriesa  bwea  bselecta  bview,a  banda  bina  bthea  bclass,a  bviewa  bcommands,a  bthisa  bcommanda  bisa  bthea  bonea  bthata  ballowsa  busa  btoa  bhavea  bthea  bclassa  bview.a  bthea  bstarta  bwithouta  bdebugginga  bcommanda  bisa  bina  bthea  bdebuga  bcategory.

![Image00105.jpg](images/Image00105.jpeg)a  b

Upa  btoa  bthisa  bpoint,a  bwea  bhavea  banalyzeda  bthea  bmosta  bimportanta  bbasica  bconceptsa  bneededa  btoa  bunderstanda  bthea  boperationa  bofa  b.net.a  bfroma  bthea  bnexta  bchapter,a  bwea  bwilla  bbegina  bwitha  boura  blearninga  bofa  bprogramminga  banda  bthea  bc#a  blanguage.

Maina  bfunctionsa  bofa  bc#

C#a  bisa  baa  bnewa  bobject-orienteda  bprogramminga  blanguage,a  bwhicha  benablesa  bprogrammersa  btoa  bwritea  bvariousa  bapplicationsa  bbaseda  bona  bmicrosofta  b.neta  bplatforma  bquickly.a  bmicrosofta  b.neta  bprovidesa  baa  bseriesa  bofa  btoolsa  banda  bservicesa  btoa  bmaximizea  bthea  bdevelopmenta  banda  butilizationa  bofa  bcomputinga  banda  bcommunicationa  bfields.a  bita  bisa  bprecisea  bbecausea  bofa  bthea  bexcellenta  bobject-orienteda  bdesigna  bofa  bc#a  bthata  bita  bisa  bana  bideala  bchoicea  bfora  bbuildinga  bvariousa  bcomponents-whethera  bita  bisa  baa  bhigh-levela  bbusinessa  bobjecta  bora  baa  bsystem-levela  bapplication.

Thea  bfunctionsa  bofa  bc#a  barea  bmainlya  bmanifesteda  bina  bthea  bfollowinga  baspects:

a  bdesigninga  bwindowsa  bapplications.

a  bcustomizea  bthea  bwindowsa  bcontrola  blibrary.

a  bdesigna  bconsolea  bapplication.

a  bdesigna  bsmarta  bdevicea  bapplications.

a  bdesigna  basp.neta  bweba  bapplication.

a  bdesigna  basp.neta  bweba  bservice.

a  bdesigna  basp.neta  bmobilea  bweba  bapplication.

a  bcustomizea  bthea  bweba  bcontrola  blibrary.

Asp.neta  bisa  bthea  bcontrola  banda  bmarkupa  bdevelopeda  bbaseda  bona  bc#.a  bina  bthea  bfielda  bofa  bintermediatea  blanguage,a  bc#a  bisa  bthea  bmosta  baffinitya  blanguage,a  bwhicha  bhasa  bthea  bmaina  bcharacteristicsa  bofa  bca  blanguagea  banda  bjavaa  blanguage,a  bpowerfula  bfunctiona  blibrary,a  banda  bconvenienta  btemplate,a  banda  bisa  bonea  bofa  bthea  bideala  blanguagesa  bata  bpresent.

Maina  bfeaturesa  bofa  bc#

C#a  blanguagea  balmosta  bcombinesa  bthea  badvantagesa  bofa  bcurrenta  bhigh-levela  blanguagesa  banda  bhasa  bthea  bfollowinga  bmaina  bfeatures.

Concisea  bgrammar

C#a  blanguage,a  blikea  bjavaa  blanguage,a  busesa  bunifieda  boperators,a  beliminatesa  bcomplexa  bexpressionsa  banda  bpseudo-keywordsa  bina  bc++a  blanguage,a  banda  bmakesa  bita  bdescribeda  bina  bthea  bsimplesta  banda  bmosta  bcommona  bform.

Excellenta  bobject-orienteda  bdesign

C#a  blanguagea  bisa  bdesigneda  baccordinga  btoa  bthea  bideaa  bofa  bobject-oriented,a  bsoa  bita  bhasa  balla  bthea  bcharacteristicsa  bthata  bobject-orienteda  bshoulda  bhave,a  bnamelya  bencapsulation,a  binheritance,a  banda  bpolymorphism.

C#a  blanguagea  bonlya  ballowsa  bsinglea  binheritance,a  bthata  bis,a  baa  bclassa  bdoesa  bnota  bhavea  bmultiplea  bbasea  bclasses,a  bthusa  bavoidinga  bthea  bconfusiona  bofa  btypea  bdefinition.a  bina  bc#a  blanguage,a  beacha  btypea  bisa  bana  bobject,a  bsoa  btherea  barea  bnoa  bconceptsa  bsucha  basa  bglobala  bfunction,a  bglobala  bvariable,a  banda  bglobala  bconstant.a  balla  bconstants,a  bvariables,a  battributes,a  bmethods,a  bindexes,a  bevents,a  betc.a  bmusta  bbea  bencapsulateda  bina  bclasses,a  bwhicha  bmakesa  bthea  bcodea  bmorea  breadablea  banda  breducesa  bthea  bpossibilitya  bofa  bnaminga  bconflicts.

Closea  bintegrationa  bwitha  bthea  bweb

Ina  bc#,a  bcomplexa  bweba  bprogramminga  banda  bothera  bnetworka  bprogramminga  barea  bmorea  blikea  boperatinga  blocala  bobjects,a  bthusa  bsimplifyinga  blarge-scalea  banda  bin-deptha  bdistributeda  bdevelopment.a  bcomponentsa  bbuilt-ina  bc#a  blanguagea  bcana  bservea  bthea  bweba  bconvenientlya  banda  bcana  bbea  bcalleda  bbya  banya  blanguagea  brunninga  bona  banya  boperatinga  bsystema  bthrougha  bthea  binternet.

Completea  bsecuritya  banda  berrora  bhandling

Languagea  bsecuritya  banda  berrora  bhandlinga  babilitya  bisa  bana  bimportanta  bbasisa  btoa  bmeasurea  bwhethera  baa  blanguagea  bisa  bexcellenta  bora  bnot.c#a  blanguagea  bcana  beliminatea  bmanya  bcommona  bmistakesa  bina  bsoftwarea  bdevelopmenta  banda  bprovidea  bcompletea  bsafetya  bperformance,a  bincludinga  btypea  bsafety.

Bya  bdefault,a  bthea  bcodesa  bdownloadeda  bfroma  bthea  binterneta  banda  bintraneta  barea  bnota  balloweda  btoa  baccessa  banya  blocala  bfiles,a  banda  bresources.c#a  blanguagea  bdoesa  bnota  ballowa  buninitializeda  bvariablesa  banda  bprovidesa  bfunctionsa  bsucha  basa  bconvenienta  bchecka  banda  boverflowa  bcheck.a  bthea  bgarbagea  bcollectiona  bmechanisma  bina  bmemorya  bmanagementa  bgreatlya  breducesa  bthea  bburdena  bofa  bmemorya  bmanagementa  bfora  bdevelopers.

Versiona  bprocessinga  btechnology

C#a  blanguagea  bhasa  bbuilt-ina  bversiona  bcontrola  bfunctions,a  bsucha  basa  bhandlinga  bfunctiona  boverloadsa  banda  bexcuses,a  banda  bfeaturea  bsupport,a  betc.,a  btoa  bensurea  bconvenienta  bdevelopmenta  banda  bupgradea  bofa  bcomplexa  bsoftware.

Flexibilitya  banda  bcompatibility

Ina  bthea  bmanageda  bstate,a  bc#a  blanguagea  bcan’ta  busea  baa  bpointera  bbuta  busesa  bdelegatea  btoa  bsimulatea  bthea  bfunctiona  bofa  baa  bpointer.a  bifa  byoua  bneeda  btoa  busea  bpointersa  bina  bclassesa  bora  bmethodsa  bofa  bclasses,a  byoua  bonlya  bneeda  btoa  bdeclarea  bthesea  bcontentsa  bunsafe.a  balso,a  balthougha  bthea  bc#a  blanguagea  bdoesa  bnota  bsupporta  bmultiplea  binheritancesa  bofa  bclasses,a  bita  bcana  bbea  brealizeda  bbya  binheritinga  binterfaces.

Compatibilitya  bmeansa  bthata  bc#a  blanguagea  ballowsa  binteroperationa  bwitha  bapia  bwitha  bc/c++a  blanguagea  bstylea  bthata  bneedsa  btoa  bpassa  bpointera  btypea  bparametersa  banda  ballowsa  binteroperationa  bbetweena  bc#a  blanguagea  bcomponentsa  banda  bothera  blanguagea  bcomponents.

Bettera  bcorrespondencea  bbetweena  bbusinessa  bprocessa  banda  bsoftwarea  bimplementation

Ifa  bana  benterprise’sa  bbusinessa  bplana  bisa  btoa  bbea  bputa  bintoa  bpractice,a  baa  bclosea  bcorrespondencea  bmusta  bbea  bestablisheda  bbetweena  bthea  babstracta  bbusinessa  bprocessa  banda  bthea  bactuala  bsoftwarea  bimplementation.a  bita  bisa  bdifficulta  btoa  bdoa  bthisa  bina  bmosta  blanguages.

C#a  blanguagea  ballowsa  btype-defined,a  bextendeda  bmetadata.a  bthesea  bmetadataa  bcana  bbea  bapplieda  btoa  banya  bobject.a  bprojecta  bbuildersa  bcana  bdefinea  bdomain-specifica  battributesa  banda  bapplya  bthema  btoa  banya  blanguagea  belement,a  bsucha  basa  bclassesa  banda  binterfaces.

Ina  baa  bword,a  bc#a  bisa  baa  bmoderna  bobject-orienteda  blanguage,a  bwhicha  benablesa  bprogrammersa  btoa  bcreatea  bsolutionsa  bbaseda  bona  bmicrosofta  b.neta  bplatforma  bquicklya  banda  bconveniently.a  bthisa  bframeworka  benablesa  bc#a  bcomponentsa  btoa  bbea  beasilya  btransformeda  bintoa  bxmla  bnetworka  bservicesa  bsoa  bthata  bapplicationsa  bofa  banya  bplatforma  bcana  bcalla  bita  bthrougha  bthea  binternet.c#a  benhancesa  bthea  befficiencya  bofa  bdevelopers.a  bata  bthea  bsamea  btime,a  bita  bisa  bcommitteda  btoa  beliminatinga  berrorsa  bina  bprogramminga  bthata  bmaya  bleada  btoa  bseverea  bresults.a  bc#a  benablesa  bc/c++a  bprogrammersa  btoa  bdevelopa  bthea  bnetworka  bquicklya  bwhilea  bmaintaininga  bthea  bstrengtha  banda  bflexibilitya  bthata  bdevelopersa  bneed.

Witha  bthis,a  bwea  bhavea  bcompleteda  baa  bbriefa  bintroductiona  btoa  bthea  bimportancea  banda  bapplicationsa  bofa  bc#a  bwitha  bvarieda  bexamples.a  bina  bthea  bnexta  bchaptera  bofa  bthisa  bbook,a  bwea  bwilla  btalka  babouta  bthea  bc#a  bdevelopmenta  benvironmenta  bthata  bisa  bessentiala  bfora  bdevelopinga  baa  bwell-verseda  bc#a  bdesktopa  bwindowa  bapplication.a  bfollowa  balonga  btoa  bknowa  bmorea  babouta  bit.

## Chaptera  b2:a  bdataa  btype

Dataa  btypes

Ina  bthea  bca  bprogramminga  blanguage,a  bdataa  btypesa  balludea  btoa  baa  bframeworka  butilizeda  bfora  bpronouncinga  bvariablesa  bora  bfunctionsa  bofa  bdistinctivea  bdataa  btypes.a  bthea  btypea  bofa  baa  bvariablea  bdecidesa  bthea  bamounta  bofa  bspacea  bita  bwilla  btakea  banda  bhowa  bthea  bbita  bpatterna  bsaveda  bina  bita  bisa  butilized.a  bthea  bfundamentala  bclassificationa  buseda  bfora  bdataa  btypesa  bisa  bgivena  bbelow:

●a  bbasica  btypes:a  btheya  barea  bnumber-crunchinga  bsortsa  banda  bcomprisesa  bofa  bthea  btwoa  bfollowinga  btypes:a  b(a)a  bintegera  bsortsa  banda  b(b)a  bfloating-pointa  bsorts.

●a  benumerateda  bsorts:a  btheya  barea  bagaina  bnumbera  bsortsa  banda  barea  butilizeda  btoa  bcharacterizea  bvariablesa  bthata  bmusta  bbea  ballocateda  bdiscretea  bnumbera  bvaluesa  balla  bthrougha  bthea  bsystem.

●a  bvoida  btype:a  bthea  bkeyworda  bvoida  bdemonstratesa  bthata  bnoa  bvaluea  bcana  bbea  bassigned.

●a  bderiveda  bsorts:a  btheya  bincorporatea  b(a)a  barray,a  b(b)a  bpointer,a  b(c)a  bunion,a  b(d)a  bstructurea  banda  b(e)a  bfunction.

Thea  barraya  banda  bstructurea  bdataa  btypesa  barea  balsoa  breferreda  btoa  basa  baggregatea  btypes.a  bthea  btypea  bofa  bfunctiona  bdefinesa  bthea  bkinda  bofa  bvaluea  bthea  bfunctiona  bwilla  breturna  bupona  btermination.a  bwea  bwilla  bdiscussa  bthea  bessentiala  bdataa  btypesa  bina  bthea  baccompanyinga  bsegments.

Integera  btypes

Herea  bisa  baa  blista  bofa  bdataa  btypesa  bthata  bfollowa  bundera  bthisa  bcategory.a  balso,a  bthea  bstoragea  bspacea  boccupieda  bbya  bthema  banda  btheira  brangea  bisa  balsoa  bspecifieda  bfora  byoura  breference.

●a  bchar

Allocateda  bmemory:a  b1a  bbytea  boa  brange:a  b-128a  btoa  b127a  bora  b0a  btoa  b255

●a  bsigneda  bchara  boa  ballocateda  bmemory:a  b1a  bbytea  boa  brange:a  b-128a  btoa  b127

●a  bunsigneda  bchara  boa  ballocateda  bmemory:a  b1a  bbytea  boa  brange:a  b0a  btoa  b255

●a  bint

Allocateda  bmemory:a  b2a  bora  b4a  bbytesa  boa  brange:a  b-32,768a  btoa  b32,767a  bora  b-2,147,483,648a  btoa  b2,147,483,647

●a  bshort

Allocateda  bmemory:a  b2a  bbytesa  boa  brange:a  b-32,768a  btoa  b32,767

●a  bunsigneda  bshorta  boa  ballocateda  bmemory:a  b2a  bbytesa  boa  brange:a  b0a  btoa  b65,535

●a  bunsigneda  binta  boa  ballocateda  bmemory:a  b2a  bora  b4a  bbytesa  boa  brange:a  b0a  btoa  b65,535a  bora  b0a  btoa  b4,294,967,295

●a  blong

Allocateda  bmemory:a  b4a  bbytesa  boa  brange:a  b-2,147,483,648a  btoa  b2,147,483,647

●a  bunsigneda  blonga  boa  ballocateda  bmemory:a  b4a  bbytes

Range:a  b0a  btoa  b4,294,967,295

Toa  bgeta  bthea  bprecisea  bsizea  bofa  baa  bvariablea  bora  bdataa  btype,a  byoua  bcana  butilizea  bthea  bsizeofa  boperator.a  bthea  bdeclarationsa  bsizeof(<dataa  btype>)a  byieldsa  bthea  bsizea  bofa  bthea  bdataa  btypea  bora  bvariablea  bina  bbytes.a  bgivena  bbelowa  bisa  bana  bexample,a  bwhicha  billustratesa  bthea  bconcept,a  bdiscusseda  bbelow:a  b#includea  b<limits.h>a  b#includea  b<stdio.h>a  binta  bmain()a  b{

Printf(“dataa  btypea  bchara  b(sizea  bina  bbytes):a  b%da  b\n”,a  bsizeof(char));a  breturna  b0;

}

Upona  bcompilationa  banda  bexecutiona  bofa  bthisa  bcode,a  byoua  bmusta  bgeta  bthea  bfollowinga  boutput:a  bdataa  btypea  bchara  b(sizea  bina  bbytes):a  b1

Floatinga  bpointa  bdataa  btypes

Herea  bisa  baa  blista  bofa  bdataa  btypesa  bthata  bfollowa  bundera  bthisa  bcategory.a  balso,a  bthea  bstoragea  bspacea  boccupieda  bbya  bthem,a  btheira  brange,a  banda  bprecisiona  bvaluea  barea  bspecifieda  bfora  byoura  breference.

●a  bfloat

Allocateda  bmemory:a  b4a  bbytea  boa  brange:a  b1.2e-38a  btoa  b3.4e+38

Precision:a  b6a  bdecimala  bplacesa  b●a  bdouble

Allocateda  bmemory:a  b8a  bbytea  boa  brange:a  b2.3e-308a  btoa  b1.7e+308

Precision:a  b15a  bdecimala  bplacesa  b●a  blonga  bdoublea  boa  ballocateda  bmemory:a  b10a  bbytea  boa  brange:a  b3.4e-4932a  btoa  b1.1e+4932

Precision:a  b19a  bdecimala  bplacesa  bthea  bheadera  bfilea  bnameda  bfloat.ha  bcharacterizesa  bmacrosa  bthata  bpermita  byoua  btoa  butilizea  bthesea  bdataa  btypea  bvalues.a  bthea  bfollowinga  bcodea  bwilla  ballowa  byoua  btoa  bfinda  bthea  bexacta  bamounta  bofa  ballocateda  bmemorya  bina  bbytesa  bona  byoura  bsystema  bfora  bthea  bconcerneda  bdataa  btype.

#includea  b<float.h>a  b#includea  b<stdio.h>a  binta  bmain(){

Printf(“allocateda  bmemorya  bfora  bfloata  b:a  b%da  b\n”,a  bsizeof(float));a  bprintf(“precision:a  b%d\n”,a  bflt_diga  b);a  bprintf(“maxa  brangea  bvalue:a  b%e\n”,a  bflt_maxa  b);a  bprintf(“mina  brangea  bvalue:a  b%e\n”,a  bflt_mina  b);a  breturna  b0;

}

Upona  bcompilationa  banda  bexecutiona  bofa  bthisa  bcode,a  byoua  bmusta  bgeta  bthea  bfollowinga  boutput:a  ballocateda  bmemorya  bfora  bfloat:a  b4

Precision:a  b6

Maxa  brangea  bvalue:a  b3.402823e+38

Maxa  brangea  bvalue:a  b1.175494e-38

Thea  bvoida  btype

Thea  bvoida  bdataa  btypea  bpointsa  bouta  bthata  bnoa  bvaluea  bisa  baccessible.a  bita  bisa  butilizeda  basa  baa  bparta  bofa  bthreea  bsortsa  bofa  bcircumstances:

●a  bvoida  breturneda  bbya  baa  bfunction.a  byoua  bmusta  bhavea  bcommonlya  bnoticeda  bthea  busea  bofa  bthea  bdataa  btypea  bvoida  basa  bthea  breturna  btypea  bofa  bfunction.a  bifa  bnot,a  byoua  bwilla  bseea  bextensivea  busea  bofa  bthea  bsamea  basa  byoua  bmovea  bforwarda  bina  byoura  bexperiencea  bwitha  bc.a  bthea  bvoida  bdataa  btypea  bsignifiesa  bthata  bthea  bfunctiona  bwilla  bnota  breturna  banything.a  bexamplea  bofa  bsucha  bana  bimplementationa  bis:a  bvoida  bprint(int)

●a  bfunctiona  bargumentsa  basa  bvoida  btherea  barea  bdifferenta  bfunctionsa  bina  bc,a  bwhicha  bdon’ta  backnowledgea  banya  bparameter.a  baa  bfunctiona  bwitha  bnoa  bparametera  bcana  backnowledgea  basa  baa  bvoid.a  bexamplea  bofa  bsucha  bana  bimplementationa  bis:a  binta  bprint(void)

●a  bpointersa  btoa  bvoida  baa  bpointera  bofa  bsorta  bvoida  b*a  bsignifiesa  bthea  blocationa  bofa  baa  bvariable.a  bfora  binstance,a  bconsidera  bthea  bfollowinga  bdeclaration:a  bvoida  b*malloc(a  bsize_ta  bsizea  b);a  bthisa  bfunctiona  breturnsa  baa  bpointera  btoa  bvoid.a  bina  bothera  bwords,a  bthisa  bfunctiona  bcana  breturna  baa  bpointera  btoa  baa  blocationa  bofa  banya  btype.

Youa  bmaya  bnota  bbea  bablea  btoa  bcomprehenda  bthea  busea  banda  bmeaninga  bofa  bthea  bvoida  bdataa  btypea  bina  bentiretya  brighta  bnow.a  bhowever,a  basa  byoua  bmovea  bforward,a  byoua  bwilla  bfinda  bita  beasiera  btoa  brelatea  btoa  banda  busea  bthisa  bdataa  btypea  bina  byoura  bcode.

## Chaptera  b3:a  boperatorsa  bvariable

Varıables

Aa  bvariablea  bisa  bsimplya  baa  bnamea  bthata  bisa  bassigneda  btoa  baa  bstoragea  barea.a  boura  bprogramsa  barea  bcapablea  bofa  bmanipulatinga  bsucha  baa  bstoragea  barea.a  beacha  bc#a  bvariablea  bisa  bassociateda  bwitha  baa  btypea  bthata  bdeterminesa  bthea  bamounta  bofa  bspacea  ballocateda  btoa  bthata  bvariablea  bina  bthea  bmemory.a  bthisa  balsoa  bdeterminesa  bthea  bkinda  bofa  boperationsa  bthata  bcana  bbea  bapplieda  btoa  bthea  bvariable.a  bfora  bexample,a  byoua  bcannota  bmultiplya  bstringa  bvariables.

Ina  bc#,a  bthea  bfollowinga  bsyntaxa  bshoulda  bbea  buseda  bina  bthea  bvariablea  bdeclaration:

<data_type>a  b<variable_list>;

Thea  bdata_typea  bina  bthea  babovea  bsyntaxa  bmusta  bbea  baa  bvalida  bdataa  btypea  bina  bc#a  blikea  bint,a  bstring,a  bfloat,a  betc.a  bthea  bvariable_lista  bcana  bbea  bmanya  bvariablea  bnamesa  bseparateda  businga  bcommas.

Belowa  barea  bexamplesa  bofa  bvalida  bvariablea  bdeclarations:

Inta  ba,a  bb,a  bc;a  bchara  bc,a  bd;a  bfloata  bx,a  bsalary;a  bdoublea  by;

Aa  bvariablea  bcana  bbea  binitializeda  bduringa  bitsa  bdeclaration.

Fora  bexample:a  binta  bxa  b=a  b40;

Variablea  binitialization

Variablea  binitializationa  brefersa  btoa  bthea  bprocessa  bofa  bassigninga  baa  bvaluea  btoa  baa  bvariable.a  bina  bc#,a  bthisa  bisa  bdonea  businga  bana  bequala  bsigna  bthena  bfolloweda  bbya  bconstanta  bexpression.a  bherea  bisa  bthea  bgenerala  bsyntaxa  bfora  binitialization:a  bvariable_namea  b=a  bvalue;a  basa  bwea  bhada  bstateda  bearlier,a  bvariablesa  bcana  bbea  binitializeda  bduringa  btheira  bdeclaration.a  bherea  barea  bmorea  bexamples:

Inta  bxa  b=a  b1,a  bya  b=a  b6;a  b/*a  binitializinga  bxa  banda  by.a  b*/

Bytea  bfa  b=a  b22;a  b/*a  binitializesa  bf.a  b*/

Doublea  bpia  b=a  b3.14159;a  b/*a  bdeclaringa  bana  bapproximationa  bofa  bpi.a  b*/

Chara  baa  b=a  b‘a’;a  b/*a  bthea  bvariablea  baa  bhasa  baa  bvaluea  bofa  b‘a’.a  b*/

Variablea  binitializationa  bshoulda  bbea  bdonea  bcorrectly;a  botherwise,a  bthea  bprograma  bmaya  bgivea  bunexpecteda  bresults.

Fora  bexample:a  businga  bsystem;a  bnamespacea  bvariabledeclarationa  b{

Classa  bmyprograma  b{

Statica  bvoida  bmain(string[]a  bargs)a  b{

Shorta  bx;a  binta  bya  b;a  bdoublea  bz;a  b/*a  bactuala  binitializationa  bofa  bvariablesa  b*/

Xa  b=a  b5;a  bya  b=a  b10;a  bza  b=a  bxa  b+a  by;a  bconsole.writeline(“xa  b=a  b{0},a  bya  b=a  b{1},a  bza  b=a  b{2}“,a  bx,a  by,a  bz);a  bconsole.readline();a  b}

}

}

Thea  bcodea  breturnsa  bthea  bfollowing:

X=5,a  by=10,a  bz=15

Gettinga  busera  binput

Thea  bconsolea  bclassa  bofa  bthea  bsystema  bnamespacea  bhasa  baa  bmethoda  bnameda  breadline()a  bthata  ballowsa  busa  btoa  bgeta  binputa  bfroma  bthea  buser.a  bthea  buser’sa  binputa  bisa  breada  banda  bstoreda  bina  baa  bvariable.a  bthea  bfollowinga  bexamplea  bdemonstratesa  bhowa  btoa  busea  bthisa  bmethod:a  businga  bsystem;a  bnamespacea  buserinputappa  b{

Classa  bmyprograma  b{

Statica  bvoida  bmain(string[]a  bargs)a  b{

Stringa  bfirstnamea  b=a  b“nicholas”;a  bstringa  blastnamea  b=a  b“samuel”;

Console.writeline(“youra  bnamea  bis:a  b“+a  bfirstnamea  b+a  b"a  b“+a  blastname);

Console.writeline(“pleasea  bentera  baa  bdifferenta  bfirsta  bname:”);a  bfirstnamea  b=a  bconsole.readline();

Console.writeline(“youra  bnewa  bnamea  bis:a  b"a  b+a  bfirstnamea  b+a  b"a  b“+a  blastname);a  bconsole.readline();a  b}

}

}

Whena  bprompteda  btoa  bentera  baa  bnewa  bvaluea  bfora  bthea  bfirsta  bname,a  bdoa  bsoa  banda  bhita  bthea  bentera  bkey.a  byoua  bwilla  brealizea  bthata  byoura  bnamea  bhasa  bchanged.

Operators

Operatorsa  barea  bsymbolsa  bthata  binstructa  bthea  bcompilera  btoa  bperforma  baa  bcertaina  blogicala  bora  bmathematicala  bmanipulation.a  bc#a  bhasa  baa  bwidea  bvarietya  bofa  boperators.a  bleta  busa  bdiscussa  bthem.

Arıthmetıca  boperators

Thesea  barea  buseda  bfora  bperforminga  bvariousa  bmathematicala  boperations.a  btheya  bcana  bbea  buseda  basa  bshowna  bina  bthea  bfollowinga  bexample:

Usinga  bsystem;a  bnamespacea  baithmeticoperatorsappa  b{

Classa  bmyprograma  b{

Statica  bvoida  bmain(string[]a  bargs)a  b{

Inta  bxa  b=a  b31;a  binta  bya  b=a  b10;a  binta  bz;a  bza  b=a  bxa  b+a  by;a  bconsole.writeline(”1:a  b-a  bza  bequalsa  btoa  b{0}“,a  bz);a  bza  b=a  bxa  b-a  by;a  bconsole.writeline(”2:a  b-a  bza  bequalsa  btoa  b{0}“,a  bz);

Za  b=a  bxa  b*a  by;a  bconsole.writeline(”3:a  b-a  bza  bequalsa  btoa  b{0}“,a  bz);a  bza  b=a  bxa  b/a  by;a  bconsole.writeline(”4:a  b-a  bza  bequalsa  btoa  b{0}“,a  bz);a  bza  b=a  bxa  b%a  by;a  bconsole.writeline(”5:a  b-a  bza  bequalsa  btoa  b{0}“,a  bz);a  bza  b=a  bx++;a  bconsole.writeline(”6:a  b-a  bza  bequalsa  btoa  b{0}“,a  bz);a  bza  b=a  bx—;a  bconsole.writeline(”7:a  b-a  bza  bequalsa  btoa  b{0}“,a  bz);a  bconsole.readline();a  b}

}

}

Mosta  bofa  bthea  babovea  boperatorsa  barea  bwella  bknowna  bexcepta  bfora  baa  bfewa  bofa  bthem.a  bthea  b++a  bisa  bthea  bincrementa  boperator,a  banda  bita  bincreasesa  bthea  bvaluea  bofa  bthea  bvariablea  bbya  b1a  bfora  beacha  biteration.a  bthea  b–a  bisa  bthea  bincrementsa  boperator,a  banda  bita  bdecrementsa  bthea  bvaluea  bofa  bthea  bvariablea  bbya  b1a  baftera  beacha  biteration.a  bthea  b%a  bisa  bknowna  basa  bthea  bmodulusa  boperator,a  banda  bita  breturnsa  bthea  bremaindera  baftera  bdivision.

Thea  bcodea  breturnsa  bthea  boutputa  bshowna  bbelow:

![Image00106.jpg](images/Image00106.jpeg)a  b

Logicala  boperators

C#a  balsoa  bhasa  baa  bnumbera  bofa  blogicala  boperators.a  bleta  busa  bdiscussa  bthema  bbriefly:

Logicala  banda  b(&&)-a  bthea  bconditiona  bisa  btruea  bifa  bbotha  boperandsa  barea  bnonzero.

Logicala  bora  b(||)-a  bthea  bconditiona  bisa  btruea  bifa  banya  bofa  bthea  boperandsa  bisa  bnonzero.

Logicala  bnota  b(!)-a  bthea  boperatora  breversesa  bthea  blogicala  bstatea  bofa  bana  boperand.a  bifa  bthea  bconditiona  bisa  btrue,a  bthisa  boperatora  bwilla  bmakea  bita  bfalse.

Thea  bfollowinga  bexamplea  bdemonstratesa  bhowa  btoa  busea  bthea  babovea  boperators:a  businga  bsystem;a  bnamespacea  blogicaloperatorsappa  b{

Classa  bmyprograma  b{

Statica  bvoida  bmain(string[]a  bargs)a  b{

Boola  bxa  b=a  btrue;a  bboola  bya  b=a  btrue;a  bif(xa  b&&a  by)a  b{

Console.writeline(”1:a  bthea  bconditiona  bisa  btrue”);a  b}

Ifa  b(xa  b||a  by)a  b{

Console.writeline(”2;a  btheconditiona  bisa  btrue”);a  b}

/*a  bleta  busa  bchangea  bthea  bvaluesa  bofa  bxa  banda  bya  b*/

Xa  b=a  bfalse;a  bya  b=a  btrue;a  bif(xa  b&&a  by)a  b{

Console.writeline(”3:a  bthea  bconditiona  bisa  btrue”);a  b}a  belsea  b{

Console.writeline(”3:a  bthea  bconditiona  bisa  bnota  btrue”);a  b}

If(!(xa  b&&a  by))a  b{

Console.writeline(”4:a  bthea  bconditiona  bisa  btrue”);a  b}

Console.readline();a  b}

}

}

Thea  bcodea  breturnsa  bthea  bfollowinga  boutput:

![Image00107.jpg](images/Image00107.jpeg)a  b

Assıgnmenta  boperators

C#a  bassignmenta  boperatorsa  bcana  bbea  buseda  basa  bdemonstrateda  bina  bthea  bfollowinga  bexample:

Classa  bmyprograma  b{

Statica  bvoida  bmain(string[]a  bargs)a  b{

Inta  bxa  b=a  b31;a  binta  bz;a  bza  b=a  bx;a  bconsole.writeline(”1:a  b=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);

Za  b+=a  bx;a  bconsole.writeline(”2:a  b+=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);

Za  b-=a  bx;a  bconsole.writeline(”3:a  b-=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);a  bza  b*=a  bx;a  bconsole.writeline(”4:a  b*=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);

Za  b/=a  bx;a  bconsole.writeline(”5:a  b/=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);a  bza  b=a  b100;a  bza  b%=a  bx;a  bconsole.writeline(”6:a  b%=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);a  bza  b<<=a  b2;a  bconsole.writeline(”7:a  b<<=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);a  bza  b>>=a  b2;a  bconsole.writeline(”8:a  b>>=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);a  bza  b&=a  b2;a  bconsole.writeline(”9:a  b&=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);a  bza  b^=a  b2;a  bconsole.writeline(”10:a  b^=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);a  bza  b|=a  b2;a  bconsole.writeline(”11:a  b|=a  bthea  bvaluea  bofa  bza  bisa  b=a  b{0}“,a  bz);a  bconsole.readline();a  b}

}

}

Thea  bcodea  breturnsa  bthea  bfollowinga  bresult:

![Image00108.jpg](images/Image00108.jpeg)a  b

## Chaptera  b4:a  bstringa  banda  blist

List

Thea  blist<t>a  bisa  bthea  bcollectiona  bclassa  bthata  bisa  bmosta  bfrequentlya  buseda  bina  balla  bcollectiona  bclasses.a  bita  bisa  baa  btypea  bwhosea  bmaina  bcharacteristica  bisa  bthea  belementa  baccessibilitya  bbya  bindex.a  basa  bmentioneda  bbefore,a  blista  bclassa  bcomesa  bundera  bthea  bsystem.a  bcollections.generica  bnamespace.a  bthea  blista  bisa  baa  bclassa  bthata  bprovidesa  baa  blota  bofa  bmethodsa  bfora  bthea  blista  banda  belementa  bmanipulation.a  bsomea  bofa  bthema  barea  bsearching,a  bsorting,a  betc.a  bita  bisa  buseda  bfora  bcreatinga  baa  bcollectiona  bofa  bmanya  bdifferenta  btypes.a  bita  bcoulda  bbea  baa  bcollectiona  bofa  bintegers,a  bstrings,a  banda  bmanya  bmore.a  bfora  bthea  breferencea  btypes,a  bthea  blista  ballowsa  bnulla  bvaluea  basa  bana  belement.a  bita  bisa  balsoa  bpossiblea  btoa  binserta  bduplicatea  bvaluesa  binsidea  banya  blista  bcollection.a  bthisa  bclassa  bcana  busea  bbotha  bthea  borderinga  banda  bequalitya  bcomparer.a  barraysa  barea  bsimilara  btoa  bthea  blists,a  bbuta  bthea  blistsa  bcana  bresizea  bdynamically,a  bbuta  barraysa  bcannot.

String

Stringa  bdataa  btypea  bina  bc#a  bisa  baa  btypea  bthata  brepresentsa  btexta  banda  bworksa  bwitha  btexta  bvariables.a  bita  bisa  bana  barraya  bofa  bcharacters.a  bdeclaringa  baa  bstringa  bdataa  btypea  bisa  bdonea  bbya  bstringa  bkeyword.a  bwhena  baa  bstringa  bkeyworda  bisa  bbeinga  bused,a  bita  bmeansa  bthata  bita  bisa  breferringa  btoa  bthea  b‘system.string’a  bclassa  b(classesa  bwilla  bbea  bexplaineda  blatera  bina  bthea  bbook).a  btherea  barea  bmanya  bextensiona  bmethodsa  bwhicha  bcoulda  bbea  buseda  bovera  bsomea  bstringa  bvariable.a  bsomea  bofa  bthea  bmosta  bpopulara  barea  bconcata  b-a  bwhicha  bisa  bconcatenatinga  btwoa  bstrings,a  bcontainsa  b-a  bwhicha  bdeterminesa  bwhethera  bthea  bstringa  bcontainsa  bthea  bgivena  bstringa  bfroma  bthea  bparametera  basa  bpasseda  bvalue,a  bequalsa  b-a  bwhicha  bdeterminesa  bwhethera  btwoa  bstringsa  bhavea  bthea  bsamea  bvalue,a  betc.a  bthea  bdefaulta  bstringa  bdataa  btypea  bisa  bana  bemptya  bstring.

## Chaptera  b5:a  bsyntax

Loopa  bstructurea  bstatement

Ina  breala  blife,a  bwea  boftena  brepeata  bthea  bsamea  bthinga  bmanya  btimes.a  bfora  bexample,a  bwhena  byoua  bscrapea  byoura  beyesa  bina  bthea  bfourtha  brounda  bofa  beyea  bexercises,a  byoua  bwilla  brepeata  bthea  bactiona  bofa  bscrapinga  byoura  beyes.a  bwhena  bplayinga  btablea  btennis,a  byoua  bwilla  brepeata  bthea  bswinga  banda  bsoa  bon.a  bina  bc#,a  btherea  bisa  baa  bstatementa  bthata  bcana  bexecutea  bthea  bsamea  bcodea  bblocka  brepeatedly,a  bwhicha  bisa  bcalleda  baa  bcirculara  bstatement.a  bloopa  bstatementsa  barea  bdivideda  bintoa  bthreea  btypes:a  bwhilea  bloopa  bstatement,a  bdo…whilea  bloopa  bstatementa  banda  bfora  bloopa  bstatement.

Whilea  bloopa  bstatement

Thea  bwhilea  bloopa  bstatementa  bisa  bsomewhata  bsimilara  btoa  bthea  bconditionala  bjudgmenta  bstatementa  bmentioneda  bina  bthea  babovea  bsection,a  bwhicha  bdeterminesa  bwhethera  btoa  bexecutea  bthea  bexecutiona  bstatementa  bina  b{}a  baccordinga  btoa  bthea  bconditionala  bjudgment.a  bthea  bdifferencea  bisa  bthata  bthea  bwhilea  bstatementa  bwilla  brepeatedlya  bjudgea  bthea  bconditions.a  basa  blonga  basa  bthea  bconditionsa  barea  btrue,a  bthea  bstatementsa  bina  b{}a  bwilla  bbea  bexecuteda  buntila  bthea  bconditionsa  barea  bnota  btruea  banda  bthea  bwhilea  bloopa  bends.

Thea  bsyntaxa  bstructurea  bofa  bthea  bwhilea  bloopa  bstatementa  bisa  basa  bfollows:

Whilea  b(cyclica  bcondition)

{

Executea  bstatement

…

}

Ina  bthea  babovea  bsyntaxa  bstructure,a  bthea  bexecutiona  bstatementa  bina  b{}a  bisa  bcalleda  bthea  bloopa  bbody,a  banda  bwhethera  bthea  bloopa  bbodya  bisa  bexecuteda  bdependsa  bona  bthea  bloopa  bcondition.a  bwhena  bthea  bloopa  bconditiona  bisa  btrue,a  bthea  bloopa  bbodya  bwilla  bexecute.a  bwhena  bthea  bloopa  bbodya  bfinishesa  bexecuting,a  bita  bwilla  bcontinuea  btoa  bjudgea  bthea  bloopa  bcondition.a  bifa  bthea  bconditiona  bisa  bstilla  btrue,a  bita  bwilla  bcontinuea  btoa  bexecute,a  banda  bthea  bwholea  bloopa  bprocessa  bwilla  bnota  benda  buntila  bthea  bloopa  bconditiona  bisa  bfalse.

Next,a  baa  bcasea  bisa  buseda  btoa  bprinta  bnaturala  bnumbersa  bfroma  b1a  btoa  b4,a  basa  bshowna  bina  bexamplea  bbelow.

Examplea  bprogram11.cs

Publica  bclassa  bprogram11

{

Publica  bstatica  bvoida  b//a  bthisa  bisa  bwherea  byoua  bneeda  btoa  bentera  bthea  blogic

{

Inta  bfirstsamplea  b=a  b1;//definea  bthea  bvariablea  b‘firstsample’a  bwitha  bthea  binitiala  bvaluea  bofa  b1

Whilea  b(firstsamplea  b<=a  b4)

//a  bcyclea  bcondition

{

Console.enteroptions(“firstsamplea  b=a  b"a  b+a  bfirstsample);

//ifa  bthea  bconditiona  bholds,a  bprinta  bthea  bvaluea  bofa  bfirstsample.

Firstsample++;

//firstsamplea  bfora  bself-increment

}

Console.readkey();

}

}

Thea  brunninga  bresultsa  barea  bshowna  bona  bthea  bcomputera  bscreen.

Fora  bexample,a  bthea  binitiala  bvaluea  bofa  bxa  bisa  b1,a  banda  bifa  bthea  bloopa  bconditiona  bxa  b<=a  b4a  bisa  bmet,a  bthea  bloopa  bwilla  bbea  brepeatedlya  bexecuted,a  banda  bthea  bvaluea  bofa  bxa  bwilla  bbea  bprinted,a  banda  bxa  bwilla  bincreasea  bautomatically.a  btherefore,a  bthea  bvaluesa  bofa  bxa  bina  bthea  bprinteda  bresultsa  barea  b1,a  b2,a  b3,a  banda  b4,a  brespectively.a  bita  bisa  bwortha  bnotinga  bthata  bthea  bcodea  bina  blinea  b9a  bofa  bthea  bexamplea  bisa  buseda  btoa  bchangea  bthea  bvaluea  bofa  bvariablea  bxa  bina  beacha  bloopa  btoa  bachievea  bthea  bpurposea  bofa  bchanginga  bthea  bloopa  bconditiona  bfinally.a  bwithouta  bthisa  blinea  bofa  bcode,a  bthea  bwholea  bloopa  bwilla  bgoa  bintoa  bana  binfinitea  bloopa  banda  bnevera  bend.

Do-whilea  bloopa  bstatement

Thea  bfunctiona  bofa  bdo-whilea  bloopa  bstatementa  bisa  bsimilara  btoa  bthata  bofa  bwhilea  bloopa  bstatement.a  bthea  bdifferencea  bbetweena  bthema  bisa  bthata  bwhilea  bthea  bstatementa  bneedsa  btoa  bjudgea  bthea  bloopa  bconditiona  bfirsta  banda  bthena  bdecidea  bwhethera  btoa  bexecutea  bthea  bcodea  bina  b{}a  baccordinga  btoa  bthea  bresulta  bofa  bthea  bloopa  bcondition.a  bina  bcontrast,a  bthea  bdo-whilea  bloopa  bstatementa  bneedsa  btoa  bexecutea  bthea  bcodea  bina  b{}a  boncea  bbeforea  bjudginga  bthea  bloopa  bcondition.

Itsa  bsyntaxa  bstructurea  bisa  basa  bfollows:

Do

{

Executea  bstatement

…

}a  bwhilea  b(cyclica  bcondition);

Ina  bthea  babovea  bsyntaxa  bstructure,a  bthea  bexecutiona  bstatementa  bina  b{}a  baftera  bthea  bkeyworda  bdoa  bisa  baa  bloopa  bbody.a  bthea  bdo-whilea  bloopa  bstatementa  bputsa  bthea  bloopa  bconditiona  bbehinda  bthea  bloopa  bbody.a  bthisa  bmeansa  bthata  bthea  bloopa  bwilla  bexecutea  bunconditionallya  bonce,a  banda  bthena  bdecidea  bwhethera  btoa  bcontinuea  bexecutiona  baccordinga  btoa  bthea  bloopa  bconditions.

Next,a  busea  bthea  bdo-whilea  bloopa  bstatementa  btoa  brewritea  bexample,a  basa  bshowna  bina  bthea  bbelowa  bexample.

Examplea  bprogram12.cs:

Publica  bclassa  bclassicprogram

{

Publica  bstatica  bvoida  b//a  bthisa  bisa  bwherea  bwea  busuallya  bentera  bthea  boptions

{

Inta  bsecondinstancea  b=a  b1;

//definea  bthea  bvariablea  b‘secondinstance’a  bwitha  bthea  binitiala  bvaluea  bofa  b1

Do

{

Console.getresults(”a  bfirstinstance=a  b"a  b+a  bsecondinstance);

//printa  bthea  bvaluea  bofa  b‘firstinstance’

Secondinstance++;

//increasea  bthea  bvaluea  bofa  b‘firstinstance’a  bbya  bitself

}

Whilea  b(firstinstancea  b<=a  b4);

//cyclea  bconditions

Console.scanprogram();

}

}

Thea  brunninga  bresultsa  bwilla  bbea  bshowna  bona  bthea  bcomputera  bscreen.

Examplesa  babovea  bhavea  bthea  bsamea  brunninga  bresults,a  bwhicha  bshowsa  bthata  baa  bdo-whilea  bloopa  banda  bwhilea  bloopa  bcana  bachievea  bthea  bsamea  bfunction.a  bhowever,a  btherea  barea  bdifferencesa  bbetweena  bthesea  btwoa  bstatementsa  bina  bthea  bprocessa  bofa  baa  bprograma  brunning.a  bifa  bthea  bloopa  bconditiona  bdoesa  bnota  bholda  bata  bthea  bbeginninga  bofa  bthea  bloopa  bstatement,a  bthea  bloopa  bbodya  bofa  bthea  bwhilea  bloopa  bwilla  bnota  bbea  bexecuteda  bonce,a  bbuta  bthea  bloopa  bbodya  bofa  bthea  bdo-whilea  bloopa  bwilla  bstilla  bbea  bexecuteda  bonce.a  bifa  bthea  bcyclea  bconditiona  bx<=4a  bina  bthea  bexamplea  bisa  bchangeda  btoa  bxa  b<a  b1,a  bthea  bexamplea  b2-12a  bwilla  bprinta  bx=1,a  bwhilea  bthea  bexamplea  b2-11a  bwilla  bprinta  bnothing.

Fora  bloopa  bstatement

Thea  bwhilea  bloopa  banda  bthea  bdo-whilea  bloopa  bwasa  bexplaineda  bina  bthea  bpreviousa  bsection.a  bina  bprograma  bdevelopment,a  banothera  bkinda  bofa  bloopa  bstatementa  bisa  boftena  bused,a  bthata  bis,a  bfora  bloopa  bstatement,a  bwhicha  bisa  busuallya  buseda  bwhena  bthea  bnumbera  bofa  bloopsa  bisa  bknown,a  banda  bitsa  bsyntaxa  bformata  bisa  basa  bfollows.

Fora  b(initializationa  bexpression;a  bcirculationa  bconditions;a  boperationa  bexpression)

{

Executea  bstatement

…

}

Ina  bthea  babovea  bsyntaxa  bstructure,a  bthea  b()a  baftera  bthea  bfora  bkeyworda  bincludesa  bthreea  bparts:a  binitializationa  bexpression,a  bloopa  bcondition,a  banda  boperationa  bexpression,a  bwitha  b“;a  b“betweena  bthea  bseparation,a  bthea  bexecutiona  bstatementa  bina  b{}a  bisa  baa  bloopa  bbody.

Next,a  bthea  binitializationa  bexpression,a  bloopa  bcondition,a  boperationa  bexpression,a  banda  bloopa  bbodya  barea  brepresenteda  bbya  b1,a  brespectively,a  banda  bthea  bexecutiona  bflowa  bofa  bthea  bfora  bloopa  bisa  banalyzeda  bina  bdetaila  bbya  bseriala  bnumber.

For（1;a  b2;3）

{

4

}

Next,a  bsuma  bnaturala  bnumbersa  b1~4a  bthrougha  baa  bcase,a  basa  bshowna  bina  bexamplea  bbelow.

Examplea  bprogram13.cs:

Publica  bclassa  bclassicprogram

{

Publica  bstatica  bvoida  b//a  bthisa  bisa  bwherea  bwea  busuallya  bentera  bthea  boptions

{

Inta  bsecondinstancea  b=a  b1;

//definea  bthea  bvariablea  b‘secondinstance’a  bwitha  bthea  binitiala  bvaluea  bofa  b1

Do

{

Console.getresults(”a  bfirstinstance=a  b"a  b+a  bsecondinstance);

//printa  bthea  bvaluea  bofa  b‘firstinstance’

Secondinstance++;

//increasea  bthea  bvaluea  bofa  b‘firstinstance’a  bbya  bitself

}

Whilea  b(firstinstancea  b<=a  b4);

//cyclea  bconditions

Fora  b(inta  bfirsta  b=a  b1;a  bfirsta  b<=a  b4;thea  bvaluea  bofa  bfirst++)

//firsta  bwilla  bchangea  bfroma  b1a  btoa  b4

{

Suma  b+=a  bfirst;

//realizea  bthea  baccumulationa  bofa  bsuma  banda  bi.

}

Ina  bexample,a  bthea  binitiala  bvaluea  bofa  bvariablea  bia  bisa  b1,a  banda  bifa  bthea  bjudgmenta  bconditiona  bi<=4a  bisa  btrue,a  bthea  bloopa  bsum+=a  bia  bwilla  bbea  bexecuted.a  baftera  bthea  bexecutiona  bisa  bfinished,a  bthea  boperationa  bexpressiona  bi++,a  bia  bwilla  bbea  bexecuted,a  banda  bthea  bvaluea  bofa  bia  bwilla  bbecomea  b2.a  bthena  bcontinuea  btoa  bjudgea  bthea  bcondition,a  banda  bstarta  bthea  bnexta  bloopa  buntila  bi=5a  banda  bthea  bconditiona  bi<=4a  bisa  bfalse,a  benda  bthea  bloop,a  bexecutea  bthea  bcodea  baftera  bthea  bfora  bloop,a  banda  bprinta  b“sum=10“.

## Chaptera  b6:a  bclasses

Classesa  banda  bobjects

Ina  bc#a  bprogramminga  blanguage,a  beverya  bcomponenta  bisa  bassociateda  bwitha  bclassesa  banda  bobjects,a  banda  bthesea  brepresenta  bthea  bbasica  bconceptsa  bofa  bobject-orienteda  bprogramming.a  baa  bclassa  bisa  bsomethinga  blikea  baa  bprototypea  bfroma  bwhicha  bthea  busera  bcreatesa  bobjects.a  baa  bclassa  brepresentsa  baa  bsingle,a  buniquea  bunita  bwitha  balla  bofa  bitsa  bmembers,a  battributes,a  banda  bfunctionality.

Thea  bobjectsa  barea  breal-life,a  bin-memorya  bentities.a  bwhena  binstantiated,a  btheya  ballocatea  bsomea  bmemorya  bspacea  banda  bhavea  breferencea  btoa  bit.a  beverya  bobjecta  bcreateda  bmusta  bbea  bofa  baa  bclassa  btype.

Class

Classesa  brepresenta  bthea  buniquea  bprogramminga  bcomponentsa  binsidea  banya  bobject-orienteda  bsoftware.a  bthea  bclassa  bisa  bdefineda  bwitha  bitsa  baccessa  bmodifier,a  bclassa  bkeyword,a  banda  baa  buniquea  bname.a  binsidea  bsomea  bclass,a  btherea  bcoulda  bbea  bmultiplea  bmembersa  bsucha  basa  bfields,a  bproperties,a  banda  bmethods.a  bthea  bdefaulta  baccessa  bmodifiera  bofa  baa  bclassa  bisa  binternal.a  bthisa  bmeansa  bthata  bifa  bthea  baccessa  bmodifiera  bisa  bnota  bspecified,a  bthena  bthata  bparticulara  bclassa  bwoulda  bbea  btreateda  basa  binternal.a  bana  bexamplea  bofa  baa  bclassa  bisa  bwrittena  bbelow:

![Image00109.jpg](images/Image00109.jpeg)a  b

Thisa  bclassa  bcontainsa  bitsa  baccessa  bmodifiera  b–a  bpublic,a  bwhicha  bcontainsa  bthea  bkeyworda  bclass;a  bita  bhasa  baa  buniquea  bname,a  btshirt.a  binsidea  bthisa  bclass,a  btherea  barea  bmultiplea  bmembersa  bdefined.a  btherea  bisa  bonea  bprivatea  bfielda  bcolor,a  bonea  bpublica  bpropertya  bcolor,a  bonea  bconstructora  bdefineda  b(witha  bonea  bparameter),a  banda  bonea  bpublica  bmethoda  babout.

Aparta  bfroma  bthea  busuala  bclasses,a  btherea  bisa  bonea  bspeciala  btypea  bofa  bclassa  b-a  bthea  babstracta  bclass.a  bana  babstracta  bclassa  bisa  baa  bspeciala  btypea  bofa  bclassa  bina  bwhicha  bana  bobjecta  bcannota  bbea  binstantiated.a  babstracta  bclassesa  barea  bmostlya  buseda  btoa  bdefinea  baa  bbasea  bclassa  bina  bthea  bhierarchy,a  banda  bita  bisa  balsoa  bknowna  basa  bana  bincompletea  bclass.a  bthea  babstracta  bclassesa  btypicallya  brepresenta  baa  bbasea  bclass.a  bita  bisa  bdesigneda  btoa  bhavea  bderiveda  bclassesa  bimplementinga  bthea  babstracta  bdefinitions.a  bina  bthea  babstracta  bclasses,a  btherea  bcoulda  basa  bwella  bbea  babstracta  bmethodsa  bora  bnon-abstracta  bmethods.a  bthea  babstracta  bmethods,a  basa  bwella  basa  beverya  bclassa  bmembera  bthata  bisa  bmarkeda  basa  babstract,a  bmusta  bbea  bimplementeda  bina  bthea  bderiveda  bclass.a  bthea  bclassesa  bthata  barea  bmarkeda  bwitha  bthea  babstracta  bkeyworda  bhavea  bthea  bpurposea  bofa  bprovidinga  bthea  bprototypea  bfora  bthea  bderiveda  bclasses.a  bana  babstracta  bclassa  bcana  bhavea  baa  bconstructora  bimplemented.a  bana  bexamplea  bisa  bprovideda  bbelow:

![Image00110.jpg](images/Image00110.jpeg)a  b

Ina  bthea  bprovideda  bexample,a  bwea  bcana  bseea  bonea  babstracta  bclassa  bwitha  bthea  bnamea  banimal.a  bina  bthisa  bclass,a  btherea  bisa  bonlya  bonea  bmember,a  banda  bthata  bisa  bana  babstracta  bvoida  bmethoda  blegsnumber().a  bwhena  bthea  bmethoda  bisa  bmarkeda  basa  babstract,a  bita  bmeansa  bthata  beverya  bclassa  bderiveda  bfroma  bthata  bclass,a  basa  bina  bthisa  bcase,a  bana  banimala  bclass,a  bmusta  bhavea  bana  boverridea  bimplementationa  bofa  bthata  bmethod.a  bbelowa  bthea  babstracta  bclass,a  btherea  barea  btwoa  bmorea  bclasses,a  bwhicha  barea  bthea  b‘normal’a  bclasses.a  bbotha  bclassesa  bhavea  bthea  boverridea  bimplementationa  bofa  baa  blegsnumber()a  bmethoda  bfroma  bthea  banimala  bclass.a  bthata  bisa  bbecausea  bbotha  bthea  belephanta  banda  bpigeona  bclassesa  binherita  bfroma  bthea  banimala  bclass.a  binheritancea  bwilla  bbea  bexplaineda  bina  bdetaila  bina  baa  blatera  bchapter,a  bbuta  bfora  bnow,a  bthea  b‘:’a  bsymbola  bnexta  btoa  bthea  belephanta  banda  bpigeona  bclassa  bmeansa  bthata  btheya  binherita  bfroma  bthea  banimala  bclass.a  bina  bthisa  bcase,a  bthisa  bmeansa  bthata  btheya  bmusta  bhavea  btheira  bimplementationa  bofa  bthea  babstracta  bmethoda  bfroma  bthea  bbasea  bclass.a  bina  bthea  bmaina  bmethoda  bofa  baa  bprograma  bclass,a  btherea  bisa  baa  bdeclarationa  bofa  bana  banimala  btypea  bvariablea  bnameda  banimal.

Notea  bthata  btherea  bisa  bnoa  binstantiationa  bofa  bthea  banimala  bclassa  bbecausea  bthata  bisa  bnota  bpossible,a  banda  bthea  breasona  bisa  bthata  bthea  banimala  bclassa  bisa  bana  babstracta  bclassa  b-a  bsoa  bita  bcannota  bbea  binstantiated.a  bina  bthea  bnexta  bline,a  bthea  bprograma  bisa  binstantiatinga  bana  bobjecta  bofa  belephanta  bclassa  bintoa  bthea  banimala  btypea  bvariable.a  bthisa  bisa  balloweda  bbecausea  banimala  bisa  bthea  bbasea  bclassa  bofa  bthea  belephanta  bclass.a  baftera  bit,a  btherea  bisa  baa  bcalla  btoa  bthea  blegsnumbera  bmethoda  bfroma  bthea  banimala  bvariable.a  bfurthermore,a  bsincea  bthea  banimala  bisa  binstantiateda  btoa  bbea  bana  belephanta  btype,a  bthisa  bcalla  bexecutesa  bthea  blegsnumbera  bmethoda  bfroma  bthea  belephanta  bclass.a  bthea  bnexta  bthinga  bisa  bthea  binstantiationa  bofa  bthea  bpigeona  bobjecta  banda  bassigninga  bita  btoa  bthea  bsamea  banimala  bvariable.a  bita  bendsa  bupa  bwitha  bcallinga  bthea  blegsnumbera  bmethoda  bagaina  bfroma  bthea  banimala  bobject.a  bthisa  btimea  bimplementationa  bofa  bthea  blegsnumbera  bfroma  bthea  bpigeona  bclassa  bisa  bused.a  bthea  bconsolea  boutputa  bwilla  blooka  blikea  bthis:

![Image00111.jpg](images/Image00111.jpeg)a  b

Object

Objectsa  bina  bc#a  brepresenta  bthea  breala  bentitiesa  bina  bthea  bsystem,a  bwitha  balla  bofa  btheira  bclassa  btypea  bcharacteristicsa  banda  bfeatures.a  btheya  barea  blocateda  bsomewherea  bina  bmemorya  banda  bhavea  breferencea  bpointera  btoa  bit.a  bwhenevera  bthea  bkeyworda  bnewa  bisa  bused,a  bana  bobjecta  bina  bmemorya  bisa  bcreated.a  bobjectsa  bmusta  bbea  bofa  baa  bclassa  btype.a  beverya  bclassa  bwhicha  bisa  bcreateda  bina  bc#a  bprogramminga  blanguagea  bisa  bderiveda  bfroma  bthea  bsystem.objecta  bclassa  b(inheritancea  bwilla  bbea  bexplaineda  bina  blatera  bchapters).a  bthisa  bmeansa  bthata  btherea  bisa  baa  bbuilt-ina  bclassa  bobjecta  bina  bca  b#,a  banda  beverya  bobjecta  bofa  banya  btypea  bisa  bderiveda  bfroma  bthata  bclass.a  beverya  bobjecta  bcreated,a  bbesidesa  bitsa  bowna  bfunctionalities,a  balsoa  bhasa  bthea  bmethodsa  bthata  barea  bavailablea  bfroma  btheira  bparenta  bclassa  bobject.a  bthesea  bmethodsa  bare:a  bequals,a  btostring,a  bfinalize,a  banda  bgethashcode.a  bthisa  bcoulda  bbea  bcheckeda  bina  bthea  bexample:

![Image00112.jpg](images/Image00112.jpeg)a  b

Thisa  bexamplea  bisa  businga  bthea  bclassa  btshirt,a  bwhicha  bwasa  bshowna  bina  bthea  bpreviousa  bexamplea  bina  bclassa  bsubchapter.a  bina  bthea  bmaina  bmethod,a  bana  bobjecta  bofa  bthea  btshirta  bclassa  btypea  bisa  binstantiated.a  bthisa  bobjecta  bisa  breferenceda  bbya  bthea  btshirta  bvariable.a  bina  bthea  bseconda  bline,a  byoua  bcana  bseea  bthea  bavailablea  bmethodsa  banda  bpropertiesa  bthata  bcoulda  bbea  bexecuteda  bovera  bthea  btshirta  bobject.a  bbesidesa  bcolora  bpropertya  banda  bthea  babouta  bmethoda  bthata  barea  bparta  bofa  bthea  btshirta  bclass,a  btherea  barea  balsoa  bfoura  bmethodsa  bfroma  bthea  bparenta  bclassa  bobjecta  b(equals,a  bgethashcode,a  bgettype,a  btostring).

Interface

Anothera  bimportanta  bcomponenta  bina  bobject-orienteda  bprogramminga  bisa  bana  binterface.a  bana  binterfacea  brepresentsa  bmultiplea  bdeclarationsa  bofa  bsomea  bfunctionalities.a  baa  bclassa  bcana  bimplementa  bonea  bora  bmorea  binterfaces,a  bbuta  bita  bcana  bonlya  binherita  bfroma  bonea  bclassa  bora  babstracta  bclass.a  bthisa  brevealsa  banothera  bc#a  bprogramminga  blanguagea  bcharacteristica  b-a  bita  bdoesa  bnota  bsupporta  bmultiplea  binheritance.a  bclassesa  bthata  bimplementa  bsomea  binterfacea  bmusta  bprovidea  baa  bfulla  bdefinitiona  bofa  balla  binterfacea  bmembers.a  bina  bthea  binterfacea  busage,a  btherea  bisa  bnoa  bmanipulationa  bwitha  baccessa  bmodifiersa  basa  balla  bthea  binterfacea  bmembersa  barea  bconsidereda  btoa  bbea  bpublic.a  bthisa  bisa  bbecausea  binterfacea  bexistencea  bisa  balla  babouta  bitsa  bfunctionalitya  btoa  bbea  bimplementeda  bbya  bothera  bclasses.a  bifa  bsomea  bclassa  bmusta  bimplementa  binterfacea  bmembers,a  bita  bmeansa  bthata  bthea  binterfacea  bmembersa  bmusta  bbea  bpublica  btoa  bbea  bimplementeda  bbya  bothera  bclasses.a  bthea  binterfacea  bisa  bana  bobject-orienteda  bcomponenta  bthata  bhasa  bdeclarations,a  bbuta  bita  bcannota  bhavea  bdefinitionsa  b-a  bimplementations.a  bifa  byoua  btrya  btoa  binserta  bsomea  bimplementationsa  bina  bthea  binterface,a  bthea  bcompile-timea  berrora  bwilla  bappear.a  bthea  binterfacea  bcana  bcontaina  bpropertiesa  banda  bmethodsa  b-a  beverythinga  bthata  bcana  bhavea  bthea  bimplementation.a  bita  bcannota  bhavea  bfieldsa  banda  baa  bconstructora  b-a  bbecausea  bita  bisa  bnota  baa  bclass,a  banda  bita  bcannota  bbea  binstantiated.a  bona  bimplementationa  bofa  bthea  binterface,a  bthea  bclassa  bmusta  bimplementa  balla  bofa  bthea  binterfacea  bmembers.a  basa  bmentioned,a  bmultiplea  binheritancea  bisa  bnota  bsupporteda  bina  bc#,a  bbuta  bita  bcana  bbea  bachieveda  bwitha  binterfacea  busagea  bsincea  baa  bclassa  bcana  bimplementa  bmultiplea  binterfaces.a  bexample:

![Image00113.jpg](images/Image00113.jpeg)a  b

Herea  bwea  bhavea  bonea  binterfacea  bdefined.a  bita  bhasa  bthreea  bbooleana  bpropertiesa  binside.a  baa  bclassa  bthata  bwilla  bimplementa  bthisa  binterfacea  bmusta  bhavea  bthea  bdefinitiona  bofa  balla  bthesea  binterfacea  bmembers.

![Image00114.jpg](images/Image00114.jpeg)a  b

Thea  bprograma  bcontainsa  bonea  bclass,a  bwhicha  bisa  baa  bpersona  bclass.a  bthisa  bclassa  bimplementsa  bthea  bipersona  binterfacea  bthata  bhasa  bbeena  bdeclared.a  bthisa  bclassa  bhasa  btwoa  bprivatea  bstringa  bfields,a  bwhicha  barea  b_firstnamea  banda  b_lastname.a  bita  balsoa  bhasa  baa  bconstructora  bwherea  bthosea  bfielda  bvaluesa  barea  bassigned.a  bbesidesa  bthat,a  bthisa  bclassa  bhasa  bthea  bdefinitiona  bofa  bthreea  bmembersa  bofa  bthea  bipersona  binterfacea  b–a  bthea  bisrunning,a  bisstanding,a  banda  bissittinga  bproperties.a  bthea  bcompilera  bisa  bokaya  bwitha  bthis,a  basa  btherea  barea  bnoa  berrors.a  bbut,a  bifa  bwea  bremovea  banya  bofa  bthesea  bthreea  bpropertiesa  bfroma  baa  bpersona  bclass,a  bthea  bcompilera  bwoulda  breporta  bana  berror.a  bfora  bexample:

![Image00115.jpg](images/Image00115.jpeg)a  b

Here,a  bwea  bhavea  bcommenteda  bona  bthea  bisrunninga  bpropertya  bthata  bisa  binsidea  bthea  bpersona  bclass.a  bthea  bcompilera  bisa  breportinga  bana  berrora  bthata  bthea  bpersona  bclassa  bdoesa  bnota  bimplementa  bthata  bproperty,a  banda  bthea  bprograma  bcoulda  bnota  bbuild.a  baftera  bthis,a  bwea  bwilla  buncommenta  bthea  bpropertya  banda  breturna  btoa  bthea  bvalida  bstatea  bofa  baa  bprogram.a  bleta  busa  bcreatea  baa  bprograma  bclassa  bwitha  bthea  bmaina  bmethoda  binside.a  bthere,a  bwea  bwilla  bcreatea  bana  binstancea  bofa  baa  bpersona  bclassa  banda  bruna  bthea  bprograma  btoa  bchecka  bifa  beverythinga  bisa  bworkinga  bwell.

![Image00116.jpg](images/Image00116.jpeg)a  b

Now,a  bruna  bthea  bprogram:

![Image00117.jpg](images/Image00111.jpeg)a  b

Everythinga  bwenta  bsmoothly.

## Chaptera  b7:a  blinq,a  bqueries,a  boperatorsa  b–a  bxaml

Linq

Languagea  bintegrateda  bquery,a  bbettera  bknowna  basa  blinq,a  brepresentsa  bquerya  bsyntaxa  bina  bc#a  bprogramminga  blanguage,a  banda  bita  bisa  buseda  bfora  bretrievala  banda  bfilteringa  bofa  bthea  bdifferenta  bsourcesa  bofa  bobjects.a  blinqa  bproducesa  baa  bsinglea  bqueryinga  binterfacea  bfora  bvariousa  bkindsa  bofa  bobjectsa  banda  bvariables.a  bthisa  bquerya  bsyntaxa  bisa  bintegrateda  bintoa  bc#a  bprogramminga  blanguage,a  basa  bwella  basa  bina  bvisuala  bbasic.a  bfora  bbettera  bunderstanding,a  bwea  bwilla  bprovidea  bana  bexamplea  btoa  bexplaina  bita  bfurther.a  btherefore,a  byoua  bhavea  bsqla  basa  baa  bstructureda  bquerya  blanguage.a  bsqla  bisa  buseda  btoa  bgeta  banda  bsavea  bsomea  bdataa  bintoa  bthea  bdatabase.a  bita  bisa  baa  blanguagea  bdesigneda  btoa  bworka  bcloselya  bwitha  bthea  bdatabase.

Ina  bthea  bsamea  bwaya  basa  bsql,a  bthea  blinqa  bisa  buseda  btoa  bgeta  banda  bfiltera  bdifferenta  bdataa  bsourcesa  blikea  bcollections,a  bdataa  bsets,a  betc.a  btherea  barea  bmanya  bwaysa  byoua  bcana  busea  blinq;a  bita  bisa  buseda  btoa  bquerya  bobjecta  bcollections,a  badoa  b.neta  bdataa  bsets,a  bxmla  bdocuments,a  bentitya  bframeworka  bdataa  bsets,a  bsqla  bdatabasea  bdirect,a  banda  bothera  bdataa  bsourcesa  bbya  bimplementinga  bthea  biquerablea  binterface.a  blinqa  bisa  blikea  baa  bbridgea  bbetweena  bsomea  bdataa  banda  bvariablesa  bina  bthea  bprogram.a  beverya  blinqa  bquerya  breturnsa  bobjectsa  basa  baa  bresult.a  bita  bisa  bgooda  bbecausea  bita  benablesa  bthea  busea  bofa  bana  bobject-orienteda  bapproacha  btoa  bthea  bdataa  bset.a  bwhena  businga  blinq,a  byoua  bdoa  bnota  bhavea  btoa  bworrya  babouta  bconvertinga  bthea  bsetupsa  bofa  bdataa  bintoa  bobjects.a  blinqa  bprovidesa  baa  bwaya  btoa  bquerya  bdataa  bwherevera  bthata  bdataa  bcamea  bfrom.a  bita  bsupportsa  bthea  bcompile-timea  bsyntaxa  bcheckinga  bsoa  bthata  bifa  byoua  bmakea  baa  bmistakea  bwhilea  bcodinga  blinq,a  bthea  bcompilera  bwilla  binforma  byoua  bimmediately.a  blinqa  ballowsa  byoua  btoa  bquerya  beverya  bcollectiona  bsucha  basa  blist,a  barray,a  benumerablea  bclasses,a  betc.

Wea  barea  bheadinga  btoa  bthea  bexamplesa  bnow:

![Image00118.jpg](images/Image00118.jpeg)a  b

Ina  bthisa  bexample,a  bwea  bhavea  bonea  bclassa  bnameda  bcar.a  bina  bthea  bcara  bclass,a  btherea  barea  bthreea  bproperties,a  bwhicha  barea  bthea  btrunkcapacity,a  bisautomatic,a  banda  bisturbocharged.a  beverya  bpropertya  brepresentsa  bread-onlya  bproperty,a  banda  btheira  binitiala  bstatea  bisa  bseta  bina  bthea  bcara  bclassa  bconstructor.a  bthea  bconstructora  btakesa  bthreea  bparametersa  banda  bassignsa  btheira  bvaluesa  btoa  bthea  bpropertiesa  bmentioneda  babove.a  bina  bthea  bmaina  bmethod,a  bwea  barea  bcreatinga  baa  blista  bofa  bcara  bobjects.a  bthea  blista  bofa  bcara  bobjectsa  bisa  bpopulateda  bina  bthea  bdeclarationa  bpart,a  bcreatinga  bfivea  bcara  bobjectsa  bwitha  bdifferenta  bvaluesa  bfora  bthea  btrunkcapacity,a  bisautomatic,a  banda  bisturbochargeda  bproperties.a  baftera  bthat,a  bwea  bwoulda  bfiltera  bthea  blista  banda  btakea  bonlya  bcarsa  bthata  bhavea  bautomatica  btransmission.a  bthisa  bwilla  bbea  bdonea  bbya  businga  bthea  blinqa  bquery.a  bwea  barea  bcreatinga  bana  bobjecta  bnameda  bcarsthatareautomatica  banda  bfilteringa  bthea  bcarsa  blista  bwitha  blinq.a  bthena  bwea  bperforma  bthea  bwherea  blinqa  bextensiona  bmethoda  btoa  bgeta  bthea  bobjectsa  bthata  bwea  bneed.a  bhowa  bdoesa  bita  bwork?a  bina  bthea  bwherea  bmethod,a  bwea  barea  bdeclaringa  bana  biterativea  bvariablea  bthata  bwilla  bbea  buseda  bfora  bfilteringa  bconditions.

Thea  bvariablea  bina  bthisa  bexamplea  bisa  bs.a  bso,a  bwhata  bthea  bfiltera  bdoesa  bnexta  bisa  bthata  bfora  beverya  bsa  bobjecta  bina  bthea  bcarsa  blist,a  bita  bwilla  bgranta  busa  bthea  bobjecta  bwhosea  bs.isautomatica  bpropertya  bisa  bequala  btoa  btrue.a  bthisa  bwill,a  bina  bturn,a ![Image00120.jpg](images/Image00120.jpeg)bcreatea  baa  bfiltereda  bienumarblea  blist.a  bina  bordera  btoa  bmakea  bthisa  baa  blista  bofa  bexplicita  btypea  bobjects,a  bwea  bwilla  bdoa  bthea  bsimplea  btolist()a  bmethoda  bovera  bthea  bfiltereda  bienumerablea  blist.a  bthisa  bwilla  bcreatea  bana  bobjecta  bofa  blist<car>a  btypea  banda  bputa  bita  bdowna  btoa  bthea  bcarsthatareautomatica  bobject.a  bnow,a  bwea  bhavea  bthea  bdataa  bthata  bwea  bneed.a  bina  bthea  bend,a  bwea  bwilla  biteratea  bthrougha  bthea  bnewlya  bcreateda  bcollectiona  bofa  bcara  bobjectsa  banda  bprinta  bmessagesa  btoa  bthea  bconsolea  boutput.a  bfora  beverya  bobjecta  bina  bthea  blist,a  bwea  bwilla  bprinta  b“thea  bcara  bwitha  bthea  btrunka  bcapacitya  bofa  b{certaina  bcapacity}a  bisa  bautomatic”.a  bwea  bknowa  bthisa  bbecausea  bwea  bfiltereda  bthea  bcarsa  banda  btooka  bonlya  bthea  bonesa  bwhoa  bhavea  bautomatica  btransmission.a  bthea  boutputa  bofa  bthisa  bprograma  blooksa  blikea  bthis:

A  b![Image00119.jpg](images/Image00119.jpeg)

Asa  byoua  bcana  bsee,a  btherea  barea  btwoa  bcarsa  bwitha  bautomatica  btransmissiona  banda  btheira  bcapacitya  bisa  b100a  banda  b300a  brespectively.a  byoua  bcana  bchecka  bthata  bina  bthea  bcreationa  bofa  bthea  bcara  blista  bata  bthea  bbeginning,a  basa  bonlya  bthea  bfirsta  banda  bthea  bthirda  bcara  bhavea  btruea  bvaluea  bfora  bana  bisautomatica  bpropertya  bpasseda  bina  bthea  bobjecta  binstantiation.

![Image00121.jpg](images/Image00121.jpeg)anothera  bexamplea  bisa  bseena  bbelow:

A  b

Ina  bthisa  bexample,a  bwea  bhavea  baa  bclassa  bnameda  bperson.a  bthisa  bclassa  bhasa  bthreea  bproperties,a  bwhicha  barea  bsalary,a  bfirstname,a  banda  blastname.a  beacha  bpersona  bclassa  brepresentsa  bonea  bemployeea  bwitha  bitsa  bbasica  binformation.a  bthea  bobject’sa  bpropertiesa  barea  bassigneda  bina  bthea  bconstructor.a  bina  bthea  bmaina  bmethod,a  btherea  bisa  baa  bcreationa  bofa  baa  blista  bwitha  bobjectsa  bofa  bthea  bpersona  bclassa  btype.a  bwea  bhavea  baddeda  bfivea  bpersona  bobject,a  beacha  bwitha  bdifferenta  bsalarya  bamount,a  bfirsta  bname,a  banda  blasta  bname.a  bthea  bmanagera  bwantsa  btoa  bfiltera  bouta  beveryonea  bthata  bhasa  baa  bsalarya  bgreatera  bthana  b3000,a  banda  bthesea  bpeoplea  bwilla  bbea  bmarkeda  basa  bseniors.a  bwea  bwilla  bdoa  bthata  bwitha  bthea  blinqa  bquery.a  basa  bina  bthea  bpreviousa  bexample,a  bwea  barea  bfilteringa  bthea  bpeoplea  blista  bwitha  bthea  bwherea  bextensiona  bmethod.a  bina  bthisa  bmethod,a  bwea  barea  bdeclaringa  bthata  bwea  bwanta  bonlya  bthea  bpersona  bobjectsa  bthata  bhavea  baa  bsalarya  bgreatera  bthana  b3000.a  baftera  bthea  bretrievala  bisa  bdone,a  bthea  btolist()a  bmethoda  btakesa  bthea  bfiltereda  bienumerablea  blista  bintoa  bthea  bpersona  bobjectsa  blist.a  bnowa  bwea  bhavea  bana  bobjecta  bthata  bisa  baa  blista  bofa  bpersona  bclassa  btypes,a  banda  bita  bcontainsa  bonlya  bthea  bpeoplea  bwhoa  bhavea  baa  bsalarya  bgreatera  bthana  b3000.a  bthisa  bvariablea  bisa  bnameda  bseniors.a  bnowa  bthea  bmanagera  brequestsa  bthata  bhea  bwantsa  bthea  btotala  bsuma  bofa  bthea  bseniora  bsalaries.a  bwea  bwilla  bthena  bdoa  bthata  bbya  bcreatinga  baa  blista  bofa  bseniora  bsalariesa  banda  bthena  bsumminga  balla  bofa  bthata  bvaluesa  bintoa  bonea  bvariablea  banda  benda  bupa  bprintinga  bita  btoa  bthea  bstandarda  boutput.a  bthea  bcreationa  bofa  bthea  bseniorsalariesa  blista  bwilla  bbea  bdonea  bwitha  bthea  bexecutiona  bofa  bthea  bselecta  blinqa  bextensiona  bmethod.a  bthea  bselecta  bmethoda  bisa  buseda  bwhena  btherea  bisa  baa  bneeda  bfora  bgettinga  bonlya  bcertaina  bpropertya  bvaluesa  bfroma  baa  bcollectiona  bofa  bobjects.a  bina  bthisa  bcase,a  bwea  bneeda  bthea  bsalarya  bpropertya  bvaluea  bfroma  beacha  bofa  bthea  bobjectsa  binsidea  bthea  bseniorsa  blist.a  bthea  bselecta  bmethoda  bdoesa  bthea  bnext:a  bfora  beacha  bxa  bobjecta  bfroma  bthea  bseniorsa  blist,a  btakea  bx.salarya  bvalue.a  bthisa  bcreatesa  baa  blista  bofa  bienumerablea  bvalues.a  baftera  bthea  btolist()a  bmethoda  bexecution,a  bwea  bsucceededa  bina  bcreatinga  baa  blist<int>a  bobjecta  bthata  bcontainsa  belementsa  bthata  barea  bseniora  bsalaries.a  bthena  bwea  bcreateda  baa  bvariablea  bina  bwhicha  bwea  bwilla  bstorea  bthea  bsummationa  bofa  balla  bofa  bthea  bseniora  bsalariesa  b-a  bseniorsalariessuma  bvariable.a  baftera  bthisa  bisa  bdone,a  bwea  bhavea  bonea  bmorea  bstatementa  bthata  bwilla  bfinisha  bthea  bwork.a  bthea  bforeacha  bmethoda  bisa  bdonea  bovera  bthea  bseniorsalariesa  blist,a  bwhicha  bwilla  bgathera  banda  bsuma  balla  bsalariesa  bintoa  bonea  bvariablea  bseniorsalariessum.a  bina  bthea  bend,a  bthea  bprograma  bwilla  bprinta  bthea  bresulta  b-a  bseniorsalariessuma  bvaluea  btoa  bthea  bstandarda  boutput.a  bthea  boutputa  bofa  bthisa  bprograma  bwilla  blooka  blikea  bthis:

A  b

Thisa  blogica  banda  bsolutiona  btoa  bthea  bproblema  bcoulda  bbea  bmucha  bsimplified,a  banda  bthea  bseniora  bsalarya  bsuma  bcoulda  bbea  bdonea  bina  bjusta  bonea  blinea  bofa  bcode.a  bthata  blinea  bwilla  blooka  bsomethinga  blikea  bthis:

![Image00122.jpg](images/Image00122.jpeg)a  b

Aftera  bthea  bwherea  bmethoda  bisa  bbeinga  bexecuted,a  bthea  bselecta  bmethoda  bwoulda  bfollow,a  baftera  bwhicha  bthea  blista  bwilla  bbea  bcreateda  bovera  bwhicha  bwea  bcoulda  biteratea  bwitha  bthea  bforeacha  bextensiona  bmethoda  banda  bdoa  bthea  bsuma  bcalculation.a  bthisa  bwilla  bproducea  bthea  bexacta  bsamea  bresult.a  bthisa  blonga  bstatementa  bisa  bjusta  bsplita  bintoa  baa  bfewa  bsmallera  bonesa  bina  bthea  bstartinga  bsolutiona  bfora  bbettera  bunderstanding.a  bleta  busa  bclosea  bthisa  blinqa  bchaptera  bwitha  bonea  bmorea  bexample:

![Image00123.jpg](images/Image00123.jpeg)a  b

Ina  bthisa  bexample,a  bwea  bhavea  bmodifieda  bthea  bpersona  bclassa  bfroma  bthea  bpreviousa  bexample.a  bnow,a  bthea  bpersona  bclassa  bcontainsa  bthea  bsalarya  bpropertya  banda  bpersonalinformationa  bclassa  btypea  bproperty,a  banda  bbotha  barea  bassigneda  bina  bthea  bpersona  bclassa  bconstructor.a  bthea  bpersonalinformationa  bclassa  bcontainsa  bthreea  bread-onlya  bproperties.a  bthesea  bpropertiesa  barea  bfirstname,a  blastname,a  banda  bpersonalid.a  bfirstnamea  banda  blastnamea  barea  bofa  baa  bstringa  bdataa  btype,a  bwhilea  bthea  bpersonalida  bisa  bofa  bana  binta  bdataa  btype.a  bthesea  bthreea  bpropertiesa  barea  bassigneda  bina  bthea  bconstructora  bwhena  binstantiatinga  bthea  bobjecta  bofa  bpersonalinformationa  bclass.a  bnow,a  blet’sa  bjumpa  bintoa  bthea  bmaina  bmethoda  bofa  bthea  bprograma  bclass.a  bhere,a  bwea  barea  bagaina  bgoinga  btoa  bcreatea  baa  blista  bofa  bpersona  bobjects,a  banda  bita  bisa  bthea  bsamea  basa  bina  bthea  bpreviousa  bexample.a  bthough,a  bthisa  btimea  bisa  bgoinga  btoa  bbea  baa  bbita  bdifferenta  bbecausea  bofa  bthea  bclassa  bmodifications.a  bwea  barea  bcreatinga  bfivea  bpersona  bobjects,a  beacha  bofa  bthema  bwitha  bsalary,a  banda  bpersonalinformationa  bobjecta  bassigned.

Fora  beverya  bperson,a  bwea  bcreatea  baa  bpersonalinformationa  bobjecta  btoa  binstantiatea  bthea  bpersona  bobjecta  bcorrectly.a  beacha  bofa  bthea  bpersonalinformationa  bobjectsa  bhasa  bthea  bfirsta  bname,a  blasta  bname,a  banda  bpersonala  bida  bpasseda  btoa  bitsa  binstantiation.a  bthisa  bway,a  bwea  bcreateda  baa  bbita  bmorea  bcomplexa  bobjecta  bthata  bcontainsa  banothera  bclassa  bobjecta  binside.a  bok,a  bwea  barea  breadya  btoa  bgo.a  bthea  bmanagera  basksa  busa  btoa  bfinda  beverya  bfirsta  bnamea  bofa  bana  bemployeea  bwhoa  bisa  btreateda  basa  baa  bseniora  banda  bhasa  baa  bpersonala  bida  bofa  blessa  bthana  bonea  bhundreda  banda  bfifty.a  bfroma  bthea  bpreviousa  bexample,a  bwea  bhavea  backnowledgeda  bthata  bthea  bseniora  bisa  bthea  bpersona  bwitha  baa  bsalarya  bgreatera  bthana  bthreea  bthousanda  b(3000).a  bwea  barea  bdoinga  bsomethinga  bsimilara  btoa  bthea  bpreviousa  bexample,a  bbuta  bthisa  btime,a  bthea  bpersona  bclassa  bhasa  bchanged.a  bita  bdoesa  bnota  bhavea  bthea  bsamea  bstructurea  basa  bina  bthea  bpreviousa  bexample.a  bso,a  bwea  bmusta  banalyzea  bthea  bclassa  bstructurea  bfirsta  banda  bthena  bcreatea  baa  bsolution.a  bthea  bfirsta  bstepa  bisa  bthata  bwea  bmusta  bfiltera  bthea  bpersona  bobjectsa  bfroma  bthea  bpeoplea  blista  bthata  bhavea  baa  bsalarya  bgreatera  bthana  b3000.a  baftera  bthat,a  bwea  bmusta  btakea  bthea  bpersonalinformationa  bobjecta  bfroma  beverya  bpersona  bobjecta  btoa  bfinda  bthea  bfirsta  bnamesa  bofa  balla  bthea  bseniors.a  bthen,a  bwhena  bpersonalinformationa  bobjectsa  barea  bgathered,a  bwea  bmusta  bfiltera  bthema  banda  btakea  bonlya  bthea  bonesa  bwitha  bthea  bpersonalida  bthata  barea  blessa  bthana  b150.a  bwhena  bthata  btaska  bisa  bdone,a  bwea  bcana  bfinallya  bselecta  bthea  bfirstnamea  bpropertya  bofa  balla  bthea  bseniors,a  bmakea  baa  blista  bouta  bofa  bit,a  biteratea  bthrougha  bthata  blist,a  banda  bprinta  bthea  bfirstnamea  bvalues.a  balla  bofa  bthisa  bisa  bdonea  bina  bthea  blittlea  bcomplexa  blinqa  bquerya  bfroma  bwhicha  bwea  bcreatea  baa  bseniorslt150a  blista  bvariable.

Thea  bfirsta  bwherea  bmethoda  bcreatesa  bana  bienumerablea  blista  bofa  bseniors.a  bthen,a  bthea  bselecta  bmethoda  btakesa  bpersonalinformationa  bobjectsa  bfroma  bseniorsa  blista  banda  bmakesa  bana  bienumerablea  blista  bofa  bthea  bseniorsa  bpersonalinformationa  bobjects.a  bthea  bseconda  bwherea  bmethoda  bisa  bworkinga  bovera  bthea  bpersonalinformationa  bobjectsa  bfroma  bthea  bpreviouslya  bcreateda  bienumerablea  blist,a  banda  btherea  bwea  bwilla  bfiltera  bthea  bpersonalinformationa  bobjecta  bthata  bhasa  bpersonalida  bpropertya  blessa  bthana  b150.a  bfroma  bthere,a  bwea  barea  bdoinga  bthea  bselecta  bmethod,a  bwhicha  bgathersa  bthea  bfirstnamea  bpropertya  bvaluea  bfora  beacha  bofa  bthea  bseniorsa  bpersonalinformationa  bobjectsa  bthata  bhasa  bpersonalida  blessa  bthana  b150.a  bina  bthea  bend,a  bwea  bthena  bexecutea  bthea  btolist()a  bmethoda  bovera  bthea  bfinala  bienumerablea  bthata  bwea  bcreated,a  banda  bthea  bfinala  bproducta  bisa  bthea  blista  bofa  bstringsa  bthata  bcontaina  bthea  bfirsta  bnamea  bofa  beverya  bseniora  bwitha  baa  bpersonala  bida  blessa  bthana  b150.a  bwhena  balla  bofa  bthisa  bisa  bfinallya  bqueried,a  bwea  bcana  bruna  bthrougha  bthea  blista  banda  bprinta  bthosea  bnamesa  btoa  bthea  bconsole.a  bthea  bonlya  bseniora  bwhoa  bwilla  bmeeta  bthesea  bcriteriaa  bisa  bmikea  bdean,a  banda  bhisa  bfirsta  bnamea  bwilla  bbea  bprinteda  btoa  bthea  bstandarda  boutput.a  bthea  bprograma  bconsolea  boutputa  bisa  bbelow:

![Image00124.jpg](images/Image00124.jpeg)a  b

## Chaptera  b8:a  bprograma  btoa  bmakea  bdecision

Decisiona  bmaking

Nota  balla  bproblemsa  barea  bsolveda  blinearly,a  bsometimesa  bita  bisa  bnecessarya  btoa  bhavea  btoa  bmakea  baa  bdecisiona  bora  bexecutea  bspecifica  bactionsa  bwhena  baa  bconditiona  bisa  bmet,a  banda  bothersa  bwhena  bita  bdoesa  bnot.a  bleta  busa  bsupposea  bthata  boura  bproblema  bisa  btoa  bmaintaina  bthea  btemperaturea  bofa  baa  bbucketa  bofa  bwarma  bwater.a  btoa  bdoa  bthis,a  bwea  bcana  badda  bhota  bora  bcolda  bwater.a  bina  bthisa  bproblem,a  bwea  bwoulda  bneeda  btoa  bdecidea  bwhata  bkinda  bofa  bwatera  btoa  badd.

Similarly,a  btherea  barea  bmanya  bproblemsa  bthata  bwea  bneeda  btoa  bknowa  baa  bconditiona  bora  bmakea  baa  bdecisiona  bona  bhowa  btoa  bsolvea  bthem.a  bina  bc#,a  bita  bisa  beasya  btoa  bachievea  bthisa  bsincea  bthea  blanguagea  bprovidesa  busa  bwitha  bdifferenta  btoolsa  btoa  bcopea  bwitha  bit.a  bwea  bwilla  bhavea  btoa  busea  bexpressions,a  banda  bthesea  bwilla  bbea  bevaluated.a  bina  bthisa  bcase,a  bwea  bwilla  busea  brelationala  bexpressions,a  banda  blogicala  bexpressions,a  bwhicha  bwilla  bbea  bevaluated,a  banda  bdependinga  bona  bthea  bresulta  bofa  bthata  bevaluation,a  bspecifica  bstepsa  bofa  bthea  balgorithma  bora  bothersa  bwilla  bbea  bcarrieda  bout.a  blet’sa  bstarta  bbya  bknowinga  bthea  bexpressionsa  bwea  bneed.

Makinga  bchoicesa  banda  bdecisions

Whilea  bwea  barea  bina  bthea  bc#a  blanguage,a  bwea  bneeda  btoa  btakea  bsomea  btimea  btoa  bworka  bwitha  bthea  bdecisiona  bcontrola  bstatementsa  bora  bconditionala  bstatements.a  bthesea  barea  bgoinga  btoa  bbea  bthea  btypesa  bofa  bcodesa  bthata  bcana  btakea  bthea  binputa  bfroma  bthea  buser,a  bcomparea  bita  btoa  bthea  bconditionsa  bthata  byoua  bseta  bwithina  bthea  bcode,a  banda  bthena  bwilla  bmakea  bsomea  bimportanta  bdecisionsa  bona  bitsa  bowna  bbaseda  bona  bbotha  bofa  bthese.

Therea  bwilla  bbea  btimesa  bwhena  byoua  bwritea  boutcode,a  banda  byoua  bwanta  btoa  bmakea  bsurea  bthata  bthisa  bprograma  bcana  bhandlea  bsomea  bdecisionsa  bona  bitsa  bown.a  byoua  bcana  bchoosea  btoa  bwritea  bita  bouta  bsoa  bthata  btherea  barea  bspecifica  bconditionsa  btoa  bfinda  bina  bthea  bcodea  baheada  bofa  btime,a  banda  bthena  bthea  bcodea  bcana  bresponda  bbaseda  bona  bthea  binputa  bthata  bthea  busera  bhasa  baddeda  bintoa  bthea  bcomputer.

Thea  bgooda  bnewsa  bwitha  bthisa  bonea  bisa  bthata  btherea  barea  baa  bfewa  boptionsa  bthata  byoua  bcana  bchoosea  bfroma  bwitha  bthesea  bconditionala  bstatements.a  beacha  bonea  bisa  bgoinga  btoa  bworka  bina  baa  bslightlya  bdifferenta  bmannera  bbaseda  bona  bwhata  byoua  barea  bhopinga  btoa  bgeta  bouta  bofa  bthea  bprograma  basa  bwell,a  banda  bhowa  byoua  bwoulda  blikea  bita  btoa  bresponda  btoa  bdifferenta  binputsa  bfroma  bthea  buser.a  basa  bwea  bgoa  bthrougha  bthea  bdifferenta  boptions,a  byoua  bwilla  bbettera  bbea  bablea  btoa  bseea  bhowa  beacha  bonea  bworksa  banda  bwhya  bita  bisa  bsucha  baa  bgreata  boptiona  bfora  byoua  btoa  bchoosea  bonea  bofa  bthema  balonga  bthea  bway.a  blet’sa  bdivea  bina  banda  btakea  baa  blooka  bata  bsomea  bofa  bthea  bmaina  bconditionala  bstatementsa  bavailablea  bina  bthea  bc#a  blanguage,a  blearna  bhowa  beacha  bonea  bisa  bgoinga  btoa  bwork,a  banda  bexplorea  bsomea  bofa  bthea  bbasicsa  bofa  bcodinga  bwitha  bthema  basa  bwell.

Aa  blooka  bata  bthea  bifa  bstatement

Thea  bfirsta  bkinda  bofa  bconditionala  bstatementa  bthata  bwea  bwanta  btoa  btakea  baa  blooka  bata  bherea  bisa  bknowna  basa  boura  bifa  bstatement.a  bouta  bofa  balla  bthea  bconditionala  bstatementsa  bthata  bwea  bwilla  blooka  bthrough,a  bthisa  bonea  bisa  bgoinga  btoa  bbea  bthea  bmosta  bbasic.a  bita  bdoesa  bmissa  bouta  baa  bbita  bona  bsomea  bofa  bthea  bfunctionalitya  bthata  bwea  bwilla  bseea  bwitha  bthesea  bstatements,a  bbuta  bita  bdoesa  bhelpa  busa  btoa  blearna  bmorea  babouta  bconditionala  bstatementsa  banda  bcana  bbea  busefula  bina  bsomea  bsituationsa  basa  bwell,a  bsoa  bita  bisa  bimportanta  btoa  blearn.

Whena  byoua  bhandlea  bthisa  bifa  bstatement,a  byoua  bwilla  bfinda  bthata  bwhena  bita  bruns,a  bthea  bcodea  bwilla  bonlya  bprovidea  busa  bwitha  baa  breplya  basa  blonga  basa  bthea  busera  bgivesa  busa  bana  binputa  bthata  bmatchesa  bwitha  bthea  bconditionsa  bthata  barea  bseta  bina  bthea  bcode.a  bwhena  bthisa  bdoesa  bhappen,a  bthena  bthea  bcodea  bwilla  bbea  bablea  btoa  bexecute,a  banda  bita  bwilla  busuallya  bcomea  bupa  bwitha  bsomea  bkinda  bofa  bmessage,a  bdependinga  bona  bwhata  bthea  bprogrammera  bputsa  bintoa  bthea  bcode.a  bsometimesa  byoua  bwilla  bseta  bita  bupa  btoa  bexecutea  bsomethinga  belsea  basa  bwell.

However,a  bifa  bthea  busera  bcomesa  bthrougha  banda  bputsa  bina  bana  binputa  bthata  bdoesa  bnota  bmatcha  bupa  bwitha  bthea  bconditionsa  bthata  bwea  bseta  bup,a  bthena  btherea  bwilla  bbea  bnothinga  bthata  bshowsa  bupa  bona  bthea  bscreen.a  bthisa  bcana  bcausea  bsomea  bproblems,a  bwhicha  bisa  bwhya  bthea  bifa  bstatementa  bmaya  bnota  bbea  buseda  basa  bmucha  basa  bsomea  bofa  bthea  bothera  boptions.

Thea  bgooda  bnewsa  bouta  bofa  balla  bofa  bthisa  bisa  bthata  byoua  bwilla  bfind,a  bevena  basa  baa  bbeginner,a  bthata  bthesea  bifa  bstatementsa  barea  beasya  btoa  bseta  bupa  banda  bworka  bwith.a  blet’sa  btakea  baa  blooka  bata  bthea  bcodinga  bbelowa  btoa  bseea  bhowa  bwea  bcana  bcreatea  bonea  bofa  bthesea  bifa  bstatementsa  bina  bthea  bc#a  blanguagea  bfora  boura  bowna  bneeds:a  bifa  b(xa  b>a  b0)

{

Console.write(“thea  bvaluea  bisa  bpositive.”);

}

Witha  bthea  bexamplea  bthata  bwea  blisteda  babove,a  bcertaina  bthingsa  bneeda  btoa  bhappen.a  bifa  bthea  bvaluea  bthata  bthea  busera  bputa  bsina  bisa  bhighera  bthana  bzero,a  bthena  bthea  bprograma  bisa  bseta  bupa  btoa  bprinta  boffa  b“thea  bvaluea  bisa  bpositive”.a  bhowever,a  bifa  bthea  bexpressiona  bturnsa  bouta  btoa  bbea  bfalse,a  bora  bthea  binputa  bisa  blessa  bthana  bzero,a  bthena  bthea  bprograma  bwilla  bignorea  bthea  bwholea  bstatementa  bthata  bcomesa  baftera  bconsole.a  bwritea  banda  bwilla  bmovea  bon.

Aa  blooka  bata  bthea  bifa  belsea  bstatement

Asa  bwea  bcana  btella  bprettya  bquicklya  bwhena  bwea  bworka  bwitha  bthea  bifa  bstatement,a  btherea  bwilla  bbea  bmanya  bsituationsa  bwherea  bthesea  bstatementsa  barea  bnota  bgoinga  btoa  bbea  bablea  btoa  bhelpa  busa  bgeta  bthingsa  bdonea  bina  bthea  bmannera  bthata  bwea  bwant.a  byoua  bdoa  bnota  bwanta  btoa  bseta  bupa  bsomea  bcodesa  bthata  barea  bnota  bstronga  benougha  btoa  bhandlea  bthea  bworka  bthata  byoua  bwant.a  bita  bisa  bnevera  baa  bgooda  bideaa  btoa  bseta  bupa  baa  bcodea  bwherea  bthea  busera  bcana  bputa  bina  bsomething,a  banda  bthena  bthea  bprograma  bjusta  bendsa  bora  bfreezesa  bup.a  banda  bthisa  bisa  bwherea  bwea  bwilla  btakea  baa  blooka  bata  baa  bnewa  bconditionala  bstatement,a  bknowna  basa  bthea  bif-elsea  bstatement.

Thea  bif-elsea  bstatementa  bisa  bgoinga  btoa  bbea  baa  bnicea  bonea  btoa  bworka  bwitha  bbecausea  bita  baddsa  bina  baa  btona  bofa  bpowera  btoa  bthea  bcodea  bthata  bwea  barea  bdoinga  banda  bwriting,a  bwhilea  bstilla  ballowinga  busa  btoa  badda  bina  bmorea  bthana  bonea  boptiona  banda  bhandlea  bprettya  bmucha  banythinga  bthata  bthea  busera  bwilla  badda  btoa  bthea  bprogram.a  bsometimesa  bwea  bwilla  bonlya  badda  bina  bonea  bora  btwoa  boptions,a  bbuta  bsometimesa  bwea  bcana  busea  bthea  bif-elsea  bstatementa  btoa  bhandlea  baa  btona  bofa  boptionsa  balonga  bthea  bwaya  basa  bwell.

Toa  bgeta  btoa  bthea  bpoint,a  bwea  bneeda  btoa  btakea  baa  blooka  bata  bthea  bsyntaxa  bfora  bthea  bif-elsea  bstatementa  bsoa  bwea  bgeta  baa  bbettera  bunderstandinga  bofa  bhowa  bthisa  bwilla  bworka  bina  bthea  bc#a  blanguage.a  baa  bgooda  bexamplea  bofa  bthea  bsyntaxa  bfora  bthisa  bonea  bwilla  bbea  bbelowa  bifa  b(thea  bbooleana  bexpression)

{thea  bstatement/sa  byoua  bwanta  btoa  bruna  bifa  bthea  bresulta  bisa  btrue;

}

Else

{thea  bstatement/sa  byoua  bwanta  btoa  bruna  bifa  bthea  bresulta  bisa  bfalse;

}

Asa  byoua  bcana  balreadya  bseea  bwitha  bthisa  bone,a  btherea  bisa  bgoinga  btoa  bbea  baa  blota  bmorea  bpowera  bthata  bcomesa  bwitha  bthea  bif-elsea  bstatement.a  bthisa  bisa  baa  bbasica  boptiona  bwitha  bthea  bif-elsea  bstatement,a  bbuta  byoua  bcana  badda  bina  bsomea  bmorea  blinesa  btoa  bmakea  bita  bmorea  bpowerful.a  bwitha  bthese,a  bif-elsea  bstatements,a  bifa  bthea  banswera  bisa  bfalse,a  byoura  bcodea  bwilla  bgoa  bona  btoa  bthea  bnexta  bparta  bofa  bthea  bstatementa  btoa  bseea  bwhethera  bora  bnota  bthata  bonea  bisa  btrue.a  bifa  btherea  barea  bmorea  bthana  btwoa  boptions,a  bita  bwilla  bkeepa  bgoinga  bdowna  bthea  bif-elsea  bstatementa  buntila  bthea  banswera  bturnsa  bouta  btrue,a  banda  bthena  bita  bwilla  bgoa  banda  bdisplaya  bthea  bmessagea  bthata  bcomesa  bup.

Nowa  bthata  bwea  bhavea  btakena  bsomea  btimea  btoa  btalka  babouta  bit,a  bita  bisa  btimea  btoa  blooka  bata  bana  bexamplea  bofa  bhowa  bthisa  bwilla  bworka  bsoa  byoua  bcana  busea  bita  bina  byoura  bcodes:

Ifa  b(a  bxa  b>a  b0)

{

Console.write(“thisa  bvaluea  bwilla  bbea  bpositive.”);

}

Else

{

Console.write(“thea  bvaluea  bisa  blessa  bthana  bora  bequala  btoa  bzero.”)

}

Youa  barea  bgoinga  btoa  bfinda  bthata  bwhena  bwea  bworka  bwitha  bthea  bexamplea  babove,a  bthea  belsea  bclausea  bisa  bgoinga  btoa  bbea  bimportant,a  bora  bata  bleasta  bhiddena  buntila  bthea  bbooleana  bexpressiona  bendsa  bupa  bbeinga  bfalse.a  bita  bisa  btherea  bwhena  bthea  bprocessa  bwilla  bneeda  bthea  belsea  bstatement.a  bbuta  bifa  bwea  benda  bupa  bgettinga  btruea  bvalue,a  bthena  bthea  bfirsta  bstatementa  bwilla  bbea  bthea  bonea  bthata  bwilla  bshowa  bupa  bsoa  bwea  bwon’ta  bneeda  bthea  belsea  bstatementa  bata  ball.

Whata  bthea  bnesteda  bconditionala  bstatementa  bisa  balla  babout

Anya  btimea  bthata  bwea  blooka  bthrougha  bsomea  bofa  bthea  bnewa  bcodesa  bthata  bcomea  bwitha  bc#,a  byoua  bshoulda  bfinda  bthata  bita  bisa  beasiera  btoa  bworka  bwitha  btwoa  bstatementsa  bthata  bwea  bhada  babove,a  bora  byoua  bcana  bcombinea  bthema  btoa  bmakea  baa  bnesteda  bconditionala  bstatementa  bfora  bsomea  bofa  byoura  bcodesa  basa  bwell.a  bwitha  baa  bnesteda  bconditionala  bstatement,a  bwea  barea  bgoinga  btoa  btakea  bonea  bofa  bthea  btypesa  bofa  bconditionala  bstatementsa  babovea  banda  bplacea  bita  binsidea  bofa  banothera  bone.a  bthea  bpointa  bofa  bdoinga  bthisa  bisa  btoa  badda  bina  bsomea  bmorea  bcomplexitya  btoa  bthea  bworka  bthata  bwea  bwanta  btoa  bseea  bwitha  bcodinga  banda  bcana  breallya  bgivea  busa  baa  bchaina  bofa  bconditionsa  bwhena  btheya  barea  bneeded.

Thea  bmaina  bthinga  bthata  bwea  bhavea  btoa  bfocusa  bona  bwhena  bita  bcomesa  btoa  bhandlinga  banya  bnesteda  bconditionala  bstatementa  bisa  bthata  bifa  btherea  bisa  bsomea  bmistakea  bthata  bhappensa  bwhena  byoua  bwritea  bouta  bthea  bstatement,a  bita  bisa  bgoinga  btoa  bcausea  bana  berrora  bina  bthea  bwholea  bthing,a  banda  bita  bcana  btakea  bsomea  btimea  btoa  bfix.a  bthisa  bmakesa  bthema  baa  bbita  bdifficulta  btoa  bhandlea  banda  bworka  bwitha  balonga  bthea  bway,a  bsoa  bbea  bcareful.

Thea  bneata  bthinga  babouta  bthem,a  bthough,a  banda  bsomethinga  bthata  bwilla  bmakea  bthema  bprettya  bappealinga  bisa  bthata  btheya  ballowa  busa  btoa  badda  bina  basa  bmany,a  bora  basa  bfew,a  blevelsa  basa  bwea  bwoulda  blike.a  bevena  bwitha  bthisa  bina  bmind,a  bmosta  bprofessionalsa  bina  bthisa  blanguagea  bwilla  brecommenda  bthata  bthea  bnesteda  bstatementsa  bstaya  barounda  bthreea  blevelsa  bora  blessa  bsoa  bthata  btheya  bdon’ta  bbecomea  btooa  bbiga  bofa  baa  bmessa  balonga  bthea  bway.

Ifa  byoua  bdoa  benda  bupa  bgoinga  bpasta  bthea  bthirda  blevela  bwhena  bworkinga  bona  bthesea  bstatements,a  bthena  byoua  bmaya  benda  bupa  bwitha  bsomethinga  bthata  bisa  bunrulya  banda  bdoesn’ta  bbehavea  bina  bthea  bmannera  bthata  byoua  bwoulda  blikea  banda  bmaya  bnota  bevena  bwork.a  basa  baa  bbeginner,a  bsticka  bwitha  bthea  bthreea  blevelsa  banda  bgoa  bupa  btoa  bmorea  basa  byoua  bgeta  bbettera  bwitha  bthea  bcoding.

Therea  barea  bmanya  bcodesa  bthata  byoua  barea  bablea  btoa  bwritea  bthata  bwilla  brelya  bona  bthesea  bconditionala  bstatements.a  btheya  bhelpa  byoua  btoa  bmakea  bthea  bcodea  bstrongera  banda  bwilla  bensurea  bthata  bwea  barea  bablea  btoa  bhandlea  bsomea  bofa  bthea  binputsa  bthata  boura  busersa  bgivea  btoa  bus,a  bevena  bifa  bwea  barea  bnota  bablea  btoa  bguessa  baheada  bofa  btimea  bwhata  banswera  bthea  busera  bisa  bgoinga  btoa  badda  btoa  bthea  bprogram.a  bthesea  bcana  bbasea  bthea  binputa  boffa  banya  bconditionsa  bthata  bwea  bseta  banda  bwilla  bensurea  bthata  bthea  bprograma  bisa  bgoinga  btoa  bbehavea  bina  bthea  bmannera  bthata  bwea  bwoulda  bprefer.a  bthisa  bmakesa  bita  bsoa  bmucha  beasiera  bfora  busa  btoa  bseea  bresultsa  banda  bfora  busa  btoa  bmakea  bsurea  bthea  bprograma  bworksa  bthea  bwaya  bthata  bwea  bwant.

## Chaptera  b9:a  bnet

Thea  b.neta  bframework

Programsa  bthata  barea  bwrittena  bouta  bina  bthisa  bkinda  bofa  bframeworka  barea  bgoinga  btoa  bbea  bablea  btoa  bexecutea  bitselfa  bina  bthea  benvironmenta  bfora  bthea  bsoftwarea  brathera  bthana  bthea  bhardwarea  benvironment,a  bknowna  basa  bthea  bclra  bora  bcommona  blanguagea  bruntime.a  bthea  bclra  bisa  bgoinga  btoa  bbea  bana  bapplicationa  bvirtuala  bmachinea  bthata  bwilla  bhelpa  btoa  bprovidea  busa  bwitha  bsomea  bdifferenta  bservices,a  bincludinga  bsecurity,a  bexceptiona  bhandling,a  banda  bmemorya  bmanagement.a  bbecausea  bofa  bthis,a  bthea  bcodesa  bthata  barea  bwrittena  bwitha  bthisa  bframeworka  bisa  bgoinga  btoa  bbea  bknowna  basa  bmanageda  bcode.a  bbotha  bthea  bclra  banda  bthea  bfcla  bthata  bwea  bhavea  btalkeda  babouta  barea  bgoinga  btoa  bmakea  bupa  bthea  b.neta  bframeworka  bthata  bwea  barea  btalkinga  babout.

First,a  bthea  bfcla  bisa  bgoinga  btoa  bbea  bimportant.a  bita  bprovidesa  busa  bwitha  bsomea  bofa  bthea  busera  binterface,a  bdatabasea  bconnectivity,a  bdataa  baccess,a  bweba  bapplicationa  bdevelopment,a  balgorithms,a  bnetworka  bcommunication,a  banda  bmore.a  bprogrammersa  bcana  bproducea  bsomea  bsoftwarea  bwhena  btheya  bcombinea  bthea  bsourcea  bcode;a  btheya  barea  bworkinga  bona  bwitha  bthea  b.neta  bframeworka  banda  bsomea  bofa  bthea  bothera  bavailablea  blibraries.

Thisa  bisa  baa  bframeworka  bthata  bisa  bdesigneda  btoa  bworka  bwella  bwitha  bmosta  bnewa  bapplicationsa  bthata  bwea  bwanta  btoa  bcreatea  bona  bthea  bwindowsa  bplatform.a  bina  baddition,a  bmicrosofta  bisa  bgoinga  btoa  bproducea  bana  bidea  bthata  bisa  bspecificallya  bfora  bthea  b.neta  bsoftwarea  bthata  bisa  bknowna  basa  bvisuala  bstudio.

Therea  barea  baa  blota  bofa  bthingsa  bthata  bwea  bcana  bworka  bwitha  bwhena  bita  bcomesa  btoa  bthea  b.neta  bframework.a  bsomea  bmethodsa  bhavea  bbeena  bdevelopeda  btoa  bworka  bnota  bonlya  bona  bthea  bwindowsa  bsystemsa  bbuta  balsoa  bwitha  bsomea  bofa  bthea  bothera  boperatinga  bsystems,a  bincludinga  blinuxa  banda  bmac.a  banda  bita  bcana  bhelpa  busa  bworka  bwitha  baa  bvarietya  bofa  blanguages,a  bespeciallya  bwitha  bc#,a  bwhilea  bbeinga  bportable,a  bsecure,a  bhigha  bina  bperformance,a  banda  bgooda  bwitha  bmanaginga  bthea  bmemorya  bthata  bwea  bneeda  bwhilea  bwritinga  bouta  bcertaina  bcodes.

Ina  bordera  btoa  bbea  bablea  btoa  bprograma  beffectivelya  bwitha  bc#,a  bonea  bneedsa  baa  blittlea  btheoreticala  bbackgrounda  bknowledge,a  bwhicha  bconcernsa  bthea  bso-called.neta  bframework.a  bthat’sa  bwhya  bthe.neta  bframeworka  bisa  bana  bintegrala  bparta  bofa  bthisa  bbook.a  bbeforea  bwea  bgeta  bmorea  binvolveda  bwitha  bthe.neta  bframework,a  byoua  bshoulda  bknowa  bthata  bita  bisa  bana  bintegrala  bparta  bofa  b.neta  btechnology.

Thea  btaska  bofa  baa  bruntimea  benvironmenta  bisa  bessentiallya  btoa  bexecutea  bthea  bcodea  bdevelopeda  bwitha  bthea  brespectivea  bprogramminga  blanguage.a  bina  bthea  bpast,a  bhowever,a  baa  bseparatea  bruntimea  blibrarya  b(runtimea  blibrary)a  busuallya  bhada  btoa  bbea  bprovideda  bfora  beacha  bprogramminga  blanguagea  b-a  banda  bina  bparta  balsoa  bfora  beacha  bversiona  b-a  bina  bordera  btoa  bbea  bablea  btoa  bexecutea  bthea  bcorrespondinga  bprograms.a  bfora  bexample,a  bca  b++a  bthea  bfilea  bmsvcrt.dlla  banda  bina  bvisuala  bbasica  b6,a  bthea  bfilea  bmsvbvm60.dll.a  bthea  bconceptsa  bofa  bthea  bsupplieda  bruntimea  benvironmentsa  bwerea  banda  barea  bstilla  bfundamentallya  bdifferenta  btoday.a  bcross-languagea  bsupporta  bprovidesa  bkeya  bbenefitsa  bofa  bthe.neta  bframework:

Onlya  bonea  bframeworka  bisa  bneeded.

Differenta  b(anda  bverya  bdifferent)a  bprogramminga  blanguagesa  bcana  bbea  bused,a  bdependinga  bona  bthea  blevela  bofa  bknowledgea  banda  bpersonala  bpreference.

Therea  bisa  bexactlya  bonea  bruntimea  benvironmenta  bfora  balla  bprogramminga  blanguages.

Froma  bthesea  badvantages,a  bfurthera  bderivationsa  bcana  bbea  bmade:

Thea  bcross-linguala  bintegration

Thea  bcross-languagea  bexceptiona  bhandlinga  b(exceptiona  bhandlinga  brefersa  btoa  bhowa  baa  bprograma  bshoulda  breacta  bwhena  beventsa  boccura  bthata  barea  bgenerallya  bnota  bexpected,a  bsucha  basa  berrors.)

Improveda  bsecuritya  b(securitya  bcana  bbea  bcontrolleda  bupa  btoa  bthea  bmethoda  blevel)

Simplifieda  bversioninga  b(severala  bversionsa  bcana  bexista  bsidea  bbya  bside)

Becausea  bthe.neta  bframeworka  bprovidesa  baa  bcross-languagea  bruntimea  benvironment,a  bita  bensuresa  binteractiona  banda  boptimala  bcollaborationa  bbetweena  bcomponentsa  bofa  bdifferenta  bprogramminga  blanguages.

Youa  bnowa  bknowa  bthata  bthe.neta  bframeworka  bisa  bparta  bofa  b.neta  btechnologya  banda  bwhata  bita  bhasa  btoa  bdo.a  bthe.neta  bframeworka  bagaina  bconsistsa  bofa  bthreea  bmaina  bcomponents:

Commona  blanguagea  bruntimea  b-a  bthea  bcross-languagea  bruntimea  benvironment

Classa  blibrariesa  b(learna  bmorea  babouta  bclassesa  banda  bclassa  blibrariesa  blater)

Asp.neta  b-a  bserver-sidea  bapplicationsa  bfora  bthea  bworlda  bwidea  bweb

Ina  bthisa  bbook,a  bwea  bwilla  bdeala  bina  bdetaila  bwitha  bthesea  bthreea  bcomponents.a  bthea  bcommona  blanguagea  bruntimea  banda  bclassa  blibrariesa  bwilla  bcomea  bupa  bagaina  banda  bagaina  bthroughouta  bthea  bbook,a  basa  bwilla  basp.neta  bina  bthea  bcontexta  bofa  bweba  bservices.a  bthea  btwoa  bcomponentsa  b-a  bcommona  blanguagea  bruntimea  banda  bclassa  blibrariesa  b-a  bofa  bthe.neta  bframeworka  barea  balsoa  breferreda  btoa  basa  bbasea  bframework.

Discovera  b.net

Thea  b.neta  bframeworka  bisa  baa  bsolutiona  btoa  balla  bthea  bproblemsa  binvolveda  bina  bthea  bdevelopmenta  bofa  bapplications,a  bprovidinga  bgreata  bbenefitsa  bnota  bonlya  btoa  bthea  bdevelopera  bbuta  balsoa  btoa  bthea  bdevelopmenta  bprocess.a  bfirsta  bofa  ball,a  b.neta  ballowsa  busa  btoa  bworka  bwitha  bexistinga  bcode;a  bwea  bcana  busea  bcoma  bcomponents,a  banda  beven,a  bina  bthea  bsituationa  bwherea  bwea  bneeda  btoa  busea  bthea  bwindowsa  bapi.a  bwhena  bthea  b.neta  bprograma  bisa  bready,a  bita  bisa  bmucha  beasiera  btoa  binstalla  bona  bthea  bclient’sa  bcomputera  bthana  btraditionala  bapplicationsa  bsincea  bita  bhasa  baa  bstronga  bintegrationa  bbetweena  blanguages.

Aa  bc#a  bprogrammera  bcana  beasilya  bunderstanda  bthea  bcodea  bofa  baa  bvisuala  bbasica  b.neta  bprogrammer,a  banda  bbotha  bcana  bprograma  bina  bthea  blanguagea  btheya  barea  bmosta  bcomfortablea  bwith.a  bthisa  bisa  bbecausea  balla  bthea  blanguagesa  bthata  bmakea  busea  bofa  b.neta  bsharea  bthea  b.neta  blibraries,a  bsoa  bita  bdoesa  bnota  bmattera  bina  bwhicha  blanguagea  bwea  bprograma  bin,a  bwea  bcana  brecognizea  bita  bina  banya  blanguage.a  bnext,a  bwea  bwilla  bknowa  bthea  bdifferenta  bcomponentsa  bofa  b.net:a  bcommona  blanguagea  bruntimea  b(clr),a  bassembly,a  banda  bcommona  bintermediatea  blanguagea  b(cil).

Clr

Thea  bfirsta  bcomponenta  bofa  b.neta  bthata  bwea  bwilla  bknowa  bisa  bthea  bcommona  blanguagea  bruntime,a  balsoa  bcalleda  bclr.a  bthisa  bisa  bana  bexecutiona  bprograma  bcommona  btoa  balla  blanguages.a  bthisa  bprograma  bisa  bina  bchargea  bofa  breadinga  bthea  bcodea  bgenerateda  bbya  bthea  bcompilera  banda  bstartsa  bitsa  bexecution.a  bita  bdoesa  bnota  bmattera  bifa  bthea  bprograma  bwasa  bcreateda  bwitha  bc#,a  bvisuala  bbasica  b.net,a  bora  bsomea  bothera  b.neta  blanguage,a  bthea  bclra  breadsa  bita  banda  bexecutesa  bit.

Assembly

Whena  bwea  bhavea  baa  bprograma  bwrittena  bina  baa  b.neta  blanguage,a  banda  bwea  bcompilea  bit,a  bthea  bassemblya  bisa  bgenerated.a  bthea  bassemblya  bcontainsa  bcila  bina  bthea  bcompileda  bprograma  banda  balsoa  bthea  binformationa  babouta  balla  bthea  btypesa  bthata  barea  buseda  bina  bthea  bprogram.

Cil

Thea  b.neta  bprogramsa  barea  bnota  bcompileda  bdirectlya  bintoa  bcompilera  bassemblya  bcode;a  binstead,a  btheya  barea  bcompileda  bintoa  bana  bintermediatea  blanguagea  bknowna  basa  bcil.a  bthisa  blanguagea  bisa  breada  banda  bexecuteda  bbya  bthea  bruntime.a  bthea  busea  bofa  bcila  banda  bruntimea  bisa  bwhata  bgivesa  b.neta  bitsa  bgreata  bflexibilitya  banda  bitsa  babilitya  btoa  bbea  bmultiplatform.

Thea  bframeworka  bofa  b.neta  bhasa  bcommona  blanguagea  bspecificationsa  bora  bcls.a  bthesea  bspecificationsa  barea  bthea  bguidelinesa  bthata  banya  blanguagea  bthata  byoua  bwanta  btoa  busea  b.neta  bmusta  bmeeta  btoa  bbea  bablea  btoa  bworka  bwitha  bthea  bruntime.a  bonea  badvantagea  bofa  bthisa  bisa  bthata  bifa  boura  bcodea  bcompliesa  bwitha  bthea  bcls,a  bwea  bcana  bhavea  binteroperabilitya  bwitha  bothera  blanguages,a  bfora  bexample,a  bita  bisa  bpossiblea  btoa  bcreatea  baa  blibrarya  bina  bca  b#,a  banda  baa  bvisuala  bbasica  b.neta  bprogrammera  bcana  busea  bita  bwithouta  banya  bproblem.

Onea  bofa  bthea  bmosta  bimportanta  bpointsa  bofa  bthesea  bguidelinesa  bisa  bthea  bctsa  bora  bcommona  btypea  bsystem.a  bina  bprogramminga  blanguages,a  bwhena  bwea  bwanta  btoa  bsavea  binformation,a  bita  bisa  bplaceda  bina  baa  bvariable,a  bthea  bvariablea  bwilla  bhavea  baa  btypea  bdependinga  bona  bthea  binformationa  btoa  bsave,a  bfora  bexample,a  bthea  btypea  bcana  bbea  btoa  bsavea  bana  binteger,a  bthea  bothera  btoa  bstorea  baa  bnumbera  bwitha  bdecimalsa  banda  bthea  bothera  btoa  bsavea  baa  bphrasea  bora  bword.a  bthea  bproblema  bwitha  bthisa  bisa  bthata  beacha  blanguagea  bstorea  binformationa  bdifferently.a  bsomea  blanguagesa  bstorea  bintegersa  bwitha  b16-bita  bmemorya  banda  bothera  bwitha  b32-bit;a  bevena  bsomea  blanguages,a  bsucha  basa  bca  banda  bc++,a  bdoa  bnota  bhavea  baa  btypea  bfora  bstoringa  bstringsa  bora  bphrases.

Toa  bsolvea  bthis,a  bthea  b.neta  bframeworka  bdefinesa  bthrougha  bctsa  bhowa  bthea  btypesa  bwilla  bworka  bina  btheira  benvironment.a  banya  blanguagea  bthata  bworksa  bwitha  b.neta  bmusta  busea  bthea  btypesa  basa  boutlineda  bina  bthea  bcts.a  bnowa  bthata  bwea  bknowa  bthea  bbasica  bconcepts,a  banda  bwea  bcana  bseea  bhowa  balla  bthisa  bcomesa  btogether.

Howa  btoa  bcreatea  baa  b.neta  bapplication

Wea  bcana  bcreatea  baa  b.neta  bapplicationa  businga  baa  bprogramminga  blanguage.a  bfora  bthisa  bpurpose,a  bita  bwilla  bbea  bc#;a  bwitha  bthisa  bprogramminga  blanguage,a  bwea  bcana  bcreatea  bthea  bsourcea  bcodea  bofa  bthea  bprograma  b(instructionsa  bthata  btella  bthea  bprograma  bwhata  btoa  bdo).

Whena  bwea  bhavea  bfinisheda  bwitha  boura  bsourcea  bcode,a  bthena  bwea  bhavea  btoa  busea  bthea  bcompiler.a  bthea  bcompilera  btakesa  bthea  bsourcea  bcodea  banda  bcreatesa  bana  bassemblya  bfora  bus.a  bthisa  bassemblya  bwilla  bhavea  bthea  bequivalenta  bofa  boura  bcode,a  bbuta  bwrittena  bina  bcil,a  bleadinga  busa  btoa  banothera  badvantagea  bofa  b.neta  b-a  bthea  bcompilera  bcana  boptimizea  boura  bcodea  bfora  bthea  bplatforma  bwherea  bwea  barea  bgoinga  btoa  busea  bthea  bprogram,a  bthata  bmeansa  bthea  bsamea  bprograma  bcana  bbea  boptimizeda  bfora  baa  bmobilea  bdevice,a  baa  bnormala  bpca  bora  baa  bserver,a  bwithouta  bmakinga  banya  bchangesa  btoa  bit.

Thea  b.neta  bframeworka  bcana  bbea  bruna  bona  bmanya  bplatforms,a  bnota  bjusta  bona  bwindows.a  bthisa  bmeansa  bthata  bwea  bcana  bprograma  bona  baa  bparticulara  bplatform,a  banda  bifa  banothera  bplatforma  bhasa  bthea  bruntime,a  boura  bprograma  bwilla  bruna  bwithouta  banya  bproblem.a  baa  b.neta  bprograma  bdevelopeda  bina  bwindowsa  bcana  bbea  bexecuteda  bina  blinux,a  basa  blonga  basa  bita  bhasa  bthea  bcorrespondinga  bruntime.

Whena  bwea  bwanta  btoa  binvokea  bthea  bprogram,a  bthena  bthea  bruntimea  bgetsa  bintoa  bthea  baction,a  breadsa  bthea  bassembly,a  banda  bcreatesa  bthea  bentirea  benvironmenta  bfora  bus.a  bthea  bruntimea  bstartsa  breadinga  bthea  bcila  binstructionsa  bfroma  bthea  bassemblya  banda  bcompilesa  bthema  basa  bita  breadsa  bthema  bfora  bthea  bmicroprocessora  bofa  bthea  bcomputera  bona  bwhicha  bthea  bprograma  bisa  brunning;a  bthisa  bisa  bknowna  basa  bjita  bora  bjust-in-timea  bcompilation.a  bina  bthisa  bway,a  bthea  bprograma  badvancesa  bina  bexecution,a  banda  bita  bisa  bcompiled;a  balla  bthisa  boccursa  btransparentlya  bfora  bthea  buser.

Thea  bjita  bcompilera  bisa  balsoa  bknowna  basa  bjitter.a  bita  bisa  bparta  bofa  bthea  bruntimea  banda  bisa  bverya  befficienta  bifa  bthea  bprograma  bneedsa  btoa  bre-runa  baa  bcodea  bthata  bhasa  balreadya  bbeena  bcompiled,a  bthea  bjittera  binsteada  bofa  brecompiling,a  brunsa  bwhata  bhasa  balreadya  bbeena  bcompiled,a  bthusa  bimprovinga  bperformancea  banda  bresponsea  btimesa  bfora  bthea  buser.

Fora  bthea  bprogramsa  bthata  barea  brunning,a  bthea  b.neta  bframeworka  bprovidesa  bthea  bservicesa  bofa  bmemorya  bmanagementa  banda  bgarbagea  bcollection.a  bina  bunmanageda  blanguagesa  bsucha  basa  bca  banda  bc++,a  bthea  bprogrammera  bisa  bresponsiblea  bfora  bmemorya  bmanagement.a  bina  blargea  bprograms,a  bthisa  bcana  bbea  baa  bcomplicateda  btask,a  bwhicha  bcana  bleada  btoa  berrorsa  bduringa  bprograma  bexecution.a  bfortunately,a  bmanageda  blanguagesa  blikea  bc#,a  bhavea  baa  bmodela  bina  bwhicha  bwe,a  basa  bprogrammers,a  bnoa  blongera  bneeda  btoa  bbea  bresponsiblea  bfora  bmemorya  busage.a  bthea  bgarbagea  bcollectora  bisa  bina  bchargea  bofa  bremovinga  balla  bobjectsa  bthata  barea  bnoa  blongera  bneededa  bwhena  bana  bobjecta  bisa  bnoa  blongera  busea  bthea  bcollectora  btakesa  bita  banda  bremovesa  bit.a  bthisa  bfreesa  bupa  bmemorya  banda  bresources.

Thea  bgarbagea  bcollectora  bworksa  bautomaticallya  bfora  busa  banda  bhelpsa  btoa  beliminatea  balla  bthea  bmemorya  banda  bresourcea  bmanagementa  bthata  bwasa  bnecessarya  bfora  bwin32.a  bina  bsomea  bspeciala  bcases,a  blikea  bfiles,a  bdatabases,a  bora  bnetworka  bconnectionsa  barea  bunmanageda  bresources.a  bfora  bthesea  bcases,a  bwea  bmusta  bexplicitlya  bindicatea  bwhena  btheya  bneeda  btoa  bbea  bdestroyed.

## Chaptera  b10:a  benuma  banda  bstruct

Enum

Ana  benuma  b(whicha  bstandsa  bfora  benumerateda  btype)a  bisa  baa  bspeciala  bdataa  btypea  bthata  ballowsa  bprogrammersa  btoa  bprovidea  bmeaningfula  bnamesa  bfora  baa  bseta  bofa  bintegrala  bconstants.

Toa  bdeclarea  bana  benum,a  bwea  busea  bthea  benuma  bkeyworda  bfolloweda  bbya  bthea  bnamea  bofa  bthea  benum.a  bthea  bmembersa  bofa  bthea  benuma  barea  bencloseda  bina  baa  bseta  bofa  bcurlya  bbracesa  banda  bseparateda  bbya  bcommas.

Ana  bexamplea  bisa  bshowna  bbelow:

Enuma  bdaysofweek

{

Sun,a  bmon,a  btues,a  bwed,a  bthurs,a  bfri,a  bsat

}

Notea  bthata  bwea  bdoa  bnota  bputa  baa  bsemi-colona  bata  bthea  benda  bofa  bthea  blasta  bmember.

Aftera  bdeclaringa  bthea  bdaysofweeka  benum,a  bwea  bcana  bdeclarea  banda  binitializea  baa  bdaysofweeka  bvariablea  blikea  bthis:

Daysofweeka  bmydaysa  b=a  bdaysofweek.mon;

Thea  bnamea  bofa  bthea  bvariablea  bisa  bmydays.a  bifa  bwea  bwrite

Console.writeline(mydays);

We’lla  bget,

Mon

Bya  bdefault,a  beacha  bmembera  bina  bthea  benuma  bisa  bassigneda  bana  bintegera  bvalue,a  bstartinga  bfroma  bzero.a  bthata  bis,a  bina  boura  bexample,a  bsuna  bisa  bassigneda  baa  bvaluea  bofa  b0,a  bmona  bisa  b1,a  btuesa  bisa  b2,a  banda  bsoa  bon.

Asa  bmembersa  bofa  bana  benuma  barea  bessentiallya  bintegers,a  bwea  bcana  bcasta  baa  bdaysofweeka  bvariablea  bintoa  bana  binta  banda  bvicea  bversa.a  bfora  binstance,

Console.writeline((int)mydays);

Givesa  busa  bthea  bintegera  b1a  bwhile

Console.writeline((daysofweek)1);

Givesa  busa  bmon.

Ifa  byoua  bwanta  btoa  bassigna  baa  bdifferenta  bseta  bofa  bintegersa  btoa  byoura  benuma  bmembers,a  byoua  bcana  bdoa  bthea  bfollowing

Enuma  bdaysofweektwo

{

Suna  b=a  b5,a  bmona  b=a  b10,a  btues,a  bwed,a  bthurs,a  bfri,a  bsat

}

Now,a  bsuna  bisa  bassigneda  baa  bvaluea  bofa  b5,a  banda  bmona  bisa  bassigneda  b10.a  basa  bwea  bdida  bnota  bassigna  bvaluesa  bfora  btuesa  btoa  bsat,a  bconsecutivea  bnumbersa  baftera  b10a  bwilla  bbea  bassigneda  btoa  bthem.a  bthata  bisa  btuesa  b=a  b11,a  bweda  b=a  b12,a  banda  bsoa  bon.

Ofa  bcourse,a  bifa  byoua  busea  baa  bbytea  bdataa  btype,a  byoua  bcannota  bdoa  bsomethinga  blike

Enuma  bdaysofweekfoura  b:a  bbyte

{

Suna  b=a  b300,a  bmon,a  btues,a  bwed,a  bthurs,a  bfri,a  bsat

}

Asa  bthea  brangea  bfora  bbytea  bisa  bfroma  b0a  btoa  b255.

Therea  barea  btwoa  bmaina  breasonsa  bfora  businga  benums.a  bthea  bfirsta  bisa  btoa  bimprovea  bthea  breadabilitya  bofa  byoura  bcode.a  bthea  bstatement

Mydaysa  b=a  bdaysofweek.mon;

Isa  bmorea  bself-explanatorya  bthana  bthea  bstatement

Mydaysa  b=a  b1;

Thea  bseconda  breasona  bisa  btoa  brestricta  bthea  bvaluesa  bthata  baa  bvariablea  bcana  btake.a  bifa  bwea  bhavea  baa  bvariablea  bthata  bstoresa  bthea  bdaysa  bofa  baa  bweek,a  bwea  bmaya  baccidentallya  bassigna  bthea  bvaluea  b10a  btoa  bit.a  bthisa  bcana  bbea  bpreventeda  bwhena  bwea  busea  bana  benuma  basa  bwea  bcana  bonlya  bassigna  bthea  bpre-defineda  bmembersa  bofa  bthea  benuma  btoa  bthea  bvariable.

Struct

Now,a  blet’sa  blooka  bata  bthea  bstructa  bdataa  btype.

Aa  bstructa  bisa  bsimilara  btoa  baa  bclassa  bina  bmanya  baspects.a  blikea  bclasses,a  btheya  bcontaina  belementsa  blikea  bproperties,a  bconstructors,a  bmethodsa  banda  bfieldsa  banda  ballowa  byoua  btoa  bgroupa  brelateda  bmembersa  bintoa  baa  bsinglea  bpackagea  bsoa  bthata  byoua  bcana  bmanipulatea  bthema  basa  baa  bgroup.

Toa  bdeclarea  baa  bstruct,a  byoua  busea  bthea  bstructa  bkeyword.a  bana  bexamplea  bis:

1a  bstructa  bmystruct

2a  b{

3a  b//fields

4a  bprivatea  binta  bx,a  by;

5a  bprivatea  banotherclassa  bmyclass;

6a  bprivatea  bdaysa  bmydays;

7

8a  b//constructor

9a  bpublica  bmystruct(inta  ba,a  binta  bb,a  binta  bc)

10a  b{

11a  bmyclassa  b=a  bnewa  banotherclass();

12a  bmyclass.numbera  b=a  ba;

13a  bxa  b=a  bb;

14a  bya  b=a  bc;

15a  bmydaysa  b=a  bdays.mon;

16a  b}

17

18a  b//method

19a  bpublica  bvoida  bprintstatement()

20a  b{

21a  bconsole.writeline(“xa  b=a  b{0},a  bya  b=a  b{1},a  bmydaysa  b=a  b{2}“,a  bx,a  by,a  bmydays);

22a  b}

23a  b}

24

25a  bclassa  banotherclass

26a  b{

27a  bpublica  binta  bnumber;

28a  b}

29

30a  benuma  bdaysa  b{a  bmon,a  btues,a  bweda  b}

Thea  bstructa  bisa  bdeclareda  bfroma  blinesa  b1a  btoa  b23.a  bona  blinea  b4,a  bwea  bdeclareda  btwoa  bprivatea  binta  bfieldsa  bfora  bthea  bstruct.a  bona  blinea  b5,a  bwea  bdeclareda  banothera  bprivatea  bfielda  bcalleda  bmyclass.a  bthisa  bfielda  bisa  bana  binstancea  bofa  bthea  bclassa  banotherclass.a  bona  blinea  b6,a  bwea  bdeclareda  bana  benuma  bvariablea  bmydays.a  bthea  btwoa  bfieldsa  b(myclassa  banda  bmydays)a  barea  bspeciallya  bincludeda  bina  bthisa  bexamplea  btoa  bdemonstratea  bhowa  bwea  bcana  bincludea  baa  bclassa  binstancea  banda  bana  benuma  bvariablea  basa  bthea  bfieldsa  bofa  baa  bstruct.a  bstructsa  b(anda  bclasses)a  bcana  bcontaina  benuma  bvariablesa  banda  binstancesa  bofa  bothera  bstructsa  banda  bclassesa  basa  bfields.

Aftera  bdeclaringa  bthea  bfields,a  bwea  bdeclareda  bthea  bconstructora  bfora  bthea  bstructa  b(linesa  b9a  btoa  b16),a  bfolloweda  bbya  baa  bmethoda  btoa  bprinta  bthea  bvaluesa  bofa  bx,a  by,a  banda  bmydays.a  b(linesa  b19a  btoa  b22).

Aftera  bdeclaringa  bthea  bstruct,a  bwea  bdeclareda  bthea  bclassa  banotherclassa  bona  blinesa  b25a  btoa  b28a  banda  bthea  benuma  bdaysa  bona  blinea  b30.a  bina  bthisa  bexample,a  bwea  bdeclareda  bthea  bclassa  banda  benuma  boutsidea  bthea  bstructa  bmystruct.a  bhowever,a  bwea  bcana  bdeclarea  bthea  benuma  bora  bclassa  binsidea  bthea  bstructa  bitself.a  bana  benum,a  bstruct,a  bora  bclassa  bcana  bbea  bnesteda  binsidea  banothera  bstructa  bora  bclass.a  bwe’lla  blooka  bata  bana  bexamplea  bofa  bana  benuma  bdeclareda  binsidea  baa  bclassa  bwhena  bwea  bworka  bthrougha  bthea  bprojecta  bata  bthea  benda  bofa  bthea  bbook.

Toa  busea  bthea  bstructa  babove,a  bwea  bcana  badda  bthea  bfollowinga  bcodea  btoa  boura  bmain()a  bmethod:

Mystructa  bexamplea  b=a  bnewa  bmystruct(2,a  b3,a  b5);

Example.printstatement();

Ifa  bwea  bruna  bthea  bcode,a  bwe’lla  bget

Xa  b=a  b3,a  bya  b=a  b5,a  bmydaysa  b=a  bmon

Therea  barea  btwoa  bmaina  bdifferencesa  bbetweena  baa  bstructa  banda  baa  bclass.a  bfirstly,a  bthea  bstructa  bdataa  btypea  bdoesa  bnota  bsupporta  binheritance.a  bhencea  byoua  bcannota  bderivea  bonea  bstructa  bfroma  banother.a  bhowever,a  baa  bstructa  bcana  bimplementa  bana  binterface.a  bthea  bwaya  btoa  bdoa  bita  bisa  bidenticala  btoa  bhowa  bita  bisa  bdonea  bwitha  bclasses.a  brefera  btoa  bchaptera  b8a  bfora  bmorea  binformation.

Thea  bseconda  bdifferencea  bbetweena  bstructsa  banda  bclassesa  bisa  bthata  bstructsa  barea  bvaluea  btypesa  bwhilea  bclassesa  barea  breferencea  btypes.

Fora  baa  bcompletea  blista  bofa  bdifferencesa  bbetweena  baa  bstructa  banda  baa  bclass,a  bchecka  bouta  bthea  bfollowinga  bpage:

[https://msdn.microsoft.com/en-us/library/saxz13w4.aspx](https://msdn.microsoft.com/en-us/library/saxz13w4.aspx)a  b

Chaptera  b11:a  bcommona  bmistakea  banda  bhowa  btoa  bavoida  bthem

Thisa  bguidebooka  bhasa  btakena  bsomea  btimea  btoa  blooka  bthrougha  balla  bofa  bthea  bdifferenta  bpartsa  bofa  bcodinga  bthata  bwea  bneeda  btoa  bknowa  btoa  butilizea  bthea  bc#a  blanguagea  btoa  bwritea  bsomea  bofa  boura  bcodes.

Therea  barea  baa  blota  bofa  bdifferenta  baspectsa  bthata  bwea  bneeda  btoa  bkeepa  bina  bminda  bwhena  bita  bcomesa  btoa  bworkinga  bona  bthisa  blanguage,a  bbuta  bwhena  bwea  bcana  bputa  bita  balla  btogether,a  bwea  bwilla  bfinda  bthata  bwea  bcana  bcreatea  bsomea  bgreata  bcodesa  banda  bprogramsa  bina  bthea  bprocess.

Evena  bthougha  bmanya  bofa  bthea  bmoderna  bcodinga  blanguagesa  bthata  barea  bouta  btherea  bhavea  bbeena  bdesigneda  btoa  bmakea  bprogramminga  beasiera  bfora  bthosea  bwhoa  barea  bbeginners,a  btherea  barea  bstilla  baa  bnumbera  bofa  bchallengesa  bthata  barea  bgoinga  btoa  bshowa  bupa  bwhena  byoua  bfirsta  bgeta  bstarted.

Onea  bofa  bthea  bthingsa  bthata  baa  bbeginnera  bhasa  btoa  bremembera  bwhena  btheya  bgoa  bthrougha  bthisa  bprocessa  bisa  bthata  btheya  bdoa  bneeda  btoa  bpractice,a  banda  btheya  bneeda  btoa  blearna  bfroma  btheira  bmistakesa  banda  bfroma  bsomea  bofa  bthea  bproblemsa  bthata  bshowa  bupa  bina  btheira  bcoding.

Evena  btakinga  baa  bbreaka  bisa  boftena  benougha  btoa  bhelpa  byoua  bgeta  bgoinga  bona  bthisa  banda  bcana  bensurea  bthata  byoua  bwon’ta  bburna  bouta  banda  bhavea  btroublea  bwitha  bthea  bprocessa  blatera  bon.

Somea  bofa  bthea  bmistakesa  byoua  bshoulda  bavoida  bincludes:

Nota  bgettinga  benougha  bpractice

Therea  barea  baa  btona  bofa  bcodesa  banda  bsuggestionsa  banda  bthingsa  btoa  blearna  babouta  bina  bthisa  bguidebook,a  bbuta  bifa  byoua  bdon’ta  bactuallya  bopena  bupa  bthea  bcompilera  bwitha  bc#a  banda  btrya  bsomea  bofa  bita  bout,a  byoua  barea  bnevera  bgoinga  btoa  bgaina  bthea  bskillsa  banda  bmorea  bthata  byoua  bneeda  btoa  bmakea  bthisa  bworka  bfora  byou.

Thata  bisa  bwhya  bthea  bfirsta  brulea  bthata  bwea  bneeda  btoa  bfollowa  bherea  bisa  btoa  bplaya  barounda  bwitha  bthea  bcodea  banda  bgeta  basa  bmucha  bpracticea  basa  bpossible.

Witha  banya  bofa  bthea  bnewa  bsubjectsa  bthata  bwea  bwanta  btoa  bexplorea  banda  blearna  babouta  bina  banya  bcodinga  blanguage,a  bthea  bsoonera  bthata  bwea  bcana  bgeta  boura  bhandsa  bdirtya  banda  bstarta  bmessinga  barounda  bwitha  bthea  bcode,a  bthea  bfastera  bthata  bwea  bcana  blearna  bsomea  bofa  bthea  bconceptsa  bthata  barea  bthere.

Youa  bcan’ta  bgoa  bthrougha  banda  breada  bthea  binformationa  bwithouta  businga  bita  baa  bbit,a  banda  bthena  bexpecta  bthata  byoua  bwilla  bremembera  bthata  binformationa  banda  bbea  bablea  btoa  butilizea  bthea  bcodea  bfora  byoura  bprograms.

Youa  bhavea  btoa  bmessa  bwitha  bthea  bcodea  banda  bseea  bhowa  bita  bworks.

Now,a  byoua  bwilla  bfinda  bthata  bthea  bbesta  bplacea  bfora  busa  btoa  bgeta  bstarteda  bwitha  bthisa  btipa  bisa  bjusta  btoa  bopena  bupa  boura  bc#a  bcompilera  banda  bstarta  btoa  bdoa  bsomea  bofa  bthea  bcodingsa  bthata  bwea  bwanta  brighta  baway.

Takea  bsomea  bofa  bthea  bexamplesa  bthata  barea  bina  bthisa  bguidebooka  banda  bjusta  bmessa  barounda  bwitha  bthema  baa  bbit.

Evena  bjusta  btypinga  bthema  bintoa  bthea  bcompilera  btoa  bstarta  bwitha  bisa  baa  bgooda  bstepa  bina  bthea  brighta  bdirectiona  banda  bwilla  bensurea  bthata  bwea  bcana  bgeta  bsomea  bpractice.

Youa  bcana  bthena  bworka  banda  bexplorea  bfroma  btherea  btoa  bgeta  bthea  brighta  bresults.

Ignoringa  bthea  bfundamentals

Evena  bthougha  bita  bsometimesa  bseemsa  blikea  bthea  bfundamentalsa  barea  bgoinga  btoa  bbea  btooa  bbasica  btoa  bworka  bwith,a  banda  byoua  bmaya  bfeela  blikea  byoua  bshoulda  bjusta  bracea  bthrougha  bthema  bwithouta  baa  bthought,a  bita  bisa  bstilla  bimportanta  btoa  bspenda  boura  btimea  blearninga  babouta  bhowa  bthisa  bwork.

Asa  beasya  basa  btheya  bare,a  btheya  barea  breallya  bimportanta  btoa  bworka  bwitha  basa  bwell.

Thea  bbettera  bthata  bwea  bcana  bworka  bwitha  bthesea  bfundamentals,a  bthea  beasiera  bita  bisa  bfora  busa  btoa  bstarta  bmasteringa  bsomea  bofa  bthea  bmorea  badvanceda  bstuffa  bthata  bisa  bgoinga  btoa  bshowa  bup.

Thosea  bprogrammersa  bwhoa  btrya  btoa  bgeta  bintoa  baa  bprogramminga  blanguagea  banda  bthena  brusha  bthrougha  bthea  bbeginninga  bpartsa  banda  bdoa  bnota  bspenda  bthea  bpropera  btimea  bona  bsomea  bofa  bthea  bfundamentalsa  barea  bgoinga  btoa  bbea  bthea  bfirsta  bonesa  bwhoa  bgeta  bstucka  bwhena  btheya  bneeda  btoa  bmakea  bthea  btransitiona  binta  bsomea  bofa  bthea  badvanceda  bmateriala  bthata  bwilla  bcomea  blater.

So,a  bbeforea  byoua  bmissa  bouta  bona  bsomea  bofa  bthea  bfirsta  bclassesa  bthata  bwea  bneeda  bherea  banda  bskipa  bthrougha  bsomea  bofa  bthea  bbasicsa  bthata  barea  bimportanta  bina  balla  bofa  bthis,a  bmakea  bsurea  btoa  blearna  bmorea  babouta  bthea  bfundamentalsa  banda  bwhata  bwea  bcana  bdoa  bwitha  bita  balonga  bthea  bway.

Nota  bwritinga  bita  bout

Ita  bisa  bnormala  btoa  bwanta  btoa  bgeta  bstarteda  bwitha  bprogramminga  banda  btoa  bopena  bupa  bthea  bcompilera  banda  bstarta  bcoding.

Anda  bwhilea  bthisa  bisa  bonea  bofa  bthea  bmethodsa  btoa  buse,a  bsometimesa  btryinga  bita  bouta  bina  baa  bdifferenta  bmanner,a  banda  bwritinga  bita  bbya  bhanda  brathera  bthana  btryinga  btoa  btypea  bita  bina  balla  bofa  bthea  btimea  bisa  bgoinga  btoa  bbea  bthea  btricka  bthata  bwilla  bhelpa  busa  btoa  bgeta  bthisa  bdone.

Bringinga  bouta  bthea  bpena  banda  bpapera  btoa  bwritea  bouta  boura  bcodesa  bwilla  bhelp.

Therea  barea  baa  btona  bofa  badvancesa  btoa  bthea  bcomputersa  bouta  bthere,a  banda  bthey’rea  baa  blota  bofa  bbenefitsa  btoa  businga  bit.

Buta  bsometimesa  bthea  bbesta  bwaya  btoa  blearna  bsomethinga  bnewa  bisa  bactuallya  btoa  bwritea  bita  bouta  banda  bworka  bfroma  bthere.

Whethera  byoua  bdecidea  btoa  busea  bsomea  bscrapa  bpaper,a  baa  bnotebook,a  baa  bwhiteboard,a  bora  banothera  boption,a  btakinga  bthea  btimea  btoa  bcodea  bouta  beverythinga  bbya  bhanda  bisa  bgoinga  btoa  btakea  bmorea  btimea  btoa  bworka  bwith.

Therea  bisa  bthea  brequirementa  btoa  busea  bmorea  bcaution,a  bprecision,a  banda  bevena  bintenta  bbehinda  balla  bofa  bthea  blinesa  bofa  bcodea  bthata  byoua  btrya  btoa  bwritea  bout.

Youa  balsoa  barea  bnota  bablea  btoa  bchecka  bouta  bthea  bcodea  bwhena  bwritinga  bita  blikea  byoua  bcana  bona  bthea  bcomputer,a  bwhicha  bforcesa  byoua  btoa  bpaya  bmorea  battention.

Thisa  bmethoda  bisa  bgoinga  btoa  btakea  bmorea  btimea  banda  bbea  breallya  bconsuminga  bwhena  bita  bisa  btimea  btoa  bgeta  bthingsa  bdone.

Buta  bita  bisa  bgoinga  btoa  bbea  baa  bgreata  bmethoda  bthata  bhelpsa  busa  btoa  bgoa  bthrougha  banda  bbecomea  baa  bbettera  bdevelopera  bina  bthea  bprocess.

Anda  bifa  byoua  bplana  btoa  busea  bthisa  bthrougha  bcollegea  bora  bfora  baa  bnewa  bjob,a  bbeinga  bablea  btoa  bwritea  bouta  bthea  bcodesa  bthata  byoua  barea  businga  banda  butilizea  bthisa  bfora  byoura  bneedsa  bisa  bgoinga  btoa  bbea  bsoa  bimportanta  btoa  bthea  bsuccessa  bthata  byoua  barea  bablea  btoa  bseea  basa  bwell.

Thea  bmorea  btimea  banda  bpracticea  bthata  byoua  barea  bablea  btoa  bgivea  btoa  bwritinga  bouta  bsomea  bofa  byoura  bcodesa  bbya  bhand,a  bthea  bbettera  byoua  bwilla  bgeta  bata  bunderstandinga  bthea  bcodinga  banda  balla  bthata  byoua  bcana  bdoa  bwitha  bit.

Ita  bforcesa  bthea  bprogrammera  btoa  bslowa  bdowna  banda  bactuallya  bfocusa  bona  bwhata  btheya  bwanta  bthea  bcodesa  btoa  bdo.

Anda  bthena  byoua  bcana  busea  bthisa  basa  baa  bwaya  btoa  bcatcha  byoura  bowna  bmistakesa  banda  blearna  bwhata  bworksa  bthea  bbesta  bfora  byoua  banda  bwhata  bdoesa  bnot.

Nota  baskinga  bfora  bhelp

Whena  bwea  bfirsta  bgeta  bstarteda  bwitha  bwritinga  bouta  bcodesa  bina  bthisa  bmanner,a  bita  bisa  bpossiblea  bthata  byoua  bhavea  baa  btona  bofa  bgranda  bideasa  bofa  bhowa  bthingsa  barea  bgoinga  btoa  bworka  banda  bhowa  byoua  bwilla  bbecomea  bthea  bgreatesta  bcodea  bwritera  bofa  balla  btime.

Youa  bmaya  bbelievea  bthata  bnothinga  bisa  bgoinga  btoa  bgoa  bwronga  bwitha  bthisa  banda  bthata  byoua  bcana  bhandlea  bita  balla  bina  bnoa  btimea  bata  ball.

Anda  bonea  bofa  bthea  bbiggesta  bmisconceptionsa  bthata  barea  bgoinga  btoa  bshowa  bupa  bwitha  bthea  bworka  bthata  bwea  bwanta  btoa  bdoa  bherea  bisa  bthata  bwea  bassumea  bwea  breallya  bdon’ta  bneeda  btoa  bstarta  banya  bkinda  bofa  bhelpa  bwitha  boura  bcodinga  bata  ball.

Whilea  bita  bwoulda  bbea  bawesomea  btoa  bgeta  bstarteda  bwitha  bcodinga  bina  banya  blanguage,a  bevena  bc#a  bona  boura  bowna  bwithouta  banya  bhelp,a  bwea  bhavea  btoa  bfacea  brealitya  baa  bbita  banda  bremembera  bthata  bwea  barea  bgoinga  btoa  blearna  bina  baa  bfastera  banda  bmorea  befficienta  bmannera  bwhena  bwea  bhavea  bthea  brighta  bkinda  bofa  bpeera  bfeedbacka  banda  bmentorsa  btoa  bhelpa  busa  bouta  bwitha  bthis.

Whata  bmaya  bseema  blikea  bana  bimpossiblea  bbuga  btoa  bworka  bwitha  bora  baa  btopica  bthata  bseemsa  blikea  bita  bisa  bunlearnablea  bwhena  byoua  bdoa  bita  bona  byoura  bown,a  byoua  bwilla  bfinda  bthata  bwhena  bsomeonea  bwitha  bmorea  bexperiencea  bstepsa  bina  banda  bcana  bhelpa  bout,a  bthingsa  bgeta  baa  blota  beasier,a  banda  byoua  bcana  bactuallya  blearna  bsomethinga  bnew.

Whethera  bita  bisa  bonlinea  bwherea  byoua  baska  bfora  bhelp,a  bora  byoua  barea  bablea  btoa  bfinda  bsomeonea  bwhoa  bisa  bablea  btoa  bcomea  btoa  byoua  bina  bpersona  banda  boffera  badvice,a  byoua  bshoulda  bnevera  bbea  bscareda  btoa  baska  bsomeonea  bfora  bhelp.

Alla  bofa  bthea  bprogrammersa  bwhoa  barea  bmorea  badvanceda  brighta  bnowa  bwerea  bata  bonea  btimea  bina  bthea  bsamea  bplacea  basa  byoua  barea  bnow.

Anda  bmosta  bdevelopersa  barea  bgoinga  btoa  blovea  bthata  btheya  bactuallya  bgeta  baa  bchancea  btoa  bcodea  bagain,a  banda  bwilla  bbea  bmorea  bthana  bwillinga  btoa  bhelpa  byoua  bouta  bwitha  bsomea  bofa  bthea  bcodingsa  bthata  byoua  bwoulda  blikea  bhelpa  bwith.

Ofa  bcourse,a  bwea  bneeda  btoa  bbea  bcarefula  bwitha  bthisa  banda  bnota  btakea  bita  bfora  badvantagea  bata  balla  bthrougha  bthea  bprocess.

Thea  bbesta  brulea  btoa  bfollowa  bherea  bisa  btoa  bnevera  btakea  bmorea  bthana  b20a  bminutesa  bgettinga  bsomeonea  btoa  bhelpa  byoua  bfigurea  bouta  bsomethinga  bwitha  byoura  bcode.

Anda  byoua  bshoulda  bnota  baska  bfora  bhelpa  bwithouta  bspendinga  bata  bleasta  b20a  bminutesa  bona  bita  baheada  bofa  btime,a  btryinga  btoa  blearna  bhowa  bita  bworksa  banda  bwhata  byoua  barea  bablea  btoa  bdoa  bwitha  bthisa  basa  bwell.

Nota  btakinga  bbreaks

Therea  barea  bgoinga  btoa  bbea  btimesa  bwhena  byoua  barea  bwritinga  bouta  bsomea  bofa  bthea  bcodesa  bthata  byoua  bwanta  btoa  bdoa  bina  bthea  bc#a  blanguage,a  banda  bthena  byoua  bgeta  bstucka  bona  bsomething.

Youa  bspenda  bsomea  btimea  bona  bit,a  bbuta  bthata  bjusta  bseemsa  btoa  bmakea  bthea  bwholea  bthinga  bworse.

Youa  bkeepa  bworkinga  bata  bita  banda  bworkinga  bata  bit,a  beffectivelya  bmakinga  bthea  bproblema  bworse,a  bora  bnota  bbeinga  bablea  btoa  bfinda  bthea  bproblema  bata  ball,a  banda  byoura  bfrustrationa  blevelsa  bkeepa  bgoinga  bup.

Youa  bwanta  btoa  bbea  bablea  btoa  bfixa  bthea  bproblema  banda  bgeta  bona  bwitha  byoura  bcoding,a  bbuta  byoua  bjusta  bgeta  bangrier,a  banda  bthea  bcodesa  bgeta  bmessiera  bina  bthea  bprocess.

Whena  bthisa  bhappens,a  banda  bthisa  bisa  bsomethinga  bthata  bcana  bhappena  btoa  beveryone,a  bwea  bmusta  btakea  bthea  btimea  btoa  btakea  baa  bbreak.

Thisa  bisa  bprobablya  bthea  blasta  bthinga  bthata  bwea  bwanta  btoa  bworrya  babouta  bwhena  bita  bcomesa  btoa  bworkinga  bwitha  bthea  bc#a  blanguagea  banda  bsomea  bofa  boura  bcodes,a  bbuta  bita  bisa  bgoinga  btoa  ballowa  busa  btoa  btakea  baa  bbreaka  bfroma  bthea  bproblema  banda  bgeta  bsomea  bfresha  bair,a  bora  bata  bleasta  bdoa  bsomethinga  belsea  bfora  bsomea  btime.

Anda  boften,a  baftera  byoua  btakea  baa  bbreaka  banda  bthena  bcomea  bbacka  btoa  bit,a  byoua  bwilla  bfinda  bthata  bthea  bproblem,a  bwhicha  bseemeda  bimpossiblea  bata  bthea  bstart,a  bisa  bactuallya  breallya  beasya  btoa  bfix.

Noa  bonea  bwantsa  btoa  bgivea  bupa  bwhena  btheya  bhavea  bputa  bina  bsoa  bmucha  btimea  banda  befforta  btoa  bthisa  bprocess,a  bbuta  bina  bthea  blonga  brun,a  bita  bcana  bcuta  bdowna  bona  bthea  bfrustrationa  banda  bwilla  bensurea  bthata  byoua  bcana  bfixa  bupa  byoura  bcodea  bina  bnoa  btime.

Ignoringa  bthea  bc#a  bcommunity

Onea  bofa  bthea  bneata  bthingsa  bthata  bwea  barea  bgoinga  btoa  bfinda  bwhena  bita  bisa  btimea  btoa  bdoa  boura  bcodinga  bina  bthea  bc#a  blanguagea  banda  bmore,a  bisa  bthata  btherea  bisa  baa  blargea  bcommunitya  bofa  bdifferenta  bprogrammersa  banda  bdevelopersa  balonga  bthea  bwaya  bwhoa  barea  bablea  btoa  bhelpa  byoua  bout.

Thesea  bcommunitiesa  barea  bgoinga  btoa  bincludea  baa  blota  bofa  bprogrammersa  bwhoa  bhavea  bbeena  bina  balla  bstagesa  bofa  bthea  bprocess.

Somea  barea  bbeginners,a  bsomea  bhavea  bbeena  bina  bthea  bgamea  bfora  baa  bbit,a  banda  bsomea  barea  bmorea  badvanced.

Thisa  bisa  bgreata  bnewsa  bfora  byoua  bbecausea  bita  ballowsa  busa  baa  bchancea  btoa  bgoa  bthrougha  banda  blearna  baa  blota  bofa  bthings.

Wea  bcana  baska  bquestionsa  bofa  bthosea  bwhoa  barea  bina  bthea  bcommunity.

Wea  bcana  bfinda  baa  blota  bofa  bthea  bcodesa  bthata  bwea  bneeda  btoa  bhelpa  busa  bworka  bona  baa  bvarietya  bofa  bprogramsa  banda  blearna  bsomethinga  bnew.

Anda  bwea  barea  bablea  btoa  btalka  btoa  bothersa  babouta  bthea  bprogramminga  blanguagea  banda  bmeeta  bsomea  bgreata  bpeoplea  bwhilea  baskinga  baa  blota  bofa  bquestionsa  balonga  bthea  bwaya  basa  bwell.

Ita  bisa  baa  bgooda  bideaa  bfora  byoua  btoa  bgoa  bthrougha  banda  bmakea  bsurea  bthata  byoua  barea  bablea  btoa  breallya  bfinda  bthea  bcommunitya  bthata  bworksa  bfora  byou.

Therea  barea  baa  btona  bofa  bthesea  bcommunitiesa  bfounda  bonline,a  banda  bwea  bjusta  bneeda  btoa  bmakea  bsurea  bthata  bwea  bfinda  bthea  bonea  bthata  bseemsa  bthea  bbesta  bfora  bus.

Thisa  bisa  baa  bgreata  bplacea  btoa  bresorta  bbacka  btoa  bwhena  btherea  barea  bsomea  bproblemsa  bwitha  byoura  bcodea  bora  bwhena  byoua  bwoulda  blikea  btoa  bbea  bablea  btoa  bgeta  bsomethinga  bfigureda  bouta  bthata  bisa  bnota  bworkinga  bouta  bthata  bwella  btoa  bstarta  bwitha  bfora  byoura  bcode.

Failurea  btoa  butilizea  bthea  bsamplea  bcodesa  bprovided

Whilea  bthisa  bguidebooka  btooka  bsomea  btimea  btoa  bshowa  byoua  baa  bfewa  bsamplesa  bofa  bcodea  btoa  bshowa  bhowa  balla  bofa  bthea  bdifferenta  btypesa  bofa  bcodinga  barea  bsupposeda  btoa  bwork,a  bita  bisa  bnota  benougha  btoa  bbuilda  bupa  byoura  bunderstandinga  bjusta  btoa  blooka  bovera  bthea  bcode.

Toa  bhelpa  bdevelopa  baa  btruea  bunderstanding,a  banda  byoua  bneeda  btoa  btakea  bsomea  btimea  btoa  bruna  banda  btinkera  bwitha  bthea  bcodea  btoa  bseea  bwhata  bita  bcana  bdo.

Thea  bmorea  btimesa  bthata  byoua  barea  bablea  btoa  bspenda  bworkinga  bona  bthea  bcode,a  bthea  bbettera  boffa  byoua  bwilla  bbea  balonga  bthea  bway.

Witha  bthea  badditiona  bofa  bthingsa  blikea  binstructionsa  banda  bcomments,a  bthea  bsamplea  bcodesa  bthata  byoua  barea  bgoinga  btoa  bworka  bwitha  barea  bpackageda  bina  baa  bmannera  bthata  bisa  bdigestiblea  bina  bana  beasya  bmannera  bbya  bthea  breader.

Buta  byoua  bwilla  bfinda  bthata  bsometimes,a  bthesea  barea  bharda  btoa  breplicatea  bfroma  bscratch.

Readinga  bisa  bnota  bgoinga  btoa  bbea  bthea  bsamea  bthinga  basa  bunderstanding,a  banda  bactuallya  bgoinga  bthrougha  bthea  bprocessa  bofa  bwritinga  bouta  bsomea  bofa  bthea  bcodea  bona  byoura  bown,a  banda  bthena  brunninga  bit,a  bisa  bgoinga  btoa  bmakea  bsurea  bthata  byoua  bcana  blearna  bhowa  btoa  bcodea  bmucha  bfastera  bthana  bbefore.

Thea  bmorea  bthata  bwea  barea  bablea  btoa  bspenda  bwritinga  banda  bpracticinga  bsomea  bofa  bthea  bcodesa  bthata  bwea  bfind,a  banda  bthena  btestinga  bthesea  bcodesa  bouta  basa  bwell,a  banda  bthea  bmorea  bthata  bwea  bcana  btinkera  bwitha  bthesea  basa  bwell,a  bthea  beasiera  bthea  bcodinga  blanguagea  bisa  bgoinga  btoa  bbea  balonga  bthea  bway.

Thisa  bisa  baa  bgreata  bwaya  btoa  bmakea  bsurea  bthata  bwea  barea  bablea  btoa  blearna  bwhata  bisa  bgoinga  bon,a  bwhata  bwilla  bnota  bworka  bwhena  bwea  bmakea  bchangesa  banda  baa  blota  bmorea  bina  bthea  bprocess.

Justa  breadinga  bthea  bcodea  bmaya  bworka  bina  bsomea  bcases,a  banda  bita  bseemsa  blikea  bita  bisa  bthea  bbettera  boptiona  btoa  bworka  bwith,a  bbuta  bita  bisa  bnota  bgoinga  btoa  bshowa  busa  bthea  bbesta  bwaya  btoa  bbea  befficienta  bina  bordera  btoa  bactuallya  bcreatea  byoura  bowna  bprograms.

Workinga  bwitha  bthea  bc#a  blanguagea  bisa  baa  bgreata  bchoicea  btoa  bmake.

Therea  barea  baa  blota  bofa  boptionsa  bthata  bwea  barea  bablea  btoa  bfocusa  bon,a  banda  bita  bisa  baa  bgooda  boptiona  bfora  bmosta  bofa  bthea  bprogramsa  bthata  bwea  bwanta  btoa  bbea  bablea  btoa  bcreate.

Evena  basa  bsomeonea  bwhoa  bisa  bbranda  bnewa  btoa  bthea  bworlda  bofa  bprogramminga  banda  bisa  bnota  buseda  btoa  bdoinga  banya  bkinda  bofa  bcoding,a  bia  bwilla  bfinda  bthata  bthea  bc#a  blanguagea  bisa  baa  bgooda  boptiona  btoa  bworka  bwith.

Whena  byoua  barea  breadya  btoa  bgeta  bstarteda  bwitha  bthea  bprocessa  bofa  blearninga  baa  bnewa  bcodinga  blanguage,a  byoua  bwilla  bfinda  bthata  bavoidinga  bthesea  bmistakesa  byoua  bwilla  bablea  btoa  bgeta  bstarteda  bona  bthea  brighta  bfoot.

## Conclusion

Ifa  byoua  bhavea  bdecideda  bthata  bthea  bc#a  blanguagea  bisa  bthea  brighta  bonea  bfora  byoua  btoa  bworka  bwith,a  bthena  byoua  barea  bina  bgooda  bcompany.

Therea  barea  bmanya  bprogrammersa  bthroughouta  bthea  bworlda  bwhoa  barea  bgoinga  btoa  busea  bthisa  blanguage,a  banda  bnowa  bthata  byoua  barea  bdonea  bwitha  bthisa  bguidebook,a  byoua  bcana  bjoina  bthea  branksa  bnowa  basa  bwell.

Therea  barea  bsoa  bmucha  bknowledgea  banda  binformationa  binsidea  bofa  bthisa  bguidebooka  bthata  bwea  barea  bablea  btoa  bworka  bwith,a  banda  byoua  bwilla  bfinda  bthata  bthisa  bisa  bgoinga  btoa  bbea  bonea  bofa  bthea  bbesta  boptionsa  bthata  bwea  barea  bablea  btoa  butilizea  bwhena  bita  bcomesa  btimea  btoa  bworka  bwitha  bthea  bc#a  blanguage.

Contributinga  btoa  bca  b#a  b‘sa  beasea  bofa  busea  bisa  bthea  breductiona  bofa  bsomea  bca  b++a  bfeatures,a  banda  bnoa  blongera  bmacros,a  btemplates,a  banda  bmultiplea  binheritances.a  bespeciallya  bfora  benterprisea  bdevelopers,a  bthea  babovea  bfeaturesa  bwilla  bonlya  bproducea  bmorea  btroublea  bthana  bbenefits.a  bnewa  bfeaturesa  bthata  bmakea  bprogramminga  beasiera  barea  bstricta  btypea  bsafety,a  bversiona  bcontrol,a  bgarbagea  bcollect,a  banda  bmore.a  bthea  bgoala  bofa  balla  bthesea  bfunctionsa  bisa  btoa  bdevelopa  bcomponent-orienteda  bsoftware.

Youra  befforta  btoa  blearna  bca  b#a  bisa  baa  bbiga  binvestmenta  bbecausea  bca  b#a  bisa  bdesigneda  bfora  bthea  bprimarya  blanguagea  bofa  bwritinga  bngwsa  bapplications.a  byoua  bwilla  bfinda  baa  blota  bofa  bfunctionsa  bthata  byoua  bcana  bachievea  bora  blaboriouslya  bimplementa  bina  bca  b++,a  bwhicha  barea  bjusta  bsomea  bbasica  bfunctionsa  bina  bca  b#.a  bfora  benterprise-levela  bprogramminga  blanguages,a  bnewa  bfinanciala  bdataa  btypesa  barea  bpopular.a  byoua  busea  baa  bnewa  bdecimala  bdataa  btypea  bthata  bisa  bdedicateda  btoa  bfinanciala  bcalculations.a  bifa  byoua  bdon’ta  blikea  bthisa  bsimplea  bready-madea  btype,a  byoua  bcana  beasilya  bcreatea  baa  bnewa  bdataa  btypea  bbaseda  bona  bthea  bspeciala  bneedsa  bofa  byoura  bapplication.

Ca  b#a  bprovidesa  byoua  bwitha  bconvenienta  bfunctionsa  bsucha  basa  bgarbagea  bcollection,a  btypea  bsafety,a  bversiona  bcontrol,a  banda  bsoa  bon.a  bthea  bonlya  b“cost”a  bisa  bthata  bcodea  boperationsa  barea  btype-safea  bbya  bdefault,a  banda  bpointersa  barea  bnota  ballowed.a  bit’sa  balla  babouta  btypea  bsafety.a  bhowever,a  bifa  byoua  bneeda  bpointers,a  byoua  bcana  bstilla  busea  bthema  bwitha  bnon-securea  bcodes,a  banda  byoua  bcannota  bhavea  bcolumna  bsetsa  bwhena  bcallinga  bnon-securea  bcodes.

C#a  bisa  bana  beasya  bprogramminga  blanguage,a  bmakinga  bita  bgooda  bevena  btoa  bthea  bbeginnersa  bina  bprogramming.a  bonea  bonlya  bneedsa  btoa  bsetupa  bthea  benvironmenta  banda  bstarta  bwritinga  banda  brunninga  btheira  bc#a  bcode.a  byoua  bcana  busea  bc#a  balonea  btoa  bdevelopa  baa  bcompletea  bcomputera  bapplication.

Asa  baa  bbeginner,a  byoua  bwilla  baccomplisha  bamazinga  bgoalsa  bwitha  bthisa  bguidebooka  banda  bgaina  bvaluablea  bknowledgea  bina  blearninga  bhowa  btoa  bworka  bwitha  bthea  bc#a  blanguage.a  bwea  bhavea  bexploreda  bmanya  bdifferenta  btopicsa  bthata  bcomea  bwitha  bthisa  blanguage,a  bsucha  basa  bhowa  btoa  bworka  bwitha  bconditionala  bstatements,a  bhowa  btoa  bworka  bwitha  bclasses,a  banda  bwhata  bthea  boperatorsa  barea  balla  babout,a  banda  bsoa  bmucha  bmore.a  bthisa  bguidebooka  bwilla  bhelpa  byoua  btoa  bgoa  bthrougha  bthea  bc#a  blanguagea  bsoa  bthata  byoua  bcana  blearna  btoa  bwritea  byoura  bowna  bcodes.

Ifa  byoua  bfeela  blikea  byou’rea  breadya  btoa  blearna  baa  bnewa  bcodinga  blanguagea  banda  bgeta  bstarteda  bona  bprogramming,a  bc#a  bisa  baa  bgreata  bonea  btoa  bgoa  bwith.a  bmakea  bsurea  btoa  bchecka  bouta  bthisa  bguidebooka  btoa  blearna  balla  bthea  bbasicsa  bthata  byoua  bneeda  btoa  bknowa  btoa  bcreatea  breallya  busefula  bcodesa  bina  bnoa  btimea  bata  ball.

Gooda  blucka  banda  bhappya  bprogramming!