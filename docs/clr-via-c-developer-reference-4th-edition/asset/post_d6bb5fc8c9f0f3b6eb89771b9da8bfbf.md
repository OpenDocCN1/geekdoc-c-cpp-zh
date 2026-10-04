
# FxCopCmd.exe.

FieldInfo objects, converting to
RuntimeFieldHandle, 609
fields backing, 230

in boxed value types, changing, 136
defined, 24, 151, 177
defining, 178
defining, without initialization, 184
encapsulating, 228
initializing, 182, 187
initializing, with convenient syntax, 183
inline initialization, 179
private, 168, 228, 231

Dispose method in, 535
exceptions thrown by, 457
liberal use of, 478
try blocks and, 457
FirstChanceException event, 573
fixed statement, 548
Flags attribute, 368
FlagsAttribute class, 430
Flatten method, 703
float type, 112
FlushAsync method, 742
For method (Parallel class), 713, 714
ForAll method, 718
forcing garbage collection, 522, 539
ForEach method (Parallel class), 713, 714
foreground threads
forcing, 679
vs. background, 688
Format method, 344, 364
overloading, 344
vs.ToString method, 364
FormatterConverter type, 628
Formatter type, 623, 628
Formatting, string, 346
Forms namespace, Timer class, 723
Framework Class Library. See FCL (Framework
Class Library)
asynchronous functions in, 742
types. See FCL types
framework projections, 645, 649
finalachable queue, 543
finalization list and, 544
naming of, 544
Free method, 548
friend assemblies, 154
modules in, 156
friendly names, 563
FromAsync method, 743
FromBase6String method, 356
FromCurrentSynchronizationContext
method, 711
Func delegate, 279, 408
functions, callback. See callback functions
FxCopCmd.exe, 480

FieldSetter method, 566
file extensions
for WinRT components, 644
.wmdn, WinRT, 645
file names, versioning, with, 66
FileAttributes type, 367
FileDef table, 47, 181
FileNotException exception, 384
FileStream
class, 532
I/O operations, 728
objects, asynchronous and synchronous
type, 525, 537
finalization, 525, 542
garbage collection and, 544
list, 542
finalachable queue and, 544
Finalize method, 525, 526, 542
CLR threaded dedicated to, 344
inherited, 543
memory leaks and, 526
overriding, 479
similarity to destructor, 526
SystemObject, 92
finally blocks, 455, 456. See also catch calls,
try blocks
as callback methods, 497
constrained execution regions and, 475

# GAC (global assembly cache)

# G

+ GAC (global assembly cache), 72
installing into, 72
permissions required for, 73
uninstalling assemblies from, 73
GACutil.exe, 72
Windows install switch, 73
garbage collection, 507
algorithm, 507
asynchronous I/O operations and, 731
for bitmaps, 538
byte array method and, 548
Collect method, 523
compacting phase, 509
concurrent vs. non-concurrent method, 521
debugging and, 510
dependency issues, 537
Dispose method, 512
vs. Dispose method, 535
finalized objects, 544
Finalize method and, 526
forcing, 529
generational, 513
generational, assumptions made by, 514
generations and, 513
handle tables, 545, 547
idle threads and, 517
large objects and, 519
latency methods, 522
lease managers, 567
marking phase, 508
memory building and, 517
memory compaction, 521
memory usage, monitoring., 524
monitoring, 524
native resources and, 538
notifications for, 518, 523
object lifetime and, 510
object lifetime, controlling manually, 545
OutOfMemory exceptions, 510
performance goals, 515
pinnning objects, 548

+ reference counting algorithms, 508
corrected objects, 544
roots and, 509
server method, 520
symbols for, 522
threads and, 673
Timer objects and, 721
triggers for, 519
for writing native resources, 525
on loaded AppDomains, 571
weak references and, 550
workstation method, 520
GCCollection enumerated type, 523
GCHandle type, 545
explicit, 548
GCHandle type, 546
GCLatencyMode property, 521
GCNotification class, 518
GCSettings class, 521
GCWatch method, 551
generation, 1, 2, 513, 514, 516
grow of, 516
promotions to, 515
generic
arguments, limiting types, 285
collection classes, 125, 270
contravariant and covariant type
parameters, 281
delegates, 278, 407
interfaces, 277, 278, 297, 303
list algorithm, 266
namespace, 313
vs. non-generic versions, 304
type identity, 275
type parameters, 305
generic methods, 265, 281
sample of, 282
overriding, 286
static, 270
type inference and, 283
generic type variables
as operands, 292
casting, 290

# GetWindowsRuntimeBuffer method

comparing to each other, 292
comparing with null, 291
setting to default value, 291
generic types, 265
constructing, 596
defining, 273
inheritance and, 274
out and ref parameters, 282
parameters, 269
type arguments, 266
type objects for, 272
using directive and, 276
generics
backwards compatibility, 270
benefits of, 267
constrains, 267
explicit declarations, 281
in and ref keywords, 281
f FCL, 270
infrastructure of, 271
interface and, 275
members of, 277
overview of, 278
performance with, 279
variability, 268
variance and, 280
GetAssemblyName, 269
GetAsync method, 291
AvailableThreads, 291
BaseException, 272
ByteArray method, 292
GetCharCount, 272
Chars method, 273
CustomAttribute, 274
Decoder method, 274
Domain method, 275
Encoding method, 276
Enumerator, 277
Enum method, 277
EnumValues, 278
Format method, 297
GenericArguments, 303
HashCode method, 281
Invocation method, 281
Lower method, 281
MinValue method, 282
MaxValue method, 282
NumericValue, 282
Object method, 283
Real method, 283
Runtime method, 285
String method, 285
Stream method, 286
Text method, 286
Unicode method, 286
UnderlyingType, 286

# GAC (global assembly cache)

# G

+ GAC (global assembly cache), 72
installing into, 72
permissions required for, 73
uninstalling assemblies from, 73
GACutil.exe, 72
Windows install switch, 73
garbage collection, 507
algorithm, 507
asynchronous I/O operations and, 731
for bitmaps, 538
byte array method and, 548
Collect method, 523
compacting phase, 509
concurrent vs. non-concurrent method, 521
debugging and, 510
dependency issues, 537
Dispose method, 512
vs. Dispose method, 535
finalized objects, 544
Finalize method and, 526
forcing, 529
generational, 513
generational, assumptions made by, 514
generations and, 513
handle tables, 545, 547
idle threads and, 517
large objects and, 519
latency methods, 522
lease managers, 567
marking phase, 508
memory building and, 517
memory compaction, 521
memory usage, monitoring., 524
monitoring, 524
native resources and, 538
notifications for, 518, 523
object lifetime and, 510
object lifetime, controlling manually, 545
OutOfMemory exceptions, 510
performance goals, 515
pinnning objects, 548

+ reference counting algorithms, 508
corrected objects, 544
roots and, 509
server method, 520
symbols for, 522
threads and, 673
Timer objects and, 721
triggers for, 519
for writing native resources, 525
on loaded AppDomains, 571
weak references and, 550
workstation method, 520
GCCollection enumerated type, 523
GCHandle type, 545
explicit, 548
GCHandle type, 546
GCLatencyMode property, 521
GCNotification class, 518
GCSettings class, 521
GCWatch method, 551
generation, 1, 2, 513, 514, 516
grow of, 516
promotions to, 515
generic
arguments, limiting types, 285
collection classes, 125, 270
contravariant and covariant type
parameters, 281
delegates, 278, 407
interfaces, 277, 278, 297, 303
list algorithm, 266
namespace, 313
vs. non-generic versions, 304
type identity, 275
type parameters, 305
generic methods, 265, 281
sample of, 282
overriding, 286
static, 270
type inference and, 283
generic type variables
as operands, 292
casting, 290

# GetWindowsRuntimeBuffer method

comparing to each other, 292
comparing with null, 291
setting to default value, 291
generic types, 265
constructing, 596
defining, 273
inheritance and, 274
out and ref parameters, 282
parameters, 269
type arguments, 266
type objects for, 272
using directive and, 276
generics
backwards compatibility, 270
benefits of, 267
constrains, 267
explicit declarations, 281
in and ref keywords, 281
f FCL, 270
infrastructure of, 271
interface and, 275
members of, 277
overview of, 278
performance with, 279
variability, 268
variance and, 280
GetAssemblyName, 269
GetAsync method, 291
AvailableThreads, 291
BaseException, 272
ByteArray method, 292
GetCharCount, 272
Chars method, 273
CustomAttribute, 274
Decoder method, 274
Domain method, 275
Encoding method, 276
Enumerator, 277
Enum method, 277
EnumValues, 278
Format method, 297
GenericArguments, 303
HashCode method, 281
Invocation method, 281
Lower method, 281
MinValue method, 282
MaxValue method, 282
NumericValue, 282
Object method, 283
Real method, 283
Runtime method, 285
String method, 285
Stream method, 286
Text method, 286
Unicode method, 286
UnderlyingType, 286

# GAC (global assembly cache)

# G

+ GAC (global assembly cache), 72
installing into, 72
permissions required for, 73
uninstalling assemblies from, 73
GACutil.exe, 72
Windows install switch, 73
garbage collection, 507
algorithm, 507
asynchronous I/O operations and, 731
for bitmaps, 538
byte array method and, 548
Collect method, 523
compacting phase, 509
concurrent vs. non-concurrent method, 521
debugging and, 510
dependency issues, 537
Dispose method, 512
vs. Dispose method, 535
finalized objects, 544
Finalize method and, 526
forcing, 529
generational, 513
generational, assumptions made by, 514
generations and, 513
handle tables, 545, 547
idle threads and, 517
large objects and, 519
latency methods, 522
lease managers, 567
marking phase, 508
memory building and, 517
memory compaction, 521
memory usage, monitoring., 524
monitoring, 524
native resources and, 538
notifications for, 518, 523
object lifetime and, 510
object lifetime, controlling manually, 545
OutOfMemory exceptions, 510
performance goals, 515
pinnning objects, 548

+ reference counting algorithms, 508
corrected objects, 544
roots and, 509
server method, 520
symbols for, 522
threads and, 673
Timer objects and, 721
triggers for, 519
for writing native resources, 525
on loaded AppDomains, 571
weak references and, 550
workstation method, 520
GCCollection enumerated type, 523
GCHandle type, 545
explicit, 548
GCHandle type, 546
GCLatencyMode property, 521
GCNotification class, 518
GCSettings class, 521
GCWatch method, 551
generation, 1, 2, 513, 514, 516
grow of, 516
promotions to, 515
generic
arguments, limiting types, 285
collection classes, 125, 270
contravariant and covariant type
parameters, 281
delegates, 278, 407
interfaces, 277, 278, 297, 303
list algorithm, 266
namespace, 313
vs. non-generic versions, 304
type identity, 275
type parameters, 305
generic methods, 265, 281
sample of, 282
overriding, 286
static, 270
type inference and, 283
generic type variables
as operands, 292
casting, 290

# GetWindowsRuntimeBuffer method

comparing to each other, 292
comparing with null, 291
setting to default value, 291
generic types, 265
constructing, 596
defining, 273
inheritance and, 274
out and ref parameters, 282
parameters, 269
type arguments, 266
type objects for, 272
using directive and, 276
generics
backwards compatibility, 270
benefits of, 267
constrains, 267
explicit declarations, 281
in and ref keywords, 281
f FCL, 270
infrastructure of, 271
interface and, 275
members of, 277
overview of, 278
performance with, 279
variability, 268
variance and, 280
GetAssemblyName, 269
GetAsync method, 291
AvailableThreads, 291
BaseException, 272
ByteArray method, 292
GetCharCount, 272
Chars method, 273
CustomAttribute, 274
Decoder method, 274
Domain method, 275
Encoding method, 276
Enumerator, 277
Enum method, 277
EnumValues, 278
Format method, 297
GenericArguments, 303
HashCode method, 281
Invocation method, 281
Lower method, 281
MinValue method, 282
MaxValue method, 282
NumericValue, 282
Object method, 283
Real method, 283
Runtime method, 285
String method, 285
Stream method, 286
Text method, 286
Unicode method, 286
UnderlyingType, 286

# GAC (global assembly cache)

# G

+ GAC (global assembly cache), 72
installing into, 72
permissions required for, 73
uninstalling assemblies from, 73
GACutil.exe, 72
Windows install switch, 73
garbage collection, 507
algorithm, 507
asynchronous I/O operations and, 731
for bitmaps, 538
byte array method and, 548
Collect method, 523
compacting phase, 509
concurrent vs. non-concurrent method, 521
debugging and, 510
dependency issues, 537
Dispose method, 512
vs. Dispose method, 535
finalized objects, 544
Finalize method and, 526
forcing, 529
generational, 513
generational, assumptions made by, 514
generations and, 513
handle tables, 545, 547
idle threads and, 517
large objects and, 519
latency methods, 522
lease managers, 567
marking phase, 508
memory building and, 517
memory compaction, 521
memory usage, monitoring., 524
monitoring, 524
native resources and, 538
notifications for, 518, 523
object lifetime and, 510
object lifetime, controlling manually, 545
OutOfMemory exceptions, 510
performance goals, 515
pinnning objects, 548

+ reference counting algorithms, 508
corrected objects, 544
roots and, 509
server method, 520
symbols for, 522
threads and, 673
Timer objects and, 721
triggers for, 519
for writing native resources, 525
on loaded AppDomains, 571
weak references and, 550
workstation method, 520
GCCollection enumerated type, 523
GCHandle type, 545
explicit, 548
GCHandle type, 546
GCLatencyMode property, 521
GCNotification class, 518
GCSettings class, 521
GCWatch method, 551
generation, 1, 2, 513, 514, 516
grow of, 516
promotions to, 515
generic
arguments, limiting types, 285
collection classes, 125, 270
contravariant and covariant type
parameters, 281
delegates, 278, 407
interfaces, 277, 278, 297, 303
list algorithm, 266
namespace, 313
vs. non-generic versions, 304
type identity, 275
type parameters, 305
generic methods, 265, 281
sample of, 282
overriding, 286
static, 270
type inference and, 283
generic type variables
as operands, 292
casting, 290

# GetWindowsRuntimeBuffer method

comparing to each other, 292
comparing with null, 291
setting to default value, 291
generic types, 265
constructing, 596
defining, 273
inheritance and, 274
out and ref parameters, 282
parameters, 269
type arguments, 266
type objects for, 272
using directive and, 276
generics
backwards compatibility, 270
benefits of, 267
constrains, 267
explicit declarations, 281
in and ref keywords, 281
f FCL, 270
infrastructure of, 271
interface and, 275
members of, 277
overview of, 278
performance with, 279
variability, 268
variance and, 280
GetAssemblyName, 269
GetAsync method, 291
AvailableThreads, 291
BaseException, 272
ByteArray method, 292
GetCharCount, 272
Chars method, 273
CustomAttribute, 274
Decoder method, 274
Domain method, 275
Encoding method, 276
Enumerator, 277
Enum method, 277
EnumValues, 278
Format method, 297
GenericArguments, 303
HashCode method, 281
Invocation method, 281
Lower method, 281
MinValue method, 282
MaxValue method, 282
NumericValue, 282
Object method, 283
Real method, 283
Runtime method, 285
String method, 285
Stream method, 286
Text method, 286
Unicode method, 286
UnderlyingType, 286

# GAC (global assembly cache)

# G

+ GAC (global assembly cache), 72
installing into, 72
permissions required for, 73
uninstalling assemblies from, 73
GACutil.exe, 72
Windows install switch, 73
garbage collection, 507
algorithm, 507
asynchronous I/O operations and, 731
for bitmaps, 538
byte array method and, 548
Collect method, 523
compacting phase, 509
concurrent vs. non-concurrent method, 521
debugging and, 510
dependency issues, 537
Dispose method, 512
vs. Dispose method, 535
finalized objects, 544
Finalize method and, 526
forcing, 529
generational, 513
generational, assumptions made by, 514
generations and, 513
handle tables, 545, 547
idle threads and, 517
large objects and, 519
latency methods, 522
lease managers, 567
marking phase, 508
memory building and, 517
memory compaction, 521
memory usage, monitoring., 524
monitoring, 524
native resources and, 538
notifications for, 518, 523
object lifetime and, 510
object lifetime, controlling manually, 545
OutOfMemory exceptions, 510
performance goals, 515
pinnning objects, 548

+ reference counting algorithms, 508
corrected objects, 544
roots and, 509
server method, 520
symbols for, 522
threads and, 673
Timer objects and, 721
triggers for, 519
for writing native resources, 525
on loaded AppDomains, 571
weak references and, 550
workstation method, 520
GCCollection enumerated type, 523
GCHandle type, 545
explicit, 548
GCHandle type, 546
GCLatencyMode property, 521
GCNotification class, 518
GCSettings class, 521
GCWatch method, 551
generation, 1, 2, 513, 514, 516
grow of, 516
promotions to, 515
generic
arguments, limiting types, 285
collection classes, 125, 270
contravariant and covariant type
parameters, 281
delegates, 278, 407
interfaces, 277, 278, 297, 303
list algorithm, 266
namespace, 313
vs. non-generic versions, 304
type identity, 275
type parameters, 305
generic methods, 265, 281
sample of, 282
overriding, 286
static, 270
type inference and, 283
generic type variables
as operands, 292
casting, 290

# GetWindowsRuntimeBuffer method

comparing to each other, 292
comparing with null, 291
setting to default value, 291
generic types, 265
constructing, 596
defining, 273
inheritance and, 274
out and ref parameters, 282
parameters, 269
type arguments, 266
type objects for, 272
using directive and, 276
generics
backwards compatibility, 270
benefits of, 267
constrains, 267
explicit declarations, 281
in and ref keywords, 281
f FCL, 270
infrastructure of, 271
interface and, 275
members of, 277
overview of, 278
performance with, 279
variability, 268
variance and, 280
GetAssemblyName, 269
GetAsync method, 291
AvailableThreads, 291
BaseException, 272
ByteArray method, 292
GetCharCount, 272
Chars method, 273
CustomAttribute, 274
Decoder method, 274
Domain method, 275
Encoding method, 276
Enumerator, 277
Enum method, 277
EnumValues, 278
Format method, 297
GenericArguments, 303
HashCode method, 281
Invocation method, 281
Lower method, 281
MinValue method, 282
MaxValue method, 282
NumericValue, 282
Object method, 283
Real method, 283
Runtime method, 285
String method, 285
Stream method, 286
Text method, 286
Unicode method, 286
UnderlyingType, 286
