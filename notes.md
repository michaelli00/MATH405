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


