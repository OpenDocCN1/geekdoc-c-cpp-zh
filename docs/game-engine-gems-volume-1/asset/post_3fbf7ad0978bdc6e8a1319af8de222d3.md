
## 1.10 Demands on the Maintainers

Programmers are busy, expensive resources. Middleware that requires a lot of effort and attention to integrate well with your flavor of build system is going to be kicked to the curb very quickly. Ideally, you simply add a library to the build process, #include a header file, and call a few functions. Ta-da! It's integrated.

Sometimes, the middleware is more invasive, and requires various #define macros to be set to configure it. Or perhaps it needs to be integrated directly into your project and compiled with your game. Additionally, some middleware has external dependencies that must be present for it to compile. Worse still, it may require introducing a new tool into the build process that may not work well with the build system. Turnkey systems are clearly preferable. I look for middleware that comes with GCC and Microsoft Visual Studio project files, but with extremely basic project configurations. This proves that the compilers I care about can handle the code, and that I can throw away the project files and integrate them my own way after an initial build using the provided project file.

## 1.11 Source Code Availability

Eventually, you may need to debug into the source code of a middleware product you plan to integrate. If it is a proprietary, closed-source product without a source code option at a reasonable price, look for alternatives. While certain "industry secret" parts of libraries may be binary-only, vendors know that source code is expected and will often provide it with a license. Those who don't provide source typically claim that their customer support obviates that need. While this may be true, the moment there's an issue that customer support can't solve, but source code could, is the moment we start searching for a replacement. Again, a big reason for using middleware is that it's proven and stable, so source code should not really be necessary. But the availability is still important should the need arise.

## 1.12 Quality of Source Code

Having source code does not always mean you have the ability to make meaningful changes. The best middleware has excellent documentation that is auto-generated from source on every new code drop. It will have a familiar and consistent bracing scheme, some kind of naming convention for functions and variables, and ideally will live inside a brief namespace.

Take a moment to peruse the important header files. Inspect for `#define` macros for language keywords or common functions such as `new`, `min`, and `max`, or in fact any macro that escapes the scope of the header which could cause issues elsewhere. Use an archive-inspection utility such as `dumpbin` (in Windows) or `nm` (in Linux) to verify that the only exported symbols the middleware library defines are in a consistent namespace to avoid conflicts with other libraries or your own code.

Questionable middleware will be littered with `#pragma` statements, will disable errors, will reduce the warning level, etc. Scrutinize this heavily. These statements being in header files can harm the quality of your code and may cause some files to stop compiling simply by including them.

## 1.13 Platform Portability

Certain kinds of middleware are likely to be platform independent, but even if you have the source code there may be lurking byte ordering (endianness) issues. Inspect the file and network stream handling for endian swapping code or perhaps different asset building tools per-platform that sets up data into native formats.

Multithreading is very common in games today. Some middleware libraries predate this shift. Determine how thread locking is handled, if the code is thread-safe, and whether the thread controls are easy to override with a different platform's interface. Be aware that any library that does nothing with threading is, by its very nature, likely to be unsafe to use in a threaded environment. Factor in time for making the library thread-safe, or at least limiting its use to a single, specific thread at all times.

Also consider whether your game may be ported to a less-capable hardware platform at some point. If it might, determine what features are unique to this middleware offering that would make porting to a different library particularly difficult if this library does not exist for lower-end platforms.

## 1.14 Licensing Requirements

I am not a lawyer, and this is not legal advice. Consult a lawyer of your own to answer specific questions, and read every license personally. Also note, most publishers and even some hardware manufacturers have strict regulations about what open source licenses are allowed in products you develop. Clear all open source licenses through their legal departments before integrating one. What follows are my informed layman's opinions.

Every open source license that I know of springs into action as the result of distributing software. What this means is, as long as you do not distribute the software outside your company, you can use whatever you like for applications used internally. Feel free to use any open source code in your internally-facing server technology or tools, but do not plan to distribute those programs.

Public domain code is completely harmless. Once you copy the code to your hard drive, you own it, and every modification you put into it is yours to keep. You may of course change the license to something else, release it back to the public domain, or keep it secret. It's yours.

The MIT, Zlib, etc., licenses appear to more or less disavow any responsibility for how you use their software. They do not require anything except a credit clause and that certain notices remain in the code. This is not a restrictive license with respect to retail use.

The LGPL license has some stipulations that require distribution of the source of the library (and possibly parts of your own application). Read this carefully before using in retail products.

The GPL license and many other similar licenses require complete code release on distribution if you integrate them into your products.

Frequently, commercial middleware licenses will require credit attributions, splash screens, an intro movie, etc. Be careful to adhere to these, and give credit where it's due—middleware authors helped make your game happen.

## 1.15 Cost

Every game has a different budget for middleware. Expect prices to vary widely from $100 to $750,000, depending on what kind of product you're looking at. Great middleware demands professional attention to detail, and when using a library professionally, good support is important (but often costs more depending on your level of need).

When looking for a library that costs money, consider whether the cost is per-seat, per-game, per-platform, or if it has a maintenance license such as per-annum. Many middleware companies have special rates for digital download titles versus retail titles. Also, be willing to call up the account manager at your chosen middleware shop and try to sweet talk them into a discount. You might be surprised at how flexible they are if this is your first title with them—they know very well that middleware tends to become entrenched and expensive to remove, so it's good for them to get you hooked on their product. Try to work out multiple project deals, if you have that kind of leverage.

Some libraries, such as Zlib, have evolved to the point where there is plenty of support online in forums and sample code, and the number of bugs is approaching zero. When libraries calcify, the fact that they are free is not an issue. However, open source libraries are not free in general unless your time has no value. Take an estimate of how many man-weeks it will take to implement the various missing features listed above, assign a price to those man-weeks and compare that with the cost of the middleware library. If they're even close to parity, go with commercial middleware, simply because it's established, tested, supported, and best of all, you will free up programmers to work on actual game features instead of patching up someone else's pet project.
