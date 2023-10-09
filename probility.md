# Probability & Leaner Algebra

## 1.  Determinant Calculation 行列式计算

### 1.1 初等变幻

对于2阶行列式 $`A = \left|\begin{array}{cc}a_{11}&a_{12}\\a_{21}&a_{22}\end{array}\right|`$进行初等变幻，有如下几种方式：

1. 行/列间加减：$`A = \left|\begin{array}{cc}a_{11}-k*a_{21}&a_{12}-k*a_{22}\\a_{21}&a_{22}\end{array}\right|`$
2. 行/列乘除：$`k*A = \left|\begin{array}{cc}k*a_{11}&k*a_{12}\\a_{21}&a_{22}\end{array}\right|`$

### 1.2 行列式求值

#### 1.2.1 二/三阶行列式求值公式

对于二阶行列式 $`A=\left|\begin{array}{cc}a_{11}&a_{12}\\\\a_{21}&a_{22}\end{array}\right|`$, 其求值公式为:
    $`A=a_{11}*a_{22}-a_{12}*a_{21}`$

对于三阶行列式 $`A=\left|\begin{array}{ccc}a_{11}&a_{12}&a_{13}\\a_{21}&a_{22}&a_{23}\\a_{31}&a_{32}&a_{33}\end{array}\right|`$, 其求值公式为：
    $`A=a_{11}*a_{22}*a_{33}+a_{12}*a_{23}*a_{31}+a_{21}*a_{32}*a_{13}-a_{13}*a_{22}*a_{31}-a_{23}*a_{32}*a_{11}-a_{12}*a_{21}*a_{33}`$

#### 1.2.2 n阶行列式求解 & 代数余子式

## 2. 矩阵相关

### 2.1 逆矩阵

由于$`A^*A = |A|E`$, 因此可得$`{A^* \over |A|} = A^{-1}`$, 其中 $`A^*`$是A的伴随矩阵，由代数余子式构成。但满足此条件必须要求$`|A|\ne0`$，否则A不可逆。

例如对于矩阵$`A=\left[\begin{array}{ccc}1&2&3\\4&5&6\\7&8&9\end{array}\right]`$, 其伴随矩阵为：

$`A=\left[\begin{array}{rrr}(5*9-6*8)&-(4*9-6*7)&(4*8-5*7)\\-(2*9-3*8)&(1*9-3*7)&-(1*8-2*7)\\(2*6-3*5)&-(1*6-4*3)&(1*5-2*4)\end{array}\right] = \left[\begin{array}{rrr}-3&6&-3\\6&-12&6\\-3&6&-3\end{array}\right]`$

但是经计算A的行列式|A| = 0，因此A是不可逆矩阵。很显然计算出的A的伴随矩阵A*并不满秩R(A*) = 1，因此也不可逆。

伴随矩阵和原矩阵秩的关系。若A满秩R(A)=n则R(A*)=n。若不满秩$`R(A)=n-1`$则$`R(A*)=1`$。其余情况$`A^*`$为0矩阵， $`R(A*)=0`$.

### 2.2 Eigenvalue & Eigenvector 特征值和特征向量

对于n阶矩阵$`A=\left[\begin{array}{cccc}a_{11}&a_{12}&...&a_{1n}\\a_{21}&a_{22}&...&a_{2n}\\...&...&...&...\\a_{n1}&a_{n2}&...&a_{nn}\end{array}\right]`$，其特征值$\lambda$求解方程为：$`|\lambda E-A|=0`$

求出lambda后，将lambda代回$`|\lambda E-A|=0`$中解齐次方程组，得到X的非零解即为特征向量。

## 3. Probbility Theories 概率论

### 3.1 Bayes 贝叶斯

$`P(AB) = P(A|B)*P(B) = P(B|A)*P(A)`$

从袋子里取球，黑球为A， 白球为B。取两次球第一次为A的概率。这是先验概率$p = P(A)$。取两次球且已知第二次为B，求第一次为A的概率，这是后验概率$`p=P(A|B)={P(AB)\over P(B)}`$

### 3.2 Markov Process 马可夫链

Markov Chain的核心是state之间的转换。 对于Markov chain可以用来解决很多复杂的实际问题。

Markov Chain有一个Initial State $\pi=[p_1,p_2,...,p_n]$ 对应物体n个初始状态的分布概率。

还有一个状态转移方阵$`R=\left[\begin{array}{cccc}p_{11}&p_{12}&...&p_{1n}\\p_{21}&p_{22}&...&p_{2n}\\...&...&...&...\\p_{n1}&p_{n2}&...&p_{nn}\end{array}\right]`$， 其中R(i,j)表示第i个状态向第j个状态转移的概率

比如抛N次的硬币，出现至少连续M次的概率，就是:

$`p = P_{1*m}[M]; P_{1*m} = \pi_{1*m}*R_{m*m}^N`$

其中$`R=\left[\begin{array}{ccccc}0.5&0.5&0&...&0\\0.5&0&0.5&...&0\\...&...&...&...&...\\0.5&0&0&...&0.5\\0&0&0&...&1\end{array}\right]`$, $`\pi=[1,0,0,...,0]`$

若非至少M次，而是正好M次，则转化方阵R的阶数为N, pi长度也为N。
