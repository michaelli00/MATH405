---
title: "MATH405: Linear Algebra"
author: Michael Li
geometry: "left=1cm,right=1cm,top=1cm,bottom=2cm"
header-includes:
    - \usepackage{amsmath}
    - \usepackage{mathrsfs}
    - \DeclareMathOperator{\lcm}{lcm}
    - \DeclareMathOperator{\Span}{span}
    - \DeclareMathOperator{\Null}{null}
    - \DeclareMathOperator{\range}{range}
    - \DeclareMathOperator{\matvect}{Mat$_{x \times n}(K)$}
output: pdf_document
---

\newpage

# Vector Space

Goals of this course is to discuss

- Vector spaces
- Linear transformations between vector spaces
- Other operations on vector spaces

## Definitions

**Definition - Field**: A set of numbers containing $0, 1$ that can be added, subtracted, multiplied, and divided (except cannot divide by $0$) that satisfy the following **Field Axioms**

1. $a,b \in K \implies a + b, ab \in K$
2. $+, \times$ are commutative so $a + b = b+ a$ and $ab = ba$
3. $+, \times$ are associative so $(a + b) + c= a + (b + c)$ and $a(bc) = (ab)c$
4. Distributive Law: $a(b + c) = ab + ac$
5. Additive Identity: $a + 0 = 0 + a = a$
6. Multiplicative Identity: $a \cdot 1 = 1 \cdot a = a$
7. Additive Inverse: $\forall a \in K, \exists b$ such that $a + b = 0$, namely $b = -a$ which is unique
8. Multiplicative Inverse: $\forall a \in K, \exists b$ such that $ab = 1$, name $b = 1/a$ which is unique

- **Example**: $R, Q$ are fields. $Z$ is not a field since there is no multiplicative inverse of $2$

&nbsp;

**Example**: $C = \{a + bi \mid a, b \in R\}$, where $i = \sqrt{-1}$ is a field under

- $+:$ $(a+bi) + (c + di) = (a + c) + (b + d)i$
- $\times:$ $(a + bi) (c + di) = (ac - bd) + (ad + bc)i$

&nbsp;

**Example**: $F_2 = \{0, 1\}$ is a field under

- $+:$ where

    $0 + 0 = 0$

    $0 + 1 = 1 + 0 = 1$

    $1 + 1 = 0$

- $\times:$ where

    $0 \cdot 0 = 0$

    $0 \cdot 1 = 1 \cdot 0 = 0$

    $1 \cdot 1 = 1$

&nbsp;

**Example**: For a prime $p$, let $F_p = \{0, \ldots, p-1\}$. Then $F_p$ is a field under

- $+:$ $a + b \pmod{p}$
- $\times: ab \pmod{p}$

&nbsp;

**Definition - Vector Space**: For an arbitrary field $K$, a $K$-vector space is a set $V$ with a distinguished element $O$ such that any 2 elements in $V$ can be added and scalar multiplied by $c \in K$

- $u, v \in V \implies u + v \in V$
- $c \in K, u \in V \implies cu \in V$

Satisfying the following properties

1. Commutative Addition: $u + v = v + u$
2. Associative Addition: $(u + v) + w = u + (v + w)$
3. Additive Identity: $u + O = u$
4. Additive Inverse: $\forall u \in V, \exists v \in V$ such that $u + v = O$, namely $v = -u$ which is unique
5. Distributive Laws: $\forall a,b \in K, a(u + v) = au + av$ and $(a + b)u = au + bu$
6. Commutative Scalar Multiplication: $(ab)u = a(bu)$
7. Multiplicative Identity: $1 \cdot u = u$

&nbsp;

**Example**: $R^3$ is an $R$-vector space defined by the operations
$$R^3 = \{(x, y , z) \mid x, y, z \in R\}$$

- $+:$ add componentwise so $(a,b,c) + (d, e, f) = (a + d, b + e, c + f)$
- Scalar $\times:$ for $r \in R$, $r(a, b, c) = (ra, rb, rc)$
- Additive Identity is $O = (0, 0, 0)$

&nbsp;

**Example**: For any field $K$, $K^2$ is a $K$-vector space defined by the oepartions
$$K^2 = \{(x, y) \mid x, y \in K\}$$

- $+:$ add componentwise so $(a, b) + (c, d) = (a + c, b + d)$
- Scalar $\times:$ for $k \in K$, $k(a, b) = (ka, kb)$
- Additive Identity is $O = (0, 0)$

&nbsp;

**Example**: $R$ is an $R$-vector space since clearly the properties hold

&nbsp;

**Example** $R$ is a $Q$-vector space since clearly the properties hold

- Notably, for $q \in Q$ and $r \in R$, we have $qr \in R$. Thus scalar multiplication is closed

&nbsp;

**Example**: For any field $K$, the set $\{O\}$ is a $K$-vector space

&nbsp;

**Example**: Let $X$ be any non-empty set and let $\mathcal{F}(X)$ be the set of all functions $f: X \rightarrow R$. Then $\mathcal{F}$ is an $R$-vector space under the operations



- $+:$ for $f, g \in \mathcal{F}(X)$, define $f + g:= (f + g)(x)$
- Scalar $\times:$ let $r \in R$, then define $rf:= r(f(x))$
- Additive Identity is $O = f(x) = 0$, the function that takes any $x$ to $0$

&nbsp;

**Example**: Take $X = N$ and let $F(X) = \{ \text{ all functions } f: N \rightarrow R\}$ is a vector space

- **Note**: $f: N \rightarrow R$ is a sequence $(a_0, \ldots, a_n)$ where $a_n = f(n)$

&nbsp;

**Lemma 1 - Cancellation**: For $u, v, w \in V$ and if $u + v = w + v$, then $u = w$

*Proof*: $v \in V$ has an additive inverse, namely $-v$. Thus we have
$$u + v - v = w + v - v \implies u = w$$

&nbsp;

**Lemma 2 - Unique Additive Inverse**: For all $v \in V$, there is a unique additive inverse, namely $-v$

*Proof*: Suppose $u, w$ are both additive inverses of $v$. Then we have
$$v + u = v + w \implies u = w$$

&nbsp;

**Lemma 3 - 0 Times a Vector**: For all $v \in V$, $0v = O$

*Proof*: $v = 1v = (0 + 1)v = 0v + 1v = 0v + v \implies 0v = O$

&nbsp;

**Lemma 4 - (-1)v is the Additive Inverse**: For all $v \in v, (-1)v$ is the unique additive inverse of $v$

*Proof*: $(-1)v + v = (-1 + 1)v = 0v = O$. Thus $(-1)v$ is the additive inverse of $v$, which is unique by Lemma 2

&nbsp;

**Definition - Subspace**: For a $K$-vector space $V$ and a non-empty subset $W \subseteq V$, $W$ is a **subspace** if it satisfies

- $w_1, w_2, \in W \implies w_1 + w_2 \in W$
- $\forall a \in K, w \in W \implies aw \in W$

&nbsp;

**Theorem 1**: Every subspace of a $K$-vector space is a $K$-vector space

*Proof*: We need to show that $W \subseteq V$ satisfies all the necessary properties of a vector space

1. Verify $O \in W$

    Since $W$ is non-empty and closed under scalar multiplication, take $0w = O \in W$ by Lemma 3

2. $u, v \in W \implies u + v \in W$ and $a \in K, v \in W \implies aw \in W$ by definition of subspace

3. Every $w \in W$ has an additive inverse, namely $-w$

    Since $W$ is closed under scalar multiplication, $(-1)w = -w \in W$ by Lemma 4

4. Other conditions (e.g. associative addition, commutative addition, etc.) hold because $u, v, w \in V \implies u, v, w \in W$

    For example, choose $u, v \in V$, then $u + v = v + u$, which also holds under $W$. Thus commutative addtion is satisfied

&nbsp;

**Example**: Take $(5, 3, 2) \in R^3$. Then let $W = \{r(5, 3, 2) \mid r \in R\}$

Then $W$ is an $R$-vector space. We prove this by showing that $W$ is a subspace of $R^3$

- $+:$ Choose $2$ arbitrary elements of $W$, $r(5, 3, 2)$ and $s(5, 3, 2)$ for $r, s \in R$

    Then $r(5, 3, 2) + s(5, 3, 2) = (r + s) (5, 3, 2) \in W$

- $\times:$ Choose $r(5,3, 2) \in W$ and take $s \in R$

    Then $s(r(5, 3, 2)) = (sr)(5, 3, 2) \in W$

&nbsp;

**Example**: Let $U = \{(x,y, z) \in R^3 \mid 2x + 3y = 0\}$. We show that $U$ is a vector space by showing it's a subspace of $R^3$

- $+:$ Take $(x_1, y_1, z_1)$ and $(x_2, y_2, z_2) \in U \implies 2x_1 + 3y_1 = 0$ and $2x_2 + 3y_2 = 0$

    Then $2(x_1 + x_2) + 3(y_1 + y_2) = 0$

    Thus $(x_1 + x_2, y_1 + y_2, z_1 + z_2) \in U$

- $\times:$ Let $(x, y, z) \in U$ and $r \in R$

    Then $2x + 3y = 0 \implies r(2x + 3y) 2rx + 3ry = 0$

    Thus $r(x, y, z) \in U$

&nbsp;

**Example**: Consider $\sin(x), \cos(x) \in \mathcal{F}(R)$ and let $W = \{a\sin(x) + b\cos(x) \mid a,b \in R\}$. Then $W$ is a subspace of $\mathcal{F}(R)$

- $+:$ Take $a_1 \sin(x) + b_1 \cos(x)$ and $a_2 \sin(x) + b_2 \cos(x) \in W$. Then $(a_1 + a_2) \sin(x) + (b_1 + b_2) \cos(x) \in W$
- $\times:$ Take $r \in R$. Then $r(a \sin(x) + b \cos(x)) = (ra) \sin(x) + (rb) \cos(x) \in W$
