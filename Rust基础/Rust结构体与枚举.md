# Rust结构体与枚举
本节将对Rust的结构体与枚举进行相关概念、使用案例进行介绍。
## 结构体
`结构体`与我们在第一讲[Rust数据类型](Rust数据类型.md)中所描述的`元组`较为类似，其可以将不同类型的数据整合起来。但与`元组`不同的一点是，我们可以对每一个内部变量进行名称的定义，我们可以用`C语言`中的结构体来进行理解。一个`User`类型的结构体定义如下：
```rust
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}
```
那么如何实例化一个`User`结构体的变量呢？我们不妨以`键:值`的形式将结构体内部变量进行赋值，案例如下：
```rust
let mut user1 = User { // user1在此处需要是可变类型
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};

user1.email = String::from("anotheremail@example.com"); //对user1结构体中的email变量进行赋值
```
