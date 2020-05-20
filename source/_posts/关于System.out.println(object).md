---
title: 关于System.out.println(object)
categories: 
- java
---

## 关于System.out.println(object)

#### 起因：
今天上java课，讲到类和对象的时候，老师演示了直接输出对象的结果，老师将其称为是“地址”，但输出的两个“地址”一个是6位16进制，一个是7位。于是心想这怎么都不可能是jvm内存地址，于是查找了资料。

#### 到底输出了什么？
首先定义一个无意义的测试类
```
public class ObjectTest {
    private String a= " ";
}
```
编写主函数如下：
```
import java.lang.*;
public class Objectout {
    public static void main(String[] args) {
        Objectout ob1= new Objectout();
        System.out.println(ob1.hashCode());
        System.out.println("hashcode的16进制表示"+Integer.toHexString(ob1.hashCode()));
        System.out.println(ob1);
    }
}
```
结果如下：
```
460141958
hashcode的16进制表示1b6d3586
Objectout@1b6d3586
````
实验得出：@后面的数字是调用Integer.toHexString(Object.hashcode())的结果。看上去我们似乎已经得到了结论，这也是大部分博客（Stackoverflow，csdn）上的回答：
> 返回的是对象的哈希值

甚至源码的第一行说明：
> Returns a hash code value for the object.

？？？</br>
我们都知道哈希值是根据哈希函数对原始索引的处理结果，目的是为了在查找时更方便的找到的目标元素。在这样的回答中，我们不能够知道其原始索引是什么。对于一个存储在jvm中的对象的索引，我们很容易想到的是对象的内存地址，但真的如此吗？

#### 为什么要哈希值？
上文已经提过，哈希表的本质是为了索引的快速。所以我们也很容易想到，如此的目的是为了方便查找到这个对象。但在jvm中，由于GC机制，对象内存地址实际是无意义的，因为在不同时期，jvm将其处理在不同的内存地址。所以在内存地址无意义的情况下，对象的唯一索引就是hashCode()。回过头来，老师今天并没有说错，这就是java对象的“地址”。只不过不是内存地址。

##### 最后
<font size="2">关于hashcode()的原始数据到底是什么，说实话，我也并不非常了解，但可以肯定的是与内存地址无关。这里提供几篇文章及实验的链接。</br>
[How does the default hashCode() work?](https://srvaroa.github.io/jvm/java/openjdk/biased-locking/2017/01/30/hashCode.html)</br>
[Memory address of variables in java](https://stackoverflow.com/questions/1961146/memory-address-of-variables-in-java/20680667#20680667)