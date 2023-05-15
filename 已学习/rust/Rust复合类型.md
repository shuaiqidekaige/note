### 切片（slice）
对 `String` 类型中某一部分的引用

```rust
let s = String::from("hello world"); 
let hello = &s[0..5]; // 获取的是hello
let world = &s[6..11];
```
1. 使用方括号包括的一个序列：**[开始索引..终止索引]**
2. 注意：这是一个右半开区间。
3. 在切片数据结构内部会保存开始的位置和切片的长度，其中长度是通过 `终止索引` - `开始索引` 的方式计算得来的
4. 字符串切片类型标识为：&str， 整数切片：&[i32]
5. 切片的索引是通过字节数来的

### 字符串
1. 字符串编码为utf-8
2. 字符串类型有两种，一种是str，属于硬编码进可执行文件，无法被修改。一种是String，是一个可增长、可改变且具有所有权的 UTF-8 编码字符串。

#### 转化String和&str
String转为&str，直接使用&，或者使用[开始索引...结束索引]


#### 字符串（String）索引
rust不允许使用字符串索引，因为rust字符串不能保证获取到的字符串一定有效。


#### 操作字符串（String）
1. push: 追加字符
2. push_str： 追加字符串
3. insert： 插入字符
4. insert_str: 插入字符串
追加和插入必须是String，且必须是mut

1. replace： 替换字符串
2. replacen：替换字符串，可选取替换个数
如上方法可适用于 `String` 和 `&str` 类型

1. replace_range： 替换某一个范围
仅适用于String，切必须是mut

1. pop：删除最后一个字符，并且返回
2. remove：删除并返回字符串中指定位置的字符
3. truncate：删除字符串中从指定位置开始到结尾的全部字符
4. clear： 清空字符串
仅适用于String，切必须是mut

#### 连接字符串
1. String使用+ 或者 += 必须右边的参数是一个Slice类型
2. format!：适用于 `String` 和 `&str`
```Rust
fn main() { 
  let s1 = "hello"; 
  let s2 = String::from("rust"); 
  let s = format!("{} {}!", s1, s2);
  println!("{}", s); 
}
```

#### 字符串转移
转义通过\方式输出ASCII 和 Unicode 字符。
1. 通过 \ + 字符的十六进制表示，转义输出一个字符。
2. \\u 可以输出一个 unicode 字符

通过\\\\方式保持字符串不转义

#### 操作UTF-8字符串
通过charts方法和bytes方法可以获取字符串的字符集合和字节集合，适用于&str（字符串字面量）和String

### 元组
元组是由多种类型组合到一起形成的，且长度固定，顺序固定。
```Rust
fn main () {
  let tup:(i32,i32,i32) = (1,2,3);
  // 模式匹配解构
  let (x,y,z) = tup;
  let x = tup.0
}
```
如何获取其中某一项数据：
1. 通过模式匹配（解构形式）
2. 通过操作符。

### 结构体
#### 结构体定义
``` Rust
struct User {
  name: String,
  age: i32,
}
```
结构体由 struct 关键字定义，每一个字段拥有其字段名和类型申明。

#### 结构体实例
``` Rust
struct User {
  name: String,
  age: i32,
}

let user = User {
  name: String::from("csk"),
  age: 2,
}
```
1.  初始化实例时，**每个字段**都需要进行初始化
2.  初始化时的字段顺序**不需要**和结构体定义时的顺序一致

#### 如何访问结构体
通过 。操作符访问，如：
``` Rust
let user = User {
  name: String::from("csk"),
  age: 2,
}

let mut user2 = User {
  name: String::from("csk"),
  age: 2,
}


const name = User.name;

user2.name = String::from("csk2")

```
1.  如果需要修改的话，还需要修饰符mut，标记其可变。⚠️注意（rust不支持某个字段可变，只能标记整个结构体可变）。
2.  跟javascript一样，rust支持缩写,如果值和结构体名称相同，可以缩写。
3. 结构体支持..符号，支持覆盖写法，但必须写在尾部，且会涉及所有权转移。
```Rust
  
let user2 = User { 
  email: String::from("another@example.com"), 
  ..user1
};
```


#### 元祖结构体
结构体必须要有名称，但是结构体的字段可以没有名称，这种结构体长得很像元组，因此被称为元组结构体。
``` Rust
struct Color (i32, i32, i32)
```

#### 单元结构体
如果你定义一个类型，但是不关心该类型的内容, 只关心它的行为时，类似单元类型
``` Rust
struct A;
```

#### 结构体中所有权
结构体内部字段的值通常都是各自拥有自己的所有权，而不是使用引用类型，如果要用，就需要引入生命周期。

#### 打印结构体
1. 结构体较为复杂，打印过程中需要实现DIsplay特征，可以使用{:?}或者{:#?}这种方式实现Display特征。
2. 实现Debug特征， 可以使用 #[derive(Debug)] 方式实现。
3. 使用dg!宏打印，但也需要实现Debug特性。