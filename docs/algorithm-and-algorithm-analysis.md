# 算法与算法分析

## 一、算法

算法是对特定问题求解步骤的一种描述。

* **有穷性**，一个算法必须总是在执行有穷步之后结束，且每一步都可在有穷时间内完成
* **确定性**，算法中每一条指令必须有明确的含义，不会产生二义性，并且在任何条件下，算法只有唯一一条执行路径，即对相同的输入只能得出相同的输出
* **可行性**，算法中描述的操作都是可以通过已经实现的基本运算执行有限次来实现的
* **输入**，一个算法有 0 个或多个输入，取自于某个特定的对象的集合
* **输出**，一个算法有 1 个或多个输出，输出是同输入有着某些特定关系的量

## 二、算法设计的要求

* **正确性**，算法应当满足具体问题的需求。四层标准，一般以 c 为准
  * a. 不含语法错误
  * b. 对于几组输入数据能够得出满足规格说明要求的结果
  * c. 对于精心选择的典型、苛刻而带有刁难性的几组输入数据能够得出满足规格说明要求的结果
  * d. 对于一切合法的输入数据都能产生满足规格说明要求的结果（一般难以实现）
* **可读性**，算法主要是为了人的阅读与交流，其次才是机器执行。可读性好有助于人对算法的理解。
* **健壮性**，当输入数据非法时，算法也能适当做出反应或进行处理，而不是产生莫名其妙的结果。并且处理出错的方法应是返回一个表示错误或错误性质的值，而不是打印错误信息或异常，并中止程序的执行，以便在更高抽象层次上进行处理
* **效率与低内存储量需求**，效率是指算法执行的时间，存储量需求指算法执行过程中所需要的最大存储空间。

## 三、算法效率的度量

算法执行的时间需通过依据该算法编制的程序在计算机上运行时所消耗的时间来度量。

* **事后统计**，计算运行时间开始与结束的差值，有两个缺陷
  * 必须先运行依据算法编制的程序
  * 所的时间的统计量依赖于计算机的硬件、软件等环境因素，有时容易掩盖算法本身的优劣
* **事前分析估算**，消耗时间取决于下列因素
  * 依据的算法选用何种策略
  * 问题的规模
  * 书写程序的语言，对于同一种算法，实现语言的级别越高，执行效率就越低
  * 编译程序所产生的机器代码的质量
  * 机器执行指令的速度

算法中基本操作重复执行的次数是问题规模 $n$ 的某个函数 $f\(n\)$，算法的时间度量记作：

$$
T(n) = O(f(n))
$$

表示岁问题规模 $n$ 的增大，算法执行时间的增长率和 $f\(n\)$ 的增长率相同，称作算法的渐近时间复杂度，简称**时间复杂度**。

被称作问题的基本操作的原操作应是其重复执行次数和算法的执行时间成正比的原操作，多数情况下它是最深层循环内的语句中的原操作，它是执行次数和包含它的语句的频度相同。语句的**频度**指的是该语句重复执行的次数。

分为常量阶 $O\(1\)$、线性阶 $O\(n\)$、平方阶 $O\(n^2\)$、对数阶 $O\(log n\)$、指数阶 $O\(2^n\)$、排列阶 $O\(n!\)$

```c
//常量阶
{ ++x; s = 0;}

//线性阶，线性阶也可以当做是常量阶
for (i=1; i<=n; ++i){ ++x; s+=x; }

//平方阶
for (j=1;j<=n;++j){
  for (i=1; i<=n; ++i){ ++x; s+=x; }
}
//对数阶
for (i=1;i<=n;i*=2){ y*=x; }
```

* 排列阶和指数阶随问题规模增长过快，一般不宜使用
* 如果算法的执行有多种可能的操作顺序，则求其平均时间复杂度
* 如果无法求取平均时间复杂度，则采用最坏情况下的时间复杂度

## 四、算法的存储空间需求

以空间复杂度作为算法所需存储空间的量度，记作：

$$
S(n) = O(f(n))
$$

