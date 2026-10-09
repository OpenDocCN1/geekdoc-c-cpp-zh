
`type(fish_type)`, `dimension(number)` :: `fish`

`type(flow_field_type)` :: `flow`

`type(food_situation_type)` :: `food`

```fortran
real :: deltt

integer :: i, time
```

```fortran
!

! 初始化鱼、流场和食物的信息：

! 在 100x100 的网格中

call random_number( fish%x )
```

## 184 现代 Fortran 实践

```fortran
call random_number( fish%y )

fish%x = 100000.0

fish%y = 100000.0

fish%age = 0.0

deltt = 0

do time = 1,100

  do i = 1,size(fish)

    call fish(i)%behave( deltt, flow, food )
```

### 11.4 抽象类型与通用编程

随着 Fortran 90 引入了指针，开发数组以外的数据结构变得简单了。事实上，任何递归定义的抽象类型（如链表和二叉树）都可以直接在 Fortran 90 中实现。

```fortran
type linked_list
    integer :: value
    type(linked_list), pointer :: next
end linked_list
```

关键特性是允许指向尚未（完全）定义的类型。定义应该出现在同一个编译单元中。要面对的主要问题是存储的数据类型。Fortran 90 不容易将不同类型存储在同一个链表或树中。这意味着对于包含数组和字符串的列表，我们需要如下构造：

```fortran
type linked_list
    real, dimension(:), pointer :: array
    character(len=*) :: string ! 如果不是数组
type(linked_list), pointer :: next
end linked_list
```

这与第 11.1 节中处理二维空间点的解决方案类似。在 Fortran 77 中，基本数据结构是数组。虽然可以将其链表的基础，但实现灵活性较低。

## 面向对象编程 185

完全不同的方法是将数据转换为你存储的类型并跟踪原始类型：

```fortran
type linked_list
    integer, dimension(:), pointer :: array
    integer :: type_indicator ! 1 - 实数数组，2 - 字符串
    type(linked_list), pointer :: next
end linked_list
```

以下带有关联例程的代码：

```fortran
subroutine store_real_array( element, array )
type(linked_list) :: element
real, dimension(:) :: array

element%type_indicator = 1
call store_integer_array(&
    element, transfer(array,element%array))
end subroutine store_real_array
```

```fortran
subroutine store_character_string( element, string )
type(linked_list) :: element
character(len=*) :: string

element%type_indicator = 2
call store_integer_array(&
    element, transfer(string,element%array))
end subroutine store_character_string
```

```fortran
! 私有例程 - 这里我们知道确切的大小
subroutine store_integer_array(element, data )
type(linked_list) :: element
integer, dimension(:) :: data

allocate(element%array(size(data)))
element%array = data
end subroutine store_integer_array
```

... 以原始形式检索数据的例程（你使用 `transfer()` 函数将数据从一种类型转换为另一种；在这里是整数数组）。如果类型是派生类型，抽象数据类型可以很容易重用以存储任何类型的数据：

```fortran
module linked_list_points2d
use points2d, stored_type => point2d
```

## 186 现代 Fortran 实践

```fortran
private
public :: linked_list, add, ...
type linked_list
    type(stored_type)      :: data
    type(linked_list), pointer :: next
end type linked_list
```

```fortran
!
! 为功能定义通用名称
! - 使使用不同类型的列表变得更容易
!
```

```fortran
interface add
module procedure :: add_element
end interface
```

... 其他接口

contains

... 需要的例程和函数

end module linked_list_points2d

由于只有一小部分特定数据类型，你可以将代码的通用部分放在包含特定实现的文件中：

```fortran
module linked_list_points2d
use points2d, stored_type => point2d
include 'generic_lists.f90'
end module linked_list_points2d
```

```fortran
module linked_list_grids
use grids, stored_type => grid
include 'generic_lists.f90'
end module linked_list_grids
```

```fortran
module linked_list_lists
use linked_list_points2d, &
linked_list_of_2points => linked_list
use linked_list_grids, &
linked_list_of_grids => linked_list
end module linked_list_lists
```

由于通用名称的存在，两种类型的列表可以在同一个程序中使用而不产生命名冲突。原始例程位于不同的模块中并被设为私有。调用程序只能看到通用名称。通过

## 面向对象编程 187

通过语句的重命名功能，派生类型的通用名称 `linked_list` 变得更加具体。

使用多态变量（声明为 `class(some_type)`），你当然可以存储任何类型的数据，只要它们的类型继承自基础类型：

```fortran
type linked_list
  class(basic_type), allocatable :: data
  type(linked_list), pointer :: next
end type linked_list
```

如果你使用声明为 `class(*)` 的调用无限制多态变量，这种限制就会消除。这些变量可以与任何数据关联，代价是需要一些额外的代码来处理它们：

```fortran
real, target :: x = 3.1415926
class(*) :: pi
```

```fortran
pi => x
select type
type is real
    write(*,) 'x = ', pi
end select
```

多态变量（无论有限限制还是无限制）带来的额外灵活性是有代价的。如果你想保证所有数据都是相同类型，你需要采取额外的措施：

```fortran
subroutine add_element( element, data )
  type(linked_list) :: element
  class(*) :: data

  if ( same_type_as( element%data, data ) ) then
    ... 添加新元素
  else
    write(*,) 'Wrong type of data!'
  endif
end subroutine add_element
```

### 11.5 改变类型的行为

在使用模块（module）时，你可以重命名变量、数据类型和例程的名称以避免命名冲突。此功能实际上允许你在不更改原始实现的情况下“混入”（mix in）功能。在 Python 或 Tcl 等动态语言的领域中，这种过程被称为添加 mixins 或过滤器 [67]。由于这些语言的动态性质，该过程是非常透明的。变量没有固的数据类型，甚至例程的实现也可以在运行时更改。在 Fortran 中，你需要多做一些。

假设你想跟踪特定类型对象的状态，常见的例子是通过这些对象记录程序的活动。那么，执行以下操作：

- 使用包含该定义的模块并重命名该类型：

```fortran
module new_points2d
  use point2d, point2d_original => point2d, &
  add_vector_2d_original => add_vector_2d
  ...
end module new_points2d
```

- 定义一个继承自原始类型的新类型 `point2d`：

```fortran
type, extends(point2d_original) :: point2d
  contains
    procedure :: add_vector => add_vector_2d
end type point2d
```

- 困难的工作是扩展所有你想跟踪的类型例程（type-bound procedures）：

```fortran
subroutine add_vector_2d(point, vector )
  class(point2d) :: point
  class(point2d_original) :: vector

  write(**) 'Calling "add_vector"'

  call point%point2d_original%add_vector( vector )
end subroutine add_vector
```

- 最后，使用新模块代替旧模块。这可以透明地完成，因为模块定义的功能以及它们从其他模块导入的功能。唯一需要注意的是模块的名称对于整个程序是全局的：

```fortran
module point2d_functionality
  !
  ! 此模块仅仅传递我们从
  ! 各种底层模块导入的功能。
  ! 这允许我们只在一个
  ! 地方更改实际的模块
  !
  ! 我们已经扩展了 point2d 类型 - 所以使用
  ! 新模块
  !
  ! use points_2d
  use new_points2d
end module point2d_functionality
```

类型实现的更改对使用它的程序是完全隐藏的。你只需要重新编译它，所有其他源代码保持不变。

### 11.6 设计模式

虽然设计模式大多在 C++ 和 Java 等编程语言的背景下被描述，但其中涉及的原理是相当通用的 [35], [28]。设计模式试图捕捉解决广泛软件问题的通用方案的精髓。Rouson、Xia 和 Xu [34] 比较了 Fortran 2003 和 C++ 中若干设计模式的实现。有些模式是广为人知的，另一些是特定领域的，因此它们在物理模拟等领域特别有用。

以下仅考虑了两个例子：工厂模式（Factory pattern）和观察者模式（Observer pattern），以说明设计模式如何应用于 Fortran 程序中（其他示例请参阅 [54] 和 [73]）。

#### 工厂模式

面向对象编程中一种流行的设计模式是所谓的工厂模式。其背后的想法是，程序可能需要一个或多个特定类型的对象，但如果它承担的不仅仅是创建对象，它就不应该承担妥善初始化或管理对象的责任 [9]。适当的初始化或管理包括以下任务：

- 为其组件分配内存。

- 设置初始值。

- 打开文件并读取其内容（如果这是对象工作方式的一部分）。

- 对象可能是对象池的一部分，然后应该一致地管理相关的资源。

工厂模式的另一个用途是允许使用程序处理通用对象而不是特定类型。这里有一个例子：工厂返回一个多态对象，其行为可以表现为均匀分布或指数分布。这对其源代码没有影响，除非可能恰要添加了新的分布：

```fortran
program test_prng_factory
  use prng_factory

  class(prng), pointer :: p
  integer :: i

  p = prng_factory(uniform, 1.0)
  do i = 1,10
    write(*, p%get())
  enddo

  p = prng_factory(exponential, 2.0)
  do i = 1,10
    write(*, p%get())
  enddo
end program test_prng_factory
```

## 190 实践中的现代 Fortran

```fortran
function prng_create( type, param1, param2 )
  character(len=*) :: type
  real             :: param1
  real, optional :: param2

  class(prng), pointer :: prng_create
  real             :: param2opt
  integer          :: i

  if ( .not. initialized ) then
    initialized = .true.
    call initialize_factory
  endif

  param2opt = 0.0
  if ( present(param2) ) then
    param2opt = param2
  endif

  prng_create => null()

  do i = 1,size(prng_creators)
    if ( prng_creators(i)%name == type ) then
      call prng_creators(i)%create( prng_create, param1, param2opt )
    endif
  enddo
end function prng_create
```

## 191 实践中的现代 Fortran

```fortran
! 私有例程 - 初始化工厂
subroutine initialize_factory
  character(len=20), dimension(2) :: prng_name
  character(len=20), dimension(2) :: libname
  type(dynamic_library) :: dylnib
  logical :: success
  integer :: i

  prng_name = (/ 'uniform', 'exponential' /
  libname = (/ 'uniform.dll', 'exponential.dll' )

  do i = 1,size(libname)
    call load_library(dylnib, libname(i), success)
    if ( success ) then
      call get_procedure(dylnib, create_prng, success)
      if ( .not. success ) then
        write(*,'Could not load create_prng - ', libname(i))
      endif
      prng_creators(i)%name = prng_name(i)
    endif
  enddo
end subroutine initialize_factory
```

## 192 实践中的现代 Fortran

```fortran
! 返回一个正确动态类型的对象
```

#### 观察者模式

从数值计算的角度来看，一种非常有趣的设计模式是观察者模式。这种模式允许你在不需要设计来扩展程序的情况下扩展程序的功能。相反

## 面向对象编程 193

在计算过程中，用户无需插入子程序调用来检查解决方案的属性，你的程序提供了一种功能，可以注册具有类型绑定过程的例程或数据对象，这些过程会在特定事件发生时被调用。

例如，在计算管道网络中的水流时，一个有趣的事件可能是时间积分中单步计算的完成。以下是实现此目的的代码片段：

在包含求解器定义的模块中，你拥有以下类型，一个作为实际观察对象的“父”类，另一个用于存储关于解决方案的所有 Solution价值的数据：

```fortran
type, abstract :: observer
contains
  procedure(check_result), deferred, pass(obs) :: check
type observer
```

```fortran
type observer_list
contains
  class(observer), pointer :: observer
end type observer_list
```
