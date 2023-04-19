# rustup

rustup是一个rust安装程序，同时也是它的一个版本管理程序。

### 安装与卸载

安装和卸载可参照官网给的[安装教程](https://www.rust-lang.org/zh-CN/tools/install)。安装后，会将rustc和cargo一同安装。

## rustc

`rustc`是 Rust 编程语言的编译器，由项目本身提供。

### Cargo

cargo是一个rust包管理器，负责下载rust包，编译包，其中也是用到了rustc编译。

创建一个项目：
``` bash
cargo new project
```

运行项目：
``` bash
cargo run
```

构建项目：
``` bash
cargo build
```


验证项目中代码正确性：
```bash
## 快速的检查一下代码能否编译通过。因此该命令速度会非常快，能节省大量的编译时间
cargo check
```

cargo使用指南：
https://course.rs/cargo/intro.html

1. cargo run 实际上做了两个工作，分别是项目编译和运行项目。
2. 默认情况下，使用cargo run和cargo build 都是使用debug模式，编译器不会做任何优化，如果想要高性能代码，则可以在命令后面加选项 `-- release`


# 开发工具

采用vscode + vscode的rust-analyzer插件进行开发。
额外插件推荐：
1.  `Even Better TOML`，支持 .toml 文件完整特性
2.  `Error Lens`, 更好的获得错误展示
3.  `One Dark Pro`, 非常好看的 VSCode 主题
4.  `CodeLLDB`, Debugger 程序

# cargo镜像

cargo默认使用[crates.io](https://crates.io/)地址下载依赖包，但因为是外网，所以总需要一些国内镜像。
可以采用如下方式解决：
``` toml
[source.crates-io] 
replace-with = 'ustc' 

[source.ustc] 
registry = "git://mirrors.ustc.edu.cn/crates.io-index"
```
首先，创建一个新的镜像源 `[source.ustc]`，然后将默认的 `crates-io` 替换成新的镜像源: `replace-with = 'ustc'`。此地址是科大的地址