---
title: 【PlantUML系列】（一）时序图
date: 2022-02-28 20:44:09
tags: plantUML 时序图
categories: 计算机
---

# 【plantUML 系列】（一）时序图

> plantUML 是一种可以方便快捷地绘制出各种逻辑图的开源语言。它支持绘制时序图、用例图、类图、对象图、活动图、组件图、部署图、状态图、定时图，同时还支持绘制 JSON Data、YAML Data、Network diagram、线框图形界面、架构图、SDL、等非 UML 图。
> 笔者因为想要在自己的 markdown 笔记中嵌入一些图表以更好地理解所学内容，故找到了这样的一个开源语言，博客内容即为笔者学习过程中的感悟，若有错误的地方可去本博客托管的[github 仓库](https://github.com/transparent-reid/MyBlog)下提 issue。

## 简单示例

{% plantuml %}
Alice -> Bob: Hi，Bob!
Alice <-- Bob: Hi,Alice!
{% endplantuml %}

```plantumlcode
@startuml
Alice -> Bob: Hi，Bob!
Alice <-- Bob: Hi,Alice!
@enduml
```

其中`->`代表实线，`-->`代表虚线。冒号后借箭头上想要写的注释。

## 声明参与者

使用`participant`关键字来声明一个参与者。
当然还有其他的一些关键字可以声明不同种类的参与者，这会改变参与者在图上的外观。
其中的关键字有：

- actor
- boundary
- control
- entity
- database
- collections
- queue

它们在图上会呈现出的样子：

{% plantuml %}
participant Participant as Foo
actor Actor as Foo1
boundary Boundary as Foo2
control Control as Foo3
entity Entity as Foo4
database Database as Foo5
collections Collections as Foo6
queue Queue as Foo7
Foo -> Foo1: To actor
Foo -> Foo2: To boundary
Foo -> Foo3: To control
Foo -> Foo4: To entity
Foo -> Foo5: To database
Foo -> Foo6: To collections
Foo -> Foo7: To queue
{% endplantuml %}

```plantumlcode
@startuml
participant Participant as Foo
actor Actor as Foo1
boundary Boundary as Foo2
control Control as Foo3
entity Entity as Foo4
database Database as Foo5
collections Collections as Foo6
queue Queue as Foo7
Foo -> Foo1: To actor
Foo -> Foo2: To boundary
Foo -> Foo3: To control
Foo -> Foo4: To entity
Foo -> Foo5: To database
Foo -> Foo6: To collections
Foo -> Foo7: To queue
@enduml
```

关键字`as`用于重命名参与者，相当于给这些参与者起了一个“小名”，后面可以用这个“小名”来表示该参与者。

可以使用 RGB 或者颜色名修改参与者的背景颜色。
比如：

{% plantuml %}
actor Bob #red
{% endplantuml %}

```plantumlcode
@startuml
actor Bob #red
@enduml
```

可以用`order`关键字自定义顺序来打印参与者。

{% plantuml %}
participant 最后 order 30
participant 中间 order 20
participant 首个 order 10
{% endplantuml %}

```plantumlcode
@startuml
participant 最后 order 30
participant 中间 order 20
participant 首个 order 10
@enduml
```

## 在参与者中使用非字母符号

可以使用引号定义参与者，还可以用关键字 as 给参与者定义别名。

{% plantuml %}
Alice -> "Bob()": Hello
"Bob()" -> "This is a very \n long sentence.": OK
{% endplantuml %}

```plantumlcode
@startuml
Alice -> "Bob()": Hello
"Bob()" -> Long as "This is a very \n long sentence.": OK
@enduml
```

有一个很有趣的现象：

```plantumlcode
@startuml
Alice -> "Bob()": Hello
"Bob()" -> Long as "This is a very \n long sentence.": OK
@enduml
```

如果把`Alice -> "Bob()"`改为`Alice -> "Bob()" as Bob`则会变成下面这样：

{% plantuml %}
Alice -> "Bob()" as Bob: Hello
"Bob()" -> "This is a very \n long sentence.": OK
{% endplantuml %}

如果将其改为`Bob as "Bob()"`也会变成这样。貌似 Bob 和“Bob()”不是同一个参与者一样。
我的猜想是，可能带引号的定义无法作为参数传递，用常规的变量定义方法才能正常传递。由此可知，带引号的定义应该算是一种临时的定义方法，一个参与者只能使用一次。

## 给自己发消息

参与者可以给自己发消息。
例如：

```plantumlcode
@startuml
Alice -> Alice: Something...
@enduml
```

## 修改箭头样式

修改箭头样式的方式有以下几种：
具体在实例中对比参照吧。

{% plantuml %}
Bob ->x Alice
Bob -> Alice
Bob ->> Alice
Bob -\ Alice
Bob \\- Alice
Bob //-- Alice

Bob ->o Alice
Bob o\\-- Alice

Bob <-> Alice
Bob <->o Alice
{% endplantuml %}

```plantumlcode
@startuml
Bob ->x Alice
Bob -> Alice
Bob ->> Alice
Bob -\ Alice
Bob \\- Alice
Bob //-- Alice

Bob ->o Alice
Bob o\\-- Alice

Bob <-> Alice
Bob <->o Alice
@enduml
```

按顺序从上到下对比参照。

## 修改箭头颜色

和修改参与者的背景颜色相似。

{% plantuml %}
Bob -[#red]> Alice
Alice --[#0000FF]>Bob
Alice -[#0000FF]->Bob
{% endplantuml %}

```plantumlcode
@startuml
Bob -[#red]> Alice
Alice --[#0000FF]>Bob
Alice -[#0000FF]->Bob
```

注意第二条和第三条的区别，这两个都可以。

## 页面标题，页眉，页脚

使用`title`关键字增加标题
使用`header`关键词增加页眉
使用`footer`关键词增加页脚

{% plantuml %}
header Page Header
footer Page %page% of %lastpage%

title Example Title

Alice -> Bob

{% endplantuml %}

```plantumlcode
@startuml
header Page Header
footer Page %page% of %lastpage%

title Example Title

Alice -> Bob

@enduml
```

## 分割示意图

关键字`newpage`用于把一张图分割成多张。
暂时没啥用，需要的自己去查吧。

## 组合消息

我们可以通过以下关键词来组合消息：

- alt/else
- opt
- loop
- par
- break
- critical
- group,后面紧跟着消息内容

可以在标头(header)添加需要显示的文字。
关键字`end`结束分组。
分组也可以嵌套使用。

{% plantuml %}
Alice -> Bob: 认证请求

alt 成功情况
Bob -> Alice: 认证接收
else 某种失败情况
Bob -> Alice: 认证失败
group 我自己的标签
Alice -> Log: 开始记录攻击日志
loop 1000 次
Alice -> Bob: DNS 攻击
end
Alice -> Log: 结束记录攻击日志
end
else 另一种失败
Bob -> Alice: 请重复
end
{% endplantuml %}

```plantumlcode
@startuml
Alice -> Bob: 认证请求

alt 成功情况
    Bob -> Alice: 认证接收
else 某种失败情况
    Bob -> Alice: 认证失败
    group 我自己的标签
    Alice -> Log: 开始记录攻击日志
        loop 1000次
            Alice -> Bob: DNS攻击
        end
    Alice -> Log: 结束记录攻击日志
    end
else 另一种失败
    Bob -> Alice: 请重复
end
@enduml
```

## 给消息添加注释

我们可以通过在消息后面添加`note left`或者`note right`关键字来给消息添加注释。
你也可以通过使用`end note`来添加多行注释。
{% plantuml %}
Alice -> Bob: hello
note left: this is a first note

Bob -> Alice: ok
note right: this is another note

Bob -> Bob: I am thinking
note left
a note
can also be defined
on several lines
end note
{% endplantuml %}

```plantumlcode
@startuml
Alice -> Bob: hello
note left: this is a first note

Bob -> Alice: ok
note right: this is another note

Bob -> Bob: I am thinking
note left
a note
can also be defined
on several lines
end note
@enduml
```

也可以使用`note left of`，`note right of`，或`note over`在节点的相对位置放置注释。
当然也可以改变颜色啦~
{% plantuml %}
participant Alice
participant Bob
note left of Alice #aqua
This is displayed
left of Alice
end note

note right of Alice: This is displayed right of Alice.

note over Alice: This is displayed over Alice.
{% endplantuml %}

```plantumlcode
@startuml
participant Alice
participant Bob
note left of Alice #aqua
This is displayed
left of Alice
end note

note right of Alice: This is displayed right of Alice.

note over Alice: This is displayed over Alice.
@enduml
```

## 改变备注框的形状【hnote 和 rnote】

使用`hnote`和`rnote`两个关键字修改备注框的形状：

- `hnote`代表六边形
- `rnote`代表正方形

## 在多个参与者添加备注【across】

可以直接在所有参与者之间添加备注，格式是：

- `note across`: 备注描述

## 在同一级对齐多个备注【/】

使用/可以在同一级对齐多个备注。
没有/备注不是对其的，像之前的例子中一样。
使用/可以对齐。
{% plantuml %}
note over Alice: Alice
/ note over Bob: Bob
Bob -> Alice: hello
{% endplantuml %}

```plantumlcode
@startuml
note over Alice: Alice
/ note over Bob: Bob
Bob -> Alice: hello
@enduml
```

## 分隔符

可以通过使用`==`关键字将图表分割为多个逻辑步骤。
{% plantuml %}
== 初始化 ==
Alice -> Bob: 认证请求
Bob -> Alice: 认证响应

== 重复 ==
Alice -> Bob: 认证请求
Alice <- Bob: 认证响应

{% endplantuml %}

```plantumlcode
@startuml
== 初始化 ==
Alice -> Bob: 认证请求
Bob -> Alice: 认证响应

== 重复 ==
Alice -> Bob: 认证请求
Alice <- Bob: 认证响应
@enduml
```

## 延迟

你可以使用`...`来表示延迟，并且还可以给延迟添加注释。
{% plantuml %}
Alice -> Bob: 认证请求
...
Bob --> Alice: 认证响应
...5 分钟后...
Bob -> Alice: 再见
{% endplantuml %}

```plantumlcode
@startuml
Alice -> Bob: 认证请求
...
Bob --> Alice: 认证响应
...5分钟后...
Bob -> Alice: 再见
@enduml
```

以上基本可以绘制出大部分图表了，想要进阶的 uu 们可以去[官网](https://plantuml.com/zh/)进一步查找用户手册。
