---
title: "Return_to_labels"
date: 2023-06-28T16:03:10+08:00
draft: false
---

对于嵌套的返回，`return`可以添加 label 名直接指定 return 的作用域。
对于不加 label 的情况，如果使用 lambda 表达式，会导致直接 return 到外头的作用域。

```kotlin
fun foo(){
    listOf(1,2,3,4,5).forEach {
        if(it == 3)return
        print(it)
    }
    // @
    print("unreachable")
}
```

如果要运行@，也就是 只 return 出 forEach 块，
需要这样完成

```kotlin
fun foo(){
    listOf(1,2,3,4,5).forEach @a{
        if(it == 3)return@a
        print(it)
    }
    print("reachable")
}
```

或者使用默认的

```kotlin
fun foo(){
    listOf(1,2,3,4,5).forEach {
        if(it == 3)return@forEach
        print(it)
    }
    print("reachable")
}
```
