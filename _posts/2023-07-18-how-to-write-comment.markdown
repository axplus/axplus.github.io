---
layout: post
title: "如何（给 fp 代码）写注释"
date: 2023-07-18 05:55:32 +0800
categories: developing
---

by yijie

## 如何写注释

### 写什么

注释应该提供代码没有的信息。

1. 最好在函数开始的地方写上一个注释，明确解释用了什么算法
2. 在 module interface 中加入对 **用法** 的注释（切记不是对函数本身的注释）

### 以及不要写什么

当然，如果代码平平无奇，没有什么难的，那就不写。另外还要注意几点：

1. 避免在函数中写注释（函数语言特有的）
2. 避免写 nocuous 注释

nocuous comment 的定义有好几种，特别要说其中一种：trivial information，这种注释特别喜欢出现在某一类语言语言中，虽然没用，但是却写的煞有介事。另外我们戏称为 kpi 注释。

```ocaml
(*
  Function print_lambda:
  print a lambda-expression given as argument.
  Arguments: lam, any lambda-expression.
  Returns: nothing.
  Remark: print_lambda can only be used for its side effect.
*)
let rec print_lambda lam =
  match lam with
  | Var s -> printf "%s" s
  | Abs l -> printf "\\ %a" print_lambda l
  | App (l1, l2) ->
     printf "(%a %a)" print_lambda l1 print_lambda l2
```

## fp 注释的特殊性

和传统的 imperative 语言注释不同，函数语言中的代码即解释（注释）：

```
函数 = 另外一种解释
```

是不是跟写编译器时候的 bnf 很像呢。

所以对函数语言的大部分注释，都是“脱裤子放屁”。

---

原文

> ## OCaml Programming Guidelines

> ### How to Comment Programs

> Don't hesitate to comment when there's a difficulty. If there's no difficulty, there's no point in commenting. It merely creates unnecessary noise.

> Avoid comments in the bodies of functions. Prefer one comment at the beginning of the function that explains how a particular algorithm works. Once more, if there is no difficulty, there is no point in commenting.

> ### Avoid Nocuous Comments

> A nocuous comment is a comment that does not add any value, e.g., trivial information. The nocuous comment is evidently not of interest; it is a nuisance that uselessly distracts the reader. It is often used to fulfill some strange criteria related to the so-called software metrology, i.e., the ratio number of comments / number of lines of code. This arbitrary ratio has no theoretical or practical interpretation.

> Absolutely avoid nocuous comments.

> An example of what to avoid, the following comment uses technical words and is thus masquerading as a real comment, but it has no additional information of interest:

> ```ocaml
> (*
>   Function print_lambda:
>   print a lambda-expression given as argument.
>
>   Arguments: lam, any lambda-expression.
>   Returns: nothing.
>
>   Remark: print_lambda can only be used for its side effect.
> *)
> let rec print_lambda lam =
>   match lam with
>   | Var s -> printf "%s" s
>   | Abs l -> printf "\\ %a" print_lambda l
>   | App (l1, l2) ->
>      printf "(%a %a)" print_lambda l1 print_lambda l2
> ```

> ### Usage in Module iIterface

> The function's usage must appear in the module's interface that exports it, not in the program that implements it. Choose comments as in the OCaml system's interface modules, which will subsequently automatically extract the documentation of the interface module if necessary.
