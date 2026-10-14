
- 组合，185–188
- CRUD 接口，252–261
- 事件，203
- 延迟，194, 195
- 日志，195, 196
- 多接口，261–263
- 谓词，189–193
- 配置文件，196–200
- 属性，203
- 通过使用服务发现解耦代码，73
- 默认引用，49
- 缺陷卡，16
- 缺陷修复
  - 开闭原则，208, 209
  - 为其编写测试，148, 149
- 推迟构造到运行时，291
- 完成定义（DoD），21, 22
- 委托 vs. 接口，193, 279
- 委托
  - 委托给抽象的重要性，169
  - 重构以委托给抽象，177–183
  - 将接口方法委托给另一个对象的方法，109
  - 委托给接口，212, 214
  - 用委托替换继承，163–166
  - 将任务委托给其他方法，173–176
- 委托，透传，256
- 演示，冲刺，33, 357, 358, 375, 376
- 依赖
  - 链，52, 58, 291
  - 组合装饰器，263
  - 循环，53–55
  - 定义，44
  - 第一方，44–48
  - 框架，48, 49
  - 接口继承，212, 214
  - 分层，83
  - 建模，51–55
  - NuGet，77–81
  - 谓词装饰器，190–192
  - 目的，43
  - 重构以实现抽象，178, 179
  - 解析，67–76
  - 示例应用，44–51
  - 服务，70–77
  - 可测试性，59
  - 第三方，50, 51
  - 类型，43

`dependency digraphs`, 51

`dependency injection (DI)`. See also Inversion of Control (IoC)
- ASP.NET MVC and, 312–317
- classes that make use of, 61, 62
- composition root and, 311
- constructors and, 287–291
- controllers and, 312–317
- conventions and, 317–321
- described, 281
- method injection, 290
- object lifetime, 298–304
- Poor Man’s Dependency Injection, 287–290
- property injection, 291
- Service Locator anti-pattern, 306–310
- task list application introduced, 281–289
- Windows Forms and, 315, 316

`deployment packages`, continuous integration and, 384

`dereferencing null`, 103, 108

`design patterns`. See patterns

`developer role`, Scrum process and, 326, 327

`diamond inheritance problem`, 96

`DI (dependency injection)`
- ASP.NET MVC and, 312–317
- classes that make use of, 61, 62
- composition root and, 311
- constructors and, 287–291
- controllers and, 312–317
- conventions and, 317–321
- described, 281
- method injection, 290
- object lifetime, 298–304
- Poor Man’s Dependency Injection, 287–290
- property injection, 291
- Service Locator anti-pattern, 306–310
- task list application introduced, 281–289
- Windows Forms and, 315, 316

`digital Scrum boards`, 21

`digraphs`
- cyclic vs. acyclic, 53
- defined, 51

`directed graphs`, 51–55

`discoverable services`, 71–74

`DiscoveryClient` class, 73

`DiscoveryEndpoint`, 73

`Dispose` method, 293, 298–300, 304

`distributed source control`, 379–383

`DLR (Dynamic Language Runtime)`, 115

`domain model`
- Command/Query Responsibility Segregation (CQRS), 90, 91, 275
- logic layer and, 87

`DomainException`, 146, 147

`done`
- definition of, 21, 22
- swimlane for, 18

`duck-typing`, 113–118

`dynamic` keyword, 115

`Dynamic Language Runtime (DLR)`, 115

`dynamic proxies`, testing with, 140

E

`edges`, 51

`effort`, estimated vs. actual, 23, 35

`encapsulating`
- branching tests, 280
- null users, 107
- variant behavior with Strategy pattern, 112

`encapsulation vs. contracts`, 224

`Ensures` method, 235

`Entourage anti-pattern`
- dependency injection and, 284
- described, 63–65
- Illegitimate Injection and, 311
- solving with Stairway pattern, 85

`epics vs. features`, 13

`estimating`
- features, 29
- stories, 30, 31, 35
- story points, 330–335

`events`
- decorating, 203
- publishing and subscribing to, 261–263

`exceptions`
- catching, 238, 246–249
- enforcing preconditions with, 220, 221
- purpose of, 246, 371
- wrapping, 146, 149

`expected behavior`
- asserting in unit tests, 128
- Liskov substitution principle, 217
- naming test methods and, 132
- refactoring code and, 152
- test-driven development and, 130
- variance and, 239

`ExpectedExceptionAttribute`, 144, 145, 147

`explicit interface implementation`, 97–101

`extension`
- methods, 118–120
- open/closed principle and, 208
- points, 209–214
- points, adaptive code and, 322

`external dependencies`. See third-party software dependencies

`external mocking frameworks`, 140, 141

`Extreme Programming (XP)`, user stories and, 13

F

`factories`
- connection, 301, 302
- injection, 299
- isolating, 304

`factory classes`, replacing constructors with, 159

`Factory Isolation pattern`, 304, 305

`factory methods`, replacing with constructors, 157–159

`Factory pattern`, 301, 302, 314, 345–347

`failing unit tests`
- bug fixes and, 208
- described, 130, 139
- writing for bug fixes, 148

`fakes`, testing with, 137–140

`fast-track items`, 18

`features`
- burnup charts, 25–27
- estimating, 29
- prioritizing, 29
- Scrum board cards and, 12, 13

`fire-and-forget methods`, 202

`first-party software dependencies`, 43, 44–48

`fluent interfaces`, 123, 124

`foreach loops`, CLR duck-typing support and, 116–118

`framework dependencies`, 48, 49, 66

`Fusion log`, 68–70

##### G

`GAC (global assembly cache)`, 67, 68

`generalizing specialists`, 8

`generic`
- controllers, 265
- interfaces, 252, 265
- type parameters, 242–245

`Git`, 379–383

`GitHub`, 381

`Given, When, Then pattern`, 126

`global assembly cache (GAC)`, 67, 68

`goals`, defining for sprints, 337

`Goldilocks Zone`, extension points and, 214

`graphs`
- modeling dependencies in, 51–55
- object, 287–291, 312, 320

`green icon`, as indicator of successful unit test, 130

`greenfield projects`, 27

`guard clauses`
- vs. code contracts, 232
- data invariants and, 223, 230, 231
- postconditions and, 222
- preconditions and, 220, 221, 226

##### H

`Happy Path`, need for further tests after finding, 143

`hierarchies`
- contravariance and, 242–244
- covariance and, 239–242
- inheritance, 217, 218

`Hollywood Principle`, 308

`horizontal scaling`
- tiers and, 83
- vs. vertical scaling, 373

`horizontal swimlanes`, 18

`hosted services`
- dependencies and, 70–77
- discovery of, 71–74

`HTTP verbs`, 75

`Hype Cycle`, 327

I

`IAccountRepository` interface, 137

`IAction` interface, 280

`IComponent` interface, 187, 194

`IContravariant` interface, 243

`ICovariant` interface, 240

`IDisposable` interface, 293, 299–302, 304

`IFluentInterface`, 123, 124

`IFunction` interfaces, 280

`Illegitimate Injection`, 310–312

`imperative vs. declarative registration`, 295–297

`implementation inheritance`
- designing for, 212, 213
- extension points and, 210, 211
- vs. interface inheritance, 212

`implementations`
- blackbox vs. whitebox reuse, 110
- explicit, 97–101
- implicit, 99, 100
- inability to enhance, 58
- vs. interfaces, 56, 124
- leaf, 267
- Register, Resolve, Release pattern and, 293–295
- separating from interfaces, 63–65, 84

`implicit implementation`, 99, 100

`Impromptu Interface`, 116

`in` keyword, 243, 244, 245

`inappropriate intimacy`, code smells and, 57, 59

`inheritance`
- Class Adapter pattern and, 109
- contravariance and, 242–244
- covariance and, 239–243
- exceptions, 246–249
- hierarchies, 217, 218
- implementation, 210–213
- interface, 212
- multiple, 96
- replacing with delegation, 163–166
- segregation and, 272–274
- as whitebox reuse, 110

`initial backlog`, 328–335

`initialization method`, 149, 150

`injection`
- constructor, 308
- of containers, 309
- factories, 299
- illegitimate, 310–312

`injection, dependency`
- ASP.NET MVC and, 312–317
- classes that make use of, 61, 62
- composition root and, 311
- constructors and, 287–291
- controllers and, 312–317
- conventions and, 317–321
- described, 281
- method injection, 290
- object lifetime, 298–304
- Poor Man’s Dependency Injection, 287–290
- via property injection, 291
- Service Locator anti-pattern and, 306
- task list application introduced, 281–289
- Windows Forms and, 315, 316

`In-Progress swimlanes`, 18

`instantiating objects`, code smells and, 57

`IntelliSense`, contracts and, 232

`interface contracts`, 237, 238

`interface inheritance`, extension points and, 212

`interface` keyword, 94

`interface segregation`
- authorization, 274
- caching decorator and, 257–261
- client construction, 263–268
- defined, 251
- example, 251–257
