# 第5章 对象改值

## 5.1 就地改值

描述想要修改的数值，然后用赋值符号`<-`更改值。R会在原始对象内部对这些值进行修改。比如：

```r
> vec <- c(1,1,1,1,1,1)
> vec
[1] 1 1 1 1 1 1
> vec[1] <- 100
> vec
[1] 100   1   1   1   1   1
```

当然也可以批量改值。比如：

```r
> vec[c(1,3,5)] <- c(100,100,100)
> vec
[1] 100   1 100   1 100   1
```

也可以创建一个原先对象中不存在的新值，R会自动延伸对象的长度以适应新值。比如：

```r
> vec[8] <- 0
> vec
[1] 100   1 100   1 100   1  NA   0
```

这为数据集添加新变量提供了一种好方法。比如：

```r
> deck$new <- 1:52
> deck
    face     suit value new
1   king   spades    13   1
2  queen   spades    12   2
3   jack   spades    11   3
4    ten   spades    10   4
5   nine   spades     9   5
6  eight   spades     8   6
7  seven   spades     7   7
8    six   spades     6   8
```

## 5.2 逻辑值取子集

### 5.2.1 逻辑测试

R的逻辑运算符：

| 运算符 | 语法 | 判别 |
| :---: | :---: | :---: |
| `>` | `a > b` | a是否大于b？ |
| `>=` | `a >= b` | a是否大于或者等于b？ |
| `<` | `a < b` | a是否小于b？ |
| `<=` | `a <= b` | a是否小于或者等于b？ |
| `==` | `a == b` | a是否等于b？ |
| `!=` | `a != b` | a是否不等于b？ |
| `%in%` | `a %in% c(a,b,c)` | c\(a,b,c\)中是否包含a？ |

如果这些运算符用于向量之间的判别，R会将两个向量中的每个元素一一比对。

```r
> 1 > 2
[1] FALSE
> 1 > c(0,1,2)
[1]  TRUE FALSE FALSE
> c(0,1,2)==c(2,1,0)
[1] FALSE  TRUE FALSE
```

> 注意，比较两对象是否相等应用双等号`==`而不是单等号`=`，`=`是赋值符号。

这样我们试着将`deck`数据框中的`ace`的`value`改成14：

```r
> deck$value[deck$face=="ace"] <- 14
> deck
    face     suit value
1   king   spades    13
2  queen   spades    12
3   jack   spades    11
4    ten   spades    10
5   nine   spades     9
6  eight   spades     8
7  seven   spades     7
8    six   spades     6
9   five   spades     5
10  four   spades     4
11 three   spades     3
12   two   spades     2
13   ace   spades    14
```

### 5.2 布尔运算符

布尔运算符（Boolean operator）是类似于与（&）和或（\|）这样的运算符。

R的布尔运算符：

| 运算符 | 语法 | 判别 |
| :---: | :---: | :---: |
| `&` | `cond1 & cond2` | `cond1`和`cond2`是否同时为真？ |
| `|` | `cond1 pipe cond2` | `cond1`和`cond2`是否至少有一个为真？ |
| `xor` | `xor(cond1, cond2)` | `cond1`和`cond2`中是否只有一个为真？ |
| `!` | `!cond1` | `cond1`是否为假？ |
| `any` | `any(cond1, cond2, cond3, ...)` | 所有条件中是否至少有一个为真？ |
| `all` | `all(cond1, cond2)` | 所有条件是否同时为真？ |

举个例子，z中的每一个值是否代表一个星期里的某一天？其中`z <- c("Monday", "Tuesday", "Friday")`。代码：

```r
> z <- c("Monday", "Tuesday", "Friday")
> all(z %in% c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"))
[1] TRUE
```

## 5.3 缺失信息

在R中，特殊字符`NA`代表不可用（not available），可用于存储缺失信息。

### 5.3.1 `na.rm`

大多数R函数都有一个可选参数`na.rm`，它代表将`NA`移除（NA remove）。

### 5.3.2 `is.na`

`is.na`函数可以帮我们快速地定位缺失值。

## 5.4 小结

我们可以结合R的记号体系语法和赋值符号帮助我们在R对象的内部快速改值。

逻辑值取子集的方法可以帮助我们快速修改或者提取数据。逻辑运算符和布尔运算符可以创建逻辑测试，然后将其作为索引值。

