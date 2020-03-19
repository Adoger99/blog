---
layout: post
title: 设计模式：可重用的面向对象软件的元素
date: 2019-06-02
author: 邶城花语
tags: [设计模式]
comments: true
toc: true
pinned: true
---
四种设计模式的帮派是《设计模式：可重用的面向对象软件的元素》一书中的23种设计模式的集合。

## GoF设计模式类型
GoF设计模式分为三类：

- 创建型模式（Creational Patterns）：涉及对象创建的设计模式。
- 结构型模式（Structural Patterns）：此类别中的设计模式涉及类结构，例如继承和组成。
- 行为型模式（Behavioral Patterns）：这种类型的设计模式提供了更好的解决方案，以实现对象之间更好的交互，如何提供解耦以及将来轻松扩展的灵活性。

## 创建型设计模式

|   模式名称    |   描述    |
|   单例模式（Singleton Pattern）    |  该模式限制类的初始化，以确保只有一个类的实例可以被创建。 |
|   工厂模式（Factory Pattern）  |  工厂模式承担了从类到工厂类实例化对象的责任。(单维度)   |
|   抽象工厂模式（Abstract Factory Pattern）    |   允许我们为工厂类创建工厂。(多维度) |
|   建造者模式（Builder Pattern）  |    逐步创建对象以及最终获取对象实例的方法。   |
|   原型模式（Prototype Pattern）    |  从另一个类似的实例创建一个新的对象实例，然后根据我们的要求进行修改。   |

## 结构型设计模式

|   模式名称    |   描述    |
|   适配器模式（Adapter Pattern）	|   在两个不相关的实体之间提供接口，以便它们可以一起工作。  |
|   组合模式（Composite Pattern）	|   当我们必须实现部分整体的层次结构时使用。例如，由其他零件（例如圆形，正方形，三角形等）制成| 的图表。    |
|   代理模式（Proxy Pattern）    |   为另一个对象提供代理或占位符，以控制对其的访问。    |
|   享元模式（Flyweight Pattern）    |   缓存和重用与不可变对象一起使用的对象实例。例如，字符串池。  |
|   外观模式（Facade Pattern）	|   在现有接口之上创建包装器接口以帮助客户端应用程序。  |
|   桥接模式（Bridge）	|   桥接设计模式用于将接口与实现分离，并从客户端程序隐藏实现细节。  |
|   装饰器模式（Decorator Pattern）	|   装饰器设计模式用于在运行时修改对象的功能。  |

## 行为设计模式

|   模式名称	|   描述    |
|   模板模式（Template Pattern）	|   用于创建模板方法存根并将某些实现步骤推迟到子类。    |
|   中介者模式（Mediator Pattern）	|   用于在系统中不同对象之间提供集中式通信介质。    |
|   责任链模式（Chain of Responsibility Pattern）	|   用于实现软件设计中的松散耦合，其中将来自客户端的请求传递给对象链以对其进行处理。    |
|   观察者模式（Observer Pattern）	|   当您对对象的状态感兴趣并希望在发生任何更改时得到通知时很有用。  |
|   策略模式（Strategy Pattern）	|   当我们对一个特定任务有多种算法，并且客户端决定在运行时使用的实际实现时，将使用策略模式。    |
|   命令模式（Command Pattern）	|   命令模式用于在请求-响应模型中实现丢失耦合。 |
|   状态模式（State Pattern）	|   当对象根据其内部状态更改其行为时，将使用状态设计模式。  |
|   访问者模式（Visitor Pattern）	|   当我们必须对一组相似类型的对象执行操作时，将使用访问者模式。    |
|   解释器模式（Interpreter Pattern）	|   定义一种语言的语法表示形式，并提供解释器来处理这种语法。    |
|   迭代器模式（Iterator Pattern	|   用于提供遍历一组对象的标准方法。    |
|   备忘录模式（Memento Pattern）	|   当我们要保存对象的状态以便以后可以恢复时，将使用memento设计模式。 |

![img](/images/designpatterns0.png)
![img](/images/designpatterns0.png)