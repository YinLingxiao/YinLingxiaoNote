---
tags: [高等数学, 场论, 积分公式, 曲面积分]
aliases: [Gauss公式, 散度定理, 高斯定理, 三重积分与曲面积分的关系]
---

# Gauss公式（Gauss Formula）—— 系统总结

> [!abstract] 一句话定位
> Gauss公式是[[格林公式]]在三维空间的推广——它将**空间闭区域上的三重积分**与该区域**边界闭曲面上的[[第二型曲面积分]]**联系起来，是计算封闭曲面上向量场通量的核心工具，也是引入"散度"概念的桥梁。

---

## 一、Gauss公式（核心定理）

### 1.1 定理陈述

设空间闭区域 $\Omega$ 由**分片光滑**的闭曲面 $\Sigma$ 所围成，且 $\Sigma$ 取**外侧**（外法向）。若函数 $P(x,y,z)$、$Q(x,y,z)$、$R(x,y,z)$ 在 $\Omega$ 上具有连续的一阶偏导数，则

> $$\boxed{\iiint_{\Omega}\left(\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}\right)dV=\iint_{\Sigma}P\,dy\,dz+Q\,dz\,dx+R\,dx\,dy}$$

### 1.2 与两类曲面积分的联系

利用方向余弦，Gauss公式也可写成第一型曲面积分形式：

> $$\boxed{\iiint_{\Omega}\left(\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}\right)dV=\iint_{\Sigma}(P\cos\alpha+Q\cos\beta+R\cos\gamma)\,dS}$$

其中 $(\cos\alpha,\cos\beta,\cos\gamma)$ 是 $\Sigma$ **外法向量**的方向余弦。

### 1.3 证明思路

Gauss公式的证明与格林公式完全平行：
1. 先证特殊情形（穿过 $\Omega$ 内部且平行于坐标轴的直线与边界交点恰好是两个）
2. 对一般区域用辅助曲面分割成若干特殊区域
3. 利用曲面积分和三重积分的可加性合并

核心等式（可分别证明）：
$$\iiint_{\Omega}\frac{\partial R}{\partial z}\,dV=\iint_{\Sigma}R\,dx\,dy,\quad\text{类似有 }P\text{ 和 }Q\text{ 的等式}$$

---

## 二、通量与散度

### 2.1 通量（Flux）

设有向量场 $\mathbf{A}=(P,Q,R)$，$\Sigma$ 为有向曲面，单位法向量 $\mathbf{n}$。

> **通量**：$\displaystyle\Phi=\iint_{\Sigma}\mathbf{A}\cdot\mathbf{n}\,dS=\iint_{\Sigma}P\,dy\,dz+Q\,dz\,dx+R\,dx\,dy$

物理意义：单位时间内通过曲面 $\Sigma$ 的流体质量（设密度为 1）。

### 2.2 散度（Divergence）

在通量表达式两边除以 $\Omega$ 的体积 $V$，令 $\Omega\to M$（缩为一点）：

> $$\boxed{\operatorname{div}\mathbf{A}=\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}}$$

**物理意义**：
- $\operatorname{div}\mathbf{A}\gt 0$：点 $M$ 处有**正源**（流体涌出）
- $\operatorname{div}\mathbf{A}\lt 0$：点 $M$ 处有**负源**（流体吸入）
- $\operatorname{div}\mathbf{A}=0$：**无源场**

### 2.3 Gauss公式的散度形式

> $$\boxed{\iint_{\Sigma}\mathbf{A}\cdot\mathbf{n}\,dS=\iiint_{\Omega}\operatorname{div}\mathbf{A}\,dV}$$

**本质**：闭曲面上的通量 = 区域内散度的累积。

---

## 三、典型例题

### 例1：立方体上的Gauss公式

**题目**：计算 $\displaystyle\iint_{\Sigma}(x^3-yz)\,dy\,dz-2x^2y\,dz\,dx+z\,dx\,dy$，其中 $\Sigma$ 为立方体 $\Omega:\;0\le x\le a,\;0\le y\le a,\;0\le z\le a$ 的**外侧**。

**解**：

$P=x^3-yz$，$Q=-2x^2y$，$R=z$

$$\frac{\partial P}{\partial x}=3x^2,\quad\frac{\partial Q}{\partial y}=-2x^2,\quad\frac{\partial R}{\partial z}=1$$

$$\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}=x^2+1$$

由Gauss公式：
$$I=\iiint_{\Omega}(x^2+1)\,dV=\int_{0}^{a}dz\int_{0}^{a}dy\int_{0}^{a}(x^2+1)\,dx$$

$$=a^2\left[\frac{x^3}{3}+x\right]_{0}^{a}=\frac{a^5}{3}+a^3$$

**答案**：$\displaystyle\frac{a^5}{3}+a^3$

> [!tip] 要点
> - 验证条件：闭曲面、分片光滑、外侧、偏导连续 ✓
> - 转化为三重积分后，长方体区域上的积分最简——直接分离变量

---

### 例2：柱面所围区域（内侧）

**题目**：计算 $\displaystyle\iint_{\Sigma}(x-y)\,dx\,dy+(y-z)x\,dy\,dz$，其中 $\Sigma$ 为柱面 $x^2+y^2=1$ 及平面 $z=0$、$z=3$ 所围空间立体的**边界曲面的内侧**。

**解**：

$P=(y-z)x$，$Q=0$，$R=x-y$（注意：需按 $P\,dy\,dz+Q\,dz\,dx+R\,dx\,dy$ 对应）

实际对应：$P=(y-z)x$（$dy\,dz$ 的系数），$Q=0$（$dz\,dx$ 的系数），$R=x-y$（$dx\,dy$ 的系数）。

$$\frac{\partial P}{\partial x}=y-z,\quad\frac{\partial Q}{\partial y}=0,\quad\frac{\partial R}{\partial z}=0$$

$$\text{被积函数}=y-z$$

**注意**：$\Sigma$ 取**内侧**，Gauss公式要求**外侧**，故需加负号：

$$I=-\iiint_{\Omega}(y-z)\,dV$$

$\Omega$：$x^2+y^2\le 1$，$0\le z\le 3$。用柱坐标：

$$I=-\int_{0}^{2\pi}d\theta\int_{0}^{1}r\,dr\int_{0}^{3}(r\sin\theta-z)\,dz$$

计算内层：$\displaystyle\int_{0}^{3}(r\sin\theta-z)\,dz=3r\sin\theta-\frac{9}{2}$

对 $\theta$ 积分：$\displaystyle\int_{0}^{2\pi}3r\sin\theta\,d\theta=0$（奇函数）

$$I=-\int_{0}^{1}r\,dr\int_{0}^{2\pi}\left(-\frac{9}{2}\right)d\theta=\frac{9}{2}\cdot 2\pi\cdot\frac{1}{2}=\frac{9\pi}{2}$$

**答案**：$\dfrac{9\pi}{2}$

> [!tip] 要点
> **内侧** $\Rightarrow$ Gauss公式结果取**负号**；柱坐标下 $y=r\sin\theta$ 对 $[0,2\pi]$ 积分为零（对称性）。

---

### 例3：非闭曲面——补面法（锥面）

**题目**：计算 $\displaystyle I=\iint_{\Sigma}(y-z)\,dy\,dz+(z-x)\,dz\,dx+(x-y^2)\,dx\,dy$，其中 $\Sigma$ 为锥面 $z=\sqrt{x^2+y^2}$ 在 $0\le z\le 1$ 部分的**外侧**。

**解**：

$\Sigma$ 不是闭曲面！**补顶面** $\Sigma_1: z=1$（$x^2+y^2\le 1$），取**上侧**。

$\Sigma+\Sigma_1$ 构成闭曲面（外侧），围成区域 $\Omega$（锥体）。

$P=y-z$，$Q=z-x$，$R=x-y^2$

$$\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}=0+0+0=0$$

由Gauss公式：$\displaystyle\iint_{\Sigma+\Sigma_1}=\iiint_{\Omega}0\,dV=0$，故
$$I=-\iint_{\Sigma_1}(y-z)\,dy\,dz+(z-x)\,dz\,dx+(x-y^2)\,dx\,dy$$

在 $\Sigma_1$ 上 $z=1$，$dz=0$，只剩
$$I=-\iint_{x^2+y^2\le1}(x-y^2)\,dxdy$$

由对称性，$\iint_Dx\,dxdy=0$，所以
$$I=\iint_Dy^2\,dxdy=\int_0^{2\pi}\int_0^1r^2\sin^2\theta\cdot r\,drd\theta=\frac{\pi}{4}$$

**答案**：$\displaystyle\frac{\pi}{4}$

> [!tip] 要点
> - **补面法**：非闭曲面 + 辅助面 → 闭曲面 → Gauss公式
> - 辅助面通常选坐标平面上的平面片（$z=$ 常数，$dz=0$，大幅简化）
> - 最后减去辅助面上的积分，并注意补面方向

---

### 例4：补面法（抛物面）

**题目**：设 $\Sigma$ 为曲面 $z=2-x^2-y^2$（$1\le z\le 2$）取**上侧**，求
$$I=\iint_{\Sigma}(x^3z+x)\,dy\,dz-x^2yz\,dz\,dx-x^2z^2\,dx\,dy$$

**解**：

补底面 $\Sigma_1: z=1$（$x^2+y^2\le 1$），取**下侧**。

$P=x^3z+x$，$Q=-x^2yz$，$R=-x^2z^2$。

$$\frac{\partial P}{\partial x}=3x^2z+1,
\quad \frac{\partial Q}{\partial y}=-x^2z,
\quad \frac{\partial R}{\partial z}=-2x^2z$$

所以
$$\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}=1$$

由Gauss公式，闭曲面 $\Sigma+\Sigma_1$ 上的积分为区域体积：
$$\iint_{\Sigma+\Sigma_1}=\iiint_\Omega1\,dV=\int_0^{2\pi}d\theta\int_0^1r(1-r^2)\,dr=\frac{\pi}{2}$$

在补面 $\Sigma_1:z=1$ 的下侧，只有 $R\,dxdy$ 项贡献，且下侧使 $dxdy$ 取负：
$$\iint_{\Sigma_1}=\iint_D(-x^2)(-dxdy)=\iint_Dx^2\,dxdy=\frac{\pi}{4}$$

因此
$$I=\iint_{\Sigma+\Sigma_1}-\iint_{\Sigma_1}=\frac{\pi}{2}-\frac{\pi}{4}=\frac{\pi}{4}$$

**答案**：$\displaystyle\frac{\pi}{4}$

> [!tip] 要点
> 抛物面 $z=2-x^2-y^2$ 补 $z=1$ 的圆盘；补面取下侧时 $dxdy$ 变号。

---

## 四、易错点 Checklist

| ❌ 常见错误 | ✅ 正确做法 |
| :--- | :--- |
| 曲面取内侧直接用Gauss公式 | 内侧 $\Rightarrow$ 结果取**负号**，或转化为外侧 |
| 非闭曲面直接用Gauss公式 | 必须**补面**构成闭曲面 |
| 补面后忘记减去辅助面上的积分 | $I=\iint_{\Sigma+\Sigma_1}-\iint_{\Sigma_1}$ |
| $P,Q,R$ 与 $dy\,dz,dz\,dx,dx\,dy$ 对应错 | 严格按 $P\,dy\,dz+Q\,dz\,dx+R\,dx\,dy$ 对应 |
| 散度公式记错 | $\operatorname{div}\mathbf{A}=\dfrac{\partial P}{\partial x}+\dfrac{\partial Q}{\partial y}+\dfrac{\partial R}{\partial z}$（不是 $\partial P/\partial y$ 等） |
| 球坐标/柱坐标体积微元错 | $dV=r^2\sin\varphi\,dr\,d\varphi\,d\theta$（球），$dV=r\,dr\,d\theta\,dz$（柱） |

---

## 五、知识网络

```
Gauss公式
    ├── 闭曲面曲面积分 → 三重积分
    ├── 补面法（非闭曲面）
    └── 物理意义
            ├── 通量 Φ = ∬ A·n dS
            └── 散度 div A = ∂P/∂x + ∂Q/∂y + ∂R/∂z
```

- **前置依赖**：[[第二型曲面积分]]、三重积分
- **与格林公式的关系**：[[格林公式]]是 2D，Gauss公式是 3D
- **后续延伸**：[[Stokes 公式|Stokes公式]]（空间闭曲线 → 曲面积分）

---

## 六、一句话核心

Gauss公式 = **三维格林公式**：闭曲面上的向量场通量 = 区域内散度的三重积分；非闭曲面用**补面法**，内侧曲面记得**变号**。

---

## 📎 相关笔记

**课程**：[[00 高等数学索引|高等数学]] ｜ **上一篇**：[[第二型曲面积分]] ｜ **下一篇**：[[Stokes 公式]] ｜ **速查**：[[高等数学下册_公式定理精华总结|公式定理精华]]

- [[格林公式]] —— 二维版本：闭曲线 → 二重积分
- [[第二型曲面积分]] —— Gauss 公式的左端对象
- [[Stokes 公式]] —— 空间曲线版本
