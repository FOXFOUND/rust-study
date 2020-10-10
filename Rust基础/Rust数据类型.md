# Rust的数据类型
首先Rust具备一些标量类型：例如整数`Integer`，浮点`Float-Point`，布尔型`Boolean`和字符`Character`等。除此之外它还具备有一些复合类型：例如元组`Tuple`，数组`Array`等。

我们在这里首先对标量类型进行逐一介绍：

## Integer整数
与其他语言类似，Rust中的整数类型同样按照位数的限制提供不同取值范围的整数类型：

表格如下：
| 长度 | 有符号 | 无符号 |
| -- | -- | -- |
| 8-bit	| i8 | u8 |
| 16-bit	| i16 | u16 |
| 32-bit	| i32 | u32 |
| 64-bit	| i64 | u64 |
| 128-bit	| i128 | u128 |
| arch	| isize | usize |

每个Integer类型数值都可以明确指定其大小，这里有符号与无符号的区别在于取值范围的不同。有符号的变量可以存储-(2<sup>(n-1)</sup>)至2<sup>(n-1)</sup>-1取值范围内的数值。例如`i8`可以存储从-(2<sup>7</sup>)到2<sup>7</sup>-1范围内的数字，也就是从-128到127。无符号的`u8`变量可以存储从0到2<sup>8</sup>-1范围内的数字，也就是0至255。

这里有一个声明Integer类型变量的案例：

```rust
let guess: u16 = "42".parse().expect("Not a number!");
```

这里值的一提的是，`isize`与`usize`依赖程序运行时所处的计算机本身CPU架构，64位架构中其是64，32位架构中其是32位的。

***Rust默认设定的是`i32`类型的整型数据***

## Float-Point浮点
Rust本身也提供两种原生的浮点类型，其分别为`f32`(单精度)与`f64`(双精度,默认)。
其案例如下：
```rust
let x = 2.0; // f64
let y: f32 = 3.0; // f32
```
接下来展示如何对其进行数值运算：
```rust
// 加法
let sum = 5 + 10;

// 减法
let difference = 95.5 - 4.3;

// 乘法
let product = 4 * 30;

// 除法
let quotient = 56.7 / 32.2;

// 取余
let remainder = 43 % 5;
```
## Boolean布尔
Rust中的布尔类型分别为`true`及`false`，我们使用`bool`进行表示：
```rust
let t = true;
let f: bool = false; // 指定Boolean类型注解
```
## Character字符类型
`char`类型是Rust原生的字母类型，其用单引号进行指定：
```rust
let c = 'z';
let z = '您';
let heart_eyed_cat = '😝';
```
Rust中的`char`类型占用4个字节。

接下来我们对复合类型进行介绍：
## Tuple元组
与Python中的`tuple`所类似，其一旦声明，其长度将被固定并不会增大或减小。
案例如下：
```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
```
我们也可以使用模式匹配来对元组值进行解构，案例如下：
```rust
let tup = (500, 6.4, 1);
let (x, y, z) = tup;
println!("The value of y is: {}", y); //y的值将为6.4
```
与此同时，我们也可以使用`.`后所跟的索引直接进行访问，例如：
```
let x: (i32, f64, u8) = (500, 6.4, 1);
let five_hundred = x.0;
let six_point_four = x.1;
let one = x.2;
```

## Array数组
与元组不同，数组中的每个元素类型必须相同，其长度也为固定不变的。如果我们想使用一个<b>允许</b>增加和缩小长度的集合，请移步到后续的`vector`相关章节。

Array类型变量声明如下：
```rust
let a = [1, 2, 3, 4, 5];

let a: [i32; 5] = [1, 2, 3, 4, 5]; // 固定长度，其中i32为每个元素类型，分号后为元素个数

let a = [3; 5]; // 一种简洁的写法，其与let a = [3, 3, 3, 3, 3];等价
```
如果我们想访问数组中某一位置中的元素时，可以按照如下方式进行访问：
```rust
let a = [1, 2, 3, 4, 5];
let first = a[0];
let second = a[1];
```