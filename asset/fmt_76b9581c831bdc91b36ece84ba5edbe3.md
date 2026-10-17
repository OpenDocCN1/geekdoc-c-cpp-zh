
splitting for architectural need, 275–279

splitting for client need, 268–275

Interface Soup anti-pattern, 267, 268

interfaces. See also user interface

assemblies and, 63, 84

classes and, 94, 284

code adaptability and, 284

coding to, 60

combining as mixins with Re-Motion Re-mix, 120–122

Composite pattern and, 186

contracts and, 219

decorating multiple, 261–263

defined, 57

vs. delegates, 193, 251, 279

described, 93

explicit implementation, 97–101

external dependencies and, 66

fluent, 123, 124

generic, 252

`IAccountRepository`, 137

`IAction`, 280

`IComponent`, 187, 194

`IContravariant`, 243

`ICovariant`, 240

`IDisposable`, 293

`IFunction`, 280

vs. implementations, 56, 124

implementing in a single class, 266, 267

`IPaymentStrategy`, 206

`IPredicate`, 192, 280

`IServiceLocator`, 306, 308

`ITargetInterface`, 118, 122

`ITask`, 279

members and, 251

mocking, 140–142

organizing with Stairway pattern, 65, 284

overuse of, 113

providing to clients, 263–269

refactoring toward abstraction and, 177–180

Register, Resolve, Release pattern and, 293–295

repository, 136

splitting for architectural need, 275–279

splitting for client need, 268–275

syntax, 94–96

Invariant method, 236

invariants, 223, 224, 229–231, 236, 244, 245

guard clauses and, 223

Inversion of Control (IoC)

composition root and, 311

containers and, 291–295

described, 291, 292

vs. Poor Man’s Dependency Injection, 292

inverting class hierarchies with contravariance, 242–244

IoC (Inversion of Control). See Inversion of Control (IoC)

`IPaymentStrategy` interface, 206

`IPredicate` interface, 192, 280

IronPython, as dynamically typed language, 115

`IServiceLocator` interface, 306, 308

IsNull property anti-pattern, 105–107

isolating factories, 304, 305

`ITargetInterface`, 118, 122

`ITask` interface, 279

iterations. See sprints

J

JIT (just-in-time) model, 67

K

keywords, dynamic, 115

known endpoints, service references and, 70

L

lambda expressions

Factory Isolation pattern and, 305

mocking and, 141

object lifetime and, 299

lambda factories, declarative registration and, 297

layering

API layer, 84

described, 81

patterns, 82–87

vs. tiers, 83

wrapping exceptions and, 146

lazy decorators, 194, 195

`Lazy<T>`, 194

leaf implementations, 267

leaky abstractions, 85

libraries

code contracts, 232

Impromptu Interface, 116

Log4Net, 181, 182

Prism, 122

Re-motion Re-mix, 118, 120–122

lifetime of objects, 298–304

line of best fit, 24

Liskov substitution principle (LSP)

contravariance, 242–245

covariance, 239–243

described, 217, 218

exceptions, 246–249

invariance, 244, 245

rules, 218, 225–231

log files, 68–70

Log4Net, 181, 182

logging decorators, 195, 196

logic layer, 86, 87

loops, 54, 55

loose mocks, 141

loosely coupled classes, 209

LSP (Liskov substitution principle)

contravariance, 242–245

covariance, 239–243

described, 217, 218

exceptions, 246–249

invariance, 244, 245

rules, 218, 225–231

### M

magic numbers, replacing with constants, 153, 154

maladaptive code, 37–41

mapping

composition root and, 311

conventions and, 318

dependency injection and, 321

interfaces to implementations, 296

markdown transforms, 367–370

marketable features, 12

Martin, Robert C., 208

meetings

for full sprint, 36

planning, for sprint, 337–339

retrospective, for sprint, 358–362

Mercurial vs. Git, 379

method injection, 290

methods. See also decorators

abstract, 211

asymmetric layering and, 89–91

asynchronous, 200

chaining, 123, 124

`Contract.Ensures`, 235

`Contract.Invariant`, 236, 238

`Contract.Requires`, 233, 234

Dispose, 293, 298–300, 304

Ensures, 235

extension, 118–120

factory, 157–159

fire-and-forget, 202

`IDisposable.Dispose()`, 298–304

Liskov contract rules and, 225–231

naming, 219

postconditions and, 222, 223

preconditions and, 220–222

private, 236

Register, 293–295

RegisterTypes, 318

Release, 293–295

request-response, 202

Requires, 233, 234

Resolve, 293–295

signatures, 98–101, 219

static, 158

synchronous, 200

tracking execution time, 197

virtual, 210, 211, 284

metrics

correlation vs. causation, 40

maladaptive code and, 39

monitoring project progress with, 22–27

story points, 23

Meyer, Bertrand, 207

Microsoft AppFabric AutoStart, 74

Microsoft Moles, 59

Microsoft .NET Framework

advantages of, 196

Impromptu Interface library, 116

software dependencies and, 43, 48, 49

Microsoft .NET Framework Reflection API, 116

minimum marketable feature (MMF)

defined, 12

vs. epics and themes, 13

minimum viable release (MVR), 12

mixins, 118–122

MMF (minimum marketable feature)

defined, 12

vs. epics and themes, 13

mocking frameworks, 39, 140, 141

mocks

Illegitimate Injection anti-pattern and, 311

setting up, 149

testing with, 140–143

modeling dependencies, 51–55

Model-View-Controller (MVC), dependency injection and, 312–317

Model-View-ViewModel (MVVM) pattern, 282

MongoDB, 276

monitoring progress with charts and metrics, 22–27

Moq, 140, 141

MSTest, 129, 149

multicast network messages, 71

multilayer solutions. See layering

multiple inheritance, 96, 118

multiple interface implementation, 95

MVC (Model-View-Controller), dependency injection and, 312–317

MVR (minimum viable release), 12

MVVM (Model-View-ViewModel) pattern, 282

### N

.NET Framework. See Microsoft .NET Framework

network boundaries, tiers and, 83

NHibernate, 276

niko-niko calendar, 32

nodes, 51

noise-to-signal ratio, contracts and, 237

NuGet

dependencies and, 77–81

testing with Moq and, 140

Null Object pattern, 103–105, 108

NullReferenceException, 103, 108, 144, 145

NullUser class, 105, 107

### O

Object Adapter pattern, 110, 111

object graphs

constructing, 287–291

conventions and, 320

resolution root and, 312

object lifetime

`IDisposable.Dispose()` method and, 298–304

release method and, 293

Object property, 141

object-oriented programming (OOP), polymorphism and, 101

Object/Relational Mapper (ORM), 50

observer effect, 22

OCP (open/closed principle). See open/closed principle (OCP)

OOP (object-oriented programming), polymorphism and, 101

open for extension rule, 208

open/closed principle (OCP)

bug fixes and, 208, 209

client awareness and, 209

peak of inflated expectations, 327

peer reviews, 340–357, 380

performing unit tests. See unit tests

persistent storage, CRUD operations and, 251, 252

pigs and chickens, 9

Plain Old CLR Object (POCO), 285

planning poker, story point estimation and, 331–335

plateau of productivity, 327

PO (product owner) role, 7, 325, 326

POCO (Plain Old CLR Object), 285

poker, planning, story point estimation and, 331–335

polymorphism

covariance and, 239, 240

described, 101, 102

replacing conditional expressions with, 154–157

Poor Man’s Dependency Injection (Poor Man’s DI)

composition root and, 311

described, 287–290

post mortems. See sprint retrospectives

postconditions

code contracts and, 235

described, 222, 223

Liskov Substitution Principle and, 227–229

PostSharp, 88

preconditions

arranging for unit tests, 126, 127

code contracts and, 232–234

of constructors, 143

contracts and, 224

described, 220–222

enforcing with exceptions, 221

enforcing with preconditions, 220

Liskov Substitution Principle and, 225–227

predicate decorators, 189–193

predicted variation, 213

prioritizing features, 29

Prism (Windows Presentation Foundation/Model-View-ViewModel library), 122

private methods, 236

product backlogs

described, 27

for readability, 153, 154

replacing conditional expressions with polymorphism, 154–157

replacing constructors with factory methods, 157–159

replacing inheritance with delegation, 163–166

replacing magic numbers with constants, 153, 154

samples, 347, 348, 350–353

technical debt and, 57

test-driven development and, 130–135

references

converting third-party to first-party, 181

defaults by project type, 49

NuGet and, 77–81

resolution process, 67

services, 70, 71

third-party, 50

Reflection Emit, 116
