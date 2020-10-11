# Rust函数与控制流
在本节中我们将对Rust的函数与控制流进行学习。
## Rust函数
在Rust应用程式开发过程中，我们建议大家使用蛇形命名(***snake case***)的方式对函数名称进行定义。在这里所有的单词均为小写并用下划线进行分开。案例如下：
```rust
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```
对于带参数类型函数来说，我们需要在函数定义处指明输入变量类型，例如：
```rust
fn main() {
    let value = another_function(5, 6);
    println!("{}", value.0);
    println!("{}", value.1);
}

fn another_function(x: i32, y: i32) -> (i32, i32){
    println!("The value of x is: {}", x);
    println!("The value of y is: {}", y);
    (x ,y) // 返回一个tuple
}
```
与`C++ NameSpace`代码块功能相类似，我们可以在函数段内部增加`{}`来对某一变量的复制
与Python`闭包`相类似，我们同样可以在Rust的函数段内部增加`fn {}`代码段并实现对某一变量的函数类型赋值，相关案例如下：
```rust
fn main() {
    fn dev() -> i32{
        3
    };
    let value = dev();
    println!("{}", value); // 3
}
```
## Rust控制流
#### 条件判断
在Rust中，我们使用`if/else/else if`条件语句来进行逻辑判断，相关案例如下：
```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```
Rust的三段式表述方法如下：
```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };
    // let number = if condition { 5 } else { "six" }; // 此行将会编译出错！因为变量必须是相同类型

    println!("The value of number is: {}", number);
}
```
#### 循环
Rust有`loop/while/for`三种循环方式。
##### loop重复执行
`loop`关键字要求我们在编写Rust时，显式的终止应用程式，相关案例：
```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {}", result);
}
```
`while`循环则需要我们制定判断的逻辑规则，相关案例：
```rust
fn main() {
    let mut number = 3;

    while number != 0 {
    // while true{ // 死循环
        println!("{}!", number);

        number = number - 1;
    }

    println!("LIFTOFF!!!");
}
```
`for`关键字为对集合中的元素/迭代器进行遍历，相关案例：
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];
    let iter = a.iter(); // 迭代器

    for element in iter {
        println!("the value is: {}", element);
    }
}
```