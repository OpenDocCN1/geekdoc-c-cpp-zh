
# 892    constructors

construction schedules, estimating,
  continued
  overview, 671
  planning estimation time, 671
  reduction of scope, 676
  reestimating, 672
  requirements specification, 672
  resources for, 677
  teams, expanding, 676
constructors
  deep vs. shallow copies, 151–152
  exceptions with, 199
  guidelines for, 151–152
  initializing data members, 151
  refactoring, 577
  singleton property, enforcing, 151
container classes, 310
containment, 88, 143
continuation lines, 754–758
continue statements, 379, 380, 381
continuous integration, 706
control structures
  boolean expressions in. See boolean expressions
  case. See case statements
  checklists, 459, 773, 780
  commenting, 804–805, 817
  complexity, contributions to, 456–459
  compound statements, 443
  conditional flow. See conditional statements
  continuation lines in, 757
  data types, relationship to, 254–255
  documentation, 780
  double indented begin-end pairs, 746–747
  gotos. See goto statements
  if statements. See if statements
  iteration, 255, 456
  key points, 460
  layout styles, 745–752
  loops. See loops
  multiple returns from routines, 391–393
  null statements, 444–445
  recursive. See recursion
  reliability correlated with complexity, 457
  returns as. See return statements
  selective data with, 254
  sequential data with, 254
  structured programming, 454–455

unindented begin-end pairs, 746
unusual, overview of, 408
conventions, coding
  benefits of, 844–845
  checklist, 69
  formatting. See layout
  hazards, avoiding with, 844
  predictability benefit, 844
converting data types, 635
cooperation skills, importance of,
  correctness, 197, 463
costs. See also performance tuning
  change estimates, 666
  collaboration benefits, 480–481
  debugging, time consumed by, 474–475
  defects contributing to, 519–520
  detection of defects, 472
  error-prone routines, 518
  estimating, 658, 828
  fixing of defects, 472–473, 519
  General Principle of Software Quality, 474–475, 522
  pair programming vs. inspections, 480–481
  resources on, 658
counted loops. See for loops
coupling
  base classes to derived classes, 143
  classes, too tightly, 142–143
  design considerations, 100–102
  flexibility of, 100–101
  goals of, 100
  loose, 80, 100–102
  object-parameter type, 101
  semantic type, 102
  simple-data-parameter type, 101
  simple-object type, 101
  size of, 100
  visibility of, 100
coverage
  monitoring tools, 526
  structured basis testing, 505–509
CRC (Class, Responsibility, Collaboration) cards, 118
creativity, importance of, 829, 857
cross-reference tools, 713
curiosity, role in character, 822–825
Currency data types, 297
customization, building metaphor for, 18

# D

daily build and smoke tests
  automation of, 704
  benefits of, 702
  broken builds, 703, 705
  build groups, 704
  checklist, 707
  defined, 702
  diagnosis benefit, 702
  holding area for additions, 704–705
  importance of, 706
  morning releases, 705
  pressure, 706
  pretest requirement, 704
  revisions, 704
  smoke tests, 703
  unsurfaced work, 702
data
  architecture prerequisites, 46
  bad classes, testing for, 514–515
  change, identifying areas of, 99
  code tuning. See data transformations for code tuning
  combined states, 509–510
  defined state, 509–510
  defined-used paths, testing, 510–512
  design, 46
  entered state, 509
  exited state, 509
  good classes, testing, 515–516
  killed state, 509–510
  legacy, compatibility with, 516
  nominal case errors, 515
  test, generators for, 524–525
  types. See data types
  used state, 509–510
data dictionaries, 715
data flow testing, 509–512
data literacy test, 238–239
data recorder tools, 526
data structures. See structures
data transformations for code tuning
  array dimension minimization, 625–626
  array reference minimization, 626–627
  caching data, 628–629
  floating point to integers, 625
  indexing data, 627–628
  purpose of, 624

data types
"a" prefix convention, 272
abstract data types. See ADTs
arrays. See arrays
BCD, 297
boolean. See boolean variables
change, identifying areas of, 99
characters. See character data types
checklist, 316–318
complex. See structures
control structures, relationship to, 254–255
creating. See type creation
Currency, 297
definitions, 278
enumerated types. See enumerated types
floating-point. See floating-point data types
integers. See integer data types
iterative data, 255
key points for, 318
naming, 273, 277, 278
numeric. See numeric data types
overloaded primitives, 567
pointers. See pointers
refactoring to classes, 567, 572
resources on, 239
selective data, 254
sequential data, 254
strings. See string data types
structures. See structures
_L_ prefix convention, 272
user-defined. See type creation
variables of, differentiating from, 272–273
databases
performance issues, 601
SQL, 65
subsystem design, 85
data-level refactoring, 571–572, 577
days-in-month, determining, 413–414
deallocation
goto statements for, 399
pointers, of, 326, 330, 332
Debug.Assert statements, 191–193
debugging
aids to. See debugging aids
binary searches of code, 546
blindness, sources of, 554–555
breakpoints, 558
breaks, taking, 548
brute-force, 548–549
changes, recent, 547
checklist, 559–561
comments, misplaced, 550
common defects lists, 547
compilers as tools for, 549, 557
confessional debugging, 547–548
costs of, 29–30, 474–475
debugger tools, 526–527, 545, 556–559, 719. See also debugging aids
defects as opportunities, 537–538
defined, 535
Diff tool, 556
execution profilers for, 557–558
expanding suspicious regions, 547
experience of programmers, effects of, 537
finding defects, 540, 559–560
fixing defects, 550–554
guessing, 539
history of, 535–536
hypothesis testing, 543–544, 546
incremental approach, 547
ineffective approach to, 539–540
key points, 562
line numbers from compilers, 549
lint tool, 557
listing possibilities, 546
locating error sources, 543–544
logic checking tools, 557
multiple compiler messages, 550
narrowing code searches, 546
obvious fixes, 539
performance variations, 536–537
project-wide compilers settings, 557
psychological considerations, 554–556
quality of software, role in, 536
quotation marks, misplaced, 550
readability improvements, 538
recommended approach, 541
reexamining defect-prone code, 547
resources for, 561
Satan’s helpers, 539–540
scaffolding for, 558
scientific method of, 540–544
self-knowledge from, 538
source-code comparators, 556
stabilizing errors, 542–543
superstitious approaches, 539–540
symbolic debuggers, 526–527
syntax checking, 549–550, 557, 560
system debuggers, 558
test case creation, 544
testing, compared to, 500
time for, setting maximums, 549
tools for, 526–527, 545, 556–559, 719. See also debugging aids
understanding the problems, 539
unit tests, 545
varying test cases, 545
warnings, treating as errors, 557
debugging aids
C++ preprocessors, 207–208
case statements, 206
early introduction recommended, 206
offensive programming, 206
planning removal of, 206–209
pointers, checking, 208–209
preprocessors, 207–208
production constraints in development versions, 205
purpose of, 205
stubs, 208–209
version control tools, 207
decision tables. See table-driven methods
declarations
commenting, 794, 802–803, 816
const recommended, 243
declare and define near first use rule, 242–243
define near first use rule, 242–243
final recommended, 243
formatting, 761–763
implicit declarations, 239–240
multiple on one line, 761–762
naming. See naming conventions
numerical data, commenting, 802
order of, 762
placement of, 762
pointers, 325–326, 763
using all declared, 257
Decorator pattern, 104
defects in code
classes prone to error, 517–518
classifications of, 518–520
clerical errors (typos), 519
Code Complete example, 490–491
construction, proportion resulting from, 520–521

defects in code, continued
cost of detection, 472
cost of fixing, 472–473
databases of, 527
detection by various techniques, table of, 470
distribution of, 517–518
ease of fixing defects, 519
error checklists, 489
expected rate of, 521–522
finding, checklist, 559–560
fixing. See debugging; fixing defects
formal inspections for detecting. See formal inspections
intermittent, 542–543
misunderstood designs as sources for, 519
opportunities presented by, 537–538
outside of construction domain, 519
percentage of, measurement, 469–472
performance issues, 601
programmers at fault for, 519
readability improvements, 538
refactoring after fixing, 582
scope of, 519
self-knowledge from, 538
size of projects, effects on, 651–653
sources of, table, 518
stabilizing, 542–543
defensive programming
assertions, 189–194
assumptions to check, list of, 190
barricades, 203–205
checklist, 211–212
debugging aids, 205–209
defined, 187
error handling for, 194–197
exceptions, 198–203, 211
friendly messages guideline, 210
graceful crashing guideline, 210
guidelines for production code, 209–210
hard crash errors guideline, 209
important errors guideline, 209
key points for, 213
logging guideline, 210
problems caused by, 210
quality improvement techniques, other, 188
robustness vs. correctness, 197
security issues, 212
trivial errors guideline, 209
validating input, 188
defined data state, 509–510
defining variables. See declarations
Delphi, recoding to assembler, 640–642
DeMorgan’s Theorems, applying, 436–437
dependencies, code-ordering checker tools, 716
circular, 95
clarifying, 348–350
concept of, 347
documentation, 350
error checking, 350
hidden, 348
initialization order, 348
naming routines, 348–349
non-obvious, 348
organization of code, 348
parameters, effective, 349
design
abstractions, forming consistent, 89–90
accidental problems, 77–78
BDUF, 119
beauty, 80
bottom-up approach to design, 112–113
business logic subsystem, 85
capturing work, 117–118
central points of control, 107
change, identifying areas of, 97–99
changes, management of, 666–667
characteristics of high quality, 80–81
checklists, 122–123, 781
classes, division into, 86
collaboration, 115
communications among subsystems, 83–84
completion of, determining, 115–117
complexity management, 77–80
construction activity, as, 73–74
contract, by, 233
coupling considerations, 100–102
database access subsystem, 85
defined, 74
diagrams, drawing, 107
discussion, summarizing, 117
divide and conquer technique, 111
documentation, as, 781
documentation overkill, 117
emergent nature of, 76
encapsulation, 90–91
enough, determining, 118–119
essential problems, 77–78
extensibility goal, 80
formality of, determining, 115–117
formalizing class contracts, 106
goals checklist, 122–123
good practices table for, 31–32
heuristic. See heuristic design
hierarchies for, 105–106
high fan-in goal, 80
IEEE standards, 122
information hiding, 92–97, 120
inheritance, 91–92
iteration practice, 111–117
key points, 123
leanness goal, 81
level of detail needed, 115–117
levels of, 82–87
loose coupling goal, 80
low-to-medium fan-out goal, 81
maintenance goals, 80
mental limitations of humans, 79
metrics, warning signs from, 848
nondeterministic nature of, 76, 87
object-oriented, resource for, 119
objects, real world, finding, 87–89
packages level, 82–85
patterns, common. See patterns
performance tuning considerations, 589–590
portability goal, 81
practice heuristics. See heuristic design
practices, 110–118, 122
prioritizing during, 76
prototyping, 114–115
resources for, 119–121
restrictive nature of, 76
reusability goal, 80
routines, of, 86–87
sloppy process nature of, 75–76
software system level, 82
standard techniques goal, 81
standards, IEEE, 122
stratification goal, 81
strong cohesion, 105
subsystem level, 82–85
