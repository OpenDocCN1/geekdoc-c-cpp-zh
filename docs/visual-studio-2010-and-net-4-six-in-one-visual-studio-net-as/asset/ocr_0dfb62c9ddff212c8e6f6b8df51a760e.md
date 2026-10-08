distributed, multi-tier enterprise applications, as well as the capability to create COMs-middleware components, thick-client, and web UI. Figure 21-2 shows the project types developers could use with Visual Basic 6.0 out-of-the-box.

To emphasize this new focus of Visual Basic, in addition to the Standard and Professional editions, 6.0 had an Enterprise edition—which was a sort of alternative for the Java language and platform born in 1995.

Visual Basic 6.0 is long-lived. Even today, there are business applications (with many COM+ components) developed with Visual Basic 6.0, which are still being used in production. Microsoft supported this application until March 2008, but the Enterprise edition can still be downloaded from MSDN.

![](bbox=[0.51, 0.07, 0.93, 0.29])

# VISUAL BASIC IN THE .NET FRAMEWORK

After the release of Visual Basic 6.0, a long time passed before a new release of the language was announced. Microsoft was working on its Common Object Run-time platform that was announced—the .NET Framework in July 2000 at Professional Developers Conference (PDC) held in Orlando, Florida. That PDC focused on the .NET Framework, and it spotted the new C# programming language. But it was clear that Visual Basic had a large camp of developers that Microsoft couldn't ignore.

When Visual Basic 1.0 was released as part of Visual Studio.NET in February 2002, the new Visual Basic 7.0—called Visual Basic.NET—was born. This change for the programming language was at least as significant as the step from unstructured to structured BASIC in the mid-1980s.

# Design Goals and Debates

The most important goal of the Visual Basic language was to transform it to a real object-oriented (OO) language free from common programming frameworks. While Microsoft communicated pre-.NET versions as OO, only the encapsulation principle was fully implemented by Microsoft, while inheritance and polymorphism were very poor—object classes could implement COM interfaces.

The Common Type System (CTS) of the .NET Framework dictated the feature language designers had to take into account. The real question was not CTS features to implement, but rather ones could be omitted from the language. In addition to this paradigm shift, reasonable design goal was to change the language syntax and semantics with the best achievable level of backward compatibility.