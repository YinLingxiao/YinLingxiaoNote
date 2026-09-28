---
tags: [高等数学, 场论, 积分公式, 曲线积分, 曲面积分]
aliases: [Stokes公式, 旋度定理, 空间曲线积分公式]
---

# Stokes公式（Stokes Formula）—— 系统总结

> [!abstract] 一句话定位
> Stokes公式是[[格林公式]]向空间曲线的推广——它将**空间闭曲线上的第二型曲线积分**转化为以该曲线为边界的**有向曲面上的[[第二型曲面积分]]**，是计算空间环量、引入"旋度"概念的核心工具。

---

## 一、Stokes公式（核心定理）

### 1.1 定理陈述

设 $\Gamma$ 为分段光滑的空间有向闭曲线，$\Sigma$ 是以 $\Gamma$ 为边界的分片光滑有向曲面，$\Gamma$ 的正向与 $\Sigma$ 的侧符合**右手定则**。若 $P,Q,R$ 在 $\Sigma$ 上具有一阶连续偏导数，则

> $$\boxed{\oint_{\Gamma}P\,dx+Q\,dy+R\,dz=\iint_{\Sigma}\left|\begin{matrix}dy\,dz & dz\,dx & dx\,dy \\ \frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\ P & Q & R\end{matrix}\right|}$$

展开即为：

> $$\boxed{\oint_{\Gamma}P\,dx+Q\,dy+R\,dz=\iint_{\Sigma}\left(\frac{\partial R}{\partial y}-\frac{\partial Q}{\partial z}\right)dy\,dz+\left(\frac{\partial P}{\partial z}-\frac{\partial R}{\partial x}\right)dz\,dx+\left(\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)dx\,dy}$$

### 1.2 第一型曲面积分形式

利用方向余弦 $(\cos\alpha,\cos\beta,\cos\gamma)$（$\Sigma$ 的单位法向量）：

> $$\boxed{\oint_{\Gamma}P\,dx+Q\,dy+R\,dz=\iint_{\Sigma}\left[\left(\frac{\partial R}{\partial y}-\frac{\partial Q}{\partial z}\right)\cos\alpha+\left(\frac{\partial P}{\partial z}-\frac{\partial R}{\partial x}\right)\cos\beta+\left(\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)\cos\gamma\right]dS}$$

### 1.3 右手定则

> [!note] 右手定则
> 四指沿 $\Gamma$ 正向弯曲，大拇指指向即为 $\Sigma$ 的法向量方向。

---

## 二、环流量与旋度

### 2.1 环流量（Circulation）

向量场 $\mathbf{A}=(P,Q,R)$ 沿有向闭曲线 $\Gamma$ 的环流量：

> $$\text{Circ}=\oint_{\Gamma}\mathbf{A}\cdot d\mathbf{r}=\oint_{\Gamma}P\,dx+Q\,dy+R\,dz$$

### 2.2 旋度（Curl/Rotation）

$$\operatorname{rot}\mathbf{A}=\nabla\times\mathbf{A}=\left|\begin{matrix}\mathbf{i} & \mathbf{j} & \mathbf{k} \\ \frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\ P & Q & R\end{matrix}\right|$$

分量形式：

> $$\boxed{\operatorname{rot}\mathbf{A}=\left(\frac{\partial R}{\partial y}-\frac{\partial Q}{\partial z},\;\frac{\partial P}{\partial z}-\frac{\partial R}{\partial x},\;\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)}$$

### 2.3 Stokes公式的旋度形式

> $$\boxed{\oint_{\Gamma}\mathbf{A}\cdot d\mathbf{r}=\iint_{\Sigma}(\operatorname{rot}\mathbf{A})\cdot\mathbf{n}\,dS}$$

**本质**：闭曲线上的环量 = 以该曲线为边界的曲面上旋度的通量。

### 2.4 记忆法

旋度的三个分量是"交叉偏导相减"：
- $x$ 分量：$\partial R/\partial y - \partial Q/\partial z$（缺 $x$，$y\to z$）
- $y$ 分量：$\partial P/\partial z - \partial R/\partial x$（缺 $y$，$z\to x$）
- $z$ 分量：$\partial Q/\partial x - \partial P/\partial y$（缺 $z$，$x\to y$）

---

## 三、典型例题

### 例1：三角形边界上的Stokes公式

**题目**：利用Stokes公式计算曲线积分 $\displaystyle\oint_{\Gamma}z\,dx-x\,dy-y\,dz$，其中 $\Gamma$ 为平面 $x+y+z=1$ 被三个坐标平面所截成的三角形的整个边界，正向与三角形上侧法向量符合右手规则。

**解**：

按 $P\,dx+Q\,dy+R\,dz$ 对应，有
$$P=z,\qquad Q=-x,\qquad R=-y$$

Stokes公式给出
$$\oint_\Gamma Pdx+Qdy+Rdz=\iint_\Sigma
\begin{vmatrix}
dydz&dzdx&dxdy\\
\partial_x&\partial_y&\partial_z\\
z&-x&-y
\end{vmatrix}$$

展开：
$$\left(\frac{\partial R}{\partial y}-\frac{\partial Q}{\partial z}\right)=-1,
\quad \left(\frac{\partial P}{\partial z}-\frac{\partial R}{\partial x}\right)=1,
\quad \left(\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)=-1$$

故
$$I=\iint_\Sigma(-dy\,dz+dz\,dx-dx\,dy)$$

平面 $x+y+z=1$ 的上侧法向量 $(1,1,1)$ 三个分量都为正，所以它在三个坐标面上的投影都取正号，且都是面积为 $\frac12$ 的直角三角形：
$$\iint_\Sigma dy\,dz=\iint_\Sigma dz\,dx=\iint_\Sigma dx\,dy=\frac12$$
于是
$$I=-\frac12+\frac12-\frac12=-\frac12$$

**答案**：$\displaystyle-\frac12$

> [!tip] 要点
> - Stokes公式的展开要仔细对应 $P,Q,R$
> - 曲线正向与曲面法向必须满足右手规则
> - 平面上的曲面积分常可投影到坐标面快速计算

---

### 例2：圆柱与平面交线（椭圆）

**题目**：求 $\displaystyle\oint_{\Gamma}(y-z)\,dx+(z-x)\,dy+(x-y)\,dz$，其中 $\Gamma$ 为圆柱面 $x^2+y^2=a^2$ 与平面 $\dfrac{x}{a}+\dfrac{z}{b}=1$（$a,b>0$）所交成的椭圆周，方向与平面上向上的法向量成右手系。

**解**：

$P=y-z$，$Q=z-x$，$R=x-y$。

旋度为
$$\operatorname{rot}\mathbf A=\left(\frac{\partial R}{\partial y}-\frac{\partial Q}{\partial z},\frac{\partial P}{\partial z}-\frac{\partial R}{\partial x},\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)=(-2,-2,-2)$$

平面 $\dfrac{x}{a}+\dfrac{z}{b}=1$ 的向上单位法向量为
$$\mathbf n=\frac{(b,0,a)}{\sqrt{a^2+b^2}}$$

于是
$$\operatorname{rot}\mathbf A\cdot\mathbf n=\frac{-2(a+b)}{\sqrt{a^2+b^2}}$$

椭圆所围区域 $\Sigma$ 在平面上的面积为
$$S_\Sigma=\pi a\sqrt{a^2+b^2}$$

故
$$I=\iint_\Sigma(\operatorname{rot}\mathbf A)\cdot\mathbf n\,dS=\frac{-2(a+b)}{\sqrt{a^2+b^2}}\cdot\pi a\sqrt{a^2+b^2}=-2\pi a(a+b)$$

**答案**：$\displaystyle-2\pi a(a+b)$

> [!tip] 要点
> - 圆柱 + 平面 → 椭圆；Stokes公式将空间曲线积分化为平面上的曲面积分
> - 计算旋度后，利用第一型曲面积分形式（点乘单位法向量）最简洁
> - 本题旋度三个分量都为 $-2$，不能漏掉第一个分量

---

## 四、易错点 Checklist

| ❌ 常见错误 | ✅ 正确做法 |
| :--- | :--- |
| $P,Q,R$ 与 $dx,dy,dz$ 的对应搞混 | 严格按 $\oint P\,dx+Q\,dy+R\,dz$ 对应 |
| 旋度公式中偏导顺序记反 | $\partial R/\partial y - \partial Q/\partial z$（交叉相减，不是 $\partial Q/\partial y - \partial R/\partial z$） |
| 右手定则判断错曲面方向 | 四指沿 $\Gamma$ 正向，大拇指指向法向量方向 |
| 曲面不是以 $\Gamma$ 为边界 | Stokes公式要求 $\partial\Sigma=\Gamma$ |
| 法向量取错方向 | 法向量方向必须与 $\Gamma$ 正向满足右手定则 |
| 混淆旋度与散度 | 旋度 = $\nabla\times\mathbf{A}$（向量），散度 = $\nabla\cdot\mathbf{A}$（标量） |

---

## 五、知识网络

```
Stokes公式
    ├── 空间闭曲线积分 → 曲面积分
    ├── 右手定则（Γ 与 Σ 的方向关系）
    └── 物理意义
            ├── 环量 = ∮ A·dr
            └── 旋度 rot A = ∇ × A
```

**三大公式的递进关系**：

| 公式 | 维度 | 左端 | 右端 |
| :--- | :--- | :--- | :--- |
| 牛顿-莱布尼茨 | 1D | 区间端点值 | 区间内导数积分 |
| 格林公式 | 2D | **平面闭曲线**积分 | **平面区域**上二重积分 |
| **Gauss公式** | **3D** | **闭曲面**积分 | **空间区域**上三重积分 |
| **Stokes公式** | **3D** | **空间闭曲线**积分 | **曲面**上面积分 |

- **前置依赖**：[[第二型曲线积分]]、[[第二型曲面积分]]、旋度
- **与格林公式的关系**：格林公式是Stokes公式在平面上的特例（$z=0$ 时）
- **与Gauss公式的关系**：Gauss公式处理闭曲面，Stokes公式处理闭曲线

---

## 六、一句话核心

Stokes公式 = **空间格林公式**：空间闭曲线上的环量 = 以该曲线为边界的曲面上旋度的通量；关键是正确写出旋度和匹配右手定则。

---

## 📎 相关笔记

**课程**：[[00 高等数学索引|高等数学]] ｜ **上一篇**：[[Gauss 公式]] ｜ **下一篇**：[[数项级数的概念]] ｜ **速查**：[[高等数学下册_公式定理精华总结|公式定理精华]]

- [[格林公式]] —— 平面特例：Stokes 公式在 $z=0$ 时退化为格林公式
- [[Gauss 公式]] —— 三维姊妹：闭曲面 → 三重积分
- [[第二型曲线积分]] —— Stokes 公式的左端对象
- [[第二型曲面积分]] —— Stokes 公式的右端对象
