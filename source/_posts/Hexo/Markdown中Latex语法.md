---
title: Markdown中Latex语法
date: 2021-04-17 10:12:06
categories: Hexo
tags: [Github,Hexo]
---
# 公式包裹方式
&emsp;&emsp;有两种方式来包裹公式内容：
* 行内公式  
&emsp;&emsp;用`$`包裹公式
* 独立公式  
&emsp;&emsp;用`$$`包裹公式。

&emsp;&emsp;以下几个字符: `# $ % & ~ _ ^ \ { }`有特殊意义，需要表示这些字符时，需要转义。

# 公式写法
## 占位符
&emsp;&emsp;两个quad空格，符号：`\qquad`，如：`x \qquad y`=> $x \qquad y$。  
&emsp;&emsp;quad空格，符号：`\quad`，如：`x \quad y`=> $x \quad y$。  
&emsp;&emsp;大空格，符号`\`，如：`x \ y`=> $x \ y$。  
&emsp;&emsp;中空格，符号`\:`，如：`x \: y`=> $x \: y$。   
&emsp;&emsp;小空格，符号`\,`，如：`x \, y`=> $x \, y$。  
&emsp;&emsp;紧贴，符号`\!`，如：`x \! y`=>  $x \! y$。  
## 上标、下标与组合
&emsp;&emsp;上标符号，符号：`^`，如：`x^4`=> $x^4$。   
&emsp;&emsp;下标符号，符号：`_`，如：`x_1`=> $x_1$。   
&emsp;&emsp;组合符号，符号：`{}`，如：`{16}_{8}O{2+}_{2}`=>${16}_{8}O{2+}_{2}$。  ​	
## 基本运算
&emsp;&emsp;加法运算，符号：`+`，如：`x + y`=> $x + y$。    
&emsp;&emsp;减法运算，符号：`-`，如：`x - y`=> $x - y$。    
&emsp;&emsp;加减运算，符号：`\pm`，如：`x \pm y`=> $x \pm y$。  
&emsp;&emsp;乘法运算，符号：`\times`，如：`x \times y`=> $x \times y$。  
&emsp;&emsp;点乘运算，符号：`\cdot`，如：`x \cdot y`=> $x \cdot y$。    
&emsp;&emsp;星乘运算，符号：`\ast`，如：`x \ast y`=> $x \ast y$。    
&emsp;&emsp;除法运算，符号：`\div`，如：`x \div y`=> $x \div y$。    
&emsp;&emsp;斜法运算，符号：`/`，如：`x / y`=> $x / y$。    
&emsp;&emsp;分式表示，符号：`\frac{分子}{分母}`，如：`\frac{x+y}{y+z}`=> $\frac{x+y}{y+z}$。  
&emsp;&emsp;分式表示，符号：`{分子} \voer {分母}`，如：`{x+y} \over {y+z}`=> ${x+y} \over {y+z}$。  
&emsp;&emsp;绝对值表示，符号：`||`，如：`|x + y|`=> $|x + y|$。  
## 高级运算
&emsp;&emsp;平均数运算，符号：`\overline{算式}`，如：`\overline{xyz}`=>$\overline{xyz}$。  
&emsp;&emsp;开二次方运算，符号：`\sqrt`，如：`\sqrt x`=>$\sqrt x$。  
&emsp;&emsp;开方运算，符号：`\sqrt[开方数]{被开方数}`，如：`\sqrt[3]{x+y}`=>$\sqrt[3]{x+y}$。  
&emsp;&emsp;对数运算，符号：`\log`，如：`\log(x)`=>$\log(x)$。  
&emsp;&emsp;极限运算，符号：`\lim`，如：`\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}`=>$\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$。  
​&emsp;&emsp;极限运算，符号：`\displaystyle \lim`，如：`\displaystyle \lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}`=>$\displaystyle \lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$。  
&emsp;&emsp;求和运算，符号：`\sum`，如：`\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}`=>$\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$。  
&emsp;&emsp;求和运算，符号：`\displaystyle \sum`，如：`\displaystyle \sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}`=>$\displaystyle \sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$。   
&emsp;&emsp;积分运算，符号：`\int`，如`\int^{\infty}_{0}{xdx}`=>$\int^{\infty}_{0}{xdx}$。  
&emsp;&emsp;积分运算，符号：`\displaystyle \int`，如：`\displaystyle \int^{\infty}_{0}{xdx}`=>$\displaystyle \int^{\infty}_{0}{xdx}$。  
&emsp;&emsp;微分运算，符号：`\partial`，如：`\frac{\partial x}{\partial y}`=>$\frac{\partial x}{\partial y}$。  
## 逻辑运算
&emsp;&emsp;等于运算，符号：`=`，如：`x + y = z`=>$x + y = z$。  
&emsp;&emsp;大于运算，符号：`>`，如：`x + y > z`=>$x + y > z$。  
&emsp;&emsp;小于运算，符号：`<`，如：`x + y < z`=>$x + y < z$。  
&emsp;&emsp;大于等于运算，符号：`\geq`，如：`x+y \geq z`=>$x+y \geq z$。  
&emsp;&emsp;小于等于运算，符号：`\leq`，如：`x+y \leq z`=>$x+y \leq z$。  
&emsp;&emsp;不等于运算，符号：`\neq`，如：`x+y \neq z`=>$x+y \neq z$。  
&emsp;&emsp;不大于等于运算，符号：`\ngeq`，如：`x+y \ngeq z`=>$x+y \ngeq z$。   
&emsp;&emsp;不小于等于运算，符号：`\nleq`，如：`x+y \nleq z`=>$x+y \nleq z$。  
&emsp;&emsp;约等于运算，符号：`\approx`，如：`x+y \approx z`=>$x+y \approx z$。  
&emsp;&emsp;恒定等于运算，符号：`\equiv`，如：`x+y \equiv z`=>$x+y \equiv z$。  
## 集合运算
&emsp;&emsp;属于运算，符号：`\in`，如：`x \in y`=>$x \in y$。  
&emsp;&emsp;不属于运算，符号：`\notin`，如：`x \notin y`=>$x \notin y$。  
&emsp;&emsp;子集运算，符号：`\subset`，如：`x \subset y`=>$x \subset y$。  
&emsp;&emsp;子集运算，符号：`\supset`，如：`x \supset y`=>$x \supset y$。  
&emsp;&emsp;真子集运算，符号：`\subseteq`，如：`x \subseteq y`=>$x \subseteq y$。  
&emsp;&emsp;真子集运算，符号：`\supseteq`，如：`x \supseteq y`=>$x \supseteq y$。  
&emsp;&emsp;非真子集运算，符号：`\subsetneq`，如：`x \subsetneq y`=>$x \subsetneq y$。  
&emsp;&emsp;非真子集运算，符号：`\supsetneq`，如：`x \supsetneq y`=>$x \supsetneq y$。  
&emsp;&emsp;并集运算，符号：`\cup`，如：`x \cup y`=>$x \cup y$。  
&emsp;&emsp;交集运算，符号：`\cap`，如：`x \cap y`=>$x \cap y$。  
&emsp;&emsp;差集运算，符号：`\setminus`，如：`x \setminus y`=>$x \setminus y$。  
&emsp;&emsp;同或运算，符号：`\bigodot`，如：`x \bigodot y`=>$x \bigodot y$。  
&emsp;&emsp;同与运算，符号：`\bigotimes`，如：`x \bigotimes y`=>$x \bigotimes y$。  
&emsp;&emsp;实数集合，符号：`\mathbb{集合名}`，如：`\mathbb{R}`=>$\mathbb{R}$。  
&emsp;&emsp;自然数集合，符号：`\mathbb{集合名}`，如：`\mathbb{Z}`=>$\mathbb{Z}$。  
&emsp;&emsp;空集，符号：`\emptyset`，如：$\emptyset$。  
## 数学符号
&emsp;&emsp;无穷，符号：`\infty`，如：$\infty$。   
&emsp;&emsp;虚数，符号：`\imath`，如：$\imath$。    
&emsp;&emsp;虚数，符号：`\jmath`，如：$\jmath$。  

&emsp;&emsp;数学符号，符号`\hat{字母}`，如：`\hat{a}`=>$\hat{a}$。
&emsp;&emsp;数学符号，符号`\check{字母}`，如：`\check{a}`=>$\check{a}$。  
&emsp;&emsp;数学符号，符号`\breve{字母}`，如：`\breve{a}`=>$\breve{a}$。  
&emsp;&emsp;数学符号，符号`\tilde{字母}`，如：`\tilde{a}`=>$\tilde{a}$。  
&emsp;&emsp;数学符号，符号`\bar{字母}`，如：`\bar{a}`=>$\bar{a}$。  
&emsp;&emsp;矢量符号，符号`\vec{字母}`，如：`\vec{a}`=>$\vec{a}$。  
&emsp;&emsp;数学符号，符号`\acute{字母}`，如：`\acute{a}`=>$\acute{a}$。  
&emsp;&emsp;数学符号，符号`\grave{字母}`，如：`\grave{a}`=>$\grave{a}$。  
&emsp;&emsp;一阶导数符号，符号`\dot{字母}`，如：`\dot{a}`=>$\dot{a}$。  
&emsp;&emsp;二阶导数符号，符号`\ddot{字母}`，如：`\ddot{a}`=>$\ddot{a}$。  

&emsp;&emsp;上箭头，符号：`\uparrow`，如：$\uparrow$。  
&emsp;&emsp;上箭头，符号：`\Uparrow`，如：$\Uparrow$。  
&emsp;&emsp;下箭头，符号：`\downarrow`，如：$\downarrow$。  
&emsp;&emsp;下箭头，符号：`\Downarrow`，如：$\Downarrow$。  
&emsp;&emsp;左箭头，符号：`\leftarrow`，如：$\leftarrow$。  
&emsp;&emsp;左箭头，符号：`\Leftarrow`，如：$\Leftarrow$。  
&emsp;&emsp;右箭头，符号：`\rightarrow`，如：$\rightarrow$。  
&emsp;&emsp;右箭头，符号：`\Rightarrow`，如：$\Rightarrow$。  

&emsp;&emsp;底端对齐的省略号，符号：`\ldots`，如：`1,2,\ldots,n`=>$1,2,\ldots,n$。  
&emsp;&emsp;中线对齐的省略号，符号：`\cdots`，如：`x_1^2 + x_2^2 + \cdots + x_n^2`=>$x_1^2 + x_2^2 + \cdots + x_n^2$。  
&emsp;&emsp;竖直对齐的省略号，符号：`\vdots`，如：$\vdots$。  
&emsp;&emsp;斜对齐的省略号，符号：`\ddots`，如：$\ddots$。  
## 希腊字母
|字母|实现|字母|实现|
|----|---|----|----|
|A|A|α|\alhpa|
|B|B|β|\beta|
|Γ|\Gamma|γ|\gamma|
|Δ|\Delta|δ|\delta|
|E|E|ϵ|\epsilon|
|Z|Z|ζ|\zeta|
|H|H|η|\eta|
|Θ|\Theta|θ|\theta|
|I|I|ι|\iota|
|K|K|κ|\kappa|
|Λ|\Lambda|λ|\lambda|
|M|M|μ|\mu|
|N|N|ν|\nu|
|Ξ|\Xi|ξ|\xi|
|O|O|ο|\omicron|
|Π|\Pi|π|\pi|
|P|P|ρ|\rho|
|Σ|\Sigma|σ|\sigma|
|T|T|τ|\tau|
|Υ|\Upsilon|υ|\upsilon|
|Φ|\Phi|ϕ|\phi|
|X|X|χ|\chi|
|Ψ|\Psi|ψ|\psi|
|Ω|\v|ω|\omega|