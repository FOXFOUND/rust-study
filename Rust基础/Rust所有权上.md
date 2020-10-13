# Rust所有权

由于所有权对于很多程序员来说是一个较新的概念，同时作为Rust的核心特性，在我们介绍所有权之前，我们首先对`栈(Stack)`和`堆(Heap)`进行简单的介绍：
```
很多的编程语言并不需要开发者过多的关注应用运行时中堆与栈的状态，但像Rust这样的系统编程语言，值位于堆或栈将对运行时造成极大的影响。当您的代码调用某一方法的时候，函数所传值与指向堆的指针和函数的局部变量将会存放于栈当中。函数执行完成后，此些值将出栈。
```
接下来我们不妨了解一下所有权的定义：
```
1、Rust中每个值都是某个所有者的变量
2、值在任意时刻有且只有一个所有者
3、当所有者销毁时，值也将被释放
```
在这里我们不妨基于字符串及`String`类型进行举例：
```rust
fn main() {
    let mut s = String::from("Hello");
    s.push_str(" World");
    println!("{}", s); // 将会打印Hello World

    // let value = "Error";
    // value.push_str(" Occurred"); // 将会编译失败
    // println!("{}", value);
}
```
其原因在于二者的存储方式不同，我们接下来不妨对其进行探究：对于`字符串`来说，我们在编译时即了解其内容并将其硬编码到最终的ELF可执行文件中；而对于所声明的`String`类型来说，我们需要在堆中为其开辟一定的的内存空间以承载内容。这就意味着程式在运行时对变量进行内存的动态开辟并在变量销毁时进行内存的回收。

此举在大多数高级编程语言中均较为常见，但`Rust`也采用了另一种策略：其采用`{}`代码段将流程包裹的方式实现对变量生命周期的管理。案例如下：
```rust
{
    let s = String::from("hello"); //定义变量
} // 变量销毁
```
### 内存分配: 移动、克隆与复制
我们不妨看一下这个例子：
```rust
fn main() {
    let x = 5;
    let y = x;

    println!("{}", x); // 5
    println!("{}", y); // 5

    let s1 = String::from("hello");
    // 编译错误：move occurs because `s1` has type `std::string::String`, which does not implement the `Copy` trait
    let s2 = s1;
    // 编译错误：value moved here
    println!("{}, world!", s1);
    // 编译错误：           ^^ value borrowed here after move
}
```
或许我们在使用别的编程语言开发的时候曾听说过`深拷贝`与`浅拷贝`的概念，并认为移动与克隆即分别为二者。但参考对rust所有权的理解，`String`的移动更类似于如下图的流程：
![xx](https://doc.rust-lang.org/book/img/trpl04-04.svg)
而我们如果想实现在堆上进行数据的全拷贝的话，我们不妨如下编写：
```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```
这时候可能我们对`let y = x;`这一行有了误解，为什么它没有调用`.clone()`就可以实现两个值的`复制`呢？这是由于在我们编译时由于已知整型类型的大小，所以类似的，像第一讲中我们已知的一些数据类型均可直接执行`复制`的操作。

### 所有权与函数
接下来我们再看一个例子：
```rust
fn main() {
    let s = String::from("hello");  // s 进入作用域

    takes_ownership(s);             // s 的值移动到函数里 ...
                                    // ... 所以到这里不再有效

    println!(s);                    // 抱歉，此处将编译失败

    let x = 5;                      // x 进入作用域

    makes_copy(x);                  // x 应该移动函数里，
                                    // 但 i32 是 Copy 的，所以在后面可继续使用 x

} // 这里, x 先移出了作用域，然后是 s。但因为 s 的值已被移走，
  // 所以不会有特殊操作

fn takes_ownership(some_string: String) { // some_string 进入作用域
    println!("{}", some_string);
} // 这里some_string移出作用域并, 占用的内存被释放

fn makes_copy(some_integer: i32) { // some_integer 进入作用域
    println!("{}", some_integer);
} // 这里some_integer移出作用域。不会有特殊操作
```
经过上节的介绍，我们现在对所有权是否有一点理解了呢？在后续小节中我们将进一步对`引用`与`借用`做出介绍。