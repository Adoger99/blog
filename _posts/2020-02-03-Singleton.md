---
layout: post
title: 单例模式
date: 2020-02-03
author: 邶城花语
tags: [设计模式]
comments: true
---

为了实现Singleton模式，我们有不同的方法，但是所有方法都具有以下共同概念。
- 私有构造函数，用于限制该类从其他类的实例化。
- 同一类的私有静态变量，是该类的唯一实例。
- 返回类实例的公共静态方法，这是外部世界获取单例类实例的全局访问点。

## 静态初始化
> 在静态的初始化中，在加载类时会创建Singleton类的实例，这是创建Singleton类的最简单方法，但是它存在一个缺点，即使客户端应用程序可能不使用它也会创建该实例。
```java
package com.journaldev.singleton;

public class EagerInitializedSingleton {
    
    private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();
    
    //private constructor to avoid client applications to use constructor
    private EagerInitializedSingleton(){}

    public static EagerInitializedSingleton getInstance(){
        return instance;
    }
}
```
> 如果您的单例类没有使用大量资源，则可以使用这种方法。但是在大多数情况下，都是为文件系统，数据库连接等资源创建Singleton类的getInstance。除非客户端调用该方法，否则应避免实例化。另外，此方法不提供任何用于异常处理的选项。


## 静态块初始化
静态块初始化实现与热切初始化类似，不同的是，类的实例是在提供了异常处理选项的静态块中创建的。
```java
package com.journaldev.singleton;

public class StaticBlockSingleton {

    private static StaticBlockSingleton instance;
    
    private StaticBlockSingleton(){}
    
    //static block initialization for exception handling
    static{
        try{
            instance = new StaticBlockSingleton();
        }catch(Exception e){
            throw new RuntimeException("Exception occured in creating singleton instance");
        }
    }
    
    public static StaticBlockSingleton getInstance(){
        return instance;
    }
}
```
急切的初始化和静态块初始化都在创建实例之前就创建了实例，这不是最佳实践。因此，在其他部分中，我们将学习如何创建支持延迟初始化的Singleton类。

3.延迟初始化
实现单例模式的惰性初始化方法在全局访问方法中创建实例。这是使用这种方法创建Singleton类的示例代码。
```java
package com.journaldev.singleton;

public class LazyInitializedSingleton {

    private static LazyInitializedSingleton instance;
    
    private LazyInitializedSingleton(){}
    
    public static LazyInitializedSingleton getInstance(){
        if(instance == null){
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}
```
上面的实现在单线程环境下可以很好地工作，但是对于多线程系统，如果多个线程同时位于if条件中，则可能导致问题。它将破坏单例模式，并且两个线程都将获得单例类的不同实例。在下一节中，我们将介绍创建线程安全的单例类的不同方法。


## 线程安全单例
创建线程安全的单例类的更简单方法是使全局访问方法同步，以便一次仅一个线程可以执行此方法。这种方法的一般实现类似于下面的类。

```java
package com.journaldev.singleton;

public class ThreadSafeSingleton {

    private static ThreadSafeSingleton instance;
    
    private ThreadSafeSingleton(){}
    
    public static synchronized ThreadSafeSingleton getInstance(){
        if(instance == null){
            instance = new ThreadSafeSingleton();
        }
        return instance;
    }
    
}
```
上面的实现可以很好地工作并提供线程安全性，但是由于与同步方法相关的成本，它降低了性能，尽管我们仅对可能创建单独实例的前几个线程需要它（请参阅：Java Synchronization）。为了避免每次额外的开销，使用了双重检查的锁定原理。在这种方法中，在if条件中使用了同步块，并进行了附加检查，以确保仅创建一个singleton类的实例。

以下代码片段提供了双重检查的锁定实现。

```java
public static ThreadSafeSingleton getInstanceUsingDoubleLocking(){
    if(instance == null){
        synchronized (ThreadSafeSingleton.class) {
            if(instance == null){
                instance = new ThreadSafeSingleton();
            }
        }
    }
    return instance;
}
```

## Bill Pugh Singleton的实施
在Java 5之前，java内存模型存在很多问题，并且上述方法在某些情况下会失败，在某些情况下，太多的线程试图同时获取Singleton类的实例。因此，比尔·普格（Bill Pugh）想出了另一种方法，可以使用内部静态帮助程序类来创建Singleton 类。Bill Pugh Singleton的实现是这样的；

```java
package com.journaldev.singleton;

public class BillPughSingleton {

    private BillPughSingleton(){}
    
    private static class SingletonHelper{
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }
    
    public static BillPughSingleton getInstance(){
        return SingletonHelper.INSTANCE;
    }
}
```
请注意，内部私有静态类包含单例类的实例。加载singleton类时，SingletonHelper该类不会加载到内存中，只有当有人调用getInstance方法时，该类才会加载并创建Singleton类实例。

这是Singleton类使用最广泛的方法，因为它不需要同步。我在许多项目中都使用了这种方法，而且也很容易理解和实现。

## 使用反射破坏单例模式
反射可用于销毁所有上述单例实现方法。让我们用一个示例类来看看。
```java
package com.journaldev.singleton;

import java.lang.reflect.Constructor;

public class ReflectionSingletonTest {

    public static void main(String[] args) {
        EagerInitializedSingleton instanceOne = EagerInitializedSingleton.getInstance();
        EagerInitializedSingleton instanceTwo = null;
        try {
            Constructor[] constructors = EagerInitializedSingleton.class.getDeclaredConstructors();
            for (Constructor constructor : constructors) {
                //Below code will destroy the singleton pattern
                constructor.setAccessible(true);
                instanceTwo = (EagerInitializedSingleton) constructor.newInstance();
                break;
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println(instanceOne.hashCode());
        System.out.println(instanceTwo.hashCode());
    }

}
```
当您运行上述测试类时，您会注意到两个实例的hashCode是不同的，这会破坏单例模式。反射非常强大，并在诸如Spring和Hibernate的许多框架中使用，请查阅Java Reflection Tutorial。


## 枚举辛格顿
为了通过反射来克服这种情况，Joshua Bloch建议使用Enum来实现Singleton设计模式，因为Java确保在Java程序中仅将一次枚举值实例化一次。由于Java枚举值可全局访问，因此单例也是如此。缺点是枚举类型有些不灵活；例如，它不允许延迟初始化。

```java
package com.journaldev.singleton;

public enum EnumSingleton {

    INSTANCE;
    
    public static void doSomething(){
        //do something
    }
}
```
## 序列化和单例
有时在分布式系统中，我们需要在Singleton类中实现Serializable接口，以便我们可以将其状态存储在文件系统中，并在以后的某个时间点检索它。这是一个小的单例类，它也实现了Serializable接口。

```java
package com.journaldev.singleton;

import java.io.Serializable;

public class SerializedSingleton implements Serializable{

    private static final long serialVersionUID = -7604766932017737115L;

    private SerializedSingleton(){}
    
    private static class SingletonHelper{
        private static final SerializedSingleton instance = new SerializedSingleton();
    }
    
    public static SerializedSingleton getInstance(){
        return SingletonHelper.instance;
    }
    
}
```
序列化单例类的问题在于，每当我们反序列化它时，它将创建该类的新实例。让我们用一个简单的程序看看它。
```java
package com.journaldev.singleton;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInput;
import java.io.ObjectInputStream;
import java.io.ObjectOutput;
import java.io.ObjectOutputStream;

public class SingletonSerializedTest {

    public static void main(String[] args) throws FileNotFoundException, IOException, ClassNotFoundException {
        SerializedSingleton instanceOne = SerializedSingleton.getInstance();
        ObjectOutput out = new ObjectOutputStream(new FileOutputStream(
                "filename.ser"));
        out.writeObject(instanceOne);
        out.close();
        
        //deserailize from file to object
        ObjectInput in = new ObjectInputStream(new FileInputStream(
                "filename.ser"));
        SerializedSingleton instanceTwo = (SerializedSingleton) in.readObject();
        in.close();
        
        System.out.println("instanceOne hashCode="+instanceOne.hashCode());
        System.out.println("instanceTwo hashCode="+instanceTwo.hashCode());
        
    }

}
```
上面程序的输出是：
```bash
instanceOne hashCode=2011117821
instanceTwo hashCode=109647522
```
因此，它破坏了单例模式，以克服这种情况，我们需要做的所有工作都提供了readResolve()方法的实现。
```java
protected Object readResolve() {
    return getInstance();
}
```
此后，您会注意到两个实例的hashCode在测试程序中相同。

- 单例模式限制了一个类的实例化，并确保在Java虚拟机中仅存在该类的一个实例。
- 单例类必须提供全局访问点才能获取该类的实例。
- 单例模式用于日志记录，驱动程序对象，缓存和线程池。
- Singleton设计模式还用于其他设计模式，例如Abstract Factory，Builder，Prototype，Facade等。
- Singleton设计模式在核心Java类的使用，例如java.lang.Runtime，java.awt.Desktop。