# LaTex公式

* 行内公式：将公式插入到本行内
  >用 `$formula$` 表示，例如: `$\sum_{i=0}^{n}i^2$` 表示 $\sum_{i=0}^{n}i^2$

* 独立公式：将公式插入到新的一行内，并且居中
  >用 `$$formula$$` 表示，例如: `$$\sum_{i=0}^{n}i^2$$` 表示：
  >$$\sum_{i=0}^{n}i^2$$


>Tips：以下几个字符 `# $ % & ~ _ ^ \ { }` 有特殊意义，当表示这些字符时，需要转义，即在每个字符前加上 `\` ，对于 `\` ，可使用 `$\backslash$` 命令得到 $\backslash$

## 常用数学表达命令

### 上下标表示

* 上标: 用 `^` 后的内容表示上标
  >例如: `$x^{(i)}$` , `$y^{(i)}$` 表示 $x^{(i)}$ , $y^{(i)}$

* 下标: 用 `_` 后的内容表示上标
  >例如: `$x_{(i)}$` , `$y_{(i)}$` 表示 $x_{(i)}$ , $y_{(i)}$

* 上下标混用
  >例如: `$x_1^2$` , `$x^{y^{z}}$` , `$x^{y_z}$` 表示 $x_1^2$ , $x^{y^{z}}$ , $x^{y_z}$

当角标位置看起来不明显时，可以强制改变角标层次或者在角标前面加上改变其大小的命令 (如 `\tiny` , `\small` , `\normalsize` , `\large` , `\Large` , `\LARGE` )，例如: `$y_N$` , `$y_{_N}$` , `$y_{\tiny{N}}$` 表示 $y_N$ , $y_{_N}$ , $y_{\tiny{N} }$ 

并且支持中文作为角标，例如: `${\partial f}_{\tiny极大值}$` , `${\partial f}_{\large 极大值}$` 表示 ${\partial f}_{\tiny极大值}$` , `${\partial f}_{\large 极大值}$

### 分数形式

分式命令：

* `$\dfrac{}{}$` , 表示该分式是以 displaystyle 设置的，例如: `$\dfrac{y}{x}$` 表示 $\dfrac{y}{x}$

* `$\tfrac{}{}$` , 表示该分式是以 textstyle 设置的，例如: `$\tfrac{y}{x}$` 表示 $\tfrac{y}{x}$

* `$\frac{}{}$` , 表示该分式根据环境设置样式，例如: `$\frac{y}{x}$` 表示 $\frac{y}{x}$

* `${}\over{}$` , 分式的另一种表达方式，一般不建议使用 (但是真的很方便)，例如: `$y \over x$` 表示 $y \over x$

其具体区别请参考：

[What is the difference between \dfrac and \frac?](https://tex.stackexchange.com/questions/135389/what-is-the-difference-between-dfrac-and-frac)

[What is the difference between \over and \frac?](https://tex.stackexchange.com/questions/73822/what-is-the-difference-between-over-and-frac)

连分式 `$x_0+\frac{1}{x_1+\frac{1}{x_2+\frac{1}{x_3+\frac{1}{x_4} } } }$` 表示 $x_0+\frac{1}{x_1+\frac{1}{x_2+\frac{1}{x_3+\frac{1}{x_4} } } }$

可以通过强制改变字体大小使得分子分母字体大小一致，例如: `$\newcommand{\FS}[2]{\dfrac{ #1}{ #2} }x_0+\FS{1}{x_1+\FS{1}{x_2+\FS{1}{x_3+\FS{1}{x_4} } } }$` 表示 $\newcommand{\FS}[2]{\dfrac{ #1}{ #2} }x_0+\FS{1}{x_1+\FS{1}{x_2+\FS{1}{x_3+\FS{1}{x_4} } } }$

其中第一行命令定义了一个新的分式命令，规定每个调用该命令的分式都按 `\displaystyle` 的格式显示分式，等价于 `$x_0+\dfrac{1}{x_1+\dfrac{1}{x_2+\dfrac{1}{x_3+\dfrac{1}{x_4} } } }$`

分数线长度值是预设为分子分母的最大长度，如果想要使分数线再长一点，可以在分子或分母两端添加一些间隔，例如: `$\frac{1}{2}$`, `$\frac{\;1\;}{\;2\;}$` 表示 $\frac{1}{2}$, $\frac{\;1\;}{\;2\;}$

### *根式*
