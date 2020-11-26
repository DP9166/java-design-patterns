# 迭代器模式

> 提供一种方法来顺序访问聚合对象中的一系列数据，而不暴露聚合对象的内部表示。

在看迭代器模式之前，我觉得应该来研究一段代码开开胃先。

## Java 中的 List 集合遍历

```java
public class Appetizer {

    public static void main(String[] args) {
        ArrayList<String> strings = new ArrayList<>();
        for (int i = 1; i <= 10; i++) {
            strings.add("第" + i + "个元素");
        }
        Iterator<String> iterator = strings.iterator();
        iterator.forEachRemaining(System.out::println);
    }
}
```

这段代码很简单，我们在日常开发中可能也是经常使用到。有的人可能会说了，啊不对，我用的都是

```java
for(int i = 0; i < strings.size(); i++)
```

还有的朋友说了，我直接用增强``for``循环啊

```java
for(String s : Strings)
```

是的，没错。在日常开发中，或多或少的人会用以上两种方式来进行一个列表的遍历。那这两者有什么区别呢？让我们通过编译出来的 ``class``  文件来一探究竟吧。

这里使用三种不同的写法来遍历一个 list

**java 源码文件**

```java
// 1. 使用迭代器遍历
Iterator<String> iterator = strings.iterator();
while(iterator.hasNext())
	iterator.next()

// 2. jdk 8 提供的 lambda 写法
strings.forEach(System.out::println);

// 3. 增强 for 循环写法
for (String string : strings) {
    System.out.println(string);
}

// 4. 下标遍历
for (int i = 0; i < strings.size(); i++) {
    System.out.println(strings.get(i));
}
```

**class 反编译的 java 文件内容**

```java
// 1. 使用迭代器遍历
Iterator<String> iterator = strings.iterator();
while(iterator.hasNext()) {
    iterator.next();
}

// 2. jdk 8 提供的 lambda 写法
var10001 = System.out;
strings.forEach(var10001::println);
Iterator var3 = strings.iterator();

// 3. 增强 for 循环写法
while(var3.hasNext()) {
    String string = (String)var3.next();
    System.out.println(string);
}

// 4. 下标遍历
for(int i = 0; i < strings.size(); ++i) {
    System.out.println((String)strings.get(i));
}
```

第一种和第三种可以算为同一种，所以就只剩下三种迭代方式

```java
// 1. 增强 for 循环（迭代器）
for(String s : Strings)
// 2. JDK8 的 foreach 方法
Strings.forEach()
// 3. 下标遍历
for(int i = 0; i < strings.size(); i++)
```

接下来我们用数据来看一下这 3 种方式的表现情况

**第一次**

```java
测试方法：iterator
测试数据量：1000000
花费时长（ms）：21
-----------------------------
测试方法：forEach
测试数据量：1000000
花费时长（ms）：132
-----------------------------
测试方法：增强 for 循环
测试数据量：1000000
花费时长（ms）：18
-----------------------------
测试方法：下标遍历
测试数据量：1000000
花费时长（ms）：1
-----------------------------
```

**第二次**

```java
测试方法：iterator
测试数据量：1000000
花费时长（ms）：17
-----------------------------
测试方法：forEach
测试数据量：1000000
花费时长（ms）：123
-----------------------------
测试方法：增强 for 循环
测试数据量：1000000
花费时长（ms）：12
-----------------------------
测试方法：下标遍历
测试数据量：1000000
花费时长（ms）：3
-----------------------------
```

**第三次**

```java
测试方法：iterator
测试数据量：1000000
花费时长（ms）：18
-----------------------------
测试方法：forEach
测试数据量：1000000
花费时长（ms）：119
-----------------------------
测试方法：增强 for 循环
测试数据量：1000000
花费时长（ms）：14
-----------------------------
测试方法：下标遍历
测试数据量：1000000
花费时长（ms）：2
-----------------------------
```





## 二级标题



## xxx模式类图 📌


## 代码 📃

## 总结 📚

----
<div align="center">
    <b>亦或繁星、亦或尘埃。星尘✨，为了梦想，学习技术，不要抱怨、坚持下去💪。</b>
    <p>关注<b style='color:blue'>星尘的一个朋友</b>获取源码、加群一起交流学习🤓。</p>
    <img alt='星尘的一个朋友' src='https://i.loli.net/2020/10/22/7swJfMCPrThebVI.png'/>
</div>
