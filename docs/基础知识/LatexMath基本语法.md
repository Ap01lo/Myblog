

## Latex Math基本语法



#### 基本知识

1. TEX 是一个计算机程序，用于文章和数学公式的排版
2. LATEX 是一个 **宏包** ，使用了 **TEX** 作为引擎
3. 以后感兴趣了或者有需要了再深入研究全部的语法。



#### LATEX字母符号

*所有的latex模块都使用$$来封装*

**1. 希腊字母**

```latex
$\Gamma$,$\iota$,$\sigma$,$\phi$,$\upsilon$,$\Pi$
```

输出如下：$\Gamma$,$\iota$,$\sigma$,$\phi$,$\upsilon$,$\Pi$

```latex
$\Bbbk$,$\heartsuit$,$\int$,$\oint$
```

输出如下：$\Bbbk$,$\heartsuit$,$\int$,$\oint$

*注意的是希腊字母有大小写之分*

**2. 三角函数，对数，指数**

```latex
$\tan$, $\sin$, $\cos$, $\lg$, $\arcsin$
```

输出如下：$\tan$, $\sin$, $\cos$, $\lg$, $\arcsin$

```latex
$\arccos$, $\arctan$, $\min$, $\max$, $\exp$, $\log$
```

输出如下：$\arccos$, $\arctan$, $\min$, $\max$, $\exp$, $\log$

**3. 运算符**

```latex
$+$, $-$, $=$, $<$, $>$, $\times$, $\div$, $\equiv$, $\leq$, $\geq$, $\neq$
```

输出如下：$+$, $-$, $=$, $<$, $>$, $\times$, $\div$, $\equiv$, $\leq$, $\geq$, $\neq$

**4. 集合符**

```latex
$\cup$, $\cap$, $\in$, $\notin$, $\ni$, $\subset$, $\subseteq$
$\subseteq$, $\N$, $\Z$, $\R$, $\infty$
```

输出如下：$\cup$, $\cap$, $\in$, $\notin$, $\ni$, $\subset$, $\subseteq$, $\N$, $\Z$, $\R$, $\infty$





#### 数学公式

**1. 内联输出与块状输出**

​	内联就是使用两个$$符号将latex代码包裹，这样可以将数学符合嵌入到文字里面，或者换一句话说，可以和文字混合输出，比如：

​	函数：$f(x) = ax+b$ 是一个一元一次函数表达式

​	函数：$f(x) = \frac{ax+b}{bx+c}$ 是一个分式

我们可以看到数学公式在段落里面。

​	如果我们要输出的公式比较复杂，就需要单独突出显示这个公式，就需要块状的公式输出。语法是用$$ $$ 来将公式包裹，比如：

```latex
$$f(x) = \frac{P(x)}{Q(x)}$$
```

就像这样：

$$f(x) = \frac{P(x)}{Q(x)}$$

但是在markdown中需要__换行__来单独显示。

**2. 简单的四则运算**

例如：

```latex
$2x-3y=8$
$3x+4y=19$
$5x \times 3y \neq 4$
$4x \div 4y = 4$
```

输出如下：

$2x-3y=8$
$3x+4y=19$
$5x \times 3y \neq 4$
$4x \div 4y = 4$

**3. 指数输出**

markdown 的指数运算是 _^_ ,例如：

```latex
$a^2+ b^2 = c^2$
```

输出如下：$a^2+ b^2 = c^2$

**4. N次方根输出**

N次方根的符号是 *\sqrt[n]{a}* 用法如下：

```latex
$\sqrt[n]{a}$
```

输出如下：$\sqrt[n]{a}$

**5. 三角公式**

三角公式注意所有的符号前面一定要加  \， 其中角是 \theta，例如：

```latex
$$\cos(2\theta) = \cos^2\theta - \sin^2\theta$$
```

输出如下：

$$\cos(2\theta) = \cos^2\theta - \sin^2\theta$$

**6. 输出分数**

分数的语法是 \frac{分子}{分母}，例如：

```latex
$$f(x) = \frac{ax+by}{cx+dy} - \frac{x-y}{x+y}$$
```

输出如下：

$$f(x) = \frac{ax+by}{cx+dy} - \frac{x-y}{x+y}$$

**7. 求和输出**

求和公式涉及上标和下标，分别使用 _ 和 ^ 表示，例如：

```latex
$$\sum_{i=1}^{\infty}a_{i}$$
```

输出如下：

$$\sum_{i=1}^{\infty}a_{i}$$

**8. 极限的输出**

极限输出与求和相同，都是用下标与上标，例如：

```latex	
$$
\lim\limits_{x \to \infty} \exp(-x) = 0
$$
```

输出如下：
$$
\lim\limits_{x \to \infty} \exp(-x) = 0
$$
**9. 阶乘输出**

与上面类似，例如：

```latex
$$
\frac{n!}{k!(n-k)!} = \binom{n}{k}
$$
```

输出如下:
$$
\frac{n!}{k!(n-k)!} = \binom{n}{k}
$$
**10. 矩阵输出**

矩阵需要使用latex的基本语法，用 \begin{matrix} 和 \end{matrix} 将公式包裹，使用两个 \\ 换行，例如：

```latex
$$
\begin{matrix}
1&2&3\\
3&5&6\\
7&8&9
\end{matrix}
$$
```

输出如下：
$$
\begin{matrix}
1&2&3\\
3&5&6\\
7&8&9
\end{matrix}
$$
**11. 分段函数**

同理使用 \begin{cases} 与 \end{cases} 来引导分段函数，例如：

```latex
$$
X(n) = 
\begin{cases}
x(n)\\
x(n-1)\\
x(n+1)
\end{cases}
$$
```

输出如下:
$$
X(n) = 
\begin{cases}
x(n)\\
x(n-1)\\
x(n+1)
\end{cases}
$$

### 流程图画法

+ 基本语法格式

  ```
  tag->type: content:>url
  ```

  + *tag* : 元素名字
  + *type* ：类型名字，有六种：
    + *start* 开始
    + *end* 结束
    + *operation* 操作
    + *subroutine* 子程序
    + *condition* 条件
    + *inputoutput* 输入或产出
  + *content* 是在框框里面写的内容，**注意** <u>要在type后面的冒号与文本之间加一个空格</u>
  + *url* 是一个链接，与框框里面的文本绑定

+ 链接元素的语法

  + 使用 *->* 来链接元素，需要注意 *condition* 类型，要写成

    ```
    cond(yes)->a->b
    ```

+ 示例1

  ```flow
  st=>start: 电灯不工作了
  cond1=>condition: 电源接好了吗
  cond2=>condition: 灯泡烧毁了吗
  io1=>inputoutput: 接好电源
  io2=>inputoutput: 更换灯泡
  io3=>inputoutput: 修理电灯
  st->cond1
  cond1(no)->io1
  cond1(yes)->cond2
  cond2(no)->io2
  cond2(yes)->io3
  ```

  

+ 示例2

  ```flow
  st=>start: Start
  op1=>operation: Please Toaster on Table
  op2=>operation: Plug Toaster into Power Outlet
  op3=>operation: Turn the Toaster on
  op4=>operation: Set the Toaster to Desired Degree
  op5=>operation: Place Two Slices of Bread into
  op6=>operation: Push the Lever Down
  op7=>operation: Wait untill Toaster is Ready
  cond1=>condition: Is the bread brown enough?
  op8=>operation: Cool the Toaster for a While
  cond2=>condition: Is the Toaster cool enough?
  op9=>operation: Remove Toast from Toaster
  op10=>operation: Spread Toast
  e=>end: End
  st->op1->op2->op3->op4->op5->op6->op7->cond1
  cond1(no)->op6
  cond1(yes)->op8->cond2
  cond2(yes)->op9->op10->e
  cond2(no)->op8
  ```

  





### 到这里基本上就会了大多数的数学公式的表达，等到不会的时候再回来查找**{docsify-ignore}**





