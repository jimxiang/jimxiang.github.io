title: "Design Patterns"
date: 2015-04-25 11:11:55
tags: 设计模式
---
## 23 Design Patterns

### Creational Patterns

#### 1.Abstract Factory:
Creates an instance of several families of classes. Provide an interface for creating families of related or dependent objects without specifying their concrete classes.   
提供一个接口，让该接口负责创建一系列相关或者相互依赖的对象，无需指定它们具体的类。

#### 2.Builder:
Separates object construction from its representation. Separate the construction of a complex object from its representation so that the same construction processes can create different representations.   
将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。

#### 3.Factory Method:
Creates an instance of several derived classes. Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

#### 4.Prototype:
A fully initialized instance to be copied or cloned. Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.   
通过复制（克隆、拷贝）一个指定类型的对象来创建更多同类型的对象。这个指定的对象可被称为“原型”对象，也就是通过复制原型对象来得到更多同类型的对象。

#### 5.Singleton:
A class of which only a single instance can exist. Ensure a class only has one instance, and provide a global point of access to it.

### Structural Patterns   

#### 6.Adapter:
Match interfaces of different classes.Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.   
适配器模式（Adapter Pattern），把一个类的接口变换成客户端所期待的另一种接口，Adapter模式使原本因接口不匹配（或者不兼容）而无法在一起工作的两个类能够在一起工作。

#### 7.Bridge:
Separates an object’s interface from its implementation. Decouple an abstraction from its implementation so that the two can vary independently.   
桥连模式：将抽象部分与实现部分分离，使它们都可以独立的变化。它是一种结构性模式，又称柄体（Handle and body）模式或者接口（Interface）模式。

#### 8.Composite:
A tree structure of simple and composite objects. Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

#### 9.Decorator:
Add responsibilities to objects dynamically.  Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

#### 10.Facade:
A single class that represents an entire subsystem. Provide a unified interface to a set of interfaces in a system. Facade defines a higher-level interface that makes the subsystem easier to use.   
外观模式：为子系统中的一组接口提供一个一致的界面， Facade模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。引入外观角色之后，用户只需要直接与外观角色交互，用户与子系统之间的复杂关系由外观角色来实现，从而降低了系统的耦合度。

#### 11.Flyweight:
A fine-grained instance used for efficient sharing. Use sharing to support large numbers of fine-grained objects efficiently. A flyweight is a shared object that can be used in multiple contexts simultaneously. The flyweight acts as an independent object in each context — it’s indistinguishable from an instance of the object that’s not shared.   
享元模式（Flyweight）：对象结构型模式运用共享技术有效地支持大量细粒度的对象。它使用共享物件，用来尽可能减少内存使用量以及分享资讯给尽可能多的相似物件；它适合用于当大量物件只是重复因而导致无法令人接受的使用大量内存。通常物件中的部分状态是可以分享。常见做法是把它们放在外部数据结构，当需要使用时再将它们传递给享元。

#### 12.Proxy:
An object representing another object. Provide a surrogate or placeholder for another object to control access to it.   
代理模式:   为其他对象提供一种代理，并以控制对这个对象的访问。

### Behavioral Patterns

#### 13.Chain of Resp:
A way of passing a request between a chain of objects. Avoid coupling the sender of a request to its receiver by giving more than one object a  chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.   
责任链模式是一种对象的行为模式。在责任链模式里，很多对象由每一个对象对其下家的引用而连接起来形成一条链。请求在这个链上传递，直到链上的某一个对象决定处理此请求。发出这个请求的客户端并不知道链上的哪一个对象最终处理这个请求，这使得系统可以在不影响客户端的情况下动态地重新组织链和分配责任。

#### 14.Command:
Encapsulate a command request as an object. Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.   
命令模式(Command Pattern)：将一个请求封装为一个对象，从而使我们可用不同的请求对客户进行参数化；对请求排队或者记录请求日志，以及支持可撤销的操作。命令模式又称为动作(Action)模式或事务(Transaction)模式。

#### 15.Interpreter:
A way to include language elements in a program. Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.   
Interpreter是一种特殊的设计模式，它建立一个解释器，对于特定的计算机程序设计语言，用来解释预先定义的文法。简单地说，Interpreter模式是一种简单的语法解释器构架。

### 16.Iterator:
Sequentially access the elements of a collection. Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.   
Iterator模式指对容器中包含的内部对象的访问委让给外部类，使用Iterator（遍历）按顺序进行遍历访问的设计模式。

#### 17.Mediator:
Defines simplified communication between classes. Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.   
Mediator模式也叫中介者模式，是由GoF提出的23种软件设计模式的一种。Mediator模式是行为模式之一，在Mediator模式中，类之间的交互行为被统一放在Mediator的对象中，对象通过Mediator对象同其他对象交互，Mediator对象起着控制器的作用。

#### 18.Memento:
Capture and restore an object's internal state. Without violating encapsulation, capture and externalize an object’s internal state so that the object can be restored to this state later.   
memento是一个保存另外一个对象内部状态拷贝的对象.这样以后就可以将该对象恢复到原先保存的状态。

#### 19.Observer:
A way of notifying change to a number of classes. Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.   
观察者模式定义了一种一对多的依赖关系，让多个观察者对象同时监听某一个主题对象。这个主题对象在状态上发生变化时，会通知所有观察者对象，使它们能够自动更新自己。

#### 20.State:
Alter an object's behavior when its state changes. Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.   
状态模式：允许一个对象在其内部状态改变时改变它的行为。对象看起来似乎修改了它的类。   
在很多情况下，一个对象的行为取决于一个或多个动态变化的属性，这样的属性叫做状态，这样的对象叫做有状态的(stateful)对象，这样的对象状态是从事先定义好的一系列值中取出的。当一个这样的对象与外部事件产生互动时，其内部状态就会改变，从而使得系统的行为也随之发生变化。

#### 21.Strategy:
Encapsulates an algorithm inside a class. Define a family of algorithms, encapsulate each one, and make them interchangeable.Strategy lets the algorithm vary independently from clients that use it.   
策略模式：定义一系列的算法,把每一个算法封装起来, 并且使它们可相互替换。本模式使得算法可独立于使用它的客户而变化。

#### 22.Template:
Defer the exact steps of an algorithm to a subclass. Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm’s structure.   
在一个方法中定义一个算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以在不改变算法结构的情况下，重新定义算法中的某些步骤。

#### 23.Visitor:
Defines a new operation to a class without change. Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.   
访问者模式的目的是封装一些施加于某种数据结构元素之上的操作。一旦这些操作需要修改的话，接受这个操作的数据结构则可以保持不变。
