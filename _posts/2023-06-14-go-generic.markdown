---
layout: post
title: "10 分钟掌握 Go 泛型"
date: 2023-06-14 05:55:32 +0800
categories: developing
---

by yijie

最近都在研究类型系统，比如 Haskell, OCaml, Swift, Rust。
还有 C++，都有很强大的类型系统。
昨天突发奇想，想看看 Go 1.18 新增的泛型类型系统如何。
（之前在互联网公司使用很长一段时间的 Go，之前的 Go 的类型系统一直是基于 interface{} 动态派发的，直到 2022 年推出的 1.18，有了泛型，interface 被重新定义了。）

## Go 泛型大纲

（只写大纲，细节的东西去官网自己看了。我很喜欢的一句话“这不重要”。）

### 重新定义 interface

一切的基础：interface 由动态匹配转变为静态约束了。

### 三种 泛型语法

定义 struct 和 receiver

```go
type S[T constraint] struct {}
func (S[T]) Receive() {}
```

定义 interface

```go
type I[T constraint] interface {}
```

定义 function

```go
func F[T constraint] Foo(v T) {}
```

### 约束

约束语法的本质是 interface。内置的有 any 和 comparable 两种。还有官方做了一个 constraints 包。

### 类型推断

Go 目前仅支持 func 的类型推断，其他的 generic struct 和 generic interface 在使用的时候都要提供类型参数。这个行为跟早期的 C++ 一样。

## 展望

### 更多泛型

Receiver 不能再有自己的泛型参数了。但这在实际项目中还是挺有用的，例如

```go
type Origin[T any] struct {
    Value T
}

func (o Origin[T]) CompareTo[Y any](other Origin[Y]) bool {}
```

这样的语法是不能编译的。

当前的匿名的方法、结构、interface 都不能用泛型参数。确实有点不方便。

### 更强大的类型推断

Go 仅对 func 进行类型推断是不够的。其他静态类型语言的类型推断是很强大的，甚至是很快速的，比如 OCaml, Swift（Haskell, Rust 也非常强大，但是我写得不多，不妄言）。

### interface 类型擦除

Go 不支持 interface 泛型参数擦除。

Swift 的 protocol(associatetype) 类型擦除堪称完美，也非常有用。

### 默认实现

Go 不支持方法的默认实现。这其实跟泛型关系不是很大，虽然可以定义一个 interface，但是不能给 interface 定义一个默认实现，如果写过 swift, rust 就知道我在说什么的。

#### 类型组合推断

举个 swift 的例子：

```swift
protocol 飞机 {
    func 起飞()
}

protocol 汽车 {
    func 遛一遛()
}

extension 汽车 where Self: 飞机 {
    var 飞行汽车: Bool {true}
}
```

这个功能挺有用的，特别在进行复杂数据结构的推理上。不过也许 Go 不打算做这么复杂吧。

## 参考

-   https://en.wikipedia.org/wiki/Type_system
-   https://go.dev/doc/tutorial/generics

---

以上内容来源于我的 [<img src="https://is1-ssl.mzstatic.com/image/thumb/Purple126/v4/71/ed/be/71edbecc-f75b-99ee-d3ab-770b6eb0d430/AppIcon-1x_U007emarketing-0-7-0-85-220.png/460x0w.webp" height="40"> d2outliner](https://apps.apple.com/us/app/d2outliner/id6446220539) 大纲笔记。
