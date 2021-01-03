# Rust结构体
本节将对Rust的结构体进行相关概念、使用案例进行介绍。
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
同时，Rust允许我们以隐式的方式在某一方法中直接返回一个自定义的Struct结构体：
```rust
fn create_user(email: String, username: String) -> User {
    User {
        // email: email,
        // username: username,
        // 重复email和username字段名称看起来有些乏味
        // 因此我们可以简写成如下形式：
        email,
        username,
        active: true,
    }
}
```
## 结构体方法
对于结构体内部来说，我们可以借助`impl`关键字进行方法的声明，案例如下：
```rust
#[derive(Debug)]
struct User {
    email: String,
    username: String,
    id: i32,
}

impl User {
    fn value(&self) -> String {
        format!("{} {} {}", self.id, &self.email, &self.username)
    }

    fn equal(&self, other: &User) -> bool{
        self.id == other.id
    }
}

fn main() {
    let user1 = User {
        email: String::from("example1.com"),
        username: String::from("test_1"),
        id: 1,
    };

    let user2 = User{
        email: String::from("example2.com"),
        username: String::from("test_2"),
        id: 2,
    };

    println!("{}" , user1.value());
    println!("{}" , user2.value());
    println!("ID Equal: {}" ,user1.equal(&user2));
    println!("Exit");
}
```
在这里需要注意一点，如果希望在`impl`方法中使用自身或某一结构体内部数据的话，需要以借用的方式进行入参。