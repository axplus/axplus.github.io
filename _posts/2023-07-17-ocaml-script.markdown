---
layout: post
title: "用 OCaml 取代 Python 来写 Shell 脚本"
date: 2023-07-17 05:55:32 +0800
categories: developing
---

by yijie

当前我用 Python 为自己的项目写各种 shell 脚本，比如版本管理、构建、打包等等。

## 不想用 Python 来写小工具

虽好，但

1. Python 需要携带一个大大的 Runtime
2. 多版本弄得我狼狈不堪，必须小心再小心
3. 动态类型，在写比较复杂的脚本时很容易犯低级错误

所以我需要一个简单，但能克服上述问题的工具。选型如下

-   go：工作中使用 go，有点审美疲劳了，分不清小脚本和项目代码的界限。而且 go 默认不使用异常来报告错误，对于临时程序非常不友好。
-   swift
-   c
-   c++
-   javascript+node
-   bash
-   haskell
-   选择 Ocaml

## ocaml 有如下优点，非常适合于在工程中使用：

-   因为不纯，所以和 shell 交互来去自由（至少不用像 haskell 那样一层又一层的套娃）
    -   幸运的是 ocaml 被设计为一种混合语言
        -   你可以用 imperative 方式把 ocaml 当成一个函数化的 c
        -   或者可以用 oop 的方式把 ocaml 当成一个简化的 c++ 或者 swift
-   非常有安全感：静态类型、类型推断，不失灵活性的同时，多了类型检查
-   不一定要安装 runtime、不需要担心版本的问题：可以编译成 bytecode 或者 native code，甚至可以 cross-compile
-   同时支持异常和返回方式的错误处理，非常方便
-   强大的 adt 和 gadt，虽然很强大，但是很简单也很方便
-   换了一种思考、解决问题的方式
-   因为 ocaml 的理论基础扎实、再加上小众，所以 opam 中的 module 质量很高、版本充分迭代，相同功能的 module 少，对选择困难症很有好处
    -   不像很多 pip, gomod 一眼就能看到 bug

## Ocaml 的缺点

-   文档中显示 ocaml 4.10 之前对 string/char 类型并不支持 unicode，之后应该会有所改进，这个具体找找文档
-   库的文档分布比较散乱，不像 python 有一个统一的地方、统一的格式
-   似乎没有 built-in 支持 doctest
    -   python doctest 是我念念不忘的特性，很多 one-file-script 直接在文件中写测试就好了，多方便
-   OCaml Platform 插件一直崩溃，谁告诉我怎么解决啊
-   ocaml 中的资源清除方式比较不统一：因为没有 finally 也没有 defer，更没有 noexcept，所以无法保证异常安全，有一些做法是使用闭包 try ... with ... 后，进行释放，但是看起来比较不“标准“
