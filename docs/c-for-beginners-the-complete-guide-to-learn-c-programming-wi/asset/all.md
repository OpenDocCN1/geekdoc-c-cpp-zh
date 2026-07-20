C++ for beginners

The complete guide to learn c++ programming with ease and confidence

Lena neill

**© copyright 2023 - all rights reserved.**

The content contained within this book may not be reproduced, duplicated or transmitted without direct written permission from the author or the publisher.

Under no circumstances will any blame or legal responsibility be held against the publisher, or author, for any damages, reparation, or monetary loss due to the information contained within this book, either directly or indirectly.

Legal notice:

This book is copyright protected. It is only for personal use. You cannot amend, distribute, sell, use, quote or paraphrase any part, or the content within this book, without the consent of the author or publisher.

Disclaimer notice:

Please note the information contained within this document is for educational and entertainment purposes only. All effort has been executed to present accurate, up to date, reliable, complete information. No warranties of any kind are declared or implied. Readers acknowledge that the author is not engaged in the rendering of legal, financial, medical or professional advice. The content within this book has been derived from various sources. Please consult a licensed professional before attempting any techniques outlined in this book.

By reading this document, the reader agrees that under no circumstances is the author responsible for any losses, direct or indirect, that are incurred as a result of the use of the information contained within this document, including, but not limited to, errors, omissions, or inaccuracies.

Table of contents

[Introduction](#index_split_003.html_id_Toc159426398)

[Chapter 1: setting up a c++ development environment](#index_split_004.html_id_Toc159426399)

[Chapter 2: basics of c++, principles of programming](#index_split_005.html_id_Toc159426400)

[Chapter 3: variables and data types](#index_split_006.html_id_Toc159426401)

[Chapter 4: operations in c++](#index_split_007.html_id_Toc159426402)

[Chapter 5: decision making in c++](#index_split_008.html_id_Toc159426403)

[Chapter 6: creating functions](#index_split_009.html_id_Toc159426404)

[Conclusion](#index_split_010.html_id_Toc159426405)

[References](#index_split_045.html_id_Toc159426406)

## Introduction

This bo.o.k is fit fo.r beginners and fo.r co.ders who. Are interested in getting into. Backend pro.gramming. Altho.ugh c++ is so.metimes po.rtrayed as a specter o.f days past, the language is still with us and it co.ntinues to. Be behind so.me o.f the biggest techno.lo.gies we use to.day–no.t mentio.ning its big imprint in the gaming wo.rld. Its po.wer and versatility co.ntinue to. Make it o.ne o.f the mo.st impo.rtant languages o.f o.ur time. It is no.t go.ing anywhere and learning it will expand yo.ur ho.rizo.ns.

C++ is o.ften utilized as a backend language fo.r big data because o.f its little pro.cessing o.verhead. Co.mpanies like spo.tify, ado.be, yo.utube, and amazo.n po.wer their backend with c++, and yo.u will so.o.n see why.

C++ is also. Behind po.werful gaming engines. Gaming engines allo.w pro.grammers to. Build a game witho.ut co.ding everything fro.m scratch and to. Effectively render co.ntent. The unity game engine and the unreal engine are examples o.f gaming engines that run o.n c++.

C++ is a beautiful, efficient language because o.f the favo.rable po.wer/hardware ratio.: it uses little hardware fo.r the amo.unt o.f po.wer it gives us. This is why tho.se who. Learn it lo.ve it.

In this bo.o.k we will co.ver the fo.llo.wing to.pics:

*   Pro.gramming termino.lo.gy and principles in pro.gramming
*   Setting up a c++ enviro.nment
*   Getting started: syntax, data types, and variables
*   Po.wer o.f c++: o.peratio.ns, lo.o.ps, switches, and decisio.n making
*   Creating custo.m functio.ns in c++

Yo.u will also. Find a useful glo.ssary at the end so. That yo.u can use the bo.o.k as a reference o.nce yo.u get cracking.

## Chapter 1: setting up a c++ develo.pment enviro.nment

At its mo.st basic, pro.gramming is writing a list o.f instructio.ns in co.de that the machine can understand. The co.de resides in executables files. These files co.me with file extensio.ns that tell a co.mpiler what language is in the file. These extensio.ns are the suffixes yo.u o.ften see at the end o.f the file, like “.js”. “.cpp” o.r “.hpp”.

To. Write co.de and save it in an executable file yo.u need the fo.llo.wing things:

1.  A text edito.r: this will allo.w yo.u to. Write and edit the co.de.
2.  A language co.mpiler: this pro.gram takes the co.de yo.u have written and translates it into. Machine language that yo.ur co.mputer can understand and fo.llo.w.

All pro.gramming languages wo.rk like this except html, css, and javascript - these pro.grams are interpreted and executed by the bro.wser (“intro.ductio.n,” n.d.). This means bro.wser languages like javascript are so.ftware-based, while c++ is co.mpiled and then run directly o.n yo.ur machine, no.t in a so.ftware enviro.nment.

This means c++ is an assembly language. Assembly languages are lo.w-level pro.gramming languages that need a co.mpiler so. They can run o.n a machine (lithmee, 2018). In this co.ntext, the wo.rd lo.w-level do.es no.t carry a bad co.nno.tatio.n; it is descriptive, meaning that the language is clo.ser to. The machine o.r just a step away fro.m it.

As yo.u can pro.bably guess, c++ is a general-purpo.se language that can run almo.st anywhere. This means it can be assembled and co.mpiled in several different ways. This will largely depend o.n yo.ur o.perating system and the creatio.n utilities yo.u are using.

O.ur c++ exercises will be co.mpiled o.n an o.nline ide. Ide stands fo.r integrated develo.pment enviro.nment and it is used to. Edit and co.mpile co.de. I bet that descriptio.n so.unds familiar. Yes, an ide is an example o.f a text edito.r, but unlike a plain text edito.r, it has extra features that are impo.rtant to. The pro.gramming pro.cess. An ide can do. Things like co.mpile co.de, debug co.de, highlight co.de, warn yo.u o.f syntax erro.rs, and mo.re.

![image44.png](images/00001.jpeg)

Geeks fo.r geeks ide: a web-based pro.gram co.mpiler

This ide can be fo.und at [https://ide.geeksfo.rgeeks.o.rg/](https://ide.geeksforgeeks.org/) and has several pro.gramming languages. We will be fo.cusing o.n c++. This ide has many co.ding utilities: a tabbed wo.rking space, an input bo.x, and a co.de manager. This co.de manager includes the two. Bo.tto.m butto.ns highlighted o.n the left. These co.de manager butto.ns allo.w yo.u to. Do.wnlo.ad and uplo.ad co.de as files with their co.rrespo.nding file extensio.n. This ide also. Allo.ws yo.u to. Run and generate a url that saves the result. We’ll be using these generated urls to. Manage o.ur lesso.ns.

In this bo.o.k, we will use a geeks fo.r geeks web-based ide, but yo.u sho.uld learn to. Set up a lo.cal ide. Fo.r the majo.rity o.f yo.ur pro.gramming career, that is where yo.u will be wo.rking. Plus, yo.u can custo.mize the ide to. Fit yo.ur needs and spruce up yo.ur co.de.

Setting up yo.ur text edito.r

Ide enviro.nments that are fo.cused o.n pro.gramming always have to. Have a text edito.r and a co.mpiler within them. No.n-ide enviro.nments separate co.mpilers and plain text edito.rs. The text edito.r serves as a pro.gramming interface in no.n-ide setups; this simply means the text edito.r will be the place yo.u tinker with the co.de.

![Text Box 56](images/00002.jpeg)

When lo.o.king fo.r a text edito.r, yo.u need o.ne with syntax highlighting and indenting as all pro.gramming languages fo.llo.w their syntax. This is because yo.u want to. Be able to. Read yo.ur co.de easily and yo.u want co.llabo.rato.rs to. Be able to. Do. So., to.o.. These text edito.rs help by impro.ving readability. This is especially impo.rtant because co.ding is no. Lo.nger and has never been a so.litary task. There is no. O.ne-man genius like in the mo.vies.

Github and pastebin are co.de aggregato.rs that have syntax highlighting add-o.ns enabled. Github will allo.w yo.u to. Ho.st yo.ur entire pro.ject o.n their site, while pastebin o.nly allo.ws co.de snippets. O.n these platfo.rms, yo.u can save co.de in a variety o.f languages.

They are very useful to. Pro.grammers because they allo.w pro.grammers to. Share co.de, co.llabo.rate, test, and so. Fo.rth. Learning ho.w to. Deplo.y a pro.ject to. Github is o.ne o.f the mo.st impo.rtant things in pro.gramming because it has beco.me so. Standardized. So., maintaining a github pro.file has also. Beco.me impo.rtant, as it ho.lds all the pro.jects yo.u are wo.rking o.n, have wo.rked o.n, and yo.ur activity (peshev, 2017). To. A po.tential emplo.yer o.r co.llabo.rato.r, this info.rmatio.n is invaluable.

![image34.png](images/00003.jpeg)

C++ co.de syntax example

This is a screensho.t fro.m paste bin with syntax highlighting enabled [(“c++ co.de,” 2015)](https://www.zotero.org/google-docs/?MBrR1L). Syntax highlighting and tabbed spacing help with making the co.de mo.re co.mprehensible. All text edito.rs with syntax highlighting will use this scheme: libraries in green, and functio.ns, data types, and data in blue. Strings will sho.w up as red.

When yo.u are wo.rking lo.cally yo.u will no.t have luxuries like these readily available. The first text edito.r yo.u will find o.n yo.ur system if yo.u are using windo.ws is no.tepad. Wo.rdpad is ano.ther o.ne that has mo.re gui features. What yo.u will no.tice as yo.u o.pen these pro.grams is ho.w plain and bo.ring they are. They are like wo.rd but wo.rse, because they sho.uldn’t be simple wo.rd pro.cesso.rs if writing efficient, elegant co.de is impo.rtant to. Us. Their wo.rd pro.cesso.r-like aspects make them mo.re suitable fo.r writing wo.rds in them, no.t co.de, altho.ugh yo.u can co.de in them.

![image7.png](images/00004.jpeg)

Side-by-side co.mpariso.n o.f windo.ws’ no.tepad utility and wo.rdpad utility

This is a screensho.t that features two. O.f windo.ws’ built-in utilities, no.tepad o.n the left and wo.rdpad o.n the right. Wo.rdpad has mo.re micro.so.ft suite gui features that may be mo.re reco.gnizable to. Yo.u, including micro.so.ft's quick access bar lo.cated abo.ve the highlighted "file" tab. No.tepad is very bare-bo.nes in co.mpariso.n. Bo.th utilities, unlike wo.rd pro.cesso.rs, allo.w yo.u to. Save in different file extensio.ns. Ho.wever, wo.rdpad is mo.re similar to. A wo.rd pro.cesso.r than no.tepad, saving files in rich text fo.rmat (.rtf). Wo.rdpad will warn yo.u that yo.u will lo.se fo.rmatting if yo.u save in an extensio.n o.ther than rich text fo.rmat.

What makes no.tepad and wo.rdpad unique is that they can save files in a variety o.f file extensio.ns, while wo.rd pro.cesso.rs canno.t. File extensio.ns are impo.rtant because they tell the co.mpiler ho.w to. Interpret what is written in the file, and that leads to. The machine having a set o.f instructio.ns it can understand and execute.

Despite their abilities, these two. Pro.grams lack crucial text edito.r features like syntax highlighting. Yo.u might think this is no. Big deal, but it is; the same wo.rds in co.de can mean different things because o.f ho.w and when they appear, so. Highlighting helps us distinguish what they refer to.. So. If everything is plain, black and white, yo.u have to. Wo.rk harder to. Figure o.ut what a piece o.f co.de refers to.. It so.unds co.mplex no.w, but o.nce yo.u co.de this will beco.me o.bvio.us and necessary.

No.tepad++, no.t to. Be co.nfused with windo.ws’ no.tepad, has highlighting features but yo.u will have to. Activate them like so.:

![image1.png](images/00005.jpeg)

Screensho.t o.f no.tepad ++ with c++ syntax

No.tepad ++ is free and, as the name suggests, was pro.grammed in c++. This screensho.t illustrates ho.w to. Enable language syntax. C++ syntax can specifically be enabled by go.ing to. Language >"c" > and navigating to. C++. No.tepad++ is o.nly available o.n the windo.ws platfo.rm (o.rin, n.d.).

Bluefish is a mo.re advanced text edito.r that co.mes with mo.re features (“bluefish edito.r: features,” n.d.). Unlike no.tepad++, bluefish is available o.n multiple platfo.rms o.ther than windo.ws. But i wo.uld no.t reco.mmend bluefish fo.r beginners because it has a lo.t o.f features that can be o.verwhelming to. A co.mplete beginner. If yo.u are no.t new to. Pro.gramming yo.u can go. Give it a sho.t; yo.u will find it has many o.f the gui features typical o.f an ide text edito.r.

O.nce in the text edito.r, yo.u must select a co.mpiler. No.w let me sho.w yo.u ho.w yo.u wo.uld set up yo.ur lo.cal enviro.nment o.n three platfo.rms: windo.ws, linux, and mac.

Windo.ws ide installatio.n and setup

All yo.u need to. Do. Is to. Install an ide. Just remember that it has to. Have a text edito.r and a co.mpiler within it. Co.de::blo.cks is a useful, o.pen-so.urce ide made fo.r c++ and it easily fits with a variety o.f co.mpilers including micro.so.ft's visual c++. Installing co.de::blo.ck is easy. Yo.u just have to. Go. To. Their do.wnlo.ads page at [http://www.co.deblo.cks.o.rg/do.wnlo.ads/26](http://www.codeblocks.org/downloads/26) and select the latest versio.n.

![image13.png](images/00006.jpeg)

Co.de::blo.cks do.wnlo.ad page

As o.f this writing, co.de::blo.cks has versio.n 20.03 fo.r windo.ws and linux distributio.ns. The page also. Includes helpful no.tes fo.r installatio.n.

O.nce the pro.gram is installed, yo.u are set. Yo.u can use it to. Write c++ pro.grams. To. Do. So. Yo.u have to. Fo.llo.w three steps: creating a file, building the pro.gram, and running the pro.gram.

Creating a new file is a bit mo.re nuanced. Here is what yo.u have to. Do.:

*   Go. To. File > new
*   Select “create an empty file” and input yo.ur co.de
*   Save the file with a “.cpp” extensio.n

And, needless to. Say, yo.u have to. Build a pro.gram befo.re yo.u can run it. Yo.u can do. This by go.ing to. Build > “build and run” in the menu.

![image20.png](images/00007.jpeg)

Screensho.t o.f “hello. Wo.rld” in co.de::blo.cks

This is a live screensho.t o.f o.ur "hello. Wo.rld" pro.gram in co.de blo.cks. After this pro.gram is run, an erro.r sho.ws up in the build messages o.f the co.de. Co.de::blo.cks highlights the erro.r o.n line 6. Given yo.ur kno.wledge o.f c++ syntax fro.m the earlier sectio.n, yo.u sho.uld see ho.w to. Repair the co.de. Ho.w can we repair the co.de?

Hint: data and functio.ns are suppo.sed to. Sho.w up in blue.

By the way, this pro.gram is very lightweight fo.r the amo.unt o.f wo.rk it allo.ws yo.u to. Do.. Co.de::blo.ck is available o.n windo.ws and linux, but there is no. Mac versio.n.

Mac o.s ide installatio.n and setup

Fo.r mac, yo.u will need to. Get xco.de. It is a free ide so.ftware develo.pment suite fo.r maco.s. Yo.u can get it o.n the mac app sto.re. Xco.de suppo.rts a variety o.f o.ther languages like java, pytho.n, and ruby.

It is geared to.ward develo.ping so.ftware fo.r maco.s o.perating systems; this can be fo.r the tvo.s fo.r appletv, watcho.s fo.r apple watches, and the ipado.s fo.r ipad tablets (“what’s new in xco.de 9,” n.d.). Xco.de o.ffers a variety o.f so.ftware develo.pment kits (sdks) fo.r different maco.s platfo.rms to. Help pro.grammers thro.ugh apple’s pro.prietary pro.gramming schemes. Sdks are a set o.f to.o.ls, pro.vided by hardware and so.ftware vendo.rs, used fo.r develo.ping applicatio.ns fo.r specific platfo.rms (“what’s new in xco.de 9,” n.d.). Sdks allo.w develo.pers to. Be fully integrated within a develo.pment co.mmunity, like apple’s o.r andro.id’s.

Mac uses pro.prietary co.mpilers that will o.nly wo.rk with xco.de, so. If yo.u are o.n mac yo.u have little cho.ice but to. Develo.p with c++ using xco.de. Yo.u can do.wnlo.ad and install xco.de by fo.llo.wing this link:

[Https://apps.apple.co.m/us/app/xco.de/id497799835?Mt=12](https://apps.apple.com/us/app/xcode/id497799835?mt=12)

O.nce the file is do.wnlo.aded and installed, o.pen xco.de and click o.n the “create a new xco.de pro.ject” ico.n. Then select “new pro.ject” in the initial windo.w.

![image12.png](images/00008.jpeg)

Initial screen fo.r xco.de: select a new pro.ject

These screensho.ts feature an xco.de build fro.m versio.n 8.3.3 (patel, 2017). Therefo.re, o.ur examples might lo.o.k different fro.m a mo.re up-to.-date build. As o.f this writing, the mo.st current versio.n is 12.1, which mo.stly includes updates to. The vario.us maco.s platfo.rm sdks (“‎xco.de,” n.d.). Despite these differences, these screensho.ts will still help yo.u o.rient yo.urself in the mo.re current build. O.ur instructio.n will still yield results.

After yo.u do. This, a pro.mpt windo.w will appear that will ask yo.u to. Cho.o.se a template. This windo.w will guide yo.u thro.ugh the rest o.f the setup. Select the maco.s sectio.ns and go. To. The applicatio.n sectio.n; in there, cho.o.se the co.mmand line to.o.l.

It lo.o.ks so.mething like this:

![image6.png](images/00009.jpeg)

1. Pro.ject selectio.n screen: maco.s > applicatio.n > co.mmand line to.o.l

Xco.de has many built-in co.de utilities fo.r running pro.grams o.n vario.us apple platfo.rms. Therefo.re, to. Run a test pro.gram yo.u wo.uld have to. Select maco.s fo.r it to. Run o.n yo.ur pro.gram. Further, to. Access assembly language so.ftware develo.pment needed fo.r c++, yo.u wo.uld have to. Use xco.de’s co.mmand-line to.o.l. This co.mmand-line to.o.l can handle o.bjective-c and c languages as well.

After yo.u select a template, the guide will present o.ptio.ns fo.r the co.mmand-line to.o.l. Here, yo.u can name the pro.ject, add yo.ur o.rganizatio.n’s name, use a bundle identifier, and select a pro.gramming language.

![image49.png](images/00010.jpeg)

2. Co.mmand line to.o.l o.ptio.ns: language > select c++

Xco.de’s co.mmand-line to.o.l can handle micro.so.ft’s pro.prietary languages like swift. This pro.gram can run alo.ngside c-based languages in mac co.mpilers, including c++. Swift is selected by default.

In the same windo.w, yo.u will be required to. Add an o.rganizatio.n identifier. Remember that xco.de’s co.mmand-line to.o.l is a pro.gramming template fo.r pro.prietary maco.s o.perating systems, so. The o.rganizatio.n identifier is used to. Create a unique idea fo.r yo.ur pro.gram in apple databases: the apple develo.per website and iclo.ud co.ntainer, itunes co.nnect po.rtal in the appsto.re. This will streamline yo.ur app into. A pro.prietary maco.s framewo.rk.

![image11.png](images/00011.jpeg)

3. Co.mmand line to.o.l o.ptio.ns: o.rganizatio.n identifier > “cpp”

The o.rganizatio.n's identifier is a naming co.nventio.n that helps pro.grammers integrate their pro.jects into. Apple’s pro.prietary so.ftware develo.pment scheme. Here, we are using “cpp” as o.ur identifier, which generates “cpp.hello.wo.rld” as o.ur bundle identifier. O.nce we indicate an identifier, the guide allo.ws us to. Pro.ceed to. The next step.

No.w, save yo.ur pro.ject in a directo.ry o.f yo.ur cho.ice. O.n the left-hand side pane, xco.de will be able to. O.pen the file. Yo.u will have to. Select main.cpp to. Access the glo.bal c++ file fo.r yo.ur pro.gram in xco.de. If yo.u so. Desire, yo.u can uplo.ad cpp files into. The directo.ry, and edit them.

![image40.png](images/00012.jpeg)

3. Xco.de co.mmand line to.o.l: “main.cpp”

This screensho.t features the ide style xco.de co.mmand line to.o.l wo.rkspace. It has the ![00013.jpeg](images/00013.jpeg) o.pened in the text edito.r (patel, 2017).

O.nce yo.u have written so.me co.de and yo.u want to. Run it, yo.u select pro.duct and click o.n run. Also., yo.u can run and build the pro.gram by selecting the butto.n.

![image36.png](images/00014.jpeg)

4. Xco.de co.mmand line to.o.l: “hello. Wo.rld” build and run

Similar to. The co.de::blo.cks ide, yo.u will also. Have to. Build and then run yo.ur pro.gram. This screensho.t also. Features the results o.f “hello. Wo.rld” and the return value (patel, 2017).

If yo.u are a pro.grammer who. Sees themselves wo.rking with apple devices, wo.rking and practicing in xco.de is a go.o.d investment. Fo.r instance, apple has a healthy share o.f the market in a wide variety o.f co.nsumer go.o.ds and services like streaming services and devices. With that said, yo.u sho.uld keep in mind that c++ is used mo.stly as a server-side language. Server-side pro.gramming is co.de that co.ntro.ls ho.w co.ntent is delivered to. A dynamic website like yo.utube. Mo.st server-side pro.gramming is do.ne o.n linux machines.

Linux co.mpiler installatio.n

Linux is a co.nso.le-based o.peratio.n system, so. It do.es no.t need a text edito.r. Instead, we will fo.cus o.n installing and setting up a pro.gramming co.mpiler. Mac and windo.ws auto.matically initialize a co.mpiler within the ide, but in linux, a mo.re hands-o.n appro.ach is required. Yo.u will be required to. Execute a backend initializatio.n. It might seem like a lo.t o.f wo.rk, but in the great scheme o.f things, it allo.ws tho.se wo.rking with linux to. Have full co.ntro.l o.f the develo.pment pro.cedure and unlo.ck mo.re co.mputing po.wer.

Because linux is an o.perating system that uses a co.nso.le interface, it will be strange to. Beginners o.r anyo.ne who. Is used to. Windo.ws o.r mac. This is because users are o.ften used to. A gui. The gui-lessness o.f linux allo.ws mo.re co.mputing po.wer to. Be freed fo.r pro.gramming – a gui takes so.me co.mputing po.wer to. Pro.duce and maintain. This is why many servers and o.ther pro.gramming enviro.nments have co.nso.le interfaces. Also., many o.f them use linux distributio.ns.

A linux distributio.n (distro.) Is an o.perating system made fro.m linux kernel-based so.ftware co.llectio.n and package management system fo.r installing additio.nal so.ftware.

The fo.llo.wing are instructio.ns fo.r installing and initializing a co.mpiler. This will be fo.r ubuntu, a po.pular linux distro. Fo.r beginners. These installatio.ns will be similar in any linux distro. Yo.u will be using.

No.te: there are many distributio.ns o.f linux that pro.vide a gui based deskto.p experience that many users lo.ve. Mo.st o.f these are o.pen-so.urce and free to. Do.wnlo.ad and install. Yo.u can explo.re these distro.s and create co.nso.le interfaces to. Practice o.n. O.ne free distro. To. Co.nsider is cento.s, which is based o.n red hat fo.r server management [(“cento.s-faq | o.pen so.urce co.mmunity,” n.d.)](https://www.zotero.org/google-docs/?xc5bIM). Red hat enterprise linux (rhel) is used in many server management setups and is no.t free. Ho.wever, cento.s uses many o.f its co.mpo.nents and is an excellent distro. Fo.r preparing to. Wo.rk in red hat enviro.nments.

In this example, we will use the gnu co.llectio.n co.mpiler o.n linux. The gnu co.llectio.n co.mpiler is a linux-based co.mpiler that suppo.rts c++ and o.ther vario.us languages like fo.rtran, ada, and java (“gcc 7 release series—changes, new features, and fixes—gnu pro.ject—free so.ftware fo.undatio.n (fsf),” n.d.). To. Install gnu gcc, fo.llo.w these steps:

*   In the co.nso.le, enter the fo.llo.wing co.mmands:

Check first if there is a versio.n already installed o.n yo.ur machine by entering this co.mmand: gcc –v

![image45.png](images/00015.jpeg)

1.  Check fo.r gnu gcc in ubuntu co.nso.le

Yo.u sho.uld check yo.ur system fo.r a co.py o.f the gcc. This screensho.t features a system with gcc already installed [(patel, 2014)](https://www.zotero.org/google-docs/?Bxua2v). After using the co.mmand, if there is no. Co.py o.f gcc in yo.ur system, it will be missing this line. If there is a co.py, it will have a similar line. Mo.st likely, yo.ur versio.n will be mo.re recent.

The fo.llo.wing co.mmands will install gcc o.n yo.ur system (agarwal, 2017b):

Sudo. Apt-get update

Sudo. Apt-get install gcc

![image19.png](images/00016.jpeg)

1.  Install gnu gcc in ubuntu co.nso.le

In the screensho.t, a gnc gcc is already present. Running the highlighted co.mmand will install the gnu gcc o.n yo.ur system if it isn’t there (patel, 2014). The co.nso.le will pro.mpt yo.u to. Type “y” fo.r it to. Begin the installatio.n. Yo.u also. Are o.ffered package management features like the ability o.f the terminal to. Info.rm yo.u o.f o.utdated o.r unnecessary packages. It will also. Suggest co.mmands that will make yo.ur system mo.re efficient. This explains the po.pularity o.f linux with pro.grammers; altho.ugh wo.rdy, it allo.ws them to. Tro.ublesho.o.t with ease, gives them mo.re co.ntro.l, and it is easy to. Navigate when co.mpared to. Guis. This is because pro.grammers are mo.re likely to. Remember a line o.f co.de than where so.mething resides in the gui.

The fo.llo.wing co.mmand will install all the libraries required to. Co.mpile co.de and eventually run c++:

Sudo. Apt-get install build-essential

![image39.png](images/00017.jpeg)

1.  Install gnu gcc in ubuntu co.nso.le

This screensho.t sho.ws a system with the build-essential libraries installed and inputting the highlighted installatio.n co.mmand (patel, 2014). Just as with installing the gcc, after using the co.mmand and finding there is no. Co.py o.f the build-essential libraries in yo.ur system, it will pro.mpt yo.u to. Install. Type in “y” and the terminal will install libraries.

*   Check the installatio.n with the fo.llo.wing co.mmand:

G++ --versio.n

If all went well it will tell yo.u what versio.n o.f gcc is installed.

Because linux has a built-in text edito.r yo.u will have to. Use the fo.llo.wing co.mmand to. Access the gui fo.r the text edito.r:

Gedit

Yo.u will be free to. Write yo.ur pro.gram as yo.u see fit. Remember to. Save the pro.grams with the “.cpp” extensio.n so. That they will be co.mpiled co.rrectly.

![image52.png](images/00018.jpeg)

Gedit in ubuntu

This screensho.t features linux’s built-in text-edito.r, gedit ([running c, c++ pro.grams in linux] ubuntu 16.04 (ubuntu tuto.rial fo.r beginners), n.d.). Gedit is a linux pro.gramming text edito.r utility that has syntax highlighting and tabbed spacing features fo.r a diverse array o.f pro.gramming languages. Be sure to. Have “c++” selected fro.m the highlighted dro.pdo.wn menu. Yo.u can save yo.ur pro.gram file in the gui by clicking the “save” butto.n. Be sure to. List which directo.ry yo.u have yo.ur file saved, as yo.u will have to. Po.int the co.mpiler to. That directo.ry to. Co.mpile and run the co.de.

To. Test and run yo.ur co.de yo.u must fo.llo.w these instructio.ns:

1.  Lead the terminal to. The files directo.ry

To. Do. This use this co.mmand. Enter it in the directo.ry repeatedly until the .cpp file is revealed.

Ls

1.  Co.mpile and test the pro.gram file

Use these co.mmands to. Do. So.:

![00019.jpeg](images/00019.jpeg)

If there are any erro.rs this co.mmand will tell yo.u which line co.ntains the erro.r just like yo.u wo.uld expect fro.m an ide. Then yo.u can o.pen the pro.gram file thro.ugh “gedit [filename.cpp]” and fix the line o.f co.de.

1.  Run the pro.gram file

The co.mpiler will create an executable file called “test” that will run the pro.gram. Yo.u can execute it by entering “. /test” in the terminal.

![image32.png](images/00020.jpeg)

Testing, co.mpiling and running a .cpp file in ubuntu

This screensho.t features the terminal testing, co.mpiling, and running the example co.de written in gedit ([running c, c++ pro.grams in linux] ubuntu 16.04 (ubuntu tuto.rial fo.r beginners), n.d.).

Linux distro.s are verbo.se co.nso.le-based systems and mo.st o.f them can handle pro.gramming in any language thro.ugh the terminal. Learning to. Wo.rk in the linux enviro.nment is beneficial as it expo.ses yo.u to. Server-side pro.gramming.

No.te: the pro.cess fo.r installing gcc and co.mpiling o.n cento.s is similar. To. Install, yo.u instead use “![00021.jpeg](images/00021.jpeg). This co.mmand auto.matically installs the needed libraries as well. The steps fo.r co.mpo.sing, co.mpiling, testing, and running the pro.gram are all the same.

Creating yo.ur o.wn pro.gramming enviro.nment helps prepare yo.u fo.r real-wo.rld scenario.s in a way that o.nline co.ding spaces canno.t. In this bo.o.k, we will be using an o.nline ide. This is because everyo.ne will have the same learning enviro.nment with standardized o.utputs and interfaces. It simplifies things.

## Chapter 2: basics o.f c++, principles o.f pro.gramming

Pro.gramming languages are like any o.ther human language: they have structure, syntax, and rules. It is no.t eno.ugh to. Kno.w the wo.rds o.f ano.ther human language. Kno.wing ho.w to. Use them and ho.w they functio.n in that language is an integral part o.f co.mmunicating effectively in that language. Pro.gramming languages functio.n the same way, but the co.mmunicatio.n they care abo.ut trying to. Help is o.ne between man and machine. While machines, at least to.day, can never be as clever and capable as we are, there is a lo.t they can understand at a rate and with an efficacy that is alien to. Us. All pro.gramming is a set o.f instructio.ns. These instructio.ns can be rules, they can be actio.ns yo.u want the machine to. Perfo.rm, o.r so.mething else. But all this co.mmunicatio.n is po.ssible because we fo.llo.w the rules o.f a pro.gramming language.

Pro.gramming rules, o.r syntax, are a list o.f delineating symbo.ls used to. Co.mmunicate aspects o.f a pro.gram like functio.ns and variables. Syntax is impo.rtant to. The co.mpiler because it tells the co.mpiler what instructio.ns it sho.uld give to. The machine.

Befo.re we start, it is wo.rth keeping a few things in mind. Unlike pytho.n o.r o.ther high-level pro.gramming languages, c++ do.es no.t resemble the language o.f humans quite easily. High-level languages like js, pytho.n, and c# are made this way because it makes them easy to. Read and manage. C++, despite being this way, is easier fo.r machines to. Understand precisely because it is no.t so. Abstracted. This is why when wo.rking with c++ yo.u o.nly need a co.mpiler and text edito.r, whereas languages like pytho.n need their enviro.nments installed.

Principles o.f pro.gramming

C++ has many ways o.f co.mpleting the same task. Just like with human languages, there are many ways o.f saying the same thing, but so.me ways are best suited fo.r certain o.ccasio.ns and so.me aren’t. C++ is the same way; so.me metho.ds are great because they reduce pro.gram o.verhead. Many develo.pers will want that because it increases the perfo.rmance o.f the entire applicatio.n, and that is the first principle o.f pro.gramming: co.mplete a task with the least amo.unt o.f functio.ns as po.ssible. Do. No.t make things mo.re co.mplicated than they need to. Be. In mo.st cases, this means using a lo.o.p o.r a switch statement in a frugal way.

The best way to. Do. This is by understanding the nature o.f the pro.blem first and ho.w best to. Implement the so.lutio.n. In o.ther wo.rds, yo.u will need to. Write an algo.rithm – a list o.f instructio.ns that yo.u want the machine to. Fo.llo.w to. Fix the pro.blem.

Yo.ur designs sho.uld always begin with the thing yo.u want the pro.gram to. Do.. This will also. Include yo.ur algo.rithm, o.r at least the pro.blem that yo.ur algo.rithm will fix. The algo.rithm will always lo.o.k so.mething like this:

1.  Input: data co.ming, where applicable
2.  Pro.cessing: o.peratio.ns perfo.rmed o.n the data and declaratio.n o.f variables
3.  O.utput: the results, o.r the actio.n yo.u want perfo.rmed.

Here is a verbo.se example o.f a c++ pro.gram fo.r displaying “hello. Wo.rld”. This is to. Illustrate ho.w c++ pro.grams are co.mpo.sed:

// simple c++ pro.gram to. Display "hello. Wo.rld"

// header file fo.r input o.utput functio.ns

#include<io.stream>

Using namespace std;

// main functio.n -

// where the executio.n o.f pro.gram begins

Int main()

{

// prints hello. Wo.rld

Co.ut<<"hello. Wo.rld";

Return 0;

}

Here is the structure:

*   Call header file fo.r input and o.utput functio.ns
*   Call the main functio.n where the executio.n happens
*   Print “hello. Wo.rld”
*   Terminating statement that indicates the state o.f the machine

We can see ho.w verbo.se c++ is, because mo.st o.f the steps regard the backend aspects o.f c++ that are needed to. Execute the co.de, such as calling the library files. Yo.ur algo.rithms do.n’t need to. Be this detailed mo.st o.f the time.

Despite being simple, this algo.rithm illustrates ho.w develo.pers take tasks and translate them into. Co.de. In the next chapter, we will use this algo.rithm to. Write o.ur pro.gram.

As yo.u have no.ticed in the example, there are co.mments in the co.de that explain what each part o.f the co.de do.es. These co.mments are preceded by “//”. The co.mpiler will no.t read any lines o.f co.de preceded by // because they do.n’t do. Anything but help o.ther peo.ple wo.rking o.n the co.de read what the co.de do.es. It is go.o.d practice to. Include co.mments in yo.ur co.de so. Peo.ple kno.w what each line o.f co.de do.es.

O.verview o.f the c++ syntax

We have talked abo.ut the impo.rtance o.f syntax fo.r the co.mpiler, but it is also. Impo.rtant to. Understand the syntax o.f a pro.gramming language because it will allo.w yo.u to. Debug the co.de. Just like with human languages, if yo.u kno.w the rules o.f a language yo.u can co.rrect yo.urself easily when yo.u make mistakes. Debugging is the pro.cess o.f finding and remo.ving erro.rs and abno.rmalities in the co.de, also. Kno.wn as “bugs” (“what is debugging?” N.d.). It is a pro.cess o.f co.rrectio.n.

Ides have debugging to.o.ls that highlight where erro.rs o.ccur in the co.de, but these features aren’t always reliable. Fo.r instance, leaving o.ut a semico.lo.n to. Terminate a line o.f co.de is a co.mmo.n erro.r, but the debugger will highlight the erro.r in the (.h) file instead o.f the co.de where the mistake happens in the pro.gram file (.cpp). Mo.st debuggers are no.t intelligent eno.ugh to. Detect an absence o.f so.mething and will thro.w the verbo.se erro.r that the co.mpiler gives when the unterminated line vio.lates a rule in the library. Ho.wever, a pro.grammer will pick up the erro.r simply when they no.tice the red semico.lo.n line delimiter is missing fro.m o.ne o.f the lines.

![image38.png](images/00022.jpeg)

“hello. Wo.rld” pro.gram in geeksfo.rgeeks ide witho.ut a line delimiter

This screensho.t features “hello. Wo.rld” with a missing delimiter. Immediately yo.u will no.tice that the ide has different syntax highlighting fo.r c++ than the pro.gramming enviro.nments we explo.red in the previo.us chapter. Syntax can vary fro.m platfo.rm to. Platfo.rm. This is why we are standardizing the pro.cess with geeksfo.rgeeks ide. In o.ur cho.sen ide, semico.lo.ns are no.t highlighted. Ho.wever, the ide can make up fo.r this by reco.gnizing and anno.tating missing semico.lo.ns, as highlighted in the screensho.t. Yo.u can practice and explo.re this pro.gram by go.ing to. Its generated url: [https://ide.geeksfo.rgeeks.o.rg/mzbupp46sl](https://ide.geeksforgeeks.org/mzbuPP46Sl).

It is easy to. See this when the co.de is small, but when wo.rking o.n a larger pro.ject the task can be difficult. I have heard o.f pro.grammers who. Spend a week and o.r mo.re trying to. Find o.r fix a line in their co.de o.nly to. Disco.ver it is so.mething very minuscule like a missing letter o.r mismatch in case. To. Make debugging easier, it is advised that yo.u separate co.de into. Smaller mo.dules (“what is debugging?” N.d.). Many erro.rs can be fo.und and easily dealt with in this way.

Let us lo.o.k at the “hello. Wo.rld” pro.gram and study its syntax in detail. While syntax highlighting may vary acro.ss different platfo.rms, these aspects o.f co.de are co.nsistently highlighted o.n all platfo.rms.

Co.mments: as i said, these are the lines o.f co.de that the co.mpiler will igno.re. They are used to. Anno.tate co.de and leave helpful explanatio.ns fo.r o.ther pro.grammers. This is great because no.rmally when we co.de we co.llabo.rate with o.thers. It advised that yo.u leave co.mments in yo.ur algo.rithm to. Simplify it fo.r o.thers. In mo.st platfo.rms co.mments will be highlighted green. Co.mments are always preceded with (//).

Header file library: lines that start with (#) are used by the co.mpiler to. Call library functio.ns. These lines are very essential, so. They appear in every pro.gram. In the “hello. Wo.rld” example we call a library that is used to. Manage strings. These lines o.f co.de will be highlighted in different co.lo.rs acro.ss different platfo.rms. In geeksfo.rgeeks the co.lo.r is purple.

Statements: statements describe the beginning o.f a line o.f co.de with instructio.ns that the co.mpiler reco.gnizes. This includes declaratio.n handling instructio.ns, like “using…” o.r “return...” In o.ur hello. Wo.rld pro.gram. They are also. Highlighted differently acro.ss multiple platfo.rms. O.n geeksfo.rgeeks they are highlighted purple.

Functio.ns: this is co.de that encapsulates instructio.ns. It may take inputs and o.utput a result. Every functio.n is written like this: “[functio.n_name] () “fo.llo.wed by curly braces {}. Anything in the curly braces is the set o.f instructio.ns that will be executed. In o.ur example, main() is the functio.n that initiates the instructio.ns that will o.utput “hello. Wo.rld” with co.ut<<. In a “.cpp” pro.gram, int main () must always appear fo.r the pro.gram to.  Functio.n.

![Text Box 58](images/00023.jpeg)

Data: these are variables and o.ther kinds o.f data functio.ns and statements. In the geeksfo.rgeeks ide, they are highlighted blue.

![image31.png](images/00024.jpeg)

Co.mpariso.n o.f “hello. Wo.rld” pro.gram in geeksfo.rgeeks ide and
the geeksfo.rgeeks embedded pro.gram articles

This screensho.t features a successful run o.f “hello. Wo.rld” with the memo.ry used to. Run the pro.gram. This ide has light syntax highlighting, fo.cusing mainly o.n co.mments, statements, and o.perand data. Co.mpared to. Geeksfo.rgeeks’ embedded co.de in their articles, their embedded co.de is much mo.re detailed [(“writing first c++ pro.gram,” 2017)](https://www.zotero.org/google-docs/?z2pVlz). The two. Screensho.ts o.n the right feature the “light-mo.de” and “dark-mo.de” views o.f the same co.de embedded in their articles. These views are mo.re detailed, highlighting co.mments, functio.ns, and distinguishing different statements. Fo.r example, data types such as int are distinguished with a different co.lo.r fro.m o.ther statements such as using namespace. Also. The embedded views, unlike the ide, distinguish strings fro.m o.ther data. This is a perfect example o.f ho.w syntax highlighting can vary acro.ss different platfo.rms.

Earlier we saw a co.de::blo.ck example with an erro.r in it. Belo.w is the very same co.de next to. O.ne that is co.rrected. Immediately yo.u can begin to. Appreciate the syntax and what went wro.ng in the co.de::blo.ck example.

![image9.png](images/00025.jpeg)

Co.mpariso.n o.f “hello. Wo.rld” in co.de::blo.cks with geeksfo.rgeeks ide

This screensho.t features a side-by-side co.mpariso.n o.f the previo.us example, “hello. Wo.rld” in co.de::blo.cks with erro.rs, and the same co.rrected co.de in geeksfo.rgeeks ide. Upo.n studying bo.th, yo.u sho.uld be able to. See that the last instructio.n in the intmain()functio.n was inco.rrectly entered in the co.de::blo.cks.as a result,the co.mpiler co.uld no.t reco.gnize the return statement.

I will admit that it is no.t as impressive in a few co.de lines like this, but being able to. No.tice erro.rs and explain them is o.ne o.f the mo.st impo.rtant skills fo.r pro.grammers. At this po.int yo.u sho.uld no.t wo.rry much abo.ut being able to. Do. This. The mo.re yo.u co.de and learn, the better equipped yo.u will be to. No.tice and fix erro.rs. So.ftware and web develo.pment are industries with a high failure rate because o.f this. To. Succeed as a develo.per yo.u need to. So.lve pro.blems quickly, find bugs mo.re efficiently, and fix them. This also. Applies o.n the administrative side, because being able to. Find, fix, and explain bugs is a large part o.f desk service level agreements.

In tech, service level agreements (slas) are agreements between a service pro.vider and a client. They agree upo.n aspects o.f the service, like suppo.rt, quality, availability, and respo.nsibilities (wieder, butler, theilmann, & yahyapo.ur, 2011). Co.mprehensive slas o.ffer a debugging debriefing, where every erro.r is lo.gged and listed with its cause, wo.rkaro.und, and so.lutio.n. This is the best way to. Do. It in techno.lo.gy management firms and develo.pment stages. Ho.wever, administrato.rs have mo.re reso.urces to. Dedicate to. Debugging than develo.pers themselves. They are co.mpensated at a higher rate as well. Fo.r instance, web develo.pers make appro.ximately 60,000 a year in the us; web administrato.rs, tho.se in charge o.f slas, make abo.ut 1/3 mo.re at 90,000 a year (“15-1199.03—web administrato.rs,” n.d.). This level o.f expertise is valuable because it understands ho.w the co.mpiler translates c++.

First pro.gram: o.utput and basic strings

“hello. Wo.rld” is every pro.gramming language’s beginner pro.ject; its aim is to. Sho.w the learner the basic syntax o.f the pro.gram and ho.w it functio.ns. As yo.u learn mo.re languages yo.u will write many “hello. Wo.rld” pro.grams. In the previo.us sectio.n, we used it to. Explo.re to.pics like algo.rithms, syntax, and c++ pro.gramming enviro.nments. In this sectio.n we will go. Further: we will manipulate the co.de.

C++ uses the co.ut o.bject fro.m the io.stream library. An o.bject is a metho.d that a co.mputer uses to. Manage data. In o.ur example, co.ut was used to. Tell the co.mpiler to. Print “hello. Wo.rld with the >> o.perato.r. Do.n’t freak o.ut; we will discuss o.perato.rs and o.bjects in later chapters. Fo.r no.w, it’s eno.ugh to. Understand that the co.mpiler reads co.ut as specific instructio.ns because that instructio.n is defined in the io.stream library that we declared.

No.w, let’s lo.o.k at “hello. Wo.rld” and the co.ut o.bject by changing the print o.ut. Find the o.riginal co.de here so. Yo.u can use it as a reference:

[Https://ide.geeksfo.rgeeks.o.rg/ea8zmekido.](https://ide.geeksforgeeks.org/eA8ZMEKiDO)

![image16.png](images/00026.jpeg)

“hello. Wo.rld” pro.gram in geeksfo.rgeeks ide

This screensho.t is the successful run o.f “hello. Wo.rld” in split-screen mo.de. As we begin to. Use the ide fo.r co.ding exercises, no.te the input and o.utput bo.xes. While there are no. Inputs fo.r this pro.gram, yo.u will input data into. The to.p bo.x labeled “input go.es here…” when pro.mpted by the pro.gram in the o.utput belo.w.

Yo.u can access this pro.gram in the saved ide here: [https://ide.geeksfo.rgeeks.o.rg/ea8zmekido.](https://ide.geeksforgeeks.org/eA8ZMEKiDO).

Yo.u can also. View a co.py o.f the co.de in the index.

Using co.ut

The co.ut o.bject uses the << o.perato.r to. Print values and text, and we can have as many o.f them as we like. Using the ide in yo.ur bro.wser, change the co.de to. Print o.ut:

Hello. Wo.rld

I am learning c++

Like this:

![image30.png](images/00027.jpeg)

Adding co.ut o.bjects

This screensho.t is the successful run o.f o.ur edited “hello. Wo.rld” pro.gram in split-screen mo.de. While the pro.gram ran witho.ut any erro.rs, it didn’t pro.duce the result we wanted. O.bserving the o.utput, the printed text is missing a new line. We will have to. Instruct the co.mpiler to. Add the new line to. Get the desired result.

Adding lines can be do.ne in several ways: we can add delimiters within the strings o.r use ano.ther manipulato.r o.bject fro.m the io.stream library.

**Using escape sequences**

Altho.ugh it might be tempting to. Write a string within co.ut and enter a line, it will no.t wo.rk. It will break the co.de and it will no.t run. Do.n’t believe me? Test it!

Yo.u can add a new line by using an escape sequence. Escape sequences are used in many instances where yo.u need to. Intro.duce special characters within strings and character streams. It can also. Add lines, like so.:

![image23.png](images/00028.jpeg)

Using in-string escape sequences to. Delimit and manipulate the o.utput

This screensho.t is the successful run o.f o.ur edited “hello. Wo.rld” pro.gram in split-screen mo.de. Using ![00029.jpeg](images/00029.jpeg), we were able to. Get o.ur expected o.utput.

As yo.u lo.o.k at the co.de, yo.u can see that do.ubles quo.tes are used. So., if yo.u want to. Add do.uble quo.tes in a string, yo.u will have to. Use an escape sequence so. That the co.mpiler kno.ws that is no.t a part o.f the co.de. No.t do.ing so. May cause unfo.reseen erro.rs o.r bugs. This is why escape sequences matter. Here is a list o.f the many instances where they can be used (“escape sequences—cppreference.co.m,” n.d.):

“![00030.jpeg](images/00030.jpeg)”: used fo.r single quo.tes

“![00031.jpeg](images/00031.jpeg)”: used fo.r do.uble quo.tes

“![00032.jpeg](images/00032.jpeg)”: used fo.r questio.n marks

“![00033.jpeg](images/00033.jpeg)”: used fo.r backslashes

“![00034.jpeg](images/00034.jpeg)”: stands fo.r “fo.rm feed” and is used to. Go. To. The next “page”

“![00029.jpeg](images/00029.jpeg)”: stands fo.r “line feed” and is used to. Go. To. The next line

“![00035.jpeg](images/00035.jpeg)”: stands fo.r “ho.rizo.natal tab” and adds 5 spaces ho.rizo.ntally

“![00036.jpeg](images/00036.jpeg)”: stands fo.r “veritical tab” and is used fo.r spacing in vertical languages

No.te: if yo.u decide to. Try different escape sequences as text delimiters, be sure to. O.nly use the ![00037.jpeg](images/00037.jpeg)![00038.jpeg](images/00038.jpeg)![00039.jpeg](images/00039.jpeg) butto.n to. Save yo.ur wo.rk at ano.ther url to. Return to. Later. To. Return to. O.ur exercise, yo.u can use o.ur saved ide wo.rkspace url ([https://ide.geeksfo.rgeeks.o.rg/psgblshe4h](https://ide.geeksforgeeks.org/PsgBLSHE4h)).
Yo.u can also. Access this co.de in the index.

Using endl: input/o.utput manipulato.rs

Like we have said, pro.gramming languages are as versatile as human language. Yo.u can express o.ne instructio.n in many ways, and terminating a string is no. Exceptio.n. The difference between an escape sequence and endl is that endl flushes and refreshes the buffer used to. Sto.re the string. Pro.grammers use endl to. Clear memo.ry after printing a lo.t o.f text. Yo.u can see why this is useful in memo.ry management. Endl is an example o.f an input/o.utput manipulato.r. Input/o.utput manipulato.rs are functio.ns that allo.w yo.u to. Co.ntro.l input/o.utput streams using the “<<” o.perato.r o.r the “>>” o.perato.r (“input/o.utput manipulato.rs—cppreference.co.m,” n.d.).

![image29.png](images/00040.jpeg)

Using an input/o.utput manipulato.r to. Delimit and manipulate the o.utput.

This screensho.t is the successful run o.f o.ur edited “hello. Wo.rld” pro.gram in split-screen mo.de. Using ![00041.jpeg](images/00041.jpeg) we were able to. Get o.ur expected o.utput. In a pro.gram this small, it is difficult to. See the effects o.f using a memo.ry manipulato.r. Manipulato.rs o.nly begin to. Make a difference when using them in called functio.ns. Yo.u can access the co.de at this url: [https://ide.geeksfo.rgeeks.o.rg/htcffytk71](https://ide.geeksforgeeks.org/htcfFytK71).

Like escape sequences, there are many mo.re input/o.utput manipulato.rs that give pro.grammers mo.re co.ntro.l o.ver data types o.r strings. Many o.f them will make sense o.nce we talk abo.ut data types and structuring classes. Here are so.me o.f them (“input/o.utput manipulato.rs—cppreference.co.m,” n.d.):

“![00042.jpeg](images/00042.jpeg)”: switches between using “0/1” to. “false/true” fo.r bo.o.lean values

“![00043.jpeg](images/00043.jpeg)”: fo.r mathematical o.utputs, co.ntro.ls whether a prefix is used to. Indicate a numeric base

“![00044.jpeg](images/00044.jpeg)” sign is used to. Indicate no.n-negative numbers

“![00045.jpeg](images/00045.jpeg)”: co.ntro.ls the usage o.f uppercase characters with particular o.utput fo.rmats

“![00046.jpeg](images/00046.jpeg)”

“![00047.jpeg](images/00047.jpeg)”: flushes the o.utput stream

“![00048.jpeg](images/00048.jpeg)” and flushes the o.utput stream

“![00049.jpeg](images/00049.jpeg)”: receives an input as a mo.netary value

“![00050.jpeg](images/00050.jpeg)”: fo.rmats and o.utputs a mo.netary value

“![00051.jpeg](images/00051.jpeg)”: receives an input as a date/time value acco.rding to. A specified fo.rmat

“![00052.jpeg](images/00052.jpeg)”: receives an input as a date/time value acco.rding to. A specified fo.rmat

No.te: recall o.ur co.nversatio.n abo.ut c++11 and c++14\. As o.f this writing, mo.st pro.gramming ides use c++11 as their default versio.n. The “get/put…” functio.ns are all in c++11\. If yo.u receive an erro.r trying to. Use these manipulato.rs, check to. See if yo.ur setup is using c++11\.
Additio.nally, “![00053.jpeg](images/00053.jpeg)” is a manipulato.r that is in c++14 o.nly. This manipulato.r allo.ws yo.u to. Insert and extract quo.ted strings with embedded spaces [(“input/o.utput manipulato.rs—cppreference.co.m,” n.d.)](https://www.zotero.org/google-docs/?6OhBz2).

O.mitting namespace

We have already spo.ken abo.ut using namespace statements. We said it helps declare strings glo.bally, but when it co.mes to. A small pro.gram like “hello. Wo.rld” it is no.t so. Impo.rtant. Fo.r larger pro.grams that use several functio.ns, it is go.o.d practice to. Use the statement to. Declare each string separately. This saves memo.ry space in the co.mpiler, o.r yo.u will find yo.urself in a situatio.n where the co.mpiler is bo.gged do.wn unnecessarily, having to. Pull the entire string namespace library to. Print co.de. Declaring each string separately might make yo.ur co.de wo.rdier, but it will reduce co.mpiler o.verhead, and it fo.cuses yo.ur instructio.ns. Std namespace has multiple o.bjects and definitio.ns that can make it difficult fo.r the co.mputer to. Find the appro.priate way to. Manipulate and define a string. The namespace co.nventio.n is impo.rtant when yo.u have functio.ns that are go.ing to. Be called by multiple pro.grams. So. Putting it in there unnecessarily has the po.tential o.f making yo.ur functio.ns po.o.rly defined and causing reco.gnitio.n erro.rs between them.

Let’s make o.ur co.de mo.re efficient by remo.ving the using namespace fro.m o.ur co.de.

![image48.png](images/00054.jpeg)

Testing stability: using a co.mment to. Remo.ve “using namespace”

This screensho.t is an unsuccessful test run o.f the “hello. Wo.rld” pro.gram with ![00055.jpeg](images/00055.jpeg)remo.ved. Yo.u can access this saved ide space thro.ugh the fo.llo.wing url: [https://ide.geeksfo.rgeeks.o.rg/vgo.bo.ao.dix](https://ide.geeksforgeeks.org/VgobOAOdiX).

“co.mmenting o.ut” lines o.f co.de is a highly efficient way o.f testing the stability o.f co.de. Yo.u can delete the do.uble fo.rward slashes to. Remo.ve the co.mment and resto.re the line o.f co.de at any time. This allo.ws yo.u to. Test the co.de witho.ut destro.ying it. O.nce yo.u have co.mpleted testing, it is go.o.d practice to. Delete any unwanted lines o.f co.de. During yo.ur testing, yo.u can always return to. This saved instance by using the url abo.ve. Yo.u can also. Access the raw co.de in the index.

When yo.u remo.ve using namespace std the fo.llo.wing erro.r o.ccurs:

Pro.g.cpp: in functio.n 'int main()':

Pro.g.cpp:13:2: erro.r: 'co.ut' was no.t declared in this sco.pe

Co.ut<<"hello. Wo.rld!" << endl;

^

Pro.g.cpp:13:2: no.te: suggested alternative:

In file included fro.m pro.g.cpp:4:0:

/usr/include/c++/5/io.stream:61:18: no.te: 'std::co.ut'

Extern o.stream co.ut; /// linked to. Standard o.utput

^

Pro.g.cpp:13:26: erro.r: 'endl' was no.t declared in this sco.pe

Co.ut<<"hello. Wo.rld!" << endl;

^

Pro.g.cpp:13:26: no.te: suggested alternative:

In file included fro.m /usr/include/c++/5/io.stream:39:0,

Fro.m pro.g.cpp:4:

/usr/include/c++/5/o.stream:590:5: no.te: 'std::endl'

Endl(basic_o.stream<_chart, _traits>& __o.s)

^

Lo.o.king clo.sely, the co.mpiler tells us that we need to. Declare co.ut and endl. It even makes suggestio.ns, like declaring them as std. Let’s do. As the co.mpiler asks and see what happens.

![image8.png](images/00056.jpeg)

Declaring the io.stream o.bjects and manipulato.rs

This screensho.t is a successful test run o.f the “hello. Wo.rld” pro.gram with ![00055.jpeg](images/00055.jpeg)remo.ved. O.nce the io.stream o.bjects and manipulato.rs were successfully declared, the unneeded line was remo.ved.

If yo.u wo.uld like to. Practice, yo.u can use this url: [https://ide.geeksfo.rgeeks.o.rg/vgo.bo.ao.dix](https://ide.geeksforgeeks.org/VgobOAOdiX)

No.te: if yo.u are having multiple erro.rs during yo.ur practice, we will always pro.vide a saved ide wo.rkspace with a successful run o.f the pro.gram to. Help yo.u tro.ublesho.o.t. To. Begin the tro.ublesho.o.ting sessio.n, o.pen up ano.ther windo.w, and navigate to. The successful run. Co.mpare yo.ur current wo.rkspace with the successful run wo.rkspace. Yo.u can find a successful run o.f “declaring the io.stream o.bjects and manipulato.rs” at this link: [https://ide.geeksfo.rgeeks.o.rg/a5zo.dswo.qu](https://ide.geeksforgeeks.org/a5zOdSWoQU).

## **Chapter 3: variables and data types**

We have talked abo.ut ho.w lo.w-level pro.gramming clo.sely resembles machine language, but they differ because they still use elements that are reminiscent o.f human languages like syntax, structures, and variables. Variables are a mathematical co.ncept that humans use to. Co.nvey meaning to. Machines. A huge chunk o.f co.mputer science is reco.gnizing that speech is a series o.f mathematical co.ncepts. This includes and and o.r gates that enable machines to. Make decisio.ns o.n a single data bit level. At a very small scale, bitwise functio.ns can help with many co.mputing pro.cesses, fro.m co.ntro.lling displays to. Switching traffic o.n a server. We will discuss these advanced to.pics later in chapter 4\. Fo.r no.w, let’s deepen o.ur understanding o.f c++ by lo.o.king at variables.

Variables are o.ne o.f the mo.st impo.rtant aspects o.f any pro.gramming language - functio.ns, and o.ther o.peratio.ns o.f a pro.gramming language, generally o.perate o.n variables. We have said that no.t all pro.grams need input o.r o.utput, but all pro.grams will have so.me variable that they are wo.rking o.n o.r there is no.thing to. Wo.rk o.n. The o.utco.me o.f a functio.n is always a state change. A state change is when a machine changes fro.m o.ne decisio.n o.r o.peratio.nal phase to. Ano.ther. This term was used to. Describe o.peratio.ns in o.ld mainframe co.mputers, but we still use it in co.mputer science to. Describe ho.w pro.grams wo.rk. In o.ur example, the ide started with an initialized main() state befo.re the pro.gram ran. Then it switched states to. Execute the o.utput co.mmand.

State changes are discussed o.ften in lo.wer-level languages because o.f ho.w clo.se they are to. Machine language. Lo.wer-level languages are also. Called co.mpiled languages because they are co.mpiled into. Machine language. This is in co.ntrast to. High-level languages like pytho.n. If yo.u remember, we spo.ke o.f ho.w higher-level languages do. No.t need variables to. Be declared with their data types because o.f their built-in libraries. Fo.r instance, pytho.n uses a pytho.n enviro.nment to. Reco.gnize variables and their data types. In c++ variables and the data types have to. Be declared. A data type tells the co.mpiler ho.w to. Treat the data. Data types make mo.re sense when yo.u think o.f vecto.rs in math; unlike integers, which co.mmunicate amo.unts, vecto.rs tell us the size and directio.n o.f space. Therefo.re, vecto.rs are a different data type than an integer. Pro.perties like these are used in so.ftware like pho.to.sho.p to. Help with rendering.

No.te: vecto.r-based images can be manipulated witho.ut lo.sing the quality o.f the image. This is because files like .jpeg o.r .png sto.re pixel lo.catio.n o.f an image as integers o.n a grid. Vecto.r files such as svg o.r .pdf use vecto.rs to. Describe their pixel lo.catio.ns. Therefo.re, when the image is made larger, the vecto.rs indicate ho.w the co.lo.rs sho.uld expand while the regular image files do. No.t. This is what causes the pixelatio.n and disto.rtio.n when manipulating no.n-vecto.r image files.

Input and o.utput: declaring variables

In the previo.us chapter, we declared so.me things as we were learning ho.w to. Use co.ut. In this sectio.n, we are go.ing to. Lo.o.k at examples o.f data types and ho.w they are declared. Belo.w are examples o.f variable declaratio.ns and what they stand fo.r (“c++ variables,” n.d.). Keep in mind that variables essentially sto.re types o.f data:

“![00057.jpeg](images/00057.jpeg)”: keywo.rd is sho.rt fo.r “integer” and sto.res who.le numbers, witho.ut decimals. This keywo.rd includes po.sitive and negative integers.

“![00058.jpeg](images/00058.jpeg)”: sto.res numbers with decimals, bo.th po.sitive and negative numbers.

“![00059.jpeg](images/00059.jpeg)”: keywo.rd is sho.rt fo.r “character” and sto.res single characters regardless o.f their capitalizatio.n. Char values are single quo.ted.

“![00060.jpeg](images/00060.jpeg)”: sto.res text, such as in o.ur "hello. Wo.rld" example. String values are do.uble quo.ted.

“![00061.jpeg](images/00061.jpeg)”: keywo.rd is sho.rt fo.r “bo.o.lean” and sto.res values with two. States: true o.r false. As previo.usly discussed, these values can be expressed as either “0/1” o.r “false/true.”

In the next sectio.n, we will discuss them in detail. No.w let us lo.o.k at examples o.f these. To. Create a variable yo.u have to. Assign it a value after the “=” o.perato.r. Their syntax lo.o.ks like this:

[datatype][variable_name] = [value];

No.te: each ![00062.jpeg](images/00062.jpeg) must be unique within yo.ur functio.n. O.therwise, it will cause an erro.r.

No.w let us create a variable called “mynum” with the int data type and a value o.f 10, then have o.ur pro.gram print it o.ut.

![image2.png](images/00063.jpeg)

**Declaring int numbers**

This screensho.t is a successful test run o.f the “mynum” pro.gram. Yo.u can access the saved ide wo.rkspace with the fo.llo.wing url: [https://ide.geeksfo.rgeeks.o.rg/t4p6qcvfkg](https://ide.geeksforgeeks.org/t4P6qCVfkg).

This co.de was implemented witho.ut ![00055.jpeg](images/00055.jpeg)as it's the best practice. Yo.u sho.uld practice implementing the same co.de successfully with the namespace. Remember that yo.u can reset the wo.rkspace to. A successful state by using the url.

We had o.ur share o.f co.ut examples in o.ur co.de. Let’s use the input bo.x in the to.p right and the cin o.bject so. O.ur pro.gram takes in inputs and o.perates o.n them.

We can do. This by writing pro.grams that take two. Numbers and adds them to.gether. To. Do. This, we have to. Declare two. Variables that will sto.re o.ur inputs fo.r o.ur pro.gram to. O.perate o.n.

We will declare multiple variables:

*   Two.  Int variables named x and y,
*   O.ne int variable named sum.

We can also. Tell the pro.gram to. Pro.mpt the user to. Give two. Inputs.

No.te: in o.ur ide, yo.u must enter the inputs befo.re yo.u run the pro.gram. Each input sho.uld be o.n its o.wn line.

![image46.png](images/00064.jpeg)

**Summing inputs and printing the result**

This screensho.t is a successful test run o.f o.ur “summing” pro.gram. Yo.u can access the saved ide wo.rkspace with the fo.llo.wing url: [https://ide.geeksfo.rgeeks.o.rg/xdxahjutdo.](https://ide.geeksforgeeks.org/xDXaHjutDO). This exercise had to. Be mo.dified fo.r o.ur ide’s input system. Therefo.re, we included additio.nal ![00065.jpeg](images/00065.jpeg)lines that co.nfirm o.ur inputs.

This co.de was implemented witho.ut ![00055.jpeg](images/00055.jpeg) as it's the best practice. Yo.u sho.uld practice implementing the same co.de successfully with the namespace. Remember that yo.u can reset the wo.rkspace to. The successful state by using the url.

**Basic data types**

Data types specify the size and types o.f info.rmatio.n sto.red in a variable. Each has its o.wn keywo.rd and an asso.ciated size (“c++ data types,” n.d) :

“![00057.jpeg](images/00057.jpeg)”: keywo.rd is sho.rt fo.r “integer” and sto.res who.le numbers. Has a size o.f 4 bytes.

“![00066.jpeg](images/00066.jpeg)”: sto.res decimal numbers with 7 decimal digits. Has a size o.f 4 bytes.

“![00058.jpeg](images/00058.jpeg)”: sto.res decimals numbers with 15 decimal digits. Has a size o.f 8 bytes.

“![00059.jpeg](images/00059.jpeg)”: keywo.rd is sho.rt fo.r “character” and sto.res single characters regardless o.f their capitalizatio.n. Has a size o.f 1 byte.

“![00061.jpeg](images/00061.jpeg)”: keywo.rd is sho.rt fo.r “bo.o.lean” and sto.res values that have a state o.f either being true o.r false. Has a size o.f 1 byte.

No.te: recall the “![00060.jpeg](images/00060.jpeg)” data type. We have wo.rked with this special datatype extensively. String values can vary in size. Due to. This, they are handled in the io.stream library to. Apply mo.re flexibility fo.r text handling. We’ll return to. Strings and discuss so.me advanced to.pics in the next sectio.n.

These sizes matter fo.r data handling. Fo.r instance, when yo.u use int with flo.at/do.uble all tho.se numbers will be co.nverted to.  Int. It is because the co.mpiler uses 4 bytes to. Calculate integers which have the allo.catio.n fo.r decimals. The pro.gram will still run but yo.ur calculatio.ns will no.t be accurate. Let’s explo.re this mo.re by mo.difying o.ur pro.gram and lo.o.king at the results. We are go.ing to. Be using a lo.ng-po.pular decimal number (pi):

![00067.jpeg](images/00067.jpeg). It will test the limits o.f flo.at and do.uble.

![image33.png](images/00068.jpeg)

Using int with flo.at o.r do.uble

This screensho.t is a successful test run o.f o.ur mo.dified pro.gram calculating ![00069.jpeg](images/00069.jpeg)

![00070.jpeg](images/00070.jpeg)

![00071.jpeg](images/00071.jpeg)

![00072.jpeg](images/00072.jpeg), which are no.t mo.dified to. Sto.re decimals. As a result, the result is missing the decimals.

To. Get the result we are lo.o.king fo.r, it wo.uld be best to. Change the variable data types. Will using flo.at data types differ fro.m do.uble data types? Can we expect a different result? Remember yo.u can reset by go.ing to. A successful state o.f the wo.rkspace using the url.

![image51.png](images/00073.jpeg)

Co.mparing flo.at and do.uble

This screensho.t is a successful test run o.f o.ur mo.dified pro.gram calculating ![00074.jpeg](images/00074.jpeg), we have remo.ved the input statements and rearranged o.ur data types. We highly suggest creating this pro.gram fo.r yo.urself using the previo.us pro.gram lo.cated at this url: [https://ide.geeksfo.rgeeks.o.rg/a8mw6tmyf8](https://ide.geeksforgeeks.org/a8Mw6tmyf8). This exercise will give yo.u practice in so.me previo.us co.ding to.pics we discussed, including:

1.  “![00061.jpeg](images/00061.jpeg)” data type keywo.rd
2.  “![00042.jpeg](images/00042.jpeg)” input-o.utput manipulato.r

It will also. Give yo.u so.me experience with a lo.gical o.perato.r. We will discuss the lo.gical o.perato.rs in detail in the next chapter. O.nce yo.u have manipulated the pro.gram, o.pen a new windo.w, and co.mpare this to. The successful run o.f the screensho.t abo.ve. Yo.u can find the saved ide wo.rkspace with the successful run at this url: [https://ide.geeksfo.rgeeks.o.rg/dniudytn7m](https://ide.geeksforgeeks.org/dNIUdYtN7M).

Po.wer o.f c++: advanced strings

Ano.ther data type we are go.ing to. Lo.o.k at is strings. Strings are o.ne o.f the mo.st po.pular data types in co.mputer science; they are sequences o.f characters. It might be helpful to. Think o.f them as sentences, but no.t every sentence represents a string. We have seen ho.w they wo.rk with o.ur “hello. Wo.rld” app. Strings are a separate data type with their o.wn library. To. Manipulate and wo.rk with them a pro.gram needs an appro.priate header – the string library. These libraries have metho.ds and features that allo.w the pro.gram to. Manipulate strings.

O.peratio.n: string co.ncatenatio.n

String co.ncatenatio.n is when different strings are put to.gether into. O.ne string. It is co.mbining strings. This is o.ne o.f the mo.st co.mmo.n functio.ns o.f a pro.gram. Fo.r instance, when yo.u enter yo.ur name at a website o.r a game and then yo.u switch to. Ano.ther page and the screen greets yo.u “hello., [yo.ur_name]!”, the pro.gram has used co.ncatenatio.n to. Do. That. It has co.mbined “hello.,” with yo.ur name and “!” In the end.

In c++, string co.ncatenatio.ns are perfo.rmed thro.ugh the “+” o.perato.r. Let’s see this in actio.n by making a pro.gram that prints an imputed string with a greeting. Fo.r this to. Wo.rk, we must include the <string> library, which co.ntains o.bjects and statements needed fo.r handling strings.

O.pen a fresh instance o.f the ide we have been using and fo.llo.w these steps:

*   In additio.n to.  ![00075.jpeg](images/00075.jpeg) library
*   O.mit ![00055.jpeg](images/00055.jpeg)
*   Remo.ve the current filler co.de within ![00076.jpeg](images/00076.jpeg)
*   Declare and set the variables ![00077.jpeg](images/00077.jpeg)
*   Declare and calculate ![00078.jpeg](images/00078.jpeg)” o.perato.r
*   Print o.ut the result as “hello. Jo.hn do.e.”

It sho.uld lo.o.k so.mething like this:

![image14.png](images/00079.jpeg)

String co.ncatenatio.n

This screensho.t is a successful test run o.f o.ur string co.ncatenatio.n pro.gram. We enco.urage yo.u to. O.pen up this pro.gram in ano.ther windo.w and co.mpare it to. Yo.ur pro.gram. Yo.u can access the successful run at this url: [https://ide.geeksfo.rgeeks.o.rg/b7xerpi9o.e](https://ide.geeksforgeeks.org/B7XErpI9OE).

No.te: be sure to. Anno.tate yo.ur co.de. Yo.u can sho.rthand the instructio.ns and use them as an impro.mptu algo.rithm to. Anno.tate yo.ur co.de. This will help yo.u keep the pro.gram in o.rder.

Usually, in fo.rums, the co.ncatenated text input is kept small as po.ssible and the fo.rmatting is do.ne by the pro.gram. In the example, we manually have to. Add space after “hello.” And “jo.hn”, but the pro.gram adds space. No.w that yo.u have seen ho.w the “+” o.perato.r wo.rks, ho.w might yo.u add space? See if yo.u can figure it o.ut by playing with the co.de in yo.ur edito.r. If things fall apart yo.u can always return to. O.ur successful ide wo.rkspace by clicking o.n the url.

No.te:

The “+” o.perato.r is used fo.r bo.th adding numbers and co.ncatenating strings.trying to. Use the o.perato.r to. Add a string and a number will pro.duce an erro.r.yo.u can test this o.n yo.ur o.wn using a mo.dified pro.gram fro.m the previo.us chapter.yo.u can also. Check o.ut a successful run o.f the pro.gram here that sho.ws ho.w to. Co.ncatenate numbers as strings at this url:

Https://ide.geeksfo.rgeeks.o.rg/glpmsldwf7.unco.mment the declaratio.ns to. Try to. Add numbers and strings to. See the erro.r fo.r yo.urself.the erro.r is very lo.ng and verbo.se,as it co.nflicts acro.ss the <io.stream> and <string>libraries.

String o.bjects: length() attribute

We kno.w fro.m real-wo.rld experience that strings, like many things, can co.me in different sizes. This is unlike o.ther data types we have explo.red so. Far. C++ makes this po.ssible because it co.nstrues strings as o.bjects with attributes. C++ defines a string length under the length() attribute as yo.u wo.uld expect in an o.bject. To. Access length, the string must be attached to. A variable and yo.u must use the “.” Syntax. It sho.uld lo.o.k so.mething like this:

[string_name].length()

Let’s return to. O.ur pro.gram and retrieve the length o.f fullname. We will need to. Mo.dify o.ur co.de by adding a new line with the syntax abo.ve and ano.ther co.ut, like this:

![image24.png](images/00080.jpeg)

**Print fullname.length()**

This screensho.t is a successful test run o.f o.ur mo.dified string co.ncatenatio.n pro.gram. We enco.urage yo.u to. Mo.dify the pro.gram at this url: [https://ide.geeksfo.rgeeks.o.rg/b7xerpi9o.e](https://ide.geeksforgeeks.org/B7XErpI9OE).

O.nce yo.u have mo.dified the pro.gram, yo.u can co.mpare it to. This successful test run by o.pening it in ano.ther windo.w. Yo.u can access this saved ide windo.w at the fo.llo.wing url: [https://ide.geeksfo.rgeeks.o.rg/xbjo.6pg3nh](https://ide.geeksforgeeks.org/xbjO6Pg3Nh).

**String indexes and arrays**

Recall o.ur co.nversatio.n o.n o.bjects. Vecto.r arrays are also. A special mathematical pheno.meno.n with their o.wn special attributes. An array is an o.rderly arrangement o.f o.bjects – o.ften ro.ws, co.lumns, o.r a matrix – where each has its o.wn specific lo.catio.n. Strings are sto.red in arrays made up o.f characters. Therefo.re, a string array is o.rderly arrangements o.f characters where each character in a string is indexed in its o.wn lo.catio.n. Arrays are accessed by using [ ] to. Find a character o.r any o.ther items in an array. String indexes start with [0]. Let’s see this in actio.n by changing o.ur pro.gram so. That it prints o.ut the 3^(rd) character in fullname.

No.te:

Remember that the index starts with [0].therefo.re the 3rd character in the string array wo.uld be at [2], no.t 3.

We are go.ing to. Use this syntax to. Do. So.:

Fullname[x]

The x stands fo.r the index o.f the character we wo.uld like to. Print o.ut. Remember to. Also. Edit the co.ut  to. Pro.perly print the letter. Yo.u will also. Need to. Use escape sequences like this:

![image10.png](images/00081.jpeg)

**Access fullname string array**

This screensho.t is a successful test run o.f o.ur mo.dified string attributes pro.gram. We enco.urage yo.u to. Mo.dify the pro.gram at this url:

[Https://ide.geeksfo.rgeeks.o.rg/xbjo.6pg3nh](https://ide.geeksforgeeks.org/xbjO6Pg3Nh).

O.nce yo.u have mo.dified the pro.gram, yo.u can co.mpare it to. This successful test run by o.pening it in ano.ther windo.w. Yo.u can access this saved ide windo.w at the fo.llo.wing url: [https://ide.geeksfo.rgeeks.o.rg/jwsg7hb2ms](https://ide.geeksforgeeks.org/JWSG7HB2Ms).

In o.ur examples we have relied a lo.t o.n co.ut capabilities, but, as i have alluded to., there are o.ther strings handling capabilities used by pro.grammers to. Field co.ntent fro.m different so.urces. These are cin o.bjects and the getline() functio.n.

Cin and getline() functio.n

In examples fro.m the previo.us chapter, we have used cin. Like co.ut, cin is an o.bject in the <io.stream> library and it allo.ws a pro.gram to. Receive input using the “>>” o.perato.r. Like co.ut, cin o.bjects must be defined with the std data type. Let’s mo.dify o.ur co.ncatenatio.n pro.grams so. That it receives the input o.f “jo.hn do.e”. Yo.u can use yo.ur name if yo.u like, as it can be fun to. Do. So.. Yo.u will need to. Fo.llo.w these instructio.ns:

*   Navigate to. The string co.ncatenato.r pro.gram at the fo.llo.wing url:
*   [Https://ide.geeksfo.rgeeks.o.rg/b7xerpi9o.e](https://ide.geeksforgeeks.org/B7XErpI9OE)
*   Declare the variables
*   Pro.mpt the user fo.r their name
*   Calculate the o.peratio.n by using the fo.llo.wing co.de snippet:

….����������������=������������������++����������������…

*   Print the results

If yo.u find yo.urself stuck, here is ho.w it sho.uld lo.o.k:

![image26.png](images/00082.jpeg)

String co.ncatenatio.n with cin

This screensho.t is a successful test run o.f o.ur mo.dified string co.ncatenatio.n pro.gram using ![00083.jpeg](images/00083.jpeg). We enco.urage yo.u to. O.pen up this pro.gram in ano.ther windo.w and co.mpare it to. Yo.ur pro.gram. Yo.u can access the successful run at this url: [https://ide.geeksfo.rgeeks.o.rg/kyulgbo.ica](https://ide.geeksforgeeks.org/KyuLgBoicA).

No.te: be sure to. Anno.tate yo.ur co.de. Yo.u can sho.rthand the instructio.ns and use them as an impro.mptu algo.rithm to. Anno.tate yo.ur co.de. This will help yo.u keep the pro.gram in o.rder.

The pro.gram will wo.rk o.nly when the user enters their first and last name separately. But mo.st peo.ples’ names are sto.red o.r put in as o.ne single string. Let’s change o.ur pro.gram so. That it greets the user when they enter their full name. Yo.u will need to. Fo.llo.w these steps:

1.  If no.t there already, o.r yo.u need to. Reset the wo.rkspace, go. To. The previo.us wo.rkspace at the fo.llo.wing url:

[Https://ide.geeksfo.rgeeks.o.rg/kyulgbo.ica](https://ide.geeksforgeeks.org/KyuLgBoicA)

1.  Declare o.nly the ![00084.jpeg](images/00084.jpeg) variable
2.  Pro.mpt the user fo.r their full name using ![00083.jpeg](images/00083.jpeg)
3.  Greet the user using ![00085.jpeg](images/00085.jpeg)

![image25.png](images/00086.jpeg)

String terminatio.n with cin

This screensho.t is an unsuccessful test run o.f o.ur mo.dified string co.ncatenatio.n pro.gram using ![00083.jpeg](images/00083.jpeg). While the pro.gram co.mpleted with no. Erro.rs, we did no.t get an expected result. If yo.ur pro.gram had erro.rs after yo.ur mo.dificatio.ns o.r did no.t get a similar result, we enco.urage yo.u to. Use o.ur successful run to. Tro.ublesho.o.t yo.ur wo.rkspace. O.pen up this successful run in ano.ther windo.w and co.mpare it to. Yo.ur pro.gram. Yo.u can access the successful run at this url: [https://ide.geeksfo.rgeeks.o.rg/au6gzpaxwn](https://ide.geeksforgeeks.org/aU6GZpAxwn).

Yo.u have witnessed typical cin behavio.r. When cin enco.unters a space it reads it as a string terminato.r and sto.ps. This is why “do.e” is no.t added to. The o.utput. To. Get it to. Read the entire string with spaces, we must use the getline() functio.n fro.m the <string> library; it extracts all characters fro.m the input and turns them into. A string array.

No.te:

Getline()is usually preferred o.ver cin to. Ensure that pro.grams can read fielded text fro.m seco.ndary so.urces,particularly since getline() can read and aggregate different so.rts o.f characters witho.ut erro.rs.

Here is an example o.f getline() functio.ns used well: https://www.geeksfo.rgeeks.o.rg/getline-string-c/

In this chapter, we have do.ne quite a bit. We have lo.o.ked at specialized functio.ns, accessing o.bjects, text manipulato.rs, and o.perato.rs. We will co.ver them in mo.re detail in the co.ming chapters. I ho.pe yo.u have seen the ro.le o.f o.perato.rs in directing data and lending pro.gram functio.nality. In the fo.llo.wing chapter, we are go.ing to. Be lo.o.king at o.perato.rs and ho.w they give pro.grams decisio.n-making capabilities.

## Chapter 4: o.peratio.ns in c++

We talked abo.ut ho.w c++ is mainly a back-end, server-side language that is suited fo.r co.ntro.lling servers and o.ther decisio.n-making utilities fo.r delivering co.ntent. In the last chapter, we lo.o.ked at small ways that c++ handles data by lo.o.king at strings. In it, we saw the central ro.le that o.peratio.ns play. O.peratio.ns allo.w us to. Co.ntro.l lo.o.ps and decisio.n making in pro.grams. A better understanding o.f o.peratio.ns allo.ws us to. Add mo.re functio.nality to. O.ur pro.grams. Functio.nality is ho.w pro.grammers use metho.ds and features o.f a language to. Achieve an end. We have seen ho.w these string handling metho.ds wo.rk, but what wo.uld be better is if we used tho.se features in a co.ntext that allo.ws us to. Achieve a particular end, like co.ntent management.

No.te: “o.perand” describes the value o.r variable being o.perated o.n. “o.perato.r” describes the symbo.l indicating the so.rt o.f o.peratio.n being carried o.ut [(“c++ o.perato.rs,” n.d.)](https://www.zotero.org/google-docs/?7v1273).

The fo.llo.wing is a list o.f o.perato.rs in c++ (“o.perato.rs-in-c.png (800×533),” n.d.):

![D:\ЗАГРУЗКИ\Nelly\1.png](images/00087.png)

This table lists the o.perato.r symbo.ls and catego.rizes them by (1) ho.w many o.perands they accept at a time > (2) the type o.f o.peratio.n they implement. Fo.r example, mo.st arithmetic o.perato.rs o.perate o.n two. O.perands at a time.

All o.perato.rs are characterized by ho.w many o.perands they can o.perate o.n at a time and the types o.f o.peratio.ns they can execute. They are divided into. Three types:

Unary - o.perato.rs that o.nly accept 1 o.perand at a time

Binary - o.perato.rs that o.nly accept 2 o.perands at a time

Ternary - o.perato.rs that accept mo.re than 2 o.perands, o.r co.nditio.nal o.perato.rs with several arguments

They are further divided into. 6 mo.re types:

1.  Arithmetic
2.  Relatio.nal
3.  Lo.gical
4.  Bitwise
5.  Assignment o.perato.rs
6.  O.ther o.perato.rs such as a co.nditio.nal, address, and redirectio.n

In this chapter, we will lo.o.k at 5 types o.f o.perato.rs and their functio.nalities.

No.te: o.perato.rs have precedence, just as in mathematical equatio.ns. Fo.r example, parentheses, which are used to. Call a functio.n, have higher precedence than additio.n o.r subtractio.n. Ho.wever, yo.u sho.uld try to. Keep yo.ur lines o.f co.de as simple as po.ssible. This makes yo.ur pro.grams easier to. Edit and debug. Having clean, unco.mplicated co.de avo.ids bugs.

Binary o.perato.rs

Binary o.perato.rs are the majo.rity o.f o.perands yo.u find in c++. They include 5 o.f the 6 types o.f o.perato.rs. This makes them the perfect place to. Start. As the name suggests, binary o.perato.rs co.mpare two. O.perands. They are perfect fo.r decisio.n-making and co.ntro.lling switches.

Arithmetic o.perato.rs

They are the mo.st co.mmo.n and well understo.o.d o.f all o.perato.rs because o.f ho.w much we use them even o.utside pro.gramming, since they are primarily mathematical. We use them to. Perfo.rm mathematical o.peratio.ns.

No.te: in the string co.ncatenatio.n example, the “![00088.jpeg](images/00088.jpeg)” used to. Co.ncatenate was no.t an arithmetic functio.n. Instead, it was a functio.n o.f the ![00089.jpeg](images/00089.jpeg) library that handled the co.ncatenatio.n.

Mo.st o.perato.rs in this catego.ry require two. O.perands. The o.nly exceptio.ns are the unary “++” and “ - -“ o.perato.rs which we use to. Increase o.r decrease within a lo.o.p. The binary o.perato.rs are (jaggi, 2015a):

“![00088.jpeg](images/00088.jpeg)”: the additio.n o.perato.r that adds two. O.perands

“![00090.jpeg](images/00090.jpeg)”: the subtractio.n o.perato.r that subtracts o.ne o.perand fro.m ano.ther

“![00091.jpeg](images/00091.jpeg)”: the multiplicatio.n o.perato.r that multiplies two. O.perands

“![00092.jpeg](images/00092.jpeg)”: the divisio.n “fo.rward slash” o.perato.r that divides the first o.perand into. The seco.nd

“![00093.jpeg](images/00093.jpeg)”: the mo.dulus o.perato.r that returns the remainder fro.m dividing the first o.perand into. The seco.nd

Let’s make a co.ut pro.gram that demo.nstrates all o.f these 5 arithmetic o.perands. Create a new c++ wo.rkspace in the ide and fo.llo.w these instructio.ns:

1.  Declare two. Variables ![00094.jpeg](images/00094.jpeg) as integers
2.  Declare a variable, ![00095.jpeg](images/00095.jpeg)
3.  Print the variables ![00096.jpeg](images/00096.jpeg)
4.  Add ![00096.jpeg](images/00096.jpeg) and print the result
5.  Subtract ![00097.jpeg](images/00097.jpeg) and print the result
6.  Multiply ![00097.jpeg](images/00097.jpeg) and print the result
7.  Divide ![00097.jpeg](images/00097.jpeg) and print the result
8.  Calculate the remainder fro.m dividing ![00096.jpeg](images/00096.jpeg) and print the result

Here is ho.w that lo.o.ks.

![image35.png](images/00098.jpeg)

Arithmetic ro.utine pro.gram

This screensho.t is a successful run o.f the arithmetic ro.utine pro.gram displaying all the arithmetic functio.ns. Yo.u can access a co.py o.f the raw co.de in the index.

If yo.u get erro.rs, i enco.urage yo.u to. Use o.ur successful run to. Tro.ublesho.o.t yo.ur wo.rkspace. O.pen it up to. Co.mpare the co.de. Here is where to. Find it:

[Https://ide.geeksfo.rgeeks.o.rg/vdcch7f5eq](https://ide.geeksforgeeks.org/vDcCH7f5EQ)

Relatio.nal o.perato.rs

Mo.st pro.grams, no.t just in c++, use co.nditio.nals and lo.o.ps to. Co.ntro.l flo.w. O.perato.rs in this sectio.n are used to. Perfo.rm co.nditio.nal switching. Fo.r instance, in games, the game engine adapts to. Ho.w the player interacts with the game. It gives the gamer mo.re o.f an engaging and dynamic experience.

If the gamer co.mpletes challenges quickly, it might mean they find the game to.o. Easy. As a result, the game adjusts by increasing difficulty, but no.t to.o. Much. If the game is to.o. Hard, the engine might respo.nd to. That by making it a little easier to. Play. This is called dynamic gameplay, and it happens because co.ding languages have co.nditio.nal switching. Co.nditio.nal switching, the adaptatio.n, happens thro.ugh relatio.nal o.perato.rs that co.mpare two. Values. All relatio.nal o.perato.rs are binary (jaggi, 2015b). Here they are:

“![00099.jpeg](images/00099.jpeg)”: “equal” o.perato.r that checks whether two. Given o.perands are equal. If the o.perands are equal, it returns a bo.o.lean “true”; if no.t, it returns false.

“![00100.jpeg](images/00100.jpeg)”: “no.t-equal” o.perato.r that also. Checks whether two. Given o.perands are equal o.r no.t. Ho.wever, this o.perato.r returns a bo.o.lean true if the o.perands are no.t equal and returns false if the o.perands are equal.

“![00101.jpeg](images/00101.jpeg)”: “greater-than” o.perato.r that checks if the o.perand o.n the left is greater than the o.perand o.n the right. If so., this o.perato.r returns a bo.o.lean true. O.therwise, it returns false.

“![00102.jpeg](images/00102.jpeg)”: “less-than” o.perato.r that checks if the o.perand o.n the left is less than the o.perand o.n the right. If so., this o.perato.r returns a bo.o.lean true. It returns bo.o.lean false o.therwise.

“![00103.jpeg](images/00103.jpeg)”: “greater-than o.r equal-to.” O.perato.r that checks if the o.perand o.n the left is greater than o.r equal to. The o.perand o.n the right. If so., this o.perand returns a bo.o.lean true. If no.t, it returns a bo.o.lean false.

“![00104.jpeg](images/00104.jpeg)”: “lesser-than o.r equal-to.” O.perato.r that checks whether the o.perand o.n the left is less than o.r equal to. The o.perand o.n the right. If so., this o.perand returns a bo.o.lean true. If no.t, it returns false.

Like we did with the arithmetic o.perato.rs, let’s create a co.ut pro.gram which demo.nstrates relatio.nal o.perato.rs, we are go.ing to. Be using co.nditio.nal if() statements in o.ur co.de. An if() statement executes the co.de within its curly braces when a specified co.nditio.n is met. If the co.nditio.n is no.t met it will execute the co.de in the else{} statement. The else do.es no.t have a co.nditio.n to. Check; it executes when the specified co.nditio.n in if() is no.t met. Co.nditio.nal statements always use a relatio.nal o.perato.r to. Test a co.nditio.n.

No.te:

The if(ဢ) and else statement is case sensitive.bo.th “if” and “else” must be lo.wercase.additio.nally,while if() can be executed witho.ut an else,the missing else statement can cause an erro.r if the co.nditio.n is false.else statements also. Canno.t be implemented witho.ut an if()statement.we will describe if()...else statements in mo.re detail in later chapters

To. Create o.ur pro.gram we have to. Fo.llo.w the fo.llo.wing steps.

1.  O.pen and edit the arithmetic ro.utine pro.gram using this url:

1.  [Https://ide.geeksfo.rgeeks.o.rg/vdcch7f5eq](https://ide.geeksforgeeks.org/vDcCH7f5EQ)

1.  Use the same variables fro.m the arithmetic ro.utine. Be sure to. Clean the co.de o.f any unneeded variables.
2.  Print an explanatio.n o.f the pro.gram
3.  Test ![00105.jpeg](images/00105.jpeg) and print the result

1.  Create an if statement printing o.ut the result if greater than
2.  Create a nested else statement printing o.ut the result if false

No.te: fo.r each ![00106.jpeg](images/00106.jpeg) fo.r all po.ssibilities. Fo.r o.ur simple pro.gram, it is o.nly two. Po.ssibilities fo.r each statement.

1.  Test ![00107.jpeg](images/00107.jpeg) and print the result
2.  Test ![00108.jpeg](images/00108.jpeg) and print the result
3.  Test ![00109.jpeg](images/00109.jpeg) and print the result
4.  Test ![00110.jpeg](images/00110.jpeg)and print the result
5.  Test ![00111.jpeg](images/00111.jpeg) and print the result

![image4.png](images/00112.jpeg)

Relatio.nal ro.utine pro.gram

This screensho.t is a successful run o.f the relatio.nal ro.utine pro.gram displaying all the relatio.nal functio.ns.

If yo.u did no.t get similar results, go. Lo.o.k at o.ur co.de here: [https://ide.geeksfo.rgeeks.o.rg/dfd3cek85y](https://ide.geeksforgeeks.org/dFD3cEk85y). Co.mpare and figure o.ut where yo.u went wro.ng. An exercise like this o.ne will equip yo.u with debugging skills.

Also., take yo.ur time to. Appreciate the co.de and understand it.

Lo.gical o.perato.rs

Lo.gical o.perato.rs add mo.re co.mplexity to. Relatio.nal o.perato.rs. These are co.mparable to. Human ideas o.f “and” o.r “o.r”. They also. Have qualities that switch the meaning o.f the relatio.nal o.perato.r. Lo.gical o.perato.rs are used in co.njunctio.n with relatio.nal o.perato.rs to. Co.mbine two. O.r mo.re co.nditio.ns to. Describe a co.nstraint. They make us catch a lo.t mo.re and do. A lo.t mo.re with o.ur co.nditio.nals. There are three lo.gical o.perato.rs (jaggi, 2015b):

“”: the lo.gical “and” o.perato.r returns a bo.o.lean true when bo.th the co.nditio.ns are met and false if they aren’t.

“![00113.jpeg](images/00113.jpeg)”: the lo.gical “o.r” o.perato.r returns a bo.o.lean true when o.ne (o.r bo.th) o.f the co.nditio.ns are met, and false if no.ne o.f the co.nditio.ns are met.

“![00114.jpeg](images/00114.jpeg)”: the lo.gical “no.t” o.perato.r returns a bo.o.lean true if the co.nditio.ns in co.nsideratio.n are no.t satisfied. If o.ne o.f the co.nditio.ns is true, then it returns a bo.o.lean false.

Lo.gical o.perato.rs are used a lo.t in machines. Imagine a “no.t” o.perato.r in the security system o.f a bank. Let’s say lo.cked do.o.rs are “0”[false], and unlo.cked do.o.rs are “1”. Because the bank sho.uld stay secure, o.ur default value is “0.” This is called a failed clo.sed system, because if things go. Wro.ng the do.o.rs will be clo.sed (the default). All signals that go. To. The do.o.r are co.ntro.lled by a “no.t” signal: if no.thing is go.ing o.n, the do.o.rs sho.uld remain lo.cked, and if there is ro.bbery they sho.uld also. Remain lo.cked. Do.o.rs that o.pen during a ro.bbery will get a “no.t” signal to. Fail-clo.se. But in a fire, these do.o.rs sho.uld o.pen, so. The fail-clo.sed “no.t” signal will return true to. O.pen do.o.rs.

Let’s explo.re lo.gical o.perato.rs by building a lo.gical ro.utine pro.gram. Fo.llo.w these instructio.ns:

1.  O.pen and edit the relatio.nal ro.utine pro.gram using this url:

[Https://ide.geeksfo.rgeeks.o.rg/dfd3cek85y](https://ide.geeksforgeeks.org/dFD3cEk85y)

1.  Edit these additio.nal variables to. Test the lo.gical o.perato.rs:

![00115.jpeg](images/00115.jpeg)

1.  Print an explanatio.n o.f the pro.gram

1.  Test if(a>b && c==d) and print the result

1.  Create an if statement printing o.ut the result if greater than
2.  Create a nested else statement printing o.ut the result if false

1.  Test (a>b || c==d) and print the result

1.  Test (!B) and print the result

1.  Clean the co.de o.f any unnecessary lines

Here is ho.w it lo.o.ks:

![image54.png](images/00116.jpeg)

Lo.gical ro.utine pro.gram

This screensho.t is a successful run o.f the lo.gical ro.utine pro.gram displaying examples o.f all the lo.gical functio.ns. Yo.u can access this wo.rkspace with this url: [https://ide.geeksfo.rgeeks.o.rg/x9ixjuydbg](https://ide.geeksforgeeks.org/x9ixjUYDBG)

As yo.u can see, the “and” functio.n may be difficult to. Print with just o.ne ![00117.jpeg](images/00117.jpeg)

![00118.jpeg](images/00118.jpeg) statements. Mo.dify this exercise to. Create a pro.gram that can explain itself better! Hint: yo.u o.nly need o.ne additio.nal ![00119.jpeg](images/00119.jpeg) statement. Yo.u can check yo.ur wo.rk against o.urs with this url -- [https://ide.geeksfo.rgeeks.o.rg/nh8yyv9kjy](https://ide.geeksforgeeks.org/nh8yYV9Kjy).

Let’s take a break fro.m ro.utines and explo.re o.ther ways we can use lo.gical o.perato.rs. Lo.gical o.perato.rs are based o.n machine lo.gic, especially lo.gical gates. Lo.gical gates are electro.nic circuits that have o.ne o.r mo.re inputs while having o.ne o.utput. Lo.gical gates have the same functio.n as lo.gical o.perato.rs. “and” gates o.nly pass “1” when all inputs are “1”; “o.r” gates pass “1” when they receive a “1” fro.m any o.f their inputs; “no.t” passes “1” when they receive a “0” as their input.

Lo.gical gates can co.ntro.l the flo.w o.f data in a circuit, the same as o.ur lo.gical o.peratio.ns when co.mbined with a co.nditio.nal statement. It is called a co.nditio.nal sho.rt-circuit in lo.gical o.perato.rs.

Lo.gical and o.perato.rs and o.r o.perato.rs sho.rt-circuit. Recall ho.w lo.gical and returns a true bo.o.lean value when bo.th relatio.nal o.perato.rs are co.nditio.nally true. What’s mo.re, relatio.nal o.perato.rs are assessed in the o.rder that they appear in a co.nditio.nal statement – if the first o.ne is false the seco.nd o.ne will no.t be evaluated, so. It sho.rt circuits.

O.r o.perato.rs do. This differently. O.nly o.ne relatio.nal o.perato.r has to. Return true fo.r it passes a true bo.o.lean value. So. If the first relatio.nal o.perato.r returns true, it wo.n't check the next o.ne.

This is very useful because we can give mo.re co.mplex instructio.ns to. A pro.gram abo.ut ho.w to. Behave in what circumstances. O.r and and are sho.rt-circuit o.ppo.sites. Let’s use this to. Write a pro.gram that tells when a co.nditio.n sho.rt-circuits and and o.r gates.

Fo.llo.w these instructio.ns:

1.  O.pen a new ide wo.rkspace
2.  Declare two.  ![00057.jpeg](images/00057.jpeg) variables:

![00120.jpeg](images/00120.jpeg)

1.  Print an explanatio.n o.f the pro.gram

1.  This pro.gram will test if the o.r gate o.r the and gate sho.rts when a is equal to. B.
2.  Print current values o.f a and b

1.  Declare and calculate two.  ![00061.jpeg](images/00061.jpeg) variables:

1.  Resand = ((a == b) && std::co.ut << "o.r circuit sho.rted")
2.  Reso.r = ((a == b) || std::co.ut << "and circuit sho.rted")

This is ho.w it lo.o.ks:

![image27.png](images/00121.jpeg)

Sho.rt circuit detectio.n pro.gram

This screensho.t is a successful run o.f o.ur sho.rt circuit detectio.n pro.gram. Using o.ur kno.wledge o.f lo.gical and, lo.gical o.r, and their relatio.nship to. Each o.ther, we were able to. Develo.p a way to. Detect sho.rt circuits. Yo.u can access this wo.rkspace with this url: [https://ide.geeksfo.rgeeks.o.rg/ublgtlbnny](https://ide.geeksforgeeks.org/uBLGtLbnnY)

Try different values o.f ![00097.jpeg](images/00097.jpeg) to. See if yo.u can trip the different “circuits.”

Co.nsider a sho.rt circuit detectio.n pro.gram. Ho.w wo.uld we use it in the real wo.rld? I have alluded to. Systems like these playing a ro.le in bank security. The questio.n is ho.w it wo.uld achieve tho.se things? Yo.u can tell yo.ur pro.gram that if a co.nditio.n is no.t (“no.t”) met to. Refuse access, like if the passwo.rd do.es no.t match.

An understanding o.f lo.gical o.perato.rs gives a go.o.d idea o.f ho.w machines and systems make their decisio.ns. Relatio.nal and lo.gical o.perato.rs give us mo.re co.ntro.l o.ver what happens in the pro.gram and ho.w it relates to. Everything aro.und it. We do. This thro.ugh vario.us libraries, statements, and o.bjects. So. Far we have written small pro.grams, but in bigger pro.grams using o.bjective co.ntro.l like these can cause o.verhead fo.r the co.mpiler. That has a no.ticeable effect in pro.gramming enviro.nments and industries like gaming engines, co.ntent delivery, and o.thers. Think abo.ut the servers at yo.utube that have to. Deliver gigabytes o.f data per seco.nd and gaming engines that need to. Render in real-time: they have to. Reduce the amo.unt o.f o.verhead while being able to. Utilize these co.ntro.l features. Thankfully, that can be achieved by using bitwise o.perato.rs.

Bitwise o.perato.rs

O.n the circuit level, machines co.mmunicate by using and and o.r gates. It gives them decisio.n-making  capabilities at a single bit data level. Bitwise o.perato.rs use tho.se micro.sco.pic level calculatio.ns to. Access co.mputing pro.cesses at the machine level, bypassing o.bjective pro.gramming. In o.ther wo.rds, they are lo.gical o.perato.rs o.perating o.n numbers at a binary level.

To. Use them, yo.u will need to. Kno.w abo.ut binary. Humans co.nceptualize numbers using base-10 numbers, also. Kno.wn as the decimal system. Fo.r instance, a number like 543 is understo.o.d as five-hundreds, three tens, and 4 single units. In base 10 it lo.o.ks like this:

![00122.jpeg](images/00122.jpeg)

In binary the same number wo.uld lo.o.k like this 0b1000010110 – the “0b” is just fo.r us humans to. Understand it is a binary number. Binary numbers are base-2, they just lo.o.k different. All binary numbers are presented as a stream o.f bits, which can either be in two. States: 1 o.r 0. Like in base-10, the po.sitio.n o.f the number determines its value. The 534 example sho.ws a binary number that is 10 bits lo.ng. Lo.o.king clo.sely at the 534 streams we can see that the 2^(nd), 3^(rd), 4^(th), and 10^(th) bits are o.n (mo.ving right to. Left), and all the o.ther bits are o.ff ( 1 is o.n, 0 is o.ff). In base 2 we calculate this as:

![00123.jpeg](images/00123.jpeg)

It is no.t easy fo.r us humans to. Calculate it, but this is ho.w co.mputers co.mmunicate, in streams o.f data bits. They are mo.re adept at reco.gnizing and co.unting these numbers just as easily as if they were base-10 numbers to. Humans. Therefo.re, using bitwise o.perato.rs that functio.n at the co.mputer’s natural level impro.ves speed and perfo.rmance [(killian, 2012)](https://www.zotero.org/google-docs/?w3RGU2) because it skips the translatio.n o.f o.bjective pro.gramming into. Machine language. This is why yo.u will find bitwise o.peratio.ns are o.ften used in co.mpetitive pro.gramming. Belo.w is a list o.f c++ bitwise o.perato.rs (“bitwise o.perato.rs in c/c++,” 2014):

“”: bitwise and takes two. Numbers (o.perands) and runs and o.n every bit within the stream o.f tho.se numbers. The results o.f the and stream will be 1 if bo.th are 1.

“![00124.jpeg](images/00124.jpeg)”: bitwise o.r takes two. Numbers(o.perands) and runs o.r o.n every bit within the stream o.f tho.se numbers. The results o.f the o.r stream is 1 if any o.f the two. Is 1.

“![00125.jpeg](images/00125.jpeg)” bitwise xo.r that takes two. Numbers as o.perands and do.es xo.r o.n every bit within the stream o.f the two. Numbers. The result stream o.f xo.r is 1 if the two. Bits are different.

“![00126.jpeg](images/00126.jpeg)” left shift o.perato.r takes two. Numbers and left shifts the bits o.f the first o.perand. The seco.nd o.perand is used to. Determine the number o.f places to. Shift.

“![00127.jpeg](images/00127.jpeg)” right shift o.perato.r takes two. Numbers and right shifts the bits o.f the first o.perand. The seco.nd o.perand is used to. Determine the number o.f places to. Shift.

“![00128.jpeg](images/00128.jpeg)” bitwise no.t o.perato.r that takes o.ne number and switches the state o.f all the bits (1s to. 0s, 0s to. 1s).

No.te: machines use registers and buffers to. Sto.re the bits fo.r calculatio.n. A register is just an array o.f sto.rage, where each bit gets its o.wn place in the array. If yo.u think o.f these data streams as an array, it will help yo.u ratio.nalize many o.f the bitwise o.perato.rs, particularly the shift o.perato.rs.

Let’s write a bitwise ro.utine pro.gram. First, we will need to. Create a bit register and study bit streams. This requires the bitset<x>() functio.n fo.r the <bitset> library. It allo.ws yo.u to. Print a binary stream with a length o.f <x>. Fo.llo.w the instructio.ns:

1.  O.pen a new ide c++ wo.rkspace
2.  In additio.n to.  ![00129.jpeg](images/00129.jpeg) library as well
3.  Declare the o.perand variables and their values

![00130.jpeg](images/00130.jpeg)

![00131.jpeg](images/00131.jpeg)

1.  Declare register c fo.r the calculatio.ns

![00132.jpeg](images/00132.jpeg)

1.  Print o.perand values and their registers:

![00133.jpeg](images/00133.jpeg)

![00134.jpeg](images/00134.jpeg)

![00135.jpeg](images/00135.jpeg)

![00136.jpeg](images/00136.jpeg)

No.te: since all numbers are less than 255, we will then use a bit stream o.f ![00137.jpeg](images/00137.jpeg) fo.r the entire exercise.

1.  Calculate bitwise and fo.r ![00138.jpeg](images/00138.jpeg)

![00139.jpeg](images/00139.jpeg)

1.  Print the result and the register in ![00140.jpeg](images/00140.jpeg)

No.te: since we are using bitwise functio.ns, it is better to. Use ![00141.jpeg](images/00141.jpeg) to. Terminate o.ur lines. This is because this functio.n clears the buffer and prevents o.verflo.w. This makes the pro.gram a little slo.wer, but it ensures that o.ur registers are clear. The speed difference is made up by using bitwise functio.ns.

1.  Calculate bitwise o.r fo.r ![00138.jpeg](images/00138.jpeg)

![00142.jpeg](images/00142.jpeg)

1.  Print the resulting value and the register in ![00140.jpeg](images/00140.jpeg)
2.  Calculate bitwise xo.r fo.r ![00138.jpeg](images/00138.jpeg)

![00143.jpeg](images/00143.jpeg)

1.  Print the resulting value and the register in ![00140.jpeg](images/00140.jpeg)
2.  Calculate bitwise no.t fo.r ![00144.jpeg](images/00144.jpeg)

![00145.jpeg](images/00145.jpeg)

1.  Print the resulting value and the register in ![00140.jpeg](images/00140.jpeg)
2.  Print a co.mpariso.n register fo.r ![00144.jpeg](images/00144.jpeg)

This will make it easier to. Co.mpare with the shifting bitwise o.peratio.ns

1.  Calculate bitwise left shift fo.r ![00146.jpeg](images/00146.jpeg)

![00147.jpeg](images/00147.jpeg)

1.  Print the result and the register in ![00140.jpeg](images/00140.jpeg)
2.  Calculate bitwise left shift fo.r ![00148.jpeg](images/00148.jpeg)

![00149.jpeg](images/00149.jpeg)

1.  Print the result and the register in ![00140.jpeg](images/00140.jpeg)

![image21.png](images/00150.jpeg)

Bitwise ro.utine with register printing

This screensho.t is a successful run o.f o.ur bitwise ro.utine pro.gram. The o.utput features visuals o.f the ![00140.jpeg](images/00140.jpeg)register array. This will allo.w yo.u to. See ho.w each bitwise is calculated and ho.w it changes the register. This is a lo.ng pro.gram with a very lo.ng o.utput. To. Study it fully, yo.u can access it o.n o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/jgnalvwo.ne](https://ide.geeksforgeeks.org/JgnAlVwONe)

No.te:

This pro.gram uses usingnamespacestd; to. Simplify the pro.gram.it wo.uld be go.o.d practice to. O.mit the namespace and declare each co.ut and bitwise o.bject separately.

The last binary o.perato.rs we will discuss are assignment o.perato.rs. Assignment o.perato.rs are used fo.r assigning value and dynamically changing values. In principles o.f pro.gramming, we talked abo.ut pro.grams needing to. Be as efficient as po.ssible while using a few instructio.ns as po.ssible. Advanced assignments o.perato.rs co.mbine with equal assignments and o.ther vario.us o.peratio.ns to. Reduce lines o.f co.de. They are all ato.mic o.peratio.ns, meaning they allo.w pro.grammers to. Manipulate sto.red values within variables, and reassign them. Belo.w is a list o.f co.mmo.n assignment o.perato.rs (prabhu, 2018):

“![00151.jpeg](images/00151.jpeg)”: equal assignment o.perato.r assigns the value o.n the right to. The variable o.n the left.

“![00152.jpeg](images/00152.jpeg)’ o.perato.rs. This o.perato.r adds the value o.f the variable o.n the left to. The value o.n the right. Then it saves the result to. The variable o.n the left. Fo.r example, ![00153.jpeg](images/00153.jpeg) witho.ut having to. Use a separate arithmetic o.perato.r.

“![00154.jpeg](images/00154.jpeg)’ o.perato.rs. This o.perato.r subtracts the value o.f the variable o.n the left fro.m the value o.n the right. Then it saves the result to. The variable o.n the left.

“![00155.jpeg](images/00155.jpeg)’ o.perato.rs. This o.perato.r multiplies the value o.f the variable o.n the left with the value o.n the right and saves the result to. The variable o.n the left.
“![00156.jpeg](images/00156.jpeg)

![00157.jpeg](images/00157.jpeg)

Witho.ut having to. Use a separate arithmetic o.perato.r.

No.te: there are also. Bitwise ato.mic assignment o.peratio.ns: “![00158.jpeg](images/00158.jpeg)”. We will fo.cus o.n the arithmetic-ato.mic functio.ns fo.r no.w.

Let’s create an assignment o.perato.r ro.utine pro.gram to. See ho.w these assignment o.peratio.ns wo.rk. Fo.llo.w these steps:

1.  O.pen a new ide wo.rkspace
2.  Declare and initialize o.ur variable

Int a = 10;

1.  Print an explanatio.n o.f the pro.gram and the starting value

No.te: when making pro.grams that print, always make them easy to. Read! Make sure yo.ur pro.gram can explain itself.

1.  Ato.mically add 10 and print the result
2.  Ato.mically subtract 10 fro.m o.ur variable and print the result
3.  Ato.mically multiply 10 and print the result
4.  Ato.mically divide o.ur variable by 10 and print the result

Here is ho.w it lo.o.ks:

![image15.png](images/00159.jpeg)

Assignment ro.utine

This screensho.t is a successful run o.f o.ur assignment ro.utine pro.gram. This pro.gram has a sequential o.utput, which means that each instructio.n impacts the result o.f the next instructio.n. This means if we were to. Change the o.rder o.f the ato.mic o.peratio.ns applied to.  ![00160.jpeg](images/00160.jpeg) that the o.utput wo.uld be different. To. Study it fully, yo.u can access it o.n o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/fbc63b0u1e](https://ide.geeksforgeeks.org/Fbc63b0u1E)

These binary assignment o.perato.rs co.mbine assignments and arithmetic functio.ns. They wo.rk well when co.ntro.lling lo.o.ps and co.nditio.nal statements, to.o.. Ato.mic assignment o.perato.rs are clo.sely related to. Unary arithmetic o.perato.rs. Bo.th are frequently used to. Co.ntro.l lo.o.ps. Let’s take a lo.o.k at unary o.peratio.ns.

Unary o.peratio.ns

Befo.re we discuss unary o.peratio.ns, let’s lo.o.k at co.de that uses them.

![image5.png](images/00161.jpeg)

While lo.o.p featuring a unary o.perato.r

This screensho.t is o.f a simple while lo.o.p that prints the value o.f the co.unter, ![00162.jpeg](images/00162.jpeg) will cause an erro.r as the while lo.o.p wo.uld no.t be able to. Advance. We will talk abo.ut lo.o.ps extensively in the [decisio.n making chapter](https://docs.google.com/document/d/1rfTukE008PScFE0mgrN2m-UKMEAv4Y8VYrXHB3BjvOU/edit). To. Study it fully, yo.u can access it o.n o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/mgmutzdlpb](https://ide.geeksforgeeks.org/MgMUtZdlpb)

The i = 1 + i is the same as i++. Using the unary fo.rm makes the co.de neater because it precludes the + arithmetic o.perato.r and the = assignment o.perato.r. We can also. Use an ato.mic additio.n o.perato.r to. Co.mplete the co.de: i+=1 is the same as i++. But a fo.rmat like that wo.uld require the co.mpiler to. Sto.re and o.perate o.n an additio.nal o.perand. Unary o.perato.rs are there to. Simplify co.de by o.nly having o.ne o.perand. Remember, unary o.perato.rs are tho.se o.perato.rs that use o.ne o.perand. Here are so.me o.f the o.ther examples o.f unary o.perato.rs (kumar, 2017) :

“![00163.jpeg](images/00163.jpeg)”: increment o.perato.r used to. Increase the value o.f an integer by 1\. It can be placed in fro.nt o.f a variable to. Increment the value immediately o.r after to. Tempo.rarily save the value befo.re increment.

“![00164.jpeg](images/00164.jpeg)”: decrement o.perato.r used to. Decrease the value o.f an integer by 1\. Similar to. The increment, pro.grammers can also. Implement pre-decrement and po.st-decrement instructio.ns.

“![00090.jpeg](images/00090.jpeg)”: unary minus o.perato.r that is used to. Change the sign o.f a variable o.r argument. Perfo.rming a unary minus o.peratio.n o.n a negative integer will make it po.sitive and vice versa.

“!”: no.t o.perato.r is used to. Reverse the bo.o.lean lo.gical state o.f an o.perand. Fo.r example, if a variable ![00165.jpeg](images/00165.jpeg).

“”: address o.f o.perato.r that is used to. Po.int to. The address o.f a variable.

Let’s make a unary o.perato.r ro.utine to. See ho.w the pre- and po.st-instructio.ns wo.rk. Fo.llo.w these instructio.ns:

1.  O.pen a new ide wo.rkspace
2.  Declare and initialize o.ur variable and a buffer

Int a = 10, buf

1.  Print an explanatio.n o.f the pro.gram and the starting value
2.  Calculate a po.st-increment equal to. The buffer and print the result
3.  Calculate a po.st-decrement equal to. The buffer and print the result

1.  Calculate a pre-increment equal to. The buffer and print the result

1.  Calculate a pre-decrement equal to. The buffer and print the result

![image22.png](images/00166.jpeg)

Unary o.perato.r ro.utine with po.st- and pre-o.peratio.ns

This screensho.t is o.f o.ur unary o.perato.r ro.utine pro.gram. To. Study it fully, yo.u can access it o.n o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/mvcytky6c4](https://ide.geeksforgeeks.org/mvcYtky6C4)

The pro.gram o.perates o.n a and while it calculates, it sto.res the value in a buffer we can o.bserve. Co.mparing a with the buffer, the po.st-o.peratio.n delays changing the value o.f a; in co.ntrast, pre-o.peratio.ns change the value immediately.

O.n to.p o.f all this, we have the sizeo.f() o.perato.r. It lo.o.ks like a functio.n but it is catego.rized as an o.perato.r. It checks the size o.f an o.bject and returns the size in bytes.

Recall o.ur co.nversatio.n abo.ut bit streams. What i didn’t say is that they are o.ften divided into. A gro.up o.f 8. O.ne byte is a single 8-bit stream that can present 255 numbers. In o.ur bitwise ro.utine, o.ur registers were 1 byte lo.ng, that was because we were wo.rking with numbers that were less than 255\.

Let’s write a pro.gram that can get the size o.f an array using sizeo.f(). Here we go.:

*   O.pen a new c++ ide wo.rkspace

1.  Declare and initialize o.ur array

![00167.jpeg](images/00167.jpeg)

1.  Print an explanatio.n o.f the pro.gram and the array

No.te: to. Print the array yo.u will have to. Create a fo.r lo.o.p. We will discuss fo.r lo.o.ps in the next chapter. Fo.r no.w, just use these lines o.f co.de: ![00168.jpeg](images/00168.jpeg)  ![00169.jpeg](images/00169.jpeg)  ![00170.jpeg](images/00170.jpeg)

1.  Calculate the size o.f the array

![00171.jpeg](images/00171.jpeg)

1.  Print the size o.f the array

![image47.png](images/00172.jpeg)

Array size repo.rting pro.gram

This screensho.t is o.f o.ur array size repo.rting pro.gram. We enco.urage yo.u to. Co.mpare yo.ur result to. O.urs. To. Study it fully, yo.u can access it o.n o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/hwpclyb4p0](https://ide.geeksforgeeks.org/HwpcLYB4P0).

That was a go.o.d example o.f two. Unary o.peratio.ns: sizeo.f() and the address po.inter &. The fo.r(){} lo.o.p we used to. Print the array is called a co.py co.nstructo.r call. Co.nstructo.r co.py calls co.nsist o.f a fo.r() lo.o.p with an index variable, an addresso.f o.perato.r, and a co.ntainer o.bject with an index. The co.py co.nstructo.r sets up [0]: [the size o.f arr] by using the addresso.f po.inter to. Auto.matically deduce the [size o.f arr] and print its co.ntents. In simple wo.rds, a co.py co.nstructo.r uses addresso.f to. Reduce the size o.f the pro.gram.

The sizeo.f() o.perato.r is an o.bjective o.peratio.n and it uses a single o.perand, the arr array o.bject. They bo.th have disadvantages and advantages. The sizeo.f() o.perato.r uses o.ne o.perand and is easier to. Spo.t witho.ut eso.teric memo.ry registers. The call co.mbinatio.n had to. Use an additio.nal o.bject ( e ), to. Print the array but it wo.uld have do.ne with less incrementing o.perato.rs. We are go.ing to. Discuss lo.o.ps and decisio.n making features o.f c++ in mo.re detail in the next chapter. Fo.r no.w, let’s turn o.ur attentio.n to. Ternary o.perato.rs.

Ternary o.perato.rs

C++ o.nly has o.ne ternary o.perato.r. Ternary o.perato.rs, also. Called co.nditio.nal o.perato.rs, take 3 o.r mo.re o.perands – they are bo.o.lean lo.gic-based o.perato.rs. The result is always determined by whether o.r no.t the first expressio.n is true, then the seco.nd will be evaluated; if the first expressio.n is false, the third expressio.n will be evaluated. If yo.u recall o.ur if()…else statement in the relatio.nal pro.gram ro.utine, it had three parts: an initial expressio.n that the functio.n evaluates, an expressio.n it evaluates if the initial expressio.n is true, and an else statement which is evaluated when the initial expressio.n is no.t true. Co.nditio.nal o.perato.rs have the same co.mpo.nents as an if()…else statement. They are just mo.re co.mpact.

Let’s make a pro.gram that illustrates these similarities:

*   O.pen a new ide c++ wo.rkspace
*   To. Use the co.nditio.nal o.perato.r yo.u will have to. Call the ![00173.jpeg](images/00173.jpeg) library
*   Print an explanatio.n fo.r the co.nditio.nal o.perato.r

This pro.gram will pick the greatest o.ne using two. Metho.ds: a co.nditio.nal o.perato.r and an ![00119.jpeg](images/00119.jpeg) statement

We expect a result o.f 5.

*   Declare the variable and execute the co.nditio.nal o.perato.r

Int arsize=sizeo.f(arr)/sizeo.f(arr[0]);

Print an explanatio.n fo.r the ![00119.jpeg](images/00119.jpeg)

![00174.jpeg](images/00174.jpeg) then print 2

![00175.jpeg](images/00175.jpeg) then print 5

![image43.png](images/00176.jpeg)

Co.nditio.nal o.peratio.ns demo.

This screensho.t is o.f o.ur co.nditio.nal o.peratio.ns demo.. This pro.gram has no. Real practical functio.nality. Ho.wever, fo.r o.ur purpo.ses, it do.es demo.nstrate the similar structures between co.nditio.nal o.perato.rs and ![00119.jpeg](images/00119.jpeg) statements. To. Study it fully, we suggest that yo.u access the co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/9kjbaaqjtk](https://ide.geeksforgeeks.org/9kJBAAqJtK).

In this chapter, we lo.o.ked at 3 types o.f o.perato.rs: unary, binary, and ternary. As yo.u have seen, these o.perato.rs allo.w pro.grammers to. Apply po.werful aspects o.f c++. Fo.r instance, binary o.perato.rs allo.w machines to. Make lo.gical decisio.ns, co.mpute values, and co.ntro.l pro.cesses by changing functio.ns. Unary functio.ns help us shrink and simplify co.mplicated co.de. Ternary o.perato.rs allo.w us to. Be mo.re succinct in o.ur co.de. They are all central to. Making decisio.ns and switching in c++.

## Chapter 5: decisio.n making in c++

We’re go.ing to. Talk abo.ut decisio.n-making functio.ns; these are functio.ns like if-else lo.o.ps. Pro.gramming rests a lo.t o.n decisio.n making, and decisio.n making is info.rmed by lo.gical expressio.ns invo.lving o.perato.rs we have seen in chapter 4\. Decisio.n-making functio.ns co.mbined with lo.gical expressio.ns give machines the ability to. Make decisio.ns based o.n criteria selected by pro.grammers.

In o.ur sizeo.f() exercise in chapter 4 we used a fo.r() lo.o.p in a co.py co.nstructo.r which fielded the array, printing all indices. The unary o.perato.r addresso.f with an auto. Data type allo.wed us to. Implement the fo.r() lo.o.p, witho.ut an additio.nal co.unter fo.r the lo.o.p. The simplicity o.f the co.py co.nstructo.r is no.t so. O.bvio.us if yo.u have never had the experience o.f initializing and implementing lo.o.ps yo.urself.

Lo.o.ps

Pro.grammers spend a lo.t o.f time auto.mating mundane, repetitive tasks thro.ugh scripts and ro.utines. What allo.ws scripts and ro.utines to. Achieve this are lo.o.ps. As the name suggests, lo.o.ps repeat the same instructio.ns as lo.ng as a certain co.nditio.n is met (“c++ while lo.o.p,” n.d.). Lo.o.ps are o.ften used to. Navigate aggregated o.bjects with indices like arrays and vecto.rs. Fo.r instance, yo.u might write a lo.o.p that keeps searching an array until a specific item is fo.und. There are two. Types o.f lo.o.ps: entry-co.ntro.lled lo.o.ps and exit lo.o.ps.

In o.ur unary arithmetic example, we had a while() lo.o.p with a co.unter. The co.unter is an arbitrary variable that is used with a unary o.perato.r to. Increment an indicated expressio.n. It is an example o.f an entry co.ntro.lled lo.o.p – it tests a co.nditio.n befo.re it executes co.de. Let’s mo.dify that example into. A while() lo.o.p to. Explo.re its co.mpo.nents. We will use it to. Print o.ut “hello. Wo.rld” 10 times. Fo.llo.w these instructio.ns:

*   O.pen the fo.llo.wing ide c++ wo.rkspace:

[Https://ide.geeksfo.rgeeks.o.rg/mgmutzdlpb](https://ide.geeksforgeeks.org/MgMUtZdlpb)

*   Print explanatio.n o.f the pro.gram

This pro.gram will number and print 10 lines--

*   Change the co.nditio.nal test to.  ![00177.jpeg](images/00177.jpeg)
*   Print “hello. Wo.rld” 10 times with numbered lines

![image53.png](images/00178.jpeg)

While lo.o.p demo.

This screensho.t is o.f o.ur while lo.o.p demo.. Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/0wjo.l6tsh4](https://ide.geeksforgeeks.org/0WjOL6TSh4).

This pro.gram sho.ws us ho.w incremental co.unters wo.rk. Fo.r it to. Wo.rk, the number must start with 1, no.t 0. Mo.st peo.ple are used to. Numbers wo.rking that way. To. Do. This, we initialized the co.unter at 1. Yet if we set the co.nditio.n to. 10 it will give us 9 print o.uts. To. Get 10 we have to. Increase the number to. 11.

Ano.ther example o.f a co.ntro.lled lo.o.p is the fo.r() lo.o.p functio.n; it requires three expressio.ns as inputs (agarwal, 2017a):

1.  An initializatio.n expressio.n that declares a data type and a variable. This variable can be either a co.unter o.r an indexing variable.
2.  A test expressio.n that pro.duces a bo.o.lean ![00179.jpeg](images/00179.jpeg). If the co.nditio.n is true then the fo.r lo.o.p will co.ntinue to. Lo.o.p its specified blo.ck o.f co.de.
3.  An update expressio.n that increments the co.unter o.r the indexing variable

Let’s see ho.w they wo.rk by writing a pro.gram similar to. O.ur while() lo.o.p example. Fo.llo.w these instructio.ns:

*   O.pen the fo.llo.wing ide c++ wo.rkspace:

[Https://ide.geeksfo.rgeeks.o.rg/0wjo.l6tsh4](https://ide.geeksforgeeks.org/0WjOL6TSh4)

*   Print explanatio.n o.f the pro.gram

This pro.gram will number and print 10 lines o.f hello. Wo.rld

*   Implement the fo.r() lo.o.p

![00180.jpeg](images/00180.jpeg)

*   Print “hello. Wo.rld” 10 times with numbered lines
*   Clean the data o.f any unneeded co.de and co.mments

![image37.png](images/00181.jpeg)

Fo.r lo.o.p demo.

This screensho.t is o.f o.ur fo.r lo.o.p demo.. Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/dj2gyw02av](https://ide.geeksforgeeks.org/Dj2gyW02av).

No.te: make sure yo.u clean yo.ur co.de o.f unnecessary lines and update yo.ur co.mments. While this do.es no.t impact the perfo.rmance o.f yo.ur co.de, it can make things co.nfusing fo.r o.ther pro.grammers o.n yo.ur team that have to. Implement yo.ur co.de. Do. Yo.u see a mistake here?

No.w that we see ho.w fo.r() lo.o.ps wo.rk and ho.w they are co.nstructed, let’s lo.o.k at the co.py co.nstructo.r we used earlier. The expressio.n used fo.r the co.py co.nstructo.r call was:

![00182.jpeg](images/00182.jpeg)

“e” being the indexing variable and “arr” the variable array. We saw that the fo.r() lo.o.p needs three expressio.ns to. Wo.rk: the initializatio.n, the test expressio.n, and the update expressio.n.

The co.py co.nstructo.r has an initializing functio.n (co.nst auto.& e). When yo.u lo.o.k clo.sely, yo.u can see this expressio.n also. Wo.rks as a test expressio.n, because the & is an addresso.f o.perato.r that po.ints to.  E which stands fo.r indices in the arr array. The : is an o.perato.r to. Break into. Class. It allo.ws the attributes o.f the co.ntainer arr array to. Pass to. The e variable. The fo.r() lo.o.p will print the e until the end o.f the array is reached.

The co.py co.nstructo.r call is go.o.d fo.r a situatio.n where the size o.f the co.ntainer is unkno.wn and yo.u want all items printed o.ut. Fo.r() lo.o.ps define the number o.f iteratio.ns that have to. Take place fro.m the get-go., while co.py co.nstructo.rs calls are defined by the size o.f the co.ntainer. While() lo.o.ps are best fo.r the situatio.n where the co.nditio.n can change at any time, during which yo.u want the iteratio.ns to. Sto.p.

The do.{}…while() lo.o.p is fo.r situatio.ns where the while() co.de may impact the test. Do.{}..while() lo.o.ps are exit co.ntro.lled, meaning co.de is executed until a co.nditio.n is met. The co.de is executed at least o.nce befo.re checking the test co.nditio.n. Think back to. That bank security example. The do.o.r will always fail-clo.se, receiving a no.t signal, except when there is a fire. Here is ho.w a do.{}..while lo.o.p will lo.o.k fo.r that:

![00183.jpeg](images/00183.jpeg)

![00184.jpeg](images/00184.jpeg)

The do.o.r will remain clo.sed as lo.ng as fire is no.t detected. Do.{}..while() lo.o.ps are useful fo.r many fail-clo.se systems. O.ther applicatio.ns include data co.rrectio.n in servers where a co.rrectio.n ro.utine is run when an erro.r is detected. Let’s co.de o.ur first do. While lo.o.p by changing o.ur while() pro.gram. Fo.llo.w these instructio.ns:

*   O.pen the fo.llo.wing ide c++ wo.rkspace:

[Https://ide.geeksfo.rgeeks.o.rg/0wjo.l6tsh4](https://ide.geeksforgeeks.org/0WjOL6TSh4)

*   Initialize co.unter to.  ![00185.jpeg](images/00185.jpeg)
*   Implement the do.{} co.de blo.ck
*   Set ![00186.jpeg](images/00186.jpeg)
*   Clean the data o.f any unneeded co.de and co.mments
*   Check the results

![image3.png](images/00187.jpeg)

Do. While lo.o.p demo. Exhibiting an exit co.ntro.lled lo.o.p

This screensho.t is o.f o.ur do. While lo.o.p demo.. Yo.u sho.uld no.tice that, despite ![00188.jpeg](images/00188.jpeg)co.de blo.ck was executed. This is because the lo.o.p is an exit co.ntro.l lo.o.p: the co.nditio.n is tested after the co.de blo.ck is executed. The co.de has the po.tential to. Execute. Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/t6zcnk2wj7](https://ide.geeksforgeeks.org/t6zcNK2Wj7).

See ho.w the message was printed despite the co.nditio.ns being false. Yo.u can apply it to. Data co.rrectio.ns in streams. Many erro.r detectio.n services pause the stream o.f data and a request fo.r retransmissio.n is sent. A do.{}…while lo.o.p will allo.w the data stream to. Co.ntinue until an erro.r is detected. These are the types o.f ro.utines used by yo.utube in server buffers. This sho.ws ho.w useful they are in co.ntro.lling data. Fo.r single switching, we wo.uld use an if()…else.

**If()…else**

So. Far we have used if()…else functio.ns in o.ur examples. They are easy to. Understand and their structure is pretty self-explanato.ry. An if()…else statement tests a co.nditio.n and based o.n the result it executes o.ne blo.ck o.f co.de o.r ano.ther. They are a co.mbinatio.n o.f two. Separate distinct statements.

Yo.u can execute the if() functio.n alo.ne but the co.mpiler expects an else statement. An else statement co.ntains the co.de that acco.mpanies the if() expressio.n. An else statement can never be executed witho.ut the if() statement.

An else if() statement specifies ano.ther co.nditio.n to. Test. It creates a chain o.f statements called nested if-else statements. If yo.u are testing a lo.t o.f co.nditio.ns, it is best to. Use a switch which we will discuss in the next sectio.n. Let’s make o.ur first nested if-else statement. Fo.llo.w these instructio.ns (“c++ | nested ternary o.perato.r,” 2018):

1.  O.pen a new ide c++ wo.rkspace
2.  Print an explanatio.n fo.r the co.nditio.nal o.perato.r

This pro.gram will go. Thro.ugh a sequential list o.f numbers 2 thro.ugh 4 and pick the greatest o.ne using a nested ![00119.jpeg](images/00119.jpeg) statement

We expect a result o.f 4.

1.  Implement a nested if-else

![00189.jpeg](images/00189.jpeg) then print 2

![00190.jpeg](images/00190.jpeg) then print 3

![00175.jpeg](images/00175.jpeg) print 4

![image41.png](images/00191.jpeg)

Nested if-else demo.

This screensho.t is o.f o.ur nested if-else demo.. Just like o.ur o.ther demo.s, this pro.gram has no. Functio.nality. Ho.wever, fo.r o.ur purpo.ses, this is an excellent exercise fo.r implementing and understanding ![00192.jpeg](images/00192.jpeg) still requires co.de blo.cks fo.r each statement. The co.de blo.cks sho.uld also. Co.rrespo.nd to. The co.nditio.n in o.rder to. Create a functio.nal pro.gram that fulfills its stated purpo.se. Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/89mlnvrwyu](https://ide.geeksforgeeks.org/89MlNvRWYU).

Let’s examine the exercise further. The nested if-else can be divided into. Two. Parts: the if() and else – if() statement that co.ntains co.nditio.ns and executio.n co.de. Yo.u no.tice that the blo.cks o.f co.de lo.gically fo.llo.w the state go.al o.f the pro.gram, which is to. Find the largest number. It makes sense to. Print numbers in ascending o.rder in case we change the co.nditio.nal statement. Co.nditio.ns within the if() statements and the blo.cks o.f co.de they co.ntain are arranged in a way that allo.ws the pro.gram to. Flo.w to. The answer. Fo.r instance, if (2 > 3) is hardco.ded to. The next nested statement. The structure fo.llo.wed the nested co.nditio.nal o.perato.r deliberately.

Nested ternary if else o.perato.r

In the previo.us chapter, we talked abo.ut co.nditio.nal o.perato.rs, ternary o.perato.rs that test co.nditio.ns and execute an expressio.n based o.n the results. We said the structure it uses is similar to. An if()...else statement but mo.re succinct. Fo.r instance, an if() statement tests a co.nditio.n and executes o.ne o.f the two. Blo.cks o.f co.de depending o.n the result o.f the test. If ()…else statements can be nested, and co.nditio.nal o.perato.rs can also. Be nested. Let's co.mpare the structures o.f bo.th. Fo.llo.w these steps to. Participate (“c++ | nested ternary o.perato.r,” 2018):

1.  If yo.u had clo.sed the nested if-else demo., o.pen up the saved ide c++ wo.rkspace with o.ur pro.gram at this url: [https://ide.geeksfo.rgeeks.o.rg/89mlnvrwyu](https://ide.geeksforgeeks.org/89MlNvRWYU)
2.  Print an explanatio.n fo.r the pro.gram

1.  This pro.gram will go. Thro.ugh a sequential list o.f numbers 2 thro.ugh 4 and pick the greatest o.ne using two. Metho.ds: a co.nditio.nal o.perato.r and a nested ![00119.jpeg](images/00119.jpeg) statement
2.  We expect a result o.f 4.

1.  Add a printed no.tificatio.n o.f the nested if-else
2.  Print a no.tificatio.n fo.r the co.nditio.nal statement
3.  Add the co.nditio.nal o.perato.r co.de: declare the variable and execute the co.nditio.nal o.perato.r

Int a = 2 > 3 ? 2 : 3 > 4 ? 3 : 4;

1.  Clean the co.de o.f any unnecessary lines and co.rrect any anno.tatio.ns

![image28.png](images/00193.jpeg)

Nested if-else and nested ternary o.peratio.n co.mpariso.n

This screensho.t is o.f o.ur mo.dified nested if-else demo.. We mo.dified o.ur demo. By implementing a nested ternary o.perato.r fo.r side-by-side co.mpariso.n. As yo.u may have experienced, the ternary o.perato.r was much easier to. Implement, using fewer statements. Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/bdfgwvg8uc](https://ide.geeksforgeeks.org/BdfgWVg8uc).

Let’s talk abo.ut what we have just do.ne there. In o.ur previo.us discussio.n, we bro.ke do.wn the nested if-else statement into. Its co.mpo.nents and a list o.f po.ssible results. Even in the case where “2” and “3” were arbitrary values, if-else  statements have to. List all po.ssible results to. Ensure great functio.nality regardless o.f the co.nditio.nal statements results.

To. See ho.w co.nditio.nal statement results o.f a nested if-else match with co.mpo.nents o.f ternary o.perato.r, we have to. Take a clo.se lo.o.k at the ternary o.perato.r. Here is the syntax:![00194.jpeg](images/00194.jpeg)![00195.jpeg](images/00195.jpeg)

Var is the variable used to. Print the result. The result o.f the nested if-else match expressio.n befo.re the ? Indicato.rs o.f the o.perato.r. The seco.nd expressio.n executes when the first expressio.n is false and co.rrespo.nds to. The else if () in the nested if-else. Yo.u can already see advantages to. The co.mpactness o.f ternary o.perato.rs, but by their nature ternary o.perato.rs are no.t suited fo.r co.de blo.cks. With three o.r mo.re expressio.ns bo.th get cluttered, so. We need so.mething else to. Handle multiple expressio.ns: the switch statement.

**Switch**

As i have said, pro.grammers need to. Strive fo.r efficient, easily understandable co.de. It makes wo.rk easier fo.r yo.u and everyo.ne else. Using switch o.ver if()..else is o.ne way yo.u can achieve this, especially in circumstances where we are handling a lo.t o.f expressio.ns. Ternary o.perato.rs reduce lines o.f co.de, and it is because o.f this that they are no.t suited fo.r situatio.ns where the co.de needs to. Span mo.re than o.ne line.

Switch statements o.ffer a so.lutio.n fo.r bo.th pro.blems. Switch statements are multibranch statements that pro.vide a clean way to. Execute a different blo.ck o.f co.de o.n o.ne variable. Here is the syntax (awasthi, n.d.):

![00196.jpeg](images/00196.jpeg)

{

![00197.jpeg](images/00197.jpeg)

![00198.jpeg](images/00198.jpeg)

![00199.jpeg](images/00199.jpeg)

![00198.jpeg](images/00198.jpeg)

![00200.jpeg](images/00200.jpeg)

}

No.te: a switch can o.nly evaluate an integer against case numbers. To. Add the co.nditio.nal co.mpo.nent, yo.u must change the variable with an o.peratio.n. The o.perato.r must pro.duce an integer.

Let’s create a switch demo. Practice the co.mpo.nents o.f a switch:

1.  O.pen a new ide c++ wo.rkspace
2.  Initialize a variable

![00201.jpeg](images/00201.jpeg)

1.  Print an explanatio.n o.f the pro.gram
2.  Initialize the switch

![00202.jpeg](images/00202.jpeg)

1.  Print o.ut “cho.ice is 1” fo.r case 1
2.  Print o.ut “cho.ice is 2” fo.r case 2
3.  Print o.ut “cho.ice is 3” fo.r case 3
4.  Print o.ut “pro.gram exit” fo.r the default;

![image50.png](images/00203.jpeg)

Switch demo.

This is a screensho.t o.f o.ur switch demo.. Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/dsehfxulz5](https://ide.geeksforgeeks.org/dSehFXULz5). We highly suggest using this demo. To. Co.nvert o.ne o.f o.ur previo.us exercises into. A switch. O.ne excellent candidate is o.ur relatio.nal ro.utine pro.gram. It had 6 if()... Else statements! This co.mes o.ut to. 12 different scenario.s. Ho.w co.uld yo.u co.nvert this pro.gram into. A switch? Hint: co.nsider creating a menu fo.r each relatio.nal ro.utine using the input functio.n. Yo.u can study the relatio.nal ro.utine fo.r yo.urself at this url: [https://ide.geeksfo.rgeeks.o.rg/dfd3cek85y](https://ide.geeksforgeeks.org/dFD3cEk85y).

No.w that we have seen what decisio.n making functio.ns are and ho.w they wo.rk, let’s turn o.ur attentio.n to. Functio.ns and their ro.le in pro.gramming.

## Chapter 6: creating functio.ns

We talked abo.ut algo.rithms as a metho.d o.f understanding pro.blems and planning ho.w yo.ur co.de will wo.rk to. Fix it. Algo.rithms receive inputs, perfo.rm actio.ns, and then give a result which then causes a state change. A functio.n is a blo.ck o.f co.de yo.u can call multiple times witho.ut having to. Write the co.de again. The co.de is usually so.mething that perfo.rms a desired task and has high re-usability. A functio.n is co.mpo.sed o.f the header and a bo.dy. Here is ho.w the syntax o.f a functio.n lo.o.ks:

[datatype]functio.n_name(arguments)

{//statements

Return0;

}

Like yo.u have seen, and like many o.ther pro.gramming languages, c++ is mo.stly just a series o.f functio.ns, statements, and o.perato.rs with o.bjects and o.ther data-ho.lding elements fo.r in-between. Everything we have written so. Far has used the main() functio.n which uses syntax similar to. The o.ne abo.ve. So. Functio.ns aren’t new to. Yo.u.

Every functio.n must return a data type, just like the main() functio.n returns the int 0. If a functio.n do.es no.t do. This, (vo.id) is used as the parameter return type. As yo.u might have guessed, the return is the statement that terminates the functio.n.

The inputs that the functio.ns receive are called parameters o.r arguments. No.t all functio.ns will take inputs as we have seen with main(); regardless o.f this, yo.u can still pass parameters into. The functio.n fo.r it to. Run. This is ho.w libraries pass o.bjects into.  Main().

Create and call a functio.n

To. Begin calling a functio.n, yo.u must declare it and define it befo.re main(). This is because c++ executes sequentially. C++ practices take precedence and functio.ns get prio.rity. This is why yo.u must declare them befo.re main() so. Yo.u can call them. They are also. Called this way because they make co.de mo.re o.rganized. O.nce a functio.n is declared, we can define it anywhere o.utside o.f main()

Let’s write a simple printing functio.n so. We can appreciate them mo.re. Fo.llo.w these instructio.ns:

1.  O.pen a new ide c++ wo.rkspace

1.  Declare yo.ur functio.n

Vo.id myfunctio.n();

1.  Call yo.ur functio.n in main ()

Myfunctio.n()

1.  Define yo.ur functio.n o.utside o.f main

![00204.jpeg](images/00204.jpeg)

![image42.png](images/00205.jpeg)

Functio.n demo.

This screensho.t is o.f o.ur functio.n demo.. Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/b9isdihapz](https://ide.geeksforgeeks.org/b9iSDihApZ). If yo.u want mo.re practice, we suggest using this exercise as a template to. Turn o.ne o.f o.ur past exercises into. A functio.n! Co.nsider o.ur exercise using ![00206.jpeg](images/00206.jpeg) will do..

Separating the declaratio.n and the definitio.n falls under go.o.d pro.gramming practices. It makes it so. Yo.u kno.w all defined functio.ns in the co.de that are available fo.r calling. Having definitio.ns at the bo.tto.m makes it easy to. Parse fo.r erro.rs within functio.ns. No.w let's turn o.ur attentio.n to. Parameter passing.

**Parameter passing**

Functio.ns are scripts that are given to. The co.mpiler. To. Co.mplete the task and be useful, these functio.ns need inputs to. Co.mpute. To. Remind yo.u, these inputs are called arguments o.r parameters. Pro.grammers describe parameters differently based o.n where they o.riginate o.r appear. Parameters that go. Into. A defined functio.n are called actual parameters. Fo.r instance, if yo.u have a summing functio.n called mysum(x,y), when main() passes 2 and 3 into. The functio.ns tho.se parameters are actual parameters. Co.nversely, x and y are fo.rmal parameters because they are variables that the data is go.ing to. Be bo.und to.. This applies to. All o.ther parameters befo.re actual parameters are passed. There are two. Ways to. Pass parameters to. Functio.ns (“functio.ns in c/c++,” 2015):

Pass by value: values o.f actual parameters are co.pied into. And sto.red in the functio.n’s fo.rmal parameters. Any changes made inside main() do. No.t impact the actual parameters that were passed.

Pass by reference: bo.th actual and fo.rmal parameters refer to. The same lo.catio.ns. Therefo.re, any changes made inside the main() functio.n will impact the actual parameters that were passed.

Let’s practice parameter passing by writing o.ur o.wn co.de. Fo.llo.w these instructio.ns:

1.  O.pen a new ide c++ wo.rkspace

1.  Declare yo.ur functio.n

Int max( int x, int y)

1.  Call yo.ur functio.n in main ()
2.  Initialize two. Actual variables

![00207.jpeg](images/00207.jpeg)

1.  Initialize a variable and call the functio.n

Int m = max(a, b);

1.  Print the result
2.  End main()
3.  Define yo.ur functio.n o.utside o.f main

1.  This functio.n sho.uld use an if() statement to. Check if x is greater than y.
2.  If x is greater than y, then return x
3.  O.therwise, return y.

![image18.png](images/00208.jpeg)

Functio.ns with parameter passing

This screensho.t is o.f o.ur functio.n demo.. Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/nnszczhx15](https://ide.geeksforgeeks.org/NnsZczhX15). If yo.u want mo.re practice, we suggest using this exercise as a template to. Turn o.ne o.f o.ur past exercises into. A functio.n! Co.nsider o.ur exercise using ![00083.jpeg](images/00083.jpeg)and passing parameters to. It. We’ll discuss ho.w to. Pass parameters in the next sectio.n, but trying it first o.n yo.ur o.wn will help yo.u grasp the co.ncept.

In o.ur example, we have used value passing well. The variables used fo.r main (a,b) are in a different lo.catio.n than tho.se used in max(), (x, y). Yo.u can see ho.w this can be very useful in larger pro.grams where several co.mplicated co.mputatio.ns might take place in main(). It is preferred to. Pass values because it ensures that actual variables remain present until the functio.n is called again.

Using a reference to. Pass arguments has its o.wn advantages, especially in larger pro.grams. References to. Pass inessential values may speed up the pro.gram and make it respo.nsive. Scripting fo.r auto.mating functio.ns is mo.re likely to. Use references to. Pass parameters since auto.mated pro.cesses are likely to. Happen repeatedly and quickly. These qualities are a selling po.int fo.r reference-based structures. Let’s no.w turn o.ur attentio.n to. Co.ndensing and o.ptimizing co.de.

Functio.n o.verlo.ading

All defined o.bjects and classes must have unique names. Yo.u canno.t run a pro.gram that has two. Variables that have the same name o.r an erro.r will be thro.wn. Yo.u might have seen this earlier while we're wo.rking o.n o.ur ro.utines and demo.s, especially when we had to. Mo.dify a pro.gram. So. Keep this in mind: variables that are declared twice cause erro.rs. But weirdly, multiple functio.ns can have the same name as o.ther functio.ns as lo.ng as they have different parameters. This is o.nly allo.wed in circumstances where the functio.ns return different data types. It is better, given that, to. O.verlo.ad a functio.n to. Return multiple data types. This is what is called functio.n o.verlo.ading; a pro.cess where pro.grammers co.mbine functio.ns to. Receive multiple data types. Why? Because it simplifies and co.nso.lidates the co.de. Take a lo.o.k at the fo.llo.wing co.de (“c++ functio.n o.verlo.ading,” n.d.):

![https://lh3.googleusercontent.com/1k77bAy1XEFsdGGyf1ZbhWuxD44qcE5OBiyzUScejTe6fZE1cTTnAfBou6dfYScFr9rcKX3SZIewD-HyxntrT3Zn-sst8BBJm7EwyJ5_yF4b9zu4Svv-_Hw-RwMiKKrfN0NI58Mt](images/00209.jpeg)

Pro.gram witho.ut functio.n o.verlo.ading

Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/qkphhzsqq5](https://ide.geeksforgeeks.org/qkpHhZsqq5). The functio.ns are declared and defined at the to.p o.f the file so. That we can o.bserve them better. Yo.u will be using this file to. Perfo.rm functio.n o.verlo.ading o.n yo.ur o.wn. Remember that yo.u can return to. This wo.rkspace at any time if yo.ur co.de is damaged during editing.

The pro.gram abo.ve declares two. Separate functio.ns that do. Similar co.mputatio.ns. In a big pro.gram that is a waste o.f real estate and it is inefficient. It makes it harder to. Edit the co.de since either o.ne o.f the functio.ns are unlikely to. Be in the same place in a larger pro.gram. To. Make things mo.re efficient, we sho.uld co.nso.lidate these functio.ns under o.ne name, and “stack” the data types. Here’s ho.w yo.u can do. This:

1.  O.pen the saved ide wo.rkspace at the fo.llo.wing url:

[Https://ide.geeksfo.rgeeks.o.rg/qkphhzsqq5](https://ide.geeksforgeeks.org/qkpHhZsqq5)

1.  Change do.uble plusfuncdo.uble...to. Do.uble plusfunc...
2.  Call do.uble plusfuncdo.uble... In place o.f do.uble plusfunc...

![https://lh3.googleusercontent.com/1k77bAy1XEFsdGGyf1ZbhWuxD44qcE5OBiyzUScejTe6fZE1cTTnAfBou6dfYScFr9rcKX3SZIewD-HyxntrT3Zn-sst8BBJm7EwyJ5_yF4b9zu4Svv-_Hw-RwMiKKrfN0NI58Mt](images/00210.jpeg)

Pro.gram functio.n o.verlo.ading

Yo.u can access a co.py o.f o.ur saved wo.rkspace using this url: [https://ide.geeksfo.rgeeks.o.rg/e1qlzi3ago.](https://ide.geeksforgeeks.org/e1qLzi3aGo). We kept the functio.ns at the to.p o.f the file fo.r easier editing. This o.verlo.ading exercise requires a few small minute detail changes in o.rder fo.r this file to. Wo.rk. Use o.ur wo.rkspace to. Co.mpare yo.ur file in the event yo.u get any lo.ng-standing erro.rs. Remember that yo.u can return to. The o.riginal wo.rkspace at any time if yo.ur co.de is damaged during editing. Yo.u can access the o.riginal wo.rkspace at this url: [https://ide.geeksfo.rgeeks.o.rg/qkphhzsqq5](https://ide.geeksforgeeks.org/qkpHhZsqq5).

When yo.u co.nso.lidate similar functio.ns, yo.u clean up yo.ur co.de. It is impo.rtant, especially when yo.u have to. Debug the co.de, since the co.mpiler will likely po.int to. Functio.ns when erro.rs o.ccur. The co.mpiler do.es this because it is po.inting to. Multiple libraries in the c++ co.de. Co.nso.lidating and o.verlo.ading functio.ns ensures that yo.ur co.mpiler will have fewer functio.ns to. Reference, making it easier fo.r yo.u to. Debug. Keep in mind that c++ is co.nstantly updating so. It beco.mes even easier to. Wo.rk with. New features are co.nstantly added, and libraries are co.ndensed and further o.rganized. So. An erro.r is c+++7 wo.uld lo.o.k different than an erro.r in c++14. Updates bring new, easy ways to. Perfo.rm mundane tasks. Fo.r instance, the co.py co.nstructo.r call co.mbinatio.ns are co.nsidered mo.re mo.dern fo.r indexing co.ntainers such as arrays. To. Stay updated and reap the benefits o.f new c++ develo.pments, yo.u have to. Keep practicing, testing yo.urself, and asking questio.ns.

## Co.nclusio.n

Learning pro.gramming is a co.gnitive jo.urney, o.ne that is stimulating, exciting, and so.metimes frustrating. As we co.me to. The end o.f this bo.o.k, it is impo.rtant to. Go. O.ver so.me o.f the impo.rtant lesso.ns we learned. They are also. Go.ing to. Be acco.mpanied by final tho.ughts and suggestio.ns that are meant to. Equip yo.u with all yo.u need to. Co.ntinue gro.wing in this field.

Expanding yo.ur practice: preparing yo.ur co.ding enviro.nment

We have used an o.nline ide to. Make it so. That everyo.ne has the same experience. If yo.u want to. Save yo.ur wo.rk yo.u can use the run+url butto.n to. Save it in ano.ther url. Yo.u can also. Bo.o.kmark all these fo.r later reference using yo.ur saved ide wo.rkspace and urls listed in this bo.o.k. Use them as a reference o.r to. Fix bro.ken co.de. I have do.ne my best to. Sho.w yo.u the best co.ding practices in all the exercises we did. Yo.u have seen that in c++ there are many ways o.f do.ing so.mething, so. Use that. Do.n’t be afraid to. Experiment and try new things, and read up o.n ho.w to. Do. O.ther things yo.u are interested in. The exercises in his bo.o.k are no.t definitive answers and no.thing like that exists in pro.gramming. So. Co.me to. This bo.o.k fo.r reference and explo.re o.ther ways o.f do.ing so.mething. We have o.ur co.des in the index o.f this ebo.o.k fo.r quick reference.

There are many pro.gramming enviro.nments and text edito.rs that can suppo.rt c++. So.me will have multiple versio.ns o.f c++. As o.f writing this, the mo.st up to. Date versio.n o.f c++ is 17 but the mo.st suppo.rted is c++14\. C++ 14 is the evo.lved versio.n o.f c++ and it features mo.re co.mprehensible language features. C++14 is mo.re intelligible to. Humans than its predecesso.r and yo.u can expect this trend to. Co.ntinue. The o.ldest, widely available c++ versio.n in mo.st pro.gramming enviro.nments is c++11\.

I enco.urage yo.u to. Set up a lo.cal ide and wo.rk o.n it. It will allo.w yo.u to. Gro.w faster and get accusto.med to. Real-wo.rld scenario.s. We have spo.ken o.f co.de::blo.cks fo.r micro.so.ft and xco.de o.f mac. If yo.u have linux there are standardized o.ptio.ns yo.u can use acro.ss all distro.s. Linux is a co.nso.le-based enviro.nment that is highly preferred by so.ftware develo.pers because co.nso.le-based enviro.nments are entrenched with many built-in features that directly interact with pro.grams.

There are many distro.s that pro.vide a gui-based deskto.p that is preferable fo.r many users. Mo.st o.f them are o.pen so.urce, free to. Do.wnlo.ad and install. We highly reco.mmend cento.s, a free linux distro. Server management. Cento.s uses many o.f red hat enterprise linux (rhel) co.mpo.nents. It is the best distro. Fo.r preparing to. Wo.rk in red hat server management enviro.nments.

Co.ding best practices: o.wnership o.f learning and co.llabo.ratio.n

In o.ur time to.gether we have seen many techniques and best practices fo.r so.ftware develo.pment. In the first chapter, we talked abo.ut ho.w pro.grams sho.uld fulfill their tasks with as little co.de as po.ssible. Thankfully, with each new versio.n o.f c++, mo.re ways o.f do.ing this are added. The majo.rity o.f beginner pro.gramming co.urses teach o.lder, less efficient metho.ds o.f implementing co.mmo.n pro.gramming tasks like parsing arrays, co.nditio.nal statements, and calling functio.ns. Yo.u will find mo.st o.f these techniques are never used in actual pro.gramming situatio.ns. Mo.st beginner co.urses are fo.cused o.n equipping beginners with a stro.ng grasp o.f the basics – the fo.undatio.n o.f yo.ur kno.wledge is o.ften as impo.rtant as ho.w yo.u are go.ing to. Pro.gress. As yo.u gro.w yo.u will find mo.re efficient ways o.f so.lving pro.blems with yo.ur co.de, but this can o.nly happen if yo.u practice and study.

If yo.u want to. Impro.ve as a pro.grammer yo.u have to. Take o.wnership o.f yo.ur learning. Learn pre-develo.pment to.o.ls like algo.rithms. It is all abo.ut learning to. Fix pro.blems. There are o.ther pre-develo.pment to.o.ls yo.u can try, like diagraming. Diagraming is go.o.d fo.r individuals who. Are visual learners. All o.f these are great fo.r gro.wing as a pro.grammer; it do.es no.t matter which yo.u cho.o.se, as lo.ng as pre-develo.pments to.o.ls are so.mething yo.u take advantage o.f.

Turning back to. Algo.rithms, mo.re detailed algo.rithms will explain all so.rts o.f data types required fo.r inputs, o.utputs, and o.ther data. The advantage o.f algo.rithms is that yo.u can use them as a sho.rthand. Yo.u can also. Anno.tate and manage yo.ur co.de. These habits will help keep yo.ur co.de o.rdered and co.herent to. Yo.ur team members. All these practices will help enhance ho.w yo.u see and think abo.ut pro.grams.

So.ftware develo.pers wo.rk in teams, with several peo.ple wo.rking o.n the same piece o.f co.de at the same time. The impo.rtance o.f anno.tating yo.ur co.de beco.mes very apparent in such situatio.ns.

It also. Happens that wo.rking with o.thers will accelerate yo.ur gro.wth. When co.ding with o.thers yo.u learn fro.m their experience and kno.wledge. As we have said, c++ has a variety o.f library o.bjects, statements, and o.ther to.o.ls. It is as rich as vo.cabulary in human languages because there are many ways o.f do.ing the same things. Yo.ur way o.f fixing a pro.blem will depend o.n yo.ur ability to. See efficient ways o.f do.ing so.. But ultimately all pro.gramming and so.ftware develo.pments are creative endeavo.rs. Wo.rking with o.thers will increase yo.ur pro.gramming “vo.cabulary” – yo.u will learn fro.m ho.w creatively they fix pro.blems and yo.u will find insights o.f yo.ur o.wn in the pro.cess. Yo.u sho.uld always keep in mind that everyo.ne can co.ntribute so.mething and what they co.ntribute is heavily influenced by the amo.unt o.f experience they have. So. Even if yo.u are new to. C++, yo.u still have a unique experience and appro.ach to. So.lving pro.blems that o.ther peo.ple do.n’t have because yo.u think differently. That in itself is valuable to. Any team, particularly if yo.u learn to. Co.mmunicate yo.ur ideas well. I highly reco.mmend yo.u use the glo.ssary as o.ne o.f the ways to. Help yo.u co.mmunicate clearly.

In additio.n to. Anno.tatio.ns, it is go.o.d practice to. Make yo.ur co.de as clean as po.ssible. I have demo.nstrated ho.w to. Co.mment lines o.f co.de to. Prevent breaking the co.de during editing. In yo.ur exercises, when yo.u break the co.de beyo.nd repair, yo.u can always start o.ver fro.m o.ur saved ides, o.r yo.u can simply refresh the bro.wser to. Start o.ver ( this will depend o.n the state yo.u ran and generated the co.de). O.nly generate urls when yo.u need to. Save yo.ur co.de, no.t while yo.u are develo.ping.

We also. Stressed the impo.rtance o.f co.de structure. Fo.r instance, we talked abo.ut the impo.rtance o.f declaring and defining functio.ns: the best practice is to. Declare yo.ur functio.ns o.n the to.p and define them after the main() functio.n. It is similar to. Declaring integers. The techniques ensure yo.u have an invento.ry o.f functio.ns, variables, and o.bjects right at the beginning. It wo.rks like an index and can help yo.u avo.id definitio.n erro.rs.

Fo.rmatting and editing yo.ur co.de o.f unnecessary lines reduces the po.ssibility o.f erro.rs during develo.pment. Yo.u sho.uld always update yo.ur co.mments when yo.u make a change. Unfo.rmatted co.de will no.t impact perfo.rmance, the lo.gic o.f the co.de will. It is a co.llabo.ratio.n co.urtesy to. Fo.rmat yo.ur co.de, no.t to. Mentio.n ho.w much easier it makes things fo.r yo.u. O.ther pro.grammers o.n yo.ur team will be able to. Implement yo.ur co.de, o.r even impro.ve it, and they will leave co.mments.

But these types o.f practices are no.t just go.o.d fo.r yo.u. As the wo.rld mo.ves fo.rward it is beco.ming mo.re and mo.re co.mplicated, so. It is go.o.d fo.r pro.grams to. Explain themselves to. The user. If yo.ur pro.gram prints, make sure it is easy to. Read. We have seen ho.w this can be do.ne in this bo.o.k. Use escape sequences like \n to. Create new lines and \t to. Create ho.rizo.ntal table so. There is eno.ugh whitespace to. Yo.ur co.de. But as a back-end pro.grammer wo.rking with servers and o.ther equipment, yo.u may no.t have to. Print o.ut as o.ften as a fro.nt-end pro.grammer who. Serves co.ntent to. The client. The o.nly users who. May need to. See yo.ur print o.uts are o.ther technicians and administrato.rs managing tho.se machines thro.ugh the terminal. Fo.rmatting practices are o.ften underused in backend pro.gramming, but it is still a go.o.d practice to. Have. It is valuable to. Administrato.rs and technicians, who. Do. No.t have the reso.urces to. Navigate eso.teric co.mpiler-generated erro.rs that pro.grammers are used to. When debugging. So. A pro.gram that is fo.rmatted and gives this info.rmatio.n clearly in the terminal o.r co.nso.les is impo.rtant.

Take away: co.mputer science co.ncepts in c++

In additio.n to. Pro.gramming, we also. Explo.red so.me basic co.mputer science co.ncepts. We lo.o.ked at the behavio.r o.f machines and their language. We talked abo.ut ho.w learning pro.gramming is like learning a new language: bo.th have syntax and rules that ensure co.mmunicatio.n is po.ssible. C++ is a back-end server language that is used fo.r managing servers that co.ntro.l o.ceans o.f data. Unlike high-level languages like pytho.n, which are mo.re human, c++ wants pro.grammers to. Be mo.re detailed in their co.de. Each variable must be unique in a functio.n o.r we will have an erro.r. All functio.ns and statements are case sensitive and have specific rules that go.vern them. We have implemented many if()…else statements and made nested if-else statements. We saw that co.nditio.nal statements like if() can be executed witho.ut the else, but a missing else statement can cause an erro.r if the co.nditio.n is false. And just as a missing verb indicates a sentence is inco.mplete, else statements canno.t be implemented witho.ut an if().

We saw ho.w co.mputers co.mmunicate in binary numbers using lo.gical math. We saw bitwise functio.n wo.rk at the bit level, co.mpleting lo.gical math co.mputatio.ns like and, o.r, and no.t. All the o.ther c++ functio.ns that are o.bject-based must be translated by the co.mpiler into. Machine language. But bitwise functio.ns are faster because they skip that step and co.mmunicate directly to. The machine. They are o.ften deplo.yed in co.mpetitive pro.gramming to. Make highly agile pro.grams and ro.utines. O.utside o.f co.mpetitive pro.gramming, bitwise functio.ns have so.me functio.nality in managing big data.

The challenge with bitwise functio.ns is that they are very difficult fo.r humans to. Understand because they are binary. To. See what co.mputers see we had a brief co.mputer science lesso.n o.n binary and binary math. We made a “byte-sized” stream o.f register with o.ur bitwise ro.utine pro.gram and we made dynamic buffers to. Sto.re bits fo.r bitwise co.mputatio.ns. Tho.se virtual buffers and registers are ho.w servers manage terabytes o.f data. Think abo.ut this; o.ur buffers and registers were all o.ne byte lo.ng, but a terabyte is ![00211.jpeg](images/00211.jpeg)![00212.jpeg](images/00212.jpeg)![00213.jpeg](images/00213.jpeg)bytes). It was serving o.ver 3.25 billio.n ho.urs o.f co.ntent (“ho.w much data do.es yo.utube sto.re? - quo.ra,” n.d.). Bitwise functio.ns give these servers the ability to. Wo.rk with this lo.ad witho.ut interruptio.n o.r massive delays. This is o.ne o.f the best examples o.f the po.wer o.f c++ and its ability to. Handle big co.mplex systems. It is a useful language fo.r pro.grammers to. Learn. If yo.u visualize these data streams as arrays o.f 8 slo.ts, it will be easier fo.r yo.u to. Ratio.nalize many bitwise o.perato.rs, especially shift o.perato.rs.

In additio.n to. Binary pro.gramming, we wo.rked with different kinds o.f data and explo.red different aspects o.f o.bject pro.gramming. We did plenty o.f exercises where we dealt with strings, fo.r example. In fact, we used and deplo.yed strings in every o.ne o.f o.ur exercises. We saw that strings are also. Arrays o.f data, and can be manipulated like o.bjects except in a few ways. Strings have a length, size and can be parsed with vario.us o.bjects in the <string> library. Think o.f the co.py co.nstructo.r call co.mbinatio.n we learned. To. Parse a co.ntainer o.f any type, vecto.r o.r array, yo.u need a fo.r()lo.o.p with an addresso.f o.perato.r element. That task has a dedicated functio.n in the <string> library where all yo.u need is the index o.f the item yo.u are parsing. If there is o.ne thing yo.u sho.uld take away fro.m this bo.o.k it is pro.ficiency in handling strings: breako.ut escape sequences, handling strings thro.ugh array indexing, and passing strings to. Different functio.ns.

We also. Learned and discussed functio.nality and design co.nsideratio.ns. We talked, fo.r instance, abo.ut ho.w and when to. Use lo.o.ps. O.ur bank security example was best illustrated by o.ur exit co.ntro.lled lo.o.p example in a fail-clo.se system. Banks, as we said, sho.uld always have their do.o.rs lo.cked and clo.sed; they fail-clo.se. Mo.st events in the bank require do.o.rs and exits to. Fail-clo.se and the o.nly time they sho.uld o.pen it in a fire. The system sho.uld keep everything in check, where a co.nditio.n is tested after the ro.utine. The exit co.ntro.l lo.o.ps are also. Useful in o.ther areas, like in data co.ntro.l. Yo.utube do.es data co.rrectio.ns as a seco.ndary ro.utine o.f no.rmal o.peratio.ns. This makes sure the system is always running, no.t hunkered by resend-data requests.

As c++ is a backend-language it has to. Handle and wo.rk with multiple types o.f data. We have had a brief discussio.n abo.ut this when we spo.ke o.f vecto.r-based images as an o.bject class and their o.ther o.bject pro.perties. Pho.to. Manipulatio.n so.ftware like pho.to.sho.p is pro.grammed in c++ where aspects like image manipulatio.n take full use o.f the pro.gram’s po.wer. Vecto.rs allo.w image manipulatio.n witho.ut lo.ss o.f quality, unlike .jped o.r .png that are arrays o.f pixels. Vecto.rs like .svg o.r .pdf use vecto.r co.ntainers to. Describe their pixel lo.catio.ns, which has mo.re class features in c++ that allo.ws preservatio.n o.f the image.

This bo.o.k is also. Meant to. Be reference, so. I enco.urage yo.u to. Use the glo.ssary and the index to. Review to.pics. The glo.ssary has all the terms bo.lded and so.me o.f the co.de snippets we lo.o.ked at. It also. Includes the sectio.n where the terms are discussed in mo.re detail.

Glo.ssary

**Term**

Definitio.n

Sectio.n

**"+",**

Binary, arithmetic o.peratio.n that sums two. Variables. Also. Used to. Co.ncatenate strings in the <string> library

O.peratio.n:string co.ncatenatio.n

**"++"**

Increment o.perato.r used to. Increase the value o.f an integer by 1\. This unary o.perato.r is o.ften used to. Increase a variable within a lo.o.p.

Unary o.perato.rs

**“--”**

Unary o.perato.r that decreases a variable within a lo.o.p. This unary o.perato.r is o.ften used to. Increase a variable within a lo.o.p.

Unary o.perato.rs

“-”, arithmetic o.perato.r

Binary o.perato.r that subtracts o.ne o.perand fro.m ano.ther

Arithmetic o.perato.rs

“-”, unary o.perato.r

Unary minus o.perato.r that is used to. Change the sign o.f a variable o.r argument. Perfo.rming a unary minus o.peratio.n o.n a negative integer will make it po.sitive and vice versa.

Unary o.perato.rs

**“-=”**

The ato.mic subtractio.n used to. Co.mbine the ‘-’ and ‘=’ o.perato.rs. This o.perato.r first subtracts the current value o.f the variable o.n the left fro.m the value o.n the right. It then assigns the result to. The variable o.n the left. Fo.r example, x-=y wo.uld be a sho.rter way o.f writing x=x-y witho.ut having to. Use a separate arithmetic o.perato.r.

Assignment o.perato.rs

“!”, binary o.perato.r

Binary lo.gical “no.t” o.perato.r that returns a bo.o.lean true if the co.nditio.ns in co.nsideratio.n are no.t satisfied. If o.ne o.f the co.nditio.ns is true, then it returns a bo.o.lean false.

Lo.gical o.perato.rs

**“!”,**

No.t o.perato.r is used to. Reverse the bo.o.lean lo.gical state o.f an o.perand. Fo.r example, if a variable x has a bo.o.lean value o.f false, !X will be true.

Unary o.perato.rs

**“!=”**

“no.t-equal” o.perato.r that also. Checks whether two. Given o.perands are equal o.r no.t. Ho.wever, this o.perato.r returns a bo.o.lean true if the o.perands are no.t equal and returns false if the o.perands are equal.

Relatio.nal o.perato.rs

**“*”**

Binary o.perato.r that multiplies two. O.perands. The o.rder o.f the o.perands do.es no.t matter.

Arithmetic o.perato.rs

**“*=”**

O.perato.r fo.r the ato.mic multiplicatio.n, used to. Co.mbine the ‘*’ and ‘=’ o.perato.rs. This o.perato.r first multiplies the current value o.f the variable o.n the left to. The value o.n the right and then assigns the result to. The variable o.n the left. Fo.r example, x*=y wo.uld be a sho.rter way o.f writing x=x*y witho.ut having to. Use a separate arithmetic o.perato.r.

Assignment o.perato.rs

**“/”**

Binary divisio.n “fo.rward slash” o.perato.r that divides the first o.perand into. The seco.nd.

Arithmetic o.perato.rs

**“/=”**

Ato.mic divisio.n o.perato.r is a co.mbinatio.n o.f ‘/’ and ‘=’ o.perato.rs. This o.perato.r first divides the current value o.f the variable o.n the left by the value o.n right and then assigns the result to. The variable o.n the left. Fo.r example, x/=y wo.uld be a sho.rter way o.f writing x=x/y witho.ut having to. Use a separate arithmetic o.perato.r.

Assignment o.perato.rs

**“\?” Escape sequence**

Used fo.r questio.n marks.

Using escape sequences

**“\’” escape sequence**

Used fo.r single quo.tes.

Using escape sequences

**“\”” escape sequence**

Used fo.r do.uble quo.tes.

Using escape sequences

**“\\” escape sequence**

Used fo.r backslashes.

Using escape sequences

**“\f” escape sequence**

Stands fo.r “fo.rm feed” and is used to. Go. To. The next “page”.

Using escape sequences

**“\n” escape sequence**

Stands fo.r “line feed” and is used to. Go. To. The next line.

Using escape sequences

**“\t” escape sequence**

Stands fo.r “ho.rizo.ntal tab” and adds 5 spaces ho.rizo.ntally.

Using escape sequences

**“\v” escape sequence**

Stands fo.r “vertical tab” and is used fo.r spacing in vertical languages.

Using escape sequences

“&” unary o.perato.r

Addresso.f o.perato.r that is used to. Po.int to. The address o.f a variable.

Unary o.perato.rs

“&”, binary o.perato.r

Bitwise and that takes two. Numbers as o.perands and do.es and o.n every bit within the stream o.f the two. Numbers. The result stream o.f and is 1 o.nly if bo.th bits are 1\.

Bitwise o.perato.rs

**“&&”**

Binary lo.gical “and” o.perato.r that returns a bo.o.lean true when bo.th the co.nditio.ns in co.nsideratio.n are satisfied. O.therwise, it returns false.

Lo.gical o.perato.rs

**“%”**

Binary mo.dulus o.perato.r that returns the remainder fro.m dividing the first o.perand into. The seco.nd.

Arithmetic o.perato.rs

**“^”**

Bitwise xo.r that takes two. Numbers as o.perands and do.es xo.r o.n every bit within the stream o.f the two. Numbers. The result stream o.f xo.r is 1 if the two. Bits are different.

Bitwise o.perato.rs

**“+=”**

O.perato.r fo.r ato.mic additio.n, used to. Co.mbine the ‘+’ and ‘=’ o.perato.rs. This o.perato.r first adds the current value o.f the variable o.n the left to. The value o.n the right. It then sto.res the result to. The variable o.n the left. Fo.r example, x+=y wo.uld be a sho.rter way o.f writing x=x+y witho.ut having to. Use a separate arithmetic o.perato.r.

Assignment o.perato.rs

**“<”**

“less-than” o.perato.r that checks whether the first o.perand is less than the seco.nd o.perand. If so., this o.perato.r returns a bo.o.lean true. O.therwise, it returns false.

Relatio.nal o.perato.rs

**“<<”**

Left shift o.perato.r that takes two. Numbers and left shifts the bits o.f the first o.perand. The seco.nd o.perand is used to. Determine the number o.f places to. Shift.

Bitwise o.perato.rs

**“<=”**

“lesser-than o.r equal-to.” O.perato.r that checks whether the first o.perand is less than o.r equal to. The seco.nd o.perand. If so., this o.perand returns a bo.o.lean true. O.therwise it returns false.

Relatio.nal o.perato.rs

**“=”**

Equal assignment o.perato.r, used to. Assign the value o.n the right to. The variable o.n the left.

Assignment o.perato.rs

**“==”**

“equal” o.perato.r that checks whether two. Given o.perands are equal. If the o.perands are equal, it returns a bo.o.lean “true”, if no.t it returns false.

Relatio.nal o.perato.rs

**“>”**

“greater-than” o.perato.r that checks whether the first o.perand is greater than the seco.nd o.perand. If so., this o.perato.r returns a bo.o.lean true. O.therwise, it returns false.

Relatio.nal o.perato.rs

**“>=”**

“greater-than o.r equal-to.” O.perato.r that checks whether the first o.perand is greater than o.r equal to. The seco.nd o.perand. If so., this o.perand returns a bo.o.lean true. O.therwise, it returns a bo.o.lean false.

Relatio.nal o.perato.rs

**“>>”**

Right shift o.perato.r that takes two. Numbers and right shifts the bits o.f the first o.perand. The seco.nd o.perand is used to. Determine the number o.f places to. Shift.

Bitwise o.perato.rs

**“|”**

Bitwise o.r that takes two. Numbers as o.perands and do.es o.r o.n every bit within the stream o.f two. Numbers. The result stream o.f o.r is 1 if any o.f the two. Bits is 1.

Bitwise o.perato.rs

**“||”**

Binary lo.gical “o.r” o.perato.r that returns a bo.o.lean true when o.ne (o.r bo.th) o.f the co.nditio.ns in co.nsideratio.n are satisfied. If no.ne o.f the co.nditio.ns are satisfied, it returns false.

Lo.gical o.perato.rs

**“~”**

Bitwise no.t o.perato.r that takes o.ne number and switches the state o.f all the bits (1s to. 0s, 0s to. 1s).

Bitwise o.perato.rs

“bo.o.l” keywo.rd

Datatype keywo.rd that is sho.rt fo.r “bo.o.lean” and sto.res values with two. States: true o.r false. Has a size o.f 1 byte. These values can be expressed as either “0/1” o.r “false/true" with a manipulato.r.

Basic data types

“bo.o.lalpha/no.bo.o.lapha” manipulato.r

Input-o.utput manipulato.r that switches between using “0/1” to. “false/true” fo.r bo.o.lean values.

Using endl: input/o.utput manipulato.rs

“char” keywo.rd

Data type keywo.rd that is sho.rt fo.r “character” and sto.res single characters regardless o.f their capitalizatio.n. Has a size o.f 1 byte. Char values are surro.unded by single quo.tes.

Basic data types

“co.ut” o.bject

C++ pro.gramming o.bject part o.f the <io.stream> library that allo.ws a pro.gram to. Print o.ut values and text using the "<<" o.perato.r. This o.bject must be defined with a datatype, usually "std".

Using co.ut

“do.uble” keywo.rd

Data type keywo.rd that is used to. Sto.re numbers with decimals with 15 decimal digits. Has a size o.f 8 bytes. This data type can ho.ld mo.re decimal numbers and is preferred fo.r mathematical calculatio.ns.

Basic data types

**“else”**

Statement is used to. Specify a co.de in the event that its acco.mpanying if() expressio.n is false. Else canno.t be used witho.ut if ().

Lo.o.ps

“endl” manipulato.r

Input-o.utput manipulato.r that o.utputs “\n” and flushes the o.utput stream.

Using endl: input/o.utput manipulato.rs

“ends” manipulato.r

Input-o.utput manipulato.r that o.utputs “\0” [zero.].

Using endl: input/o.utput manipulato.rs

“flo.at” keywo.rd

Keywo.rd data type that sto.res numbers with decimals with 7 decimal digits. Has a size o.f 4 bytes. This data type is preferred fo.r ho.lding mo.netary numbers.

Basic data types

“flush” manipulato.r

Input-o.utput manipulato.r that flushes the o.utput stream.

Using endl: input/o.utput manipulato.rs

“get_mo.ney” manipulato.r

Input-o.utput manipulato.r that receives an input as a mo.netary value. This manipulato.r wo.rks in c++11 o.nly and may cause erro.rs in o.utdated c++ pro.gramming enviro.nments.

Using endl: input/o.utput manipulato.rs

“get_time” manipulato.r

Input-o.utput manipulato.r that receives an input as a date/time value acco.rding to. A specified fo.rmat. This manipulato.r wo.rks in c++11 o.nly and may cause erro.rs in o.utdated c++ pro.gramming enviro.nments.

Using endl: input/o.utput manipulato.rs

“int” keywo.rd

Data type keywo.rd that is sho.rt fo.r “integer” and sto.res who.le numbers. Has a size o.f 4 bytes. This keywo.rd includes po.sitive and negative integers.

Basic data types

“put_mo.ney” manipulato.r

Input-o.utput manipulato.r that fo.rmats and o.utputs a mo.netary value. This manipulato.r wo.rks in c++11 o.nly and may cause erro.rs in o.utdated c++ pro.gramming enviro.nments.

Using endl: input/o.utput manipulato.rs

“put_time” manipulato.r

Input-o.utput manipulato.r that receives an input as a date/time value acco.rding to. A specified fo.rmat. This manipulato.r wo.rks in c++11 o.nly and may cause erro.rs in o.utdated c++ pro.gramming enviro.nments.

Using endl: input/o.uput manipulato.rs

“quo.ted” manipulato.r

Input-o.utput manipulato.r allo.ws yo.u to. Insert and extract quo.ted strings with embedded spaces. This manipulato.r wo.rks in c++14 o.nly.

Using endl: input/o.utput manipulato.rs

“sho.wbase/no.sho.wbase” manipulato.r

Input-o.utput manipulato.r specifically fo.r mathematical o.utputs that co.ntro.ls whether a prefix is used to. Indicate a numeric base.

Using endl: input/o.utput manipulato.rs

“sho.wpo.s/no.sho.wpo.s” manipulato.r

Input-o.utput manipulato.r that co.ntro.ls whether the “+” sign is used to. Indicate no.n-negative numbers.

Using endl: input/o.utput manipulato.rs

“uppercase/no.uppercase” manipulato.r

Input-o.utput manipulato.r that co.ntro.ls whether uppercase characters are used with so.me o.utput fo.rmats.

Using endl: input/o.utput manipulato.rs

**“using namespace std;” statement**

Line o.f co.de frequently used to. Unilaterally declare the "std" datatype fo.r io.stream library o.bjects and manipulato.rs. This unilateral declaratio.n makes the co.de easier to. See. Ho.wever, this is disco.uraged o.utside o.f practice because it can make string handling ill-defined in pro.grams, thus, causing erro.rs that are difficult to. Mitigate. Exercises in this bo.o.k will avo.id using this statement.

O.mitting namespace

**[string_name].length() attribute**

Co.ding syntax fo.r calling the "length" string o.bject attribute .

String o.bjects: length( ) attribute

**Actual parameters**

Parameters co.ming into. A defined functio.n.

Parameter passing

Algo.rithm

An o.rganizatio.nal to.o.l used to. Plo.t o.ut the aspects o.f a pro.gram including (1) data in, if applicable, (2) o.peratio.ns perfo.rmed o.n declared variables, and (3) the result o.f running the pro.gram.

Principles o.f pro.gramming

Arithmetic o.perato.rs

Binary and unary o.peratio.ns that are used to. Perfo.rm co.mmo.n mathematical o.peratio.ns.

Arithmetic o.perato.rs

**Assembly language**

Describes a lo.w-level pro.gramming language that requires a co.mpiler to. Co.nvert it into. Machine co.de.

Chapter 1: setting up a c++ develo.pment enviro.nment

Assignment o.perato.rs

Used to. Assign a value to. A variable and change values o.n the fly, reducing the number o.f instructio.ns in a pro.gram.

Assignment o.perato.rs

Ato.mic o.peratio.ns

O.peratio.ns that co.mbine assignments with o.ther o.peratio.ns. Ato.mic o.peratio.ns allo.w pro.grammers to. Manipulate a value sto.red within a variable and reassign it immediately.

Assignment o.perato.rs

**Base-10**

Number system used by human beings assign place value to. Numerals. Base-10 is also. Kno.wn as the decimal system because a digit's value in a number is determined by where it lies in relatio.n to. The decimal po.int. The value is multiplied by a base po.wer o.f 10, where each po.int away fro.m the left o.f the decimal is 10^(n+1) and each po.int to. The right o.f the decimal is 10^(n-1).

Bitwise o.perato.rs

**Binary number system**

See base-2

Bitwise o.perato.rs

Binary o.perato.r

Classificatio.n o.f o.perato.rs that execute with two. O.perands.

Chapter 4: o.peratio.ns in c++

Bitwise o.perato.rs

Lo.gic o.perato.rs that o.perate o.n numbers at the binary level.

Bitwise o.perato.rs

**Bluefish**

A free so.ftware advanced text edito.r with a variety o.f to.o.ls fo.r pro.gramming in general and the develo.pment o.f dynamic websites.

Setting up the text edito.r

**Byte**

Measurement o.f data co.mpo.sed o.f 8 bits. A byte can represent up to. 225 numbers ( 0b 1111111 ).

Unary o.perato.rs

**C++14**

Advanced versio.n o.f c++ that makes this versio.n slightly mo.re intelligible fo.r humans to. Pro.gram in. "standard c++" usually refers to. C++11, also. Kno.wn as c++0x.

Chapter 1: setting up a c++ develo.pment enviro.nment.

Cento.s

A free, co.mmunity-suppo.rted. Linux distributio.n o.perating system that is functio.nally co.mpatible with red hat enterprise linux (rhel).

Linux co.mpiler installatio.n

Co.de

See executable file

Chapter 1: setting up a c++ develo.pment enviro.nment

Co.de::blo.cks

A free o.pen so.urce ide designed fo.r c++. This ide suppo.rts many c++ co.mpilers including gcc, clang, and visual c++ in micro.so.ft. This ide can pro.gram in c++, c, and fo.rtran.

Windo.ws ide installatio.n

Co.mmand-line interface (cli)

Metho.d o.f interacting with a co.mputer pro.gram where the user co.ntro.ls the pro.gram with entering lines o.f co.de.

Setting up a text edito.r

Co.mments

Lines o.f co.de that are igno.red by the co.mpiler and indicated by a do.uble slash at the beginning o.f the line in c++. Co.mments are used to. Anno.tate co.de and leave no.tes to. Guide o.ther pro.grammers studying yo.ur co.de.

O.verview o.f c++ syntax

Co.mpiled language

See lo.w-level language

Chapter 3

Co.ncatenatio.n, string

A co.mmo.n pro.gramming feature that allo.ws pro.grammers to. Dynamically co.ntro.l text by fielding co.ntent fro.m a so.urce and serving it within their pro.gram. In c++ string co.ncatenatio.n is do.ne thro.ugh "+", an arithmetic o.perato.r.

O.peratio.n:string co.ncatenatio.n

Co.nditio.nal o.perato.r

Bo.o.lean lo.gic based o.perato.r with three o.perand expressio.ns. The o.utco.me o.f the co.nditio.nal o.perato.r depends o.n the first expressio.n.

Ternary o.perato.rs

Co.nditio.nal sho.rt-circuit

When pro.gram develo.pers use lo.gical o.perato.rs and co.nditio.nal statements to. Co.ntro.l ho.w a pro.gram behaves.

Lo.gical o.perato.rs

Co.py co.nstructo.r call

Metho.d o.f searching and printing indexes. Co.nsists o.f fo.r() lo.o.p with an index variable with an addresso.f o.perato.r, and a co.ntainer o.bject with an index such as an array.

Unary o.perato.rs

Co.unter

An arbitrary variable that is used in co.njunctio.n with an arithmetic unary o.perato.r to. Incrementally lo.o.p an indicated expressio.n.

Lo.o.ps

**Data**

O.perands, o.r the vario.us kinds o.f data that the functio.ns and statements are acting o.n

O.verview o.f syntax

**Data type**

Attribute o.f a variable which tells the co.mpiler o.r interpreter ho.w the pro.grammer intends to. Use the data. Co.mmo.n data types include real numbers, integers, and "true-false" bo.o.lean variables.

Chapter 3

**Debugging**

Pro.cess o.f lo.catio.n and remo.ving co.mputer pro.gram erro.rs and abno.rmalities, also. Kno.wn as "bugs." as a general rule, smaller, mo.dularized co.de that calls o.n functio.ns is easier to. Debug than larger files.

O.verview o.f syntax

**Decimal number system**

See base-10

Bitwise o.perato.rs

Do. {}...while() lo.o.p

Exit co.ntro.lled lo.o.p that tests a single co.nditio.n and lo.o.ps a blo.ck o.f co.de until the co.nditio.n is met.

Lo.o.ps

**Else if()**

Co.nditio.nal statement co.mbinatio.n used to. Nest co.nditio.nal if()... Else statements. Pro.grammers are advised to. Use a switch if there are numero.us co.nditio.ns to. Test.

Lo.o.ps

**Escape sequence**

Special in-string character co.mbinatio.ns that are used to. Represent certain special characters within strings and character streams. Escape sequences allo.w pro.grammers to. Include symbo.ls in strings witho.ut co.nfusing the co.mpiler.

Using escape sequences

**Executable file**

List o.f instructio.ns that are used to. Perfo.rm the o.peratio.ns o.f a pro.gram.

Chapter 1

File extensio.n

File suffix that info.rms the co.de co.mpiler what language the executable file is in. The c++ language is indicated by ".cpp" o.r ".hpp" extensio.ns.

Chapter 1

First principal o.f pro.gramming

A pro.gram must be designed to. Co.mplete a task in the smallest number o.f functio.ns po.ssible. This principle reduces o.verhead and increases perfo.rmance o.f a pro.gram.

Principles o.f pro.gramming

Fo.r() lo.o.p

Entry co.ntro.lled lo.o.p that has three inputs: an initializatio.n expressio.n, a test expressio.n and an update expressio.n. The fo.r lo.o.p will execute its blo.ck o.f co.de until the test expressio.n repo.rts false.

Lo.o.ps

Fo.rmal parameters

Variables used to. Define the initial arguments, and any arguments in the functio.n befo.re the actual parameters are passed.

Parameter passing

Functio.n

A blo.ck o.f co.de that takes inputs to. Perfo.rm an actio.n and runs when called.

Chapter 6: creating...

Functio.n o.verlo.ading

Pro.gramming technique o.f co.nso.lidating co.de thro.ugh stacking several data types o.nto. O.ne functio.n.

Functio.n o.verlo.ading

Functio.nality

Ho.w pro.gram features and utilities can be implemented in a co.de to. Achieve a specific result.

Chapter 4: o.peratio.ns in c++

Functio.ns

Co.de that encapsulates instructio.ns that may take inputs and o.utput so.me result. Every functio.n “[functio.n-name]()”, where [functio.n_name] is so.me arbitrary functio.n, is always fo.llo.wed by curly brackets {} and every explicitly stated instructio.n within the curly brackets will be executed by the co.mpiler.

O.verview o.f syntax

**Gedit**

Free, o.pen-so.urce, general-purpo.se text edito.r that includes to.o.ls fo.r editing so.urce co.de and structured text such as markup languages.

Linux co.mpiler installatio.n

Getline() functio.n

C++ functio.n fro.m the <string> library that extracts all characters fro.m an input string into. A string array.

Cin and getline() functio.n

Gnu co.llectio.n co.mpiler (gcc)

An o.pen so.urce co.mpiler system pro.duced by the gnu pro.ject suppo.rting vario.us pro.gramming languages. Gcc is a key co.mpo.nent o.f the gnu to.o.lchain and is the standard co.mpiler fo.r mo.st linux pro.jects.

Linux co.mpiler installatio.n

**Graphical user interface (gui)**

Metho.d o.f interacting with a co.mputer pro.gram that allo.ws users to. Interact with graphical ico.ns and visual indicato.rs such as seco.ndary no.tatio.n instead o.f inputting co.mmands.

Setting up text

**Header file library**

Lines that start with the po.und sign (#) that are used by the co.mpiler to. Call library functio.ns.

O.verview o.f syntax

**If() .... Else statement**

Co.nditio.nal statement functio.n co.mbinatio.n that tests a single co.nditio.n and executes explicitly stated blo.cks o.f co.de based o.n the results o.f the test.

Lo.o.ps

**If()... Else statement**

A nested functio.n that executes all instructio.ns within its curly brackets “{}” given a specified co.nditio.n is met. O.therwise, it executes the items with the enclo.sed else {} statement. These statements always deplo.y a relatio.nal o.perand to. Test the co.nditio.n.

Relatio.nal o.perato.rs

Integrated develo.pment enviro.nment (ide)

Pro.gramming enviro.nment used to. Write co.de, test fo.r erro.rs and translate a pro.gram.

Chapter 1

Linux distributio.n (distro.)

An o.perating system made fro.m a linux kernel based so.ftware co.llectio.n and package management system fo.r installing additio.nal so.ftware.

Linux co.mpiler installatio.n

Lo.gic gates

Physical electro.nic circuits that have o.ne o.r mo.re inputs while o.nly having o.ne o.utput. And gates o.nly pass a “1” when all inputs are “1”; o.r gates pass a “1” as their o.utput when they receive a “1” at any o.f their inputs; no.t gates pass a “1” when they receive a “0” at their input.

Lo.gical o.perato.rs

Lo.gical o.perato.rs

Binary o.perato.rs used in co.mbinatio.n with the relatio.nal o.perato.rs co.mbine two. O.r mo.re co.nditio.ns to. Describe a specific co.nstraint.

Lo.gical o.perato.rs

Lo.o.ps

Functio.n that execute a blo.ck o.f co.de as lo.ng as a specified co.nditio.n is reached

Lo.o.ps

Lo.w-level language

A pro.gramming language that clo.sely fo.llo.ws a co.mputer's instructio.n set architecture—co.mmands o.r functio.ns in the language map clo.sely to. Pro.cesso.r instructio.ns. This reduces the o.verhead fo.r running the pro.gram as the co.mpiler takes less reso.urces to. Translate lo.w-level languages into. Machine co.de.

Chapter 2

**Machine language**

Co.ding language that is directly co.mpiled and executed by a cpu. See "assembler language"

Chapter 1

Manipulato.r, input/o.utput

Helper functio.ns within the c++ io.stream library that make it po.ssible to. Co.ntro.l input/o.utput streams using the "<<" o.perato.r o.r the ">>" o.perato.r.

Using endl: input/o.utput manipulato.rs

No.tepad ++

Text edito.r and so.urce co.de edito.r fo.r use with micro.so.ft windo.ws.

Setting up text

O.bject

A general co.mputing term that describes a metho.d that the co.mputer uses to. Manage data.

First pro.gram: o.utput and basic strings

O.perand

O.peratio.n co.mpo.nent that describes the value, o.bject, o.r variable being o.perated o.n.

No.te: o.perand...

O.peratio.ns

Features such as co.ntro.l lo.o.ps that implement decisio.n-making in pro.grams.

Chapter 4: o.peratio.ns in c++

O.perato.r

O.peratio.n co.mpo.nent that describes the symbo.l indicating the so.rt o.f o.peratio.n being carried o.ut. O.perato.rs are described by ho.w many o.perands they can o.perate o.n at a time: unary, binary, and ternary.

No.te: o.perand...

O.rganizatio.n identifier

Pro.prietary apple naming co.nventio.n that is used to. Create a unique id fo.r pro.grams acro.ss vario.us apple databases: the apple develo.per website, and iclo.ud co.ntainer, itunes co.nnect po.rtal in the appsto.re. The o.rganizatio.n identifier is used as the first argument o.f a “reversed do.main” that ensures that all develo.ped pro.jects can be streamlined into. The pro.prietary maco.s framewo.rk.

Mac ide installatio.n

**Parameter pass by reference**

Bo.th actual and fo.rmal parameters refer to. The same lo.catio.ns. Therefo.re, any changes made inside the main() functio.n will impact the actual parameters that were passed.

Parameter passing

**Parameter pass by value**

Values o.f actual parameters are co.pied into. And sto.red in the functio.n’s fo.rmal parameters. Any changes made inside main() do.es no.t impact the actual parameters that were passed.

Parameter passing

**Red hat enterprise linux (rhel)**

A co.mmercial linux distributio.n develo.ped by red hat fo.r the co.mmercial market.

Linux co.mpiler installatio.n> no.te: there are many distributio.ns…

**Register**

An array o.f binary sto.rage where each bit gets its o.wn place in the array. Registers are used to. Calculate bitwise o.perato.rs.

Bitwise o.perato.rs

Relatio.nal o.perato.rs

Binary o.perato.rs that are used to. Co.mpare two. Values and return a bo.o.lean respo.nse.

Relatio.nal o.perato.rs

**Script**

Supplementary list o.f co.mmands executed by certain pro.grams o.r scripting engines.

Chapter 6: creating...

**See base-2**

Number system used by machines to. Calculate co.mputatio.ns. Also. Kno.wn as the binary number system. Binary numbers are represented as a stream o.f bits, where each singular bit can be o.ne o.f the two. States: 1 o.r 0. The po.sitio.n o.f the 1 bit in the stream determines the value o.f the number.

Bitwise o.perato.rs

Server-side pro.gramming

Writing co.de that nego.tiates and delivers co.ntent to. A dynamic, o.r changing website. C++ is, majo.rly, a server side language.

Mac ide installatio.n

**Service level agreement (sla)**

Term in it management that describes a co.mmitment between the techno.lo.gy administrato.r, the o.ne pro.viding the service, and a client.

O.verview o.f syntax

Sizeo.f()

Unary o.peratio.n that queries the size o.f an o.bject and delivers its size in bytes.

Unary o.perato.rs

So.ftware develo.pment kit (sdk)

A set o.f to.o.ls used fo.r develo.ping applicatio.ns pro.vided by hardware and so.ftware pro.viders.

Mac ide installatio.n

**Statements**

General term to. Describe the beginning line o.f co.de with specific instructio.ns that the co.mpiler reco.gnizes o.utside o.f functio.ns. Ho.w these are highlighted in language syntax enviro.nments depend o.n the type o.f the statement and the co.nventio.ns o.f the pro.gramming enviro.nment.

O.verview o.f syntax

**String array**

An o.rderly arrangement o.f characters where each character o.f the string is indexed in its o.wn numerical lo.catio.n.

String indexes and arrays

**Strings**

A co.mputer pro.gramming data type that represents a sequence o.f characters, either as a literal co.nstant o.r as so.me kind o.f variable.

Advanced strings

**Switch () statement**

Multibranch statement used to. Execute different co.de blo.cks based o.n the value o.f an evaluated expressio.n

Lo.o.ps

Ternary o.perato.r

Classificatio.n o.f o.perato.rs that accept mo.re than 2 o.perands, o.r co.nditio.nal o.perato.rs with several arguments.

Ternary o.perato.r

Text edito.r

Pro.gram that enables editing o.f the co.de.

Chapter 1

Unary o.perato.r

Classificatio.n o.f o.perato.rs that execute with a single o.perand.

Unary o.perato.r

**Variables**

A co.ncept bo.rro.wed fro.m mathematics to. Describe a symbo.lic value who.'s asso.ciated value can be changed and o.perated upo.n. Variables are used to. Co.ntro.l a pro.gram thro.ugh o.peratio.nal functio.ns.

Chapter 3

While() lo.o.p

Entry co.ntro.lled lo.o.p that tests a single co.nditio.n and lo.o.ps a blo.ck o.f co.de until the co.nditio.n is met.

Lo.o.ps

Xco.de

A free ide so.ftware develo.pment suite fo.r the maco.s. This ide has utilities fo.r develo.ping c++ based pro.grams fo.r maco.s o.riented o.perating systems like tvo.s fo.r apple tv, watcho.s fo.r apple watches, and ipado.s fo.r ipad tablets.

Mac ide installatio.n

Index

Fo.r yo.ur co.nvenience, all co.ding pro.gram exercises have been po.sted here.

“hello. Wo.rld” pro.gram in geeksfo.rgeeks ide

// simple c++ pro.gram to. Display "hello. Wo.rld"

// header file fo.r input o.utput functio.ns

#include<io.stream>

Using namespace std;

// main functio.n -

// where the executio.n o.f pro.gram begins

Int main()

{

// prints hello. Wo.rld

Co.ut<<"hello. Wo.rld";

Return 0;

}

Using in-string escape sequences to. Delimit and manipulate the o.utput

// simple c++ pro.gram to. Display "hello. Wo.rld"

// header file fo.r input o.utput functio.ns

#include<io.stream>

Using namespace std;

// main functio.n -

// where the executio.n o.f pro.gram begins

Int main()

{

// prints hello. Wo.rld

Co.ut<<"hello. Wo.rld!\n";

Co.ut<<"i am learning c++";

Return 0;

}

Using a input/o.utput manipulato.r to. Delimit and manipulate the o.utput

// simple c++ pro.gram to. Display "hello. Wo.rld"

// header file fo.r input o.utput functio.ns

#include<io.stream>

Using namespace std;

// main functio.n -

// where the executio.n o.f pro.gram begins

Int main()

{

// prints hello. Wo.rld

Co.ut<<"hello. Wo.rld!\n";

Co.ut<<"i am learning c++";

Return 0;

}

Testing stability: using a co.mment to. Remo.ve “using namespace”

// simple c++ pro.gram to. Display "hello. Wo.rld"

// header file fo.r input o.utput functio.ns

#include<io.stream>

//using namespace std;

// main functio.n -

// where the executio.n o.f pro.gram begins

Int main()

{

// prints hello. Wo.rld

Co.ut<<"hello. Wo.rld!" << endl;

Co.ut<<"i am learning c++";

Return 0;

}

Declaring the io.stream o.bjects and manipulato.rs

With namespace

// simple c++ pro.gram to. Display "hello. Wo.rld"

// header file fo.r input o.utput functio.ns

#include<io.stream>

// main functio.n -

// where the executio.n o.f pro.gram begins

Int main()

{

// prints hello. Wo.rld

Std::co.ut<<"hello. Wo.rld!"

<< std::endl;

Std::co.ut<<"i am learning c++";

Return 0;

}

Witho.ut namespace

// simple c++ pro.gram to. Display "hello. Wo.rld"

// header file fo.r input o.utput functio.ns

#include<io.stream>

//using namespace std;

// main functio.n -

// where the executio.n o.f pro.gram begins

Int main()

{

// prints hello. Wo.rld

Co.ut<<"hello. Wo.rld!" << endl;

Co.ut<<"i am learning c++";

Return 0;

}

Declaring int numbers

// simple c++ pro.gram to. Display "hello. Wo.rld"

// header file fo.r input o.utput functio.ns

#include<io.stream>

// main functio.n -

// where the executio.n o.f pro.gram begins

Int main()

{

//declares an int 'mynum'

Int mynum = 10;

// prints hello. Wo.rld + mynum

Std::co.ut<<"hello. Wo.rld!\n\t";

Std::co.ut<< mynum;

Std::co.ut<<" is my number.";

Return 0;

}

Summing inputs and printing the result

Inputs

11

12
co.de

#include<io.stream>

Int main()

{

// explains pro.gram to. User

Std::co.ut<<"welco.me! Enter two. Numbers and \ni will sum them.\n";

//declares input variables

Int x, y;

//declares o.utput variable

Int sum;

//pro.mpts user fo.r inputs

Std::co.ut<<"type a number: ";

Std::cin >> x;

Std::co.ut << x <<"\n";

Std::co.ut << "type ano.ther number: ";

Std::cin>> y;

Std::co.ut << y <<"\n";

//o.perates o.n the variables

Sum= x+y;

//prints results

Std::co.ut<<"sum is: "<<sum;

Return 0;

}

Using int with flo.at o.r do.uble

Inputs

22

7

Co.de

#include<io.stream>

Int main()

{

// explains pro.gram to. User

Std::co.ut<<"welco.me! Enter two. Numbers and \ni will divide them.\n";

//declares input variables

Int x, y;

//declares o.utput variable

Flo.at result;

//pro.mpts user fo.r inputs

Std::co.ut<<"type a number: ";

Std::cin >> x;

Std::co.ut << x <<"\n";

Std::co.ut << "type ano.ther number: ";

Std::cin>> y;

Std::co.ut << y <<"\n";

//o.perates o.n the variables

Result= x/y;

//prints results

Std::co.ut<<"result is: "<<result;

Return 0;

}

Co.mparing flo.at and do.uble

#include <io.stream>

Int main()

{

//declares o.peratio.n variables

Flo.at x=27, y=7;

Do.uble xd=22, yd=7;

//declares o.utput variable

Flo.at result;

Do.uble resultd;

Bo.o.l test;

//o.perates o.n the variables

Result= x/y;

Resultd= xd/yd;

Test=(result==resultd);

//prints results

Std::co.ut<< "true o.r false?: \n\tflo.at(" << x << "/" << y <<")";

Std::co.ut<< " is equal to. Do.uble(" << xd << "/" << yd <<")\n";

//std::co.ut<<"is flo.at is equal to. Do.uble?: ";

Std::co.ut << std::bo.o.lalpha

<< "\t"<<test;

Return 0;

}

String co.ncatenatio.n

#include<io.stream>

//call the library fo.r string handling

#include <string>

Int main()

{

//declare variables and co.mplete o.peratio.n

Std::string firstname = "jo.hn ";

Std::string lastname = "do.e";

Std::string fullname = firstname + lastname;

// prints results

Std::co.ut<<"hello. "

<< fullname <<".";

Return 0;

}

Print fullname.length()

#include<io.stream>

//call the library fo.r string handling

#include <string>

Int main()

{

//declare variables and co.mplete o.peratio.n

Std::string firstname = "jo.hn";

Std::string lastname = "do.e";

Std::string fullname = firstname +" "+lastname;

// prints results

Std::co.ut<<"hello. "

<< fullname <<".\n";

Std::co.ut<<"yo.ur full name is "

<<fullname.length()

<<" characters lo.ng.";

Return 0;

}

Access fullname string array

#include<io.stream>

//call the library fo.r string handling

#include <string>

Int main()

{

//declare variables and co.mplete o.peratio.n

Std::string firstname = "jo.hn";

Std::string lastname = "do.e";

Std::string fullname = firstname +" "+lastname;

// prints results

Std::co.ut<<"hello. "

<< fullname <<".\n";

Std::co.ut<<"the third character o.f yo.ur full name \nis \'"

<<fullname[2]

<<"\'.";

Return 0;

}

String co.ncatenatio.n with cin

Input

Jo.hn

Do.e

Co.de

#include<io.stream>

//call the library fo.r string handling

#include <string>

Int main()

{

//declare variables

Std::string firstname;

Std::string lastname;

//pro.mpt user fo.r name

Std::co.ut<<"what is yo.ur name?\n";

Std::cin>> firstname;

Std::co.ut<< firstname <<"\n";

Std::cin>> lastname;

Std::co.ut<< lastname <<"\n";

//calculate o.peratio.n

Std::string fullname = firstname + " "+ lastname;

// prints results

Std::co.ut<<"\nhello. "

<< fullname <<".";

Return 0;

}

String terminatio.n with cin

Input

Jo.hn do.e

Co.de

#include<io.stream>

//call the library fo.r string handling

#include <string>

Int main()

{

//declare variables

Std::string fullname;

//pro.mpt user fo.r name

Std::co.ut<<"what is yo.ur full name?\n";

Std::cin>> fullname;

// greet user

Std::co.ut<<"\nhello. "

<< fullname <<".";

Return 0;

}

Arithmetic ro.utine pro.gram

#include<io.stream>

Int main()

{

//declare variables

Int a=25, b=3;

Int result;

// printing a and b

Std::co.ut<< "this pro.gram will go. Thro.ugh an\narithmetic ro.utine with the fo.llo.wing\nvariables where: "

<<"a is "<<a<<" and b is "<<b<<"\n";

// additio.n

Result = a + b;

Std::co.ut << "\ta+b is: "<< result << "\n";

// subtractio.n

Result = a - b;

Std::co.ut << "\ta-b is: "<< result << "\n";

// multiplicatio.n

Result = a * b;

Std::co.ut << "\ta*b is: "<< result << "\n";

// divisio.n

Result = a / b;

Std::co.ut << "\ta/b is: "<< result << "\n";

// mo.dulus

Result = a % b;

Std::co.ut << "\ta%b is: "<< result << "\n";

Return 0;

}

Relatio.nal ro.utine pro.gram

#include<io.stream>

Int main()

{

//declare variables

Int a=25, b=3;

// print an explanatio.n o.f the pro.gram

Std::co.ut<< "this pro.gram will go. Thro.ugh an\nrelatio.nal ro.utine with the fo.llo.wing\nvariables where: "

// print a and b

<<"a is "<<a<<" and b is "<<b<<"\n";

// greater than example

If (a > b)

Std::co.ut << "\ta is greater than b\n";

Else

Std::co.ut << "\ta is less than o.r equal to. B\n";

// greater than equal to.

If (a >= b)

Std::co.ut << "\ta is greater than o.r equal to. B\n";

Else

Std::co.ut << "\ta is lesser than b\n";

// less than example

If (a < b)

Std::co.ut << "\ta is less than b\n";

Else

Std::co.ut << "\ta is greater than o.r equal to. B\n";

// lesser than equal to.

If (a <= b)

Std::co.ut << "\ta is lesser than o.r equal to. B\n";

Else

Std::co.ut << "\ta is greater than b\n";

// equal to.

If (a == b)

Std::co.ut << "\ta is equal to. B\n";

Else

Std::co.ut << "\ta and b are no.t equal\n";

// no.t equal to.

If (a != b)

Std::co.ut << "\ta is no.t equal to. B\n";

Else

Std::co.ut << "\ta is equal b\n";

Return 0;

}

Lo.gical ro.utine pro.gram

#include<io.stream>

Int main()

{

//declare variables

Int a=5, b=0, c=12, d=24;

// print an explanatio.n o.f the pro.gram

Std::co.ut<< "this pro.gram will go. Thro.ugh a\nlo.gical ro.utine with the fo.llo.wing\nvariables where: "

// print a and b

<<"a is "<<a<<" and b is "<<b<<"\n"

<<"c is "<<c<<" and d is "<<d<<"\n";

// lo.gical and example

If (a>b && c==d)

Std::co.ut << "\ta is greater than b and c is equal to. D\n";

Else

Std::co.ut << "\t and co.nditio.n no.t satisfied--\n"

<< "\t\t(a>b && c==d)\n";

// lo.gical o.r example

If (a>b || c==d)

Std::co.ut << "\ta is greater than b o.r c is equal to. D\n";

Else

Std::co.ut << "\tneither a is greater than b no.r c is equal "

<< " to. D\n";

// lo.gical no.t example

If (!B)

Std::co.ut << "\tb is zero.\n";

Else

Std::co.ut << "\tb is no.t zero.\n";

Return 0;

}

Sho.rt circuit detectio.n pro.gram

#include <io.stream>

Using namespace std;

Int main() {

//declare two. Variables

Int a=10, b=4;

//print explainatio.n o.f the pro.gram

Co.ut<< "this this pro.gram will test if the o.r gate \n"

<<"o.r the and gate sho.rts when a is equal to. B. \n";

Co.ut<< "\tcurrent value o.f a: "

<<a <<"\n";

Co.ut<< "\tcurrent value o.f b: "

<<b <<"\n";

Bo.o.l resand = ((a == b) && co.ut << "--- o.r gate sho.rt circuited.\n");

Bo.o.l reso.r = ((a == b) || co.ut << "--- and gate sho.rt circuited.\n");

Return 0;

}

Bitwise ro.utine with register printing

#include <io.stream>

#include <bitset>

Using namespace std;

Int main() {

//declare o.perand numbers

Unsigned int a = 60; // 60 = 0011 1100

Unsigned int b = 13; // 13 = 0000 1101

//declare register c where calculatio.ns will take place

Int c = 0;

//print o.perand registers

Co.ut<<"o.perand registers a: "<< a

<<" and b: " << b

<< "\n\tregister a: -0b "<< bitset<8>(a)

<< "\n\tregister b: -0b "<< bitset<8>(b)<< endl ;

//bitwise and

C = a & b; // 12 = 0000 1100

Co.ut << "line 1 - value o.f c is : " << c

//print register

<< "\n\t and registers a&b: -0b "<< bitset<8>(c)<< endl ;

//bitwise o.r

C = a | b; // 61 = 0011 1101

Co.ut << "line 2 - value o.f c is: " << c

//print register

<< "\n\t o.r register a|b: -0b "<< bitset<8>(c)<< endl ;

//bitwise xo.r

C = a ^ b; // 49 = 0011 0001

Co.ut << "line 3 - value o.f c is: " << c

//print register

<< "\n\t xo.r register a^b: -0b "<< bitset<8>(c)<< endl ;

//bitwise no.t

C = ~a; // -61 = 1100 0011

Co.ut << "line 4 - value o.f c is: " << c

//print register

<< "\n\t no.t register ~a: -0b "<< bitset<8>(c)

<< "\n\t co.mpare to. Register a: -0b "<< bitset<8>(a)<< endl ;

//left shift

C = a << 2; // 240 = 1111 0000

Co.ut << "line 5 - value o.f c is: " << c

//print register

<< "\n\t left shift register a<<2: -0b "<< bitset<8>(c)<< endl ;

//right shift

C = a >> 2; // 15 = 0000 1111

Co.ut << "line 6 - value o.f c is: " << c

//print register

<< "\n\t right shift register a>>2: -0b "<< bitset<8>(c)<< endl ;

Return 0;

}

Assignment ro.utine

#include <io.stream>

Using namespace std;

Int main() {

// assigning value 10 to. A

// using "=" o.perato.r

Int a = 10;

Co.ut<<"this pro.gram will ato.mically manipulate the value o.f a"

<<"\n\tthe value o.f a is " <<a;

// assigning value by adding 10 to. A

// using "+=" o.perato.r

A += 10;

Co.ut<<"\n ato.mically + 10: the value o.f a is no.w " <<a;

// assigning value by subtracting 10 fro.m a

// using "-=" o.perato.r

A -= 10;

Co.ut<<"\n ato.mically - 10 fro.m a: the value o.f a is no.w " <<a;

// assigning value by multiplying 10 to. A

// using "*=" o.perato.r

A *= 10;

Co.ut<<"\n ato.mically * 10: the value o.f a is no.w " <<a;

// assigning value by dividing 10 fro.m a

// using "/=" o.perato.r

A /= 10;

Co.ut<<"\n ato.mically dividing by 10: the value o.f a is no.w " <<a ;

Return 0;

}

While lo.o.p featuring a unary o.perato.r

#include <io.stream>

Using namespace std;

Int main() {

//initialize the co.unter, i

Int i = 0;

//while i is less than five, print i

While (i < 5) {

Co.ut << i << "\n";

I++; //unary co.unter i

}

Return 0;

}

Unary o.perato.r ro.utine with po.st- and pre o.peratio.ns

#include <io.stream>

Using namespace std;

Int main() {

Int a = 10, buf;

Co.ut<<"this pro.gram will use unary o.perato.rs to. Increment \nand decrement variable a and a buffer"

<<"\n\tthe value o.f a is " <<a;

// po.st-increment

Buf = a++;

// a beco.mes 11 no.w

Co.ut << "\npo.st-increment: a is "<<a<<" and buf is "<<buf;

// po.st-decrement example:

Buf = a--;

// a beco.mes 10 no.w

Co.ut << "\npo.st-decrement:a is "<<a<<" and buf is "<<buf;

// pre-increment example:

// buf is assigned 11 no.w since a is updated here itself

Buf = ++a;

// a and res have same values = 11

Co.ut << "\npre-increment:a is "<<a<<" and buf is "<<buf;

// pre-decrement example:

// res is assigned 10 o.nly since a is updated here itself

Buf = --a;

// a and res have same values = 10

Co.ut << "\npre-decrementt:a is "<<a<<" and buf is "<<buf;

Return 0;

}

Co.nditio.nal o.peratio.ns demo.

#include <bits/stdc++.h>

Using namespace std;

Int main()

{

Co.ut << "this pro.gram will pick the greatest o.ne using two. "

<<"\nmetho.ds:a co.nditio.nal o.perato.r and"

<<" an \nif()... Else statement."

<< "\n\twe expect a result o.f 5.";

Co.ut << "\n\nexecute expressio.n using"

<< " ternary o.perato.r: ";

// execute expressio.n using

// ternary o.perato.r

Int a = 2 > 5 ? 2 : 5;

Co.ut << a << endl;

Co.ut << "\nexecute expressio.n using "

<< "if else statement: ";

// execute expressio.n using if else

If ( 2 > 5)

Co.ut << "2";

Else

Co.ut << "5";

Return 0;

}

While lo.o.p demo.

#include <io.stream>

Using namespace std;

Int main() {

//initialize the co.unter, i

Int i = 1;

//print explanatio.n o.f pro.gram

Co.ut <<"this pro.gram will number and print 10 lines--";

//while i is less than 11, print "hello. Wo.rld"

While (i < 11) {

Co.ut <<"\n\t"<< i << " hello. Wo.rld";

I++; //unary co.unter i

}

Return 0;

}

Fo.r lo.o.p demo.

#include <io.stream>

Using namespace std;

Int main() {

//print explanatio.n o.f pro.gram

Co.ut <<"this pro.gram will number and print 10 lines--";

//while i is less than 11, print "hello. Wo.rld"

Fo.r (int i= 1; i < 11; i++ ) {

Co.ut <<"\n\t"<< i << " hello. Wo.rld";

}

Return 0;

}

Do. While lo.o.p demo. Exhibiting an exit co.ntro.lled lo.o.p

#include <io.stream>

Using namespace std;

Int main() {

//initialize the co.unter, i

Int i = 11;

//print explanatio.n o.f pro.gram

Co.ut <<"this pro.gram may o.r may no.t print o.ne \"hello. Wo.rld\"";

//while i is less than 11, print "hello. Wo.rld"

Do. {

Co.ut <<"\n\t"<< i << " hello. Wo.rld";

I++; //unary co.unter i

}

While (i < 11);

Return 0;

}

Nested if-else demo.

#include <io.stream>

Using namespace std;

Int main() {

Co.ut << "this pro.gram will go. Thro.ugh a sequential"

<<"\nlist o.f numbers 2 thro.ugh 4 and pick the "

<<"\ngreatest no.ne using a nested if-else "

<<"\nstatement."

<<"\ngreatest number:\n\t";

If ( 2 > 3 )

Co.ut << "2";

Else if ( 3 > 4 )

Co.ut << "3";

Else

Co.ut << "4";

Return 0;

}

Nested if-else and nested ternary o.peratio.n co.mpariso.n

#include <io.stream>

Using namespace std;

Int main() {

Co.ut << "this pro.gram will go. Thro.ugh a sequential"

<<"\nlist o.f numbers 2 thro.ugh 4 and pick the "

<<"\ngreatest no.ne using two. Metho.ds:"

<<"\na nested if-else and a nested ternary o.perato.r"

<<"\n nested if-else greatest number:\n\t";

If ( 2 > 3 )

Co.ut << "2";

Else if ( 3 > 4 )

Co.ut << "3";

Else

Co.ut << "4";

Co.ut <<"\n nested ternary o.perato.r greatest number:\n\t";

Int a = 2 > 3 ? 2 : 3 > 4 ? 3 : 4;

Co.ut<<a;

Return 0;

}

Switch demo.

#include <io.stream>

Using namespace std;

Int main() {

//initialize variable

Int x = 2;

//print explanatio.n

Co.ut<< "this pro.gram prints a cho.ice given x.\n"

<<"\n variable x is equal to.: "<< x

<<"\n\t";

// pro.gram switch

Switch (x)

{

Case 1:

Co.ut << "cho.ice is 1";

Break;

Case 2:

Co.ut << "cho.ice is 2";

Break;

Case 3:

Co.ut << "cho.ice is 3";

Break;

Default:

Co.ut << "pro.gram exit";

Break;

}

Return 0;

}

Functio.n demo.

#include <io.stream>

Using namespace std;

// functio.n declaratio.n

Vo.id myfunctio.n();

// the main metho.d

Int main() {

Myfunctio.n(); // call the functio.n

Return 0;

}

// functio.n definitio.n

Vo.id myfunctio.n() {

Co.ut << "i just go.t executed!";

}

Functio.ns with parameter passing

#include <io.stream>

Using namespace std;

//declare functio.n

Int max(int x, int y);

//main

Int main() {

Int a = 10, b = 20;

// calling abo.ve functio.n to. Find max o.f 'a' and 'b'

Int m = max(a, b);

Co.ut << "m is " << m;

Return 0;

}

//define functio.n

Int max(int x, int y)

{

If (x > y)

Return x;

Else

Return y;

}

Pro.gram witho.ut functio.n o.verlo.ading

#include <io.stream>

Using namespace std;

Int plusfuncint(int x, int y) {

Return x + y;

}

Do.uble plusfuncdo.uble(do.uble x, do.uble y) {

Return x + y;

}

Int main() {

Int mynum1 = plusfuncint(8, 5);

Do.uble mynum2 = plusfuncdo.uble(4.3, 6.26);

Co.ut << "int: " << mynum1 << "\n";

Co.ut << "do.uble: " << mynum2;

Return 0;

}

Pro.gram functio.n o.verlo.ading

#include <io.stream>

Using namespace std;

Int plusfuncint(int x, int y) {

Return x + y;

}

//change functio.n

Do.uble plusfuncint(do.uble x, do.uble y) {

Return x + y;

}

Int main() {

Int mynum1 = plusfuncint(8, 5);

//call functio.n in place o.f the o.ld o.ne

Do.uble mynum2 = plusfuncint(4.3, 6.26);

Co.ut << "int: " << mynum1 << "\n";

Co.ut << "do.uble: " << mynum2;

Return 0;

}

## References

[[ running c,c++ pro.grams in linux ] ubuntu 16.04 ( ubuntu tuto.rial fo.r beginners )](https://www.zotero.org/google-docs/?NpoF3N)[. (n.d.). Retrieved fro.m https://www.yo.utube.co.m/watch?V=a7ny-ro.1ht0](https://www.zotero.org/google-docs/?NpoF3N)

[15-1134.00—web develo.pers. (n.d.). Retrieved september 20, 2019, fro.m https://www.o.neto.nline.o.rg/link/summary/15-1134.00](https://www.zotero.org/google-docs/?NpoF3N)

[15-1199.03—web administrato.rs. (n.d.). Retrieved o.cto.ber 1, 2019, fro.m https://www.o.neto.nline.o.rg/link/summary/15-1199.03](https://www.zotero.org/google-docs/?NpoF3N)

[Agarwal, h. (2017a, january 13). Lo.o.ps in c and c++. Retrieved august 28, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/lo.o.ps-in-c-and-cpp/](https://www.zotero.org/google-docs/?NpoF3N)

[Agarwal, h. (2017b, may 16). Setting up c++ develo.pment enviro.nment. Retrieved august 13, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/setting-c-develo.pment-enviro.nment/](https://www.zotero.org/google-docs/?NpoF3N)

[Awasthi, s. (n.d.). Switch statement in c/c++—geeksfo.rgeeks. Retrieved o.cto.ber 3, 2019, fro.m https://www.geeksfo.rgeeks.o.rg/switch-statement-cc/](https://www.zotero.org/google-docs/?NpoF3N)

[Bluefish edito.r: features. (n.d.). Retrieved august 28, 2019, fro.m bluefish edito.r: features website: http://bluefish.o.peno.ffice.nl/features.html](https://www.zotero.org/google-docs/?NpoF3N)

[C++ | nested ternary o.perato.r. (2018, o.cto.ber 15). Retrieved o.cto.ber 3, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/c-nested-ternary-o.perato.r/](https://www.zotero.org/google-docs/?NpoF3N)

[C++ co.de [paste site]. (2015, december 5). Retrieved august 28, 2019, fro.m pastebin.co.m website: https://pastebin.co.m/f7kkzvyf](https://www.zotero.org/google-docs/?NpoF3N)

[C++ functio.n o.verlo.ading. (n.d.). Retrieved o.cto.ber 4, 2019, fro.m https://www.w3scho.o.ls.co.m/cpp/cpp_functio.n_o.verlo.ading.asp](https://www.zotero.org/google-docs/?NpoF3N)

[C++ functio.ns. (n.d.). Retrieved o.cto.ber 3, 2019, fro.m https://www.w3scho.o.ls.co.m/cpp/cpp_functio.ns.asp](https://www.zotero.org/google-docs/?NpoF3N)

[C++ o.perato.rs. (n.d.). Retrieved august 28, 2019, fro.m https://www.w3scho.o.ls.co.m/cpp/cpp_o.perato.rs.asp](https://www.zotero.org/google-docs/?NpoF3N)

[C++ variables. (n.d.). Retrieved august 28, 2019, fro.m https://www.w3scho.o.ls.co.m/cpp/cpp_variables.asp](https://www.zotero.org/google-docs/?NpoF3N)

[C++ while lo.o.p. (n.d.). Retrieved o.cto.ber 3, 2019, fro.m https://www.w3scho.o.ls.co.m/cpp/cpp_while_lo.o.p.asp](https://www.zotero.org/google-docs/?NpoF3N)

[Cento.s-faq | o.pen so.urce co.mmunity. (n.d.). Retrieved september 30, 2019, fro.m https://co.mmunity.redhat.co.m/cento.s-faq/](https://www.zotero.org/google-docs/?NpoF3N)

[Deb, r. (n.d.). What is the base-10 number system? Retrieved o.cto.ber 2, 2019, fro.m tho.ughtco. Website: https://www.tho.ughtco..co.m/definitio.n-o.f-base-10-2312365](https://www.zotero.org/google-docs/?NpoF3N)

[Escape sequences—cppreference.co.m. (n.d.). Retrieved o.cto.ber 1, 2019, fro.m https://en.cppreference.co.m/w/cpp/language/escape](https://www.zotero.org/google-docs/?NpoF3N)

[Gcc 7 release series—changes, new features, and fixes—gnu pro.ject—free so.ftware fo.undatio.n (fsf). (n.d.). Retrieved september 30, 2019, fro.m https://gcc.gnu.o.rg/gcc-7/changes.html](https://www.zotero.org/google-docs/?NpoF3N)

[Ho.w much data do.es yo.utube sto.re? - quo.ra. (n.d.). Retrieved o.cto.ber 4, 2019, fro.m https://www.quo.ra.co.m/ho.w-much-data-do.es-yo.utube-sto.re](https://www.zotero.org/google-docs/?NpoF3N)

[Input/o.utput manipulato.rs—cppreference.co.m. (n.d.). Retrieved o.cto.ber 1, 2019, fro.m https://en.cppreference.co.m/w/cpp/io./manip](https://www.zotero.org/google-docs/?NpoF3N)

[Intro.ductio.n. (n.d.). Retrieved august 28, 2019, fro.m https://web.stanfo.rd.edu/class/cs98si/slides/o.verview.html](https://www.zotero.org/google-docs/?NpoF3N)

[Jaggi, a. (2015a, july 28). O.perato.rs in c | set 1 (arithmetic o.perato.rs). Retrieved august 28, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/o.perato.rs-in-c-set-1-arithmetic-o.perato.rs/](https://www.zotero.org/google-docs/?NpoF3N)

[Jaggi, a. (2015b, july 29). O.perato.rs in c | set 2 (relatio.nal and lo.gical o.perato.rs). Retrieved august 28, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/o.perato.rs-in-c-set-2-relatio.nal-and-lo.gical-o.perato.rs/](https://www.zotero.org/google-docs/?NpoF3N)

[Killian, j. (2012). Understanding bitwise o.perato.rs. Retrieved august 28, 2019, fro.m https://co.de.tutsplus.co.m/articles/understanding-bitwise-o.perato.rs--active-11301](https://www.zotero.org/google-docs/?NpoF3N)

[Kito.wska, k. (2019, april 23). What is c++ used fo.r? 10 extremely po.werful apps written in c++ - blo.g. Retrieved august 28, 2019, fro.m bo.o.sthigh so.ftware develo.pment co.mpany website: https://bo.o.sthigh.co.m/10-extremely-po.werful-apps-written-in-cpp/](https://www.zotero.org/google-docs/?NpoF3N)

[Kumar, h. (2017, june 2). Unary o.perato.rs in c/c++. Retrieved august 28, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/unary-o.perato.rs-cc/](https://www.zotero.org/google-docs/?NpoF3N)

[List o.f game engines. (2019). In](https://www.zotero.org/google-docs/?NpoF3N) [wikipedia](https://www.zotero.org/google-docs/?NpoF3N)[. Retrieved fro.m https://en.wikipedia.o.rg/w/index.php?Title=list_o.f_game_engines&o.ldid=911528135](https://www.zotero.org/google-docs/?NpoF3N)

[Lithmee. (2018, o.cto.ber 18). What is the difference between machine co.de and assembly language. Retrieved september 11, 2019, fro.m pediaa.co.m website: https://pediaa.co.m/what-is-the-difference-between-machine-co.de-and-assembly-language/](https://www.zotero.org/google-docs/?NpoF3N)

[Manideep, p. (2017, o.cto.ber 26). Server side and client side pro.gramming. Retrieved september 30, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/server-side-client-side-pro.gramming/](https://www.zotero.org/google-docs/?NpoF3N)

[O.perato.rs-in-c.png (800×533). (n.d.). Retrieved august 28, 2019, fro.m https://www.geeksfo.rgeeks.o.rg/wp-co.ntent/uplo.ads/o.perato.rs-in-c.png](https://www.zotero.org/google-docs/?NpoF3N)

[O.rin, a. (n.d.). Behind the app: the sto.ry o.f no.tepad++ | lifehacker australia. Retrieved august 28, 2019, fro.m https://www.lifehacker.co.m.au/2015/06/behind-the-app-the-sto.ry-o.f-no.tepad/](https://www.zotero.org/google-docs/?NpoF3N)

[Patel, y. (2014).](https://www.zotero.org/google-docs/?NpoF3N) [Ho.w do. I install gcc o.n ubuntu linux](https://www.zotero.org/google-docs/?NpoF3N)[. Retrieved fro.m https://www.yo.utube.co.m/watch?V=co.tkjrewaz0](https://www.zotero.org/google-docs/?NpoF3N)

[Patel, y. (2017).](https://www.zotero.org/google-docs/?NpoF3N) [Ho.w to. Create first c++ hello. Wo.rld pro.ject using xco.de mac o.s x](https://www.zotero.org/google-docs/?NpoF3N)[. Retrieved fro.m https://www.yo.utube.co.m/watch?Time_co.ntinue=21&v=-h_eyiqbnda](https://www.zotero.org/google-docs/?NpoF3N)

[Peshev, m. (2017, no.vember 3). As a pro.grammer, is it impo.rtant to. Have a github pro.file? - quo.ra. Retrieved september 11, 2019, fro.m https://www.quo.ra.co.m/as-a-pro.grammer-is-it-impo.rtant-to.-have-a-github-pro.file](https://www.zotero.org/google-docs/?NpoF3N)

[Prabhu, r. (2018, december 11). Assignment o.perato.rs in c/c++. Retrieved august 28, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/assignment-o.perato.rs-in-c-c/](https://www.zotero.org/google-docs/?NpoF3N)

[Pro.gramming so.ftware and the ide - revisio.n 1—gcse co.mputer science. (n.d.). Retrieved september 11, 2019, fro.m bbc bitesize website: https://www.bbc.co..uk/bitesize/guides/zgmpr82/revisio.n/1](https://www.zotero.org/google-docs/?NpoF3N)

[Pytho.n vs c++—find o.ut the 9 impo.rtant differences. (2018, july 1). Retrieved september 30, 2019, fro.m educba website: https://www.educba.co.m/pytho.n-vs-c-plus-plus/](https://www.zotero.org/google-docs/?NpoF3N)

[What are scripts? - definitio.n fro.m techo.pedia. (n.d.). Retrieved o.cto.ber 3, 2019, fro.m techo.pedia.co.m website: https://www.techo.pedia.co.m/definitio.n/10324/scripts](https://www.zotero.org/google-docs/?NpoF3N)

[What is a so.ftware develo.pment kit (sdk)? - definitio.n fro.m techo.pedia. (n.d.). Retrieved september 29, 2019, fro.m techo.pedia.co.m website: https://www.techo.pedia.co.m/definitio.n/3878/so.ftware-develo.pment-kit-sdk](https://www.zotero.org/google-docs/?NpoF3N)

[What is debugging? - definitio.n fro.m techo.pedia. (n.d.). Retrieved september 28, 2019, fro.m techo.pedia.co.m website: https://www.techo.pedia.co.m/definitio.n/16373/debugging](https://www.zotero.org/google-docs/?NpoF3N)

[What’s new in xco.de 9. (n.d.). Retrieved september 28, 2019, fro.m https://develo.per.apple.co.m/library/archive/do.cumentatio.n/develo.perto.o.ls/co.nceptual/whatsnewxco.de/xco.de_9/xco.de_9.html](https://www.zotero.org/google-docs/?NpoF3N)

[Wieder, p., butler, j. M., theilmann, w., & yahyapo.ur, r. (2011).](https://www.zotero.org/google-docs/?NpoF3N) [Service level agreements fo.r clo.ud co.mputing](https://www.zotero.org/google-docs/?NpoF3N)[. Springer science & business media.](https://www.zotero.org/google-docs/?NpoF3N)

[Writing first c++ pro.gram: hello. Wo.rld example. (2017, may 17). Retrieved o.cto.ber 1, 2019, fro.m geeksfo.rgeeks website: https://www.geeksfo.rgeeks.o.rg/writing-first-c-pro.gram-hello.-wo.rld-example/](https://www.zotero.org/google-docs/?NpoF3N)

[‎xco.de. (n.d.). Retrieved september 29, 2019, fro.m mac app sto.re website: https://apps.apple.co.m/us/app/xco.de/id497799835?Mt=12](https://www.zotero.org/google-docs/?NpoF3N)