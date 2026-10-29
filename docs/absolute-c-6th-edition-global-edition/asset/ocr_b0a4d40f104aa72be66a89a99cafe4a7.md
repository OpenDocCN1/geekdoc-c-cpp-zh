# ## 3.2.2 使用 `use` 关键字将路径引入作用域

必须使用路径来调用函数的写法可能会显得冗长且重复。幸运的是，我们可以使用 `use` 关键字将路径一次性引入作用域，然后就可以像使用本地项一样调用路径中的项。

在示例 3-6 中，我们将 `crate::front_of_house::hosting` 模块引入了 `eat_at_restaurant` 函数的作用域，这样我们只需要指定 `hosting::add_to_waitlist` 即可调用 `add_to_waitlist` 函数。在示例 3-6 中，我们还指定了如何调用 `eat_at_restaurant` 函数。

```
```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```
```

示例 3-6：使用 `use` 将模块引入作用域

在作用域中增加 `use` 和路径类似于在文件系统中创建符号链接。通过在 crate 根中增加 `use crate::front_of_house::hosting`，`hosting` 现在就是 crate 根中一个有效的名称，就像 `hosting` 模块是在 crate 根中定义的一样。通过 `use` 引入作用域的路径也会检查私有性，就像其它路径那样。

还可以使用 `use` 和相对路径将项引入作用域。示例 3-7 展示了如何指定相对路径而不是绝对路径。

```
```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```
```

示例 3-7：使用 `use` 和相对路径将模块引入作用域