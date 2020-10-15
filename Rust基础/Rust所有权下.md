# Rust所有权下
上一节中我们学习了Rust的所有权并在最后一个Demo中了解到值`String::from("hello")`的所有权在`takes_ownership`中被变量`some_string`剥夺，因此当`takes_ownership`方法退出后，`s`变量失去了对该值的所有权，进而`s`变量被销毁。

那么我们该如何对方法内部进行值传递呢？请参考如下demo：
```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize { //通过引用的方式，将值传递进方法内部
    s.len()
}
```
这其中的`&s1`语法即为`s1`变量所创建的`引用`，该引用并非`s1`所有，因此在方法结束后其所指向的值将不会被删除。或者我们换一种说法，当函数使用引用作为参数而非实际值的时候，我们不需返回这些值即可将所有权归回，因为我们从未使用该值的所有权。在这里我们不妨再看一个案例：
```rust
fn main() {
    let s = String::from("hello");

    change(&s);
}

fn change(some_string: &String) {
    some_string.push_str(", world"); // 尝试修改借用值，但此处将编译失败
}
```
这个案例向我们展示，不可变类型变量的引用是无法修改的。我们如果进行可变引用的话，就可以实现对某一变量的修改了，案例如下：
```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
    
    s.push_str("!!!");
    println!("{}" , s); // hello, world!!!
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```
到此，我们就完成了对引用与借用的学习。在下一小节中我们将对Rust的自定义结构体进行学习