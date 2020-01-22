# 设计模式

## DRY

don't repeat yourself  dry

1. 三种代码重复的情况：

实现逻辑重复，功能语义重复，代码执行重复。实现逻辑重复而功能语义不重复的代码不违反dry原则，而功能语义重复的代码违反dry原则。代码重复执行也违反dry原则
</br>
2. 提高代码复用性

* 减少代码耦合

* 满足但一职责原则

* 模块化

* 业务与非业务逻辑分离

* 通用代码下沉

* 继承、多态、封装、抽象

* 应用模板等设计模式

## LOD

Law of Demeter

The least knowledge Principle

Each Unit should have only limited knowledge about other units,only units closely related to the current unit. Or Each unit should only talk to its frieds,don't talk to strangers.

1. 如何理解高内聚、松耦合
高内聚、松耦合是一个非常重要的设计思想，能够有效提高代码的可读性和可维护性。缩小功能改动导致的代码改动范围。高内聚用来指导类本身的设计，松耦合用来指导类鱼类之间依赖关系的设计。所谓高内聚，是指相近的功能放到同一个类中，可以集中修改。松耦合指的是类与类之间的依赖关系简单清晰。即使有依赖关系，一个类的改动也不会或者很少导致依赖类的改动

2. 如何理解迪米特法则
不该有直接依赖关系的类，不要有依赖。有依赖关系的类之间，尽量只依赖必要的接口。迪米特法则是希望减少类之间的耦合，让类独立。
