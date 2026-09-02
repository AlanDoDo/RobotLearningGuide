## 0 记笔记方法

- 黑色 
- 红色 警告，订正和标志关键的知识点，不理解的问题
- 蓝色 (需要记忆/还没有掌握的知识) 重点和难点
- 绿色 记录疑问，提出问题
## 1 Markdown简介

[Markdown速查表](https://markdown.com.cn/cheat-sheet.html)

[Markdown在线编辑器](https://markdown.com.cn/editor/)

[数学公式速查](https://katex.org/docs/supported.html)


## 2 Markdown语法教程

### 2.1 标题

不同数量的`#`可以完成不同的标题，`#`后面有一个空格，如下：
# 一级标题

## 二级标题

### 三级标题

#### 四级标题       
##### 五级标题      
###### 六级标题     

### 2.2 字体

粗体、斜体、粗体和斜体，删除线，需要在文字前后加不同的标记符号。如下：

**这个是粗体**

*这个是斜体*

***这个是粗体加斜体***

~~这里是删除线~~

注：如果想给字体换颜色、字体或者居中显示，需要使用内嵌HTML来实现。

示例如下:  

<font face='楷体' color=#ff0000 size=4>我是正文</font>

这里的【楷体】，也可以改成【宋体】、【黑体】、【微软雅黑】等等。

这里的size，是规定文本尺寸的大小。一般是从1-7，浏览器默认为3。

至于这里的color，建议可以用十六进制来表示，也可以用rgb来表示。如下表：

查看[RGB颜色值与十六进制颜色码对照表](https://link.csdn.net/?target=https%3A%2F%2Fwww.cnblogs.com%2Fremember-forget%2Fp%2F8134849.html%3Flogin%3Dfrom_csdn)

### 2.3 无序列表

无序列表的使用，在符号`-`后加空格使用(符号`+`也可以)。如下：

- 无序列表 1
- 无序列表 2
- 无序列表 3

如果要控制列表的层级，则需要在符号`-`前使用空格。如下：

- 无序列表 1
  - 无序列表 1.1
  - 无序列表 1.2
- 无序列表 2
  - 无序列表 2.1
  - 无序列表 2.2
    - 无序列表 3.1
    - 无序列表 3.1

**这里最多支持到三级列表**。

### 2.4 有序列表

有序列表的使用，在数字及符号`.`后加空格后输入内容，如下：

1. 有序列表 1
2. 有序列表 2
3. 有序列表 3

### 2.5 引用

引用的格式是在符号`>`后面书写文字。如下：

> 读一本好书，就是在和高尚的人谈话。 ——歌德

> 雇用制度对工人不利，但工人根本无力摆脱这个制度。 ——阮一峰

>**这是一个加粗的引用**

### 2.7 链接

[我的B站动态主页](https://space.bilibili.com/1116074436/dynamic)
### 2.8 图片

插入图片，格式如下：

![](assets/Markdown随时查/file-20251216015943790.png)

支持 jpg、png、gif、svg 等图片格式，svg 文件示例如下：

![](https://markdown.com.cn/images/i-am-svg.svg)

支持图片**拖拽和截图粘贴**到编辑器中。

注：支持图片 ***拖拽和截图粘贴*** 到编辑器中，仅支持 https 的图片。

### 2.9 分割线

可以在一行中用三个以上的减号来建立一个分隔线，同时需要在分隔线的上面空一行。如下：

---

### 2.10 表格

可以使用冒号来定义表格的对齐方式，如下：

| 姓名   | 年龄 |     工作 |
| :----- | :--: | -------: |
| 小可爱 |  18  | 吃可爱多 |
| 小小勇敢 |  20  | 爬棵勇敢树 |
| 小小小机智 |  22  | 看一本机智书 |

### 2.11 特殊符号

对于 Markdown 中的语法符号，前面加反斜线\即可显示符号本身。

\\          表示一个反斜线
\*          表示一个*
\{\}        表示一个{}
...（其他的类似，不再举例）

## 3. 特殊语法

### 3.1 脚注

[^1]: This is the footnote.

### 3.2 代码块

如果在一个行内需要引用代码，只要用反引号引起来就好，如下：

Use the `printf()` function.

在需要高亮的代码块的前一行及后一行使用三个反引号，同时**第一行反引号后面表示代码块所使用的语言**，如下：

```java
// FileName: HelloWorld.java
public class HelloWorld {
  // Java 入口程序，程序从此入口
  public static void main(String[] args) {
    System.out.println("Hello,World!"); // 向控制台打印一条语句
  }
}
```

支持以下语言种类：

```
bash
clojure，cpp，cs，css
dart，dockerfile, diff
erlang
go，gradle，groovy
haskell
java，javascript，json，julia
kotlin
lisp，lua
makefile，markdown，matlab
objectivec
perl，php，python
r，ruby，rust
scala，shell，sql，swift
tex，typescript
verilog，vhdl
xml
yaml
```

如果想要更换代码高亮样式，可在上方**代码主题**中挑选。

### 3.3 数学公式

参考官方文档

[KATE​X's Supported Functions(opens new window)](https://katex.org/docs/supported.html)

[KATE​X's Support Table](https://katex.org/docs/support_table.html)

使用两个”$”符号引用公式:

$公式$

使用四个”$”符号引用公式:

$$公式$$

行内公式使用方法，比如这个化学公式：$\ce{Hg^2+ ->[I-] HgI2 ->[I-] [Hg^{II}I4]^2-}$

块公式使用方法如下：

$$H(D_2) = -\left(\frac{2}{4}\log_2 \frac{2}{4} + \frac{2}{4}\log_2 \frac{2}{4}\right) = 1$$

矩阵：

$$
  \begin{pmatrix}
  1 & a_1 & a_1^2 & \cdots & a_1^n \\
  1 & a_2 & a_2^2 & \cdots & a_2^n \\
  \vdots & \vdots & \vdots & \ddots & \vdots \\
  1 & a_m & a_m^2 & \cdots & a_m^n \\
  \end{pmatrix}
$$

具体数学公式：

(1)指数与下标

$a^3_{2}$

(2)平方根

$\sqrt{x}$

(3)在上方或者下方的下划线(可以表示取反等)

$\overline{m+n}$   和    $\underline{m+n}$

(4)向量

$\vec a$  表示向量a
$\overrightarrow{AB}$  表示向量AB，箭头指向右(即A->B)	
$\overleftarrow{AB}$   表示向量BA，箭头指向左(即A<-B)

(5)分数

$\frac{x^{2}}{k+1}$

(6)积分、求和、求积运算符

求和：$\sum_{i=1}^{n}$		//按照$\sum_{...}^{...}$的格式
积分：$\int_{0}^{\pi}$		//按照$\int_{...}^{...}$的格式
求积：$\prod_{0}^{n}$		//同上两种类似，按照$\prod_{...}^{...}$的格式

## 4 其他语法

### 4.1 HTML

支持原生 HTML 语法，请写内联样式，如下：

<span style="display:block;text-align:light;color:orangered;">橙色居左</span>
<span style="display:block;text-align:right;color:orangered;">橙色居右</span>
<span style="display:block;text-align:center;color:orangered;">橙色居中</span>

### 标签语法

> [!abstract]

>[!todo]

> [!info]

> [!tip]

> [!success]

> [!question]

> [!warning]

> [!failure]

> [!danger]

> [!bug]

> [!example]

> [!quote]

