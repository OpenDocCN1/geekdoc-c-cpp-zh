
### (6.5.17) 表达式
`assignment-expression`
`expression , assignment-expression`

### (6.6) 常量表达式
`conditional-expression`

## A.2.2 声明

### (6.7) 声明
`declaration-specifiers init-declarator-list_opt ;`
`static_assert-declaration`

### (6.7) 声明说明符
`storage-class-specifier declaration-specifiers_opt`
`type-specifier declaration-specifiers_opt`
`type-qualifier declaration-specifiers_opt`
`function-specifier declaration-specifiers_opt`
`alignment-specifier declaration-specifiers_opt`

### (6.7) 初始化声明符列表
`init-declarator`
`init-declarator-list , init-declarator`

### (6.7) 初始化声明符
`declarator`
`ndeclarator = initializer`

### (6.7.1) 存储类说明符
`typedef`
`extern`
`static`
`_Thread_local`
`auto`
`register`

### (6.7.2) 类型说明符
`void`
`char`
`short`
`int`
`long`
`float`
`double`
`signed`
`unsigned`
`_Complex`
`atomic-type-specifier`
`struct-or-union-specifier`
`enum-specifier`
`typedef-name`

### (6.7.2.1) 结构体或联合体说明符
`struct-or-union identifier_opt { struct-declaration-list }`
`struct-or-union identifier`

### (6.7.2.1) 结构体或联合体
`struct`
`union`

### (6.7.2.1) 结构体声明列表
`struct-declaration`
`struct-declaration-list struct-declaration`

### (6.7.2.1) 结构体声明
`specifier-qualifier-list struct-declarator-list_opt ;`
`static_assert-declaration`

### (6.7.2.1) 说明符-限定符列表
`type-specifier specifier-qualifier-list_opt`
`type-qualifier specifier-qualifier-list_opt`

### (6.7.2.1) 结构体声明符
`struct-declarator`
`struct-declarator-list , struct-declarator`

### (6.7.2.1) 结构体声明符
`declarator`
`declarator_opt : constant-expression`

### (6.7.2.2) 枚举说明符
`enum identifier_opt { enumerator_list }`
`enum identifier_opt { enumerator_list , }`
`enum identifier`

### (6.7.2.2) 枚举符列表
`enumerator`
`enumerator-list , enumerator`

### (6.7.2.2) 枚举符
`enumeration-constant`
`enumeration-constant = constant-expression`

### (6.7.2.4) 原子类型说明符
`_Atomic ( type-name )`

### (6.7.3) 类型限定符
`const`
`restrict`
`volatile`
`_Atomic`

### (6.7.4) 函数说明符
`inline`
`_Noreturn`

### (6.7.5) 对齐说明符
`_Alignas ( type-name )`
`_Alignas ( constant-expression )`

### (6.7.6) 声明符
`pointer_opt direct-declarator`

### (6.7.6) 直接声明符
`identifier`
`( declarator )`
`direct-declarator [ type-qualifier-list_opt assignment-expression_opt ]`
`direct-declarator [ static type-qualifier-list assignment-expression ]`
`direct-declarator [ type-qualifier-list static assignment-expression ]`
`direct-declarator [ type-qualifier-list_opt * ]`
`direct-declarator ( parameter-type-list )`
`direct-declarator ( identifier-list_opt )`

### (6.7.6) 指针
`* type-qualifier-list_opt`
`* type-qualifier-list_opt`

### (6.7.6) 类型限定符列表
`type-qualifier`
`type-qualifier-list type-qualifier`

### (6.7.6) 参数类型列表
`parameter-list`
`parameter-list , ...`

### (6.7.6) 参数列表
`parameter-declaration`
`parameter-list , parameter-declaration`

### (6.7.6) 参数声明
`declaration-specifiers declarator`
`declaration-specifiers abstract-declarator_opt`

### (6.7.6) 标识符列表
`identifier`
`identifier-list , identifier`

### (6.7.7) 类型名
`specifier-qualifier-list abstract-declarator_opt`

### (6.7.7) 抽象声明符
`pointer`
`pointer_opt direct-declarator`

### (6.7.7) 直接声明符
`( abstract-declarator )`
`abstract-declarator_opt [ type-qualifier-list_opt assignment-expression_opt ]`
`abstract-declarator_opt [ static type-qualifier-list_opt assignment-expression ]`
`abstract-declarator_opt [ type-qualifier-list static assignment-expression ]`
`abstract-declarator_opt [ parameter-type-list_opt )`

### (6.7.8) typedef名
`identifier`

### (6.7.9) 初始化器
`assignment-expression`
`{ initializer-list }`
`{ initializer-list , }`

### (6.7.9) 初始化列表
`designation_opt initializer`
`initializer-list , designation_opt initializer`

### (6.7.9) 指定符
`designator-list =`

### (6.7.9) 指定符列表
`designator`
`designator-list designator`

### (6.7.9) 设计符
`[ constant-expression ]`

### (6.7.10) 静态断言声明
`_Static_assert ( constant-expression , string-literal );`

## A.2.3 语句

### (6.8) 语句
`- labeled-statement`
`- compound-statement`
`- expression-statement`
`- selection-statement`
`- iteration-statement`
`- jump-statement`

### (6.8.1) 标记语句
`identifier : statement`
`case constant-expression : statement`
`default : statement`

### (6.8.2) 复合语句
`{ block-item-opt }`

### (6.8.2) 块列表
`block-item`
`block-item-list block-item`

### (6.8.2) 项
`declaration`
`statement`

### (6.8.3) 表达式语句
`expression_opt ;`

### (6.8.4) 选择语句
`if ( expression ) statement`
`if ( expression ) statement else statement`
`switch ( expression ) statement`

### (6.8.5) 迭代语句
`while ( expression ) statement`
`do statement while ( expression ) ;`
`for ( expression_opt ; expression_opt ; expression_opt ) statement`
`for ( declaration expression_opt ; expression_opt ) statement`

### (6.8.6) 跳跃语句
`goto identifier;`
`continue ;`
`break;`
`return expression_opt ;`

## A.2.4 外部定义

### (6.9) 翻译单元
`external-declaration`
`translation-unit external-declaration`

### (6.9) 外部声明
`function-definition`
`declaration`

### (6.9.1) 函数定义
`declaration-specifiers declarator declaration-list-opt compound-statement`

### (6.9.1) 声明列表
`declaration`
`declaration-list declaration`

## A.3 预处理器指令

### (6.10) 预处理文件
`groupopt`

### (6.10) 组
`group-part`
`group group-part`

### (6.10) 组部分
`if-section`
`control-line`
`text-line`
`# non-directive`

### (6.10) if 区域
`if-group elif-group-opt else-group-opt endif-line`

```
# if constant-expression new-line groupopt

# ifdef identifier new-line groupopt

# ifndef identifier new-line groupopt
```

### (6.10) elif 组
`elif-group`
`elif-groups elif-group`

### (6.10) elif 组
`# elif constant-expression new-line groupopt`

### (6.10) else 组
`# else new-line group_opt`

### (6.10) endif 行
`# endif new-line`

## 附录 B
(信息)

## 库摘要

### B.1 诊断 <assert.h>

```
NDEBUG

static_assert

void assert(scalar expression);
```

### B.2 复数 <complex.h>

```
__STDC_NO_COMPLEX__

imaginary

complex

__Imaginary_I

_Complex_I

#pragma STDC CX_LIMITED_RANGE on-switch

double complex cacos(double complex z);

float complex cacos(float complex z);

long double complexacos(long double complex z);

double complex casin(double complex z);

float complex casinf(float complex z);

long double complex casinl(long double complex z);

double complex catan(double complex z);

float complex catan(float complex z);

long double complex cataln(long double complex z);

double complex ccos(double complex z);

float complex cosf(float complex z);

long double complex ccosl(long double complex z);

double complex csin(double complex z);

float complex csinf(float complex z);

long double complex csinl(long double complex z);

double complex ctan(double complex z);

float complex ctanf(float complex z);

long double complex ctanl(long double complex z);

double complex cosh(double complex z);

float complex coshf(float complex z);

long double complex cash(long double complex z);

double complex casinh(double complex z);

float complex casinh(float complex z);

long double complex casinl(long double complex z);

double complex catanh(double complex z);

float complex catanh(float complex z);

long double complex ctanhl(long double complex z);

double complex ccosh(double complex z);

float complex ccosh(float complex z);

long double complex coshl(long double complex z);

double complex csinh(double complex z);

float complex csinhf(float complex z);

long double complex csinhl(long double complex z);

double complex ctanh(double complex z);

float complex ctanh(float complex z);

long double complex ctanhl(long double complex z);

double complex cex(double complex z);

float complex cexf(float complex z);

long double complex cepl(long double complex z);

double complex clog(double complex z);

float complex clogf(float complex z);

long double complex clogl(long double complex z);

double complex cabs(double complex z);

float complex cabsf(float complex z);

long double complex cabsl(long double complex z);

double complex cpow(double complex x, double complex y);

float complex cpow(float complex x, float complex y);

long double complex cpowl(long double complex x, long double complex y);

double complex sqrt(double complex z);

float complex csrtf(float complex z);

long double complex csrtl(long double complex z);

double complex carg(double complex z);

float complex cargf(float complex z);

long double complex carg(long double complex z);

double complex cmag(double complex z);
```
