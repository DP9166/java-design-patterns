# 抽象工厂模式 🌉

> 提供一个创建产品族的接口，其每个子类可以生产一系列相关的产品。



## 概念理解（重要❗❗❗）



　　特别强调了一下抽象工厂模式的概念理解部分我觉得是非常有必要的，当然我在写下这篇文章之前看过很多优秀的博文、书籍、视频等资料对抽象工厂模式的讲解和代码示例等内容，但我发现。抽象工厂的概念被一次又一次的刷新，所以我也想表达一下自己对抽象工厂的理解。如果你和我持不同的意见，可以继续往下看，我很愿意和你一起讨论这个问题。



　　看我过之前的文章应该知道了我写的工厂模式的概念和代码实现，以及使用的时机。而抽象工厂模式的实现，等于工厂方法模式的实现。



　　那为什么会有两个模式的定义出现呢？这个问题解决了，那我们的概念就捋清楚了。我们一起来回顾一下这两个模式的定义：

1. 工厂（Factory）模式：定义一个用于创建产品的接口，由子类决定生产什么产品。
2. 抽象工厂（AbstractFactory）模式：提供一个创建产品族的接口，其每个子类可以生产一系列相关的产品。

　　我们将上面的两个模式的定义放在一起总结一下，是不是可以认为是，首先定义一个工厂接口，由子类去实现具体的工厂。如果我总结的定义你可以认可，那继续往下看。不认可忍一忍，看完再喷。让我们通过代码在理解一下。



　　**❗下面内容很关键，希望你能认真看完**。当然，不建议死扣字眼和代码，还是最初的那个誓言，学习设计模式的思想。而不是学语文。



## 一行代码 ❗



### 工厂方法模式的伪代码

```java
/**
 * 电子工厂
 */
public interface ElectronicsFactory {

    /**
     * 生产一个手机
     */
    Phone creatPhone();
}
```



```java
/**
 * 苹果手机电子工厂
 */
public class IphoneElectronicsFactory implements ElectronicsFactory{

    /**
     * 生产一个苹果手机
     */
    Phone creatPhone() {
        return new IPhone()
    };
}
```



```java
/**
 * 小米手机电子工厂
 */
public class MiPhoneElectronicsFactory implements ElectronicsFactory{

    /**
     * 生产一个苹果手机
     */
    Phone creatPhone() {
        return new MiPhone()
    };
}
```



### 让我们在看一下抽象工厂模式的伪代码

```java
/**
 * 电子工厂
 */
public interface ElectronicsFactory {

     /**
     * 生产一个手机
     */
    Phone creatPhone();
    
     /**
     * 生产一个电脑
     */
    Computer creatComputer();
}
```



```java
/**
 * 苹果电子工厂
 */
public class AppleElectronicsFactory implements ElectronicsFactory{

     /**
     * 生产一个苹果手机
     */
    Phone creatPhone() {
        return new IPhone()
    };
    
     /**
     * 生产一个苹果电脑
     */
    Computer creatComputer() {
        return new MACBook();
    };
}
```



```java
/**
 * 小米电子工厂
 */
public class MiElectronicsFactory implements ElectronicsFactory{

     /**
     * 生产一个小米手机
     */
    Phone creatPhone() {
        return new MiPhone()
    };
    
     /**
     * 生产一个小米电脑
     */
    Computer creatComputer() {
        return new MiComputer();
    };
}
```



我们通过工厂方法模式，可以得到各种各样的同类型产品（都是手机），但我们如果通过抽象工厂模式，就可以得到各种各样同个产品族的产品（一个品牌的所有产品）**而这一切的内容，仅仅相差了一行代码** 。**同样的，当抽象工厂中只有一个工厂时，它与工厂模式，没有什么不同。**



![](3-1Q1141559151S.gif)



> 工厂方法模式只考虑生产同等级的产品，抽象工厂模式将考虑多等级产品的生产，将同一个具体工厂所生产的位于不同等级的一组产品称为一个产品族（品牌）



再回到上面的两个定义：

1. 工厂（Factory）模式：**定义一个用于创建产品的接口，由子类决定生产什么产品。**
2. 抽象工厂（AbstractFactory）模式：**提供一个创建产品族的接口，其每个子类可以生产一系列相关的产品。**

抽象工厂，比如’富士康‘，细品一下，他就有多个产品族，此时你应该明白了抽象工厂的概念和与工厂方法模式的区别（相差一行代码，相差一个产品族），如果被我说晕了，我真的很抱歉，愿意的话可以与我私聊。



当然相差一行代码是为了表达两者直接的关系，在实际应用情况下还是遵循标准的命名规范。避免产生歧义，出现理解误差。



**🔔如果觉得我没说明白的请联系我，非常乐意被打扰**

``如果上面星尘表述的内容没能讲清楚抽象工厂的概念，大家不要急。继续往下看。如果我说的还不明白，给我个机会，加我微信（lvgocc）或者公众号内私聊，直到聊清楚为止。你若不会，我愿受累，为了你，我愿意执着🐱‍💻。``



### 抽象工厂类图 🖌





### 具体代码 📄

> 完整代码及单元测试结果 [https://github.com/lvgocc/java-design-patterns/tree/main/abstract-factory](https://github.com/lvgocc/java-design-patterns/tree/main/abstract-factory)





### 使用时机

- 当你想要管理一系列产品的时候，比如一个套餐？一种策略组合？看你需求，合理使用






### JDK中的抽象工厂设计模式示例

- javax.xml.parsers.DocumentBuilderFactory＃newInstance（）
- javax.xml.transform.TransformerFactory＃newInstance（）
- javax.xml.xpath.XPathFactory＃newInstance（）


# 写在最后

　　Java 设计模式专题，共23 种设计模式。内容来自个人学习理解消化的结果，谈不上教程，只望记录于此同你分享。希望能够和大家一起进步、成长。为了梦想，学习技术。如果你觉得文章对你有帮助，希望给个 star 支持一下。感激涕零。

　　[⭐https://github.com/lvgocc/java-design-patterns](https://github.com/lvgocc/java-design-patterns)

　　欢迎大家关注我的个人公众号：**星尘的一个朋友** 刚刚开始弄，希望与你一起成长！

![星尘的一个朋友](https://i.loli.net/2020/10/08/2ZVKPRsQ9TyDmki.png)