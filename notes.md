---
title: "MATH405: Linear Algebra"
author: Michael Li
geometry: "left=1cm,right=1cm,top=1cm,bottom=2cm"
header-includes:
    - \usepackage{amsmath}
    - \usepackage{mathrsfs}
    - \DeclareMathOperator{\lcm}{lcm}
    - \DeclareMathOperator{\Span}{span}
    - \DeclareMathOperator{\mat}{Mat}
    - \DeclareMathOperator{\Null}{null}
    - \DeclareMathOperator{\range}{range}
    - \DeclareMathOperator{\Img}{Im}
    - \DeclareMathOperator{\Ker}{Ker}
    - \DeclareMathOperator{\matvect}{Mat$_{x \times n}(K)$}
    - \DeclareMathOperator{\id}{id}
    - \DeclareMathOperator{\proj}{proj}
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

&nbsp;

**Example**: $R, Q$ are fields. $Z$ is not a field since there is no multiplicative inverse of $2$

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

**Definition - Vector Space**: For an arbitrary field $K$, a $K$-vector space is a set $V$, with a distinguished element $O$, such that any 2 elements in $V$ can be added and scalar multiplied by $c \in K$

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

**Example**: For any field $K$, $K^2$ is a $K$-vector space defined by the operations
$$K^2 = \{(x, y) \mid x, y \in K\}$$

- $+:$ add componentwise so $(a, b) + (c, d) = (a + c, b + d)$
- Scalar $\times:$ for $k \in K$, $k(a, b) = (ka, kb)$
- Additive Identity is $O = (0, 0)$

&nbsp;

**Example**: $R$ is an $R$-vector space since clearly the necessary properties hold

&nbsp;

**Example** $R$ is a $Q$-vector space since clearly the necessary properties hold

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
- $O \in W$

&nbsp;

**Theorem 1**: Every subspace of a $K$-vector space is a $K$-vector space

*Proof*: We need to show that $W \subseteq V$ satisfies all the necessary properties of a vector space

1. Verify $O \in W$

    Since $W$ is non-empty and closed under scalar multiplication, take $0w = O \in W$ by Lemma 3

2. $u, v \in W \implies u + v \in W$ and $a \in K, v \in W \implies aw \in W$ by definition of subspace

3. Every $w \in W$ has an additive inverse, namely $-w$

    Since $W$ is closed under scalar multiplication, $(-1)w = -w \in W$ by Lemma 4

4. Other conditions (associative addition, commutative addition, etc.) hold because $u, v, w \in W \implies u, v, w \in V$

    For example, choose $u, v \in W$, then $u + v = v + u$, since $u, v \in V$. Thus commutative addtion is satisfied

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

    Then $2x + 3y = 0 \implies r(2x + 3y) = 2rx + 3ry = 0$

    Thus $r(x, y, z) \in U$

&nbsp;

**Example**: Consider $\sin(x), \cos(x) \in \mathcal{F}(R)$ and let $W = \{a\sin(x) + b\cos(x) \mid a,b \in R\}$. Then $W$ is a subspace of $\mathcal{F}(R)$

- $+:$ Take $a_1 \sin(x) + b_1 \cos(x)$ and $a_2 \sin(x) + b_2 \cos(x) \in W$. Then $(a_1 + a_2) \sin(x) + (b_1 + b_2) \cos(x) \in W$
- $\times:$ Take $r \in R$. Then $r(a \sin(x) + b \cos(x)) = (ra) \sin(x) + (rb) \cos(x) \in W$

## Basis

**Definition - Linear Combination**: For vectors $\{v_1, \ldots, v_n\} \subseteq V$, a **linear combination** of $\{v_1, \ldots, v_n\}$ is a vector of the form
$$a_1 v_1 + \cdots + a_n v_n \quad \quad a_i \in K$$

&nbsp;

**Definition - Span**: $\Span(\{v_1, \ldots, v_n\}) = \{\text { all linear combinations of } \{v_1, \ldots, v_n\}\}$

&nbsp;

**Proposition 1**: $W = \Span(\{v_1, \ldots, v_n\})$ is a subspace of $V$ and thus is itself a $K$-Vector Space

*Proof*: We show that $W$ satisfies the necessary criteria to be a subspace of $V$

- $+:$ Let $a = a_1 v_1 + \cdots + a_n v_n \in W$ and $b = b_1 v_1 + \cdots + b_n v_n \in W$

    Then $a + b = (a_1 + b_1) v_1 + \cdots + (a_n + b_n)v_n \in W$

    Thus $W$ is closed under addition

- Scalar $\times:$ Let $a = a_1 v_1 + \cdots + a_n v_n \in W$ and let $c \in K$

    Then $ca = (c a_1)v_1 + \cdots + (c a_n)v_n \in W$

    Thus $W$ is closed under scalar multiplication

&nbsp;

**Example**: Take $(5, 3, 1)$ and $(4, 0 , -2) \in R^3$

$\Span(\{(5, 3, 1), (4, 0, -2)\})$ is a plane in $R^3$ passing through $(0, 0, 0)$

&nbsp;

**Example**: Take $(5, 3, 1)$ and $(10, 6 , 2) \in R^3$

$\Span(\{(5, 3, 1), (10, 6, 2)\})$ is a line in $R^3$ passing through $(0, 0, 0)$

- **Note**: $(10, 6, 2) = 2(5, 3, 1)$. Thus $\Span(\{(5, 3, 1), (10, 6, 2)\}) = a_1 (5, 3, 1) + a_2 (10, 6, 2) = (a_1 + 2a_2) (5, 3, 1)$

&nbsp;

**Definition - Linearly Independent**: $\{v_1, \cdots, v_n\}$ is **linearly independent** if whenever $a_1 v_1 + \cdots + a_n v_n = 0$, then $a_1 = \cdots = a_n = 0$

- Otherwise $\{v_1, \ldots, v_n\}$ is **linearly dependent**

&nbsp;

**Proposition 2**: $\{v_1, \ldots, v_n\}$ is linearly independent if and only if no $v_i$ is a linearly combination of the other $n-1$ vectors

*Proof*: $\implies$ Assume $\{v_1, \ldots, v_n\}$ is linearly independent

BWOC, assume some $v_i = a_1 v_1 + \cdots + a_n v_n$ for some $v_i \notin \{v_1, \ldots, v_n\}$

Then we have
$$O = a_1 v_1 + \cdots + a_n v_n + (-1)v_i$$
Since $v_i$ is a linear combination of $\{v_1, \ldots, v_n\}$, the above equation shows that $\{v_1, \ldots, v_n\}$ is linearly dependent. Contradiction

Thus $v_i$ cannot be written as a linear combination of the other vectors

$\impliedby$ Assume by way of contraposition that $\{v_1, \ldots, v_n\}$ is not linearly independent

Thus choose $a_1, \ldots, a_n \in K$, not all $0$ such that

$$a_1 v_1 + \cdots + a_n v_n = O$$
WLOG, assume $a_1 \neq 0$. Then $v_2 a_2 + \cdots + a_n v_n = a_1 v_n$

Since $a_1 \neq 0$ and $K$ is a field, we have
$$v_1 = \frac{a_2}{-a_1} v_2 + \cdots + \frac{a_n}{-a_1}v_n$$
Thus we have shown that $v_1$ is a linear combination of the other $n-1$ vectors

&nbsp;

**Corollary 3**: $\{v_1, \ldots, v_n\}$ is linearly independent if and only if for each $i$, $v_i \notin \Span(\{v_1, \ldots, v_n\} \setminus \{v_i\})$

*Proof*: This follows from the previous proposition

&nbsp;

**Definition - Spans**: Let $W$ be a $K$-Vector Space and $\{v_1, \ldots, v_n\} \subseteq W$. If $\Span(\{v_1, \ldots, v_n\}) = W$, then $\{v_1, \ldots, v_n\}$ **spans** $W$, so every $w \in W$ is a linear combination of $\{v_1, \ldots, v_n\}$

&nbsp;

**Definition - Basis**: $\{v_1, \ldots, v_n\}$ is a **basis** of $W$ if it spans $W$ and is linearly independent

&nbsp;

**Example**: $\{(5, 3, 1), (4, 0, -2)\}$ is a basis for $\Span(\{(5, 3, 1), (4, 0, -2)\})$

**Example**: $\{(5, 3, 1), (10, 6, 2)\}$ is not a basis for $\Span(\{(5, 3, 1), (10, 6, 2)\})$ since it is not linearly independent

&nbsp;

**Proposition 4**: Let $\{v_1, \ldots, v_n\}$ be a basis for $W$ and let $w \in W$ be arbitrary. Then $w$ can be written uniquely as
$$w = a_1 v_1 + \cdots + a_n v_n \quad \quad a_i \in K$$

*Proof*: Since $\{v_1, \ldots, v_n\}$ spans $W$, every $w \in W$ is a linear combination of $\{v_1, \ldots, v_n\}$

For uniqueness, suppose
$$w = a_1 v_1 + \cdots + a_n v_n = b_1 v_1 + \cdots + b_n v_n$$
Then we have
$$O = (b_1 - a_1) v_1 + \cdots (b_n - a_n)$$
Since $\{v_1, \ldots, v_n\}$ is linearly independent, we must have $b_i - a_i = 0$, and thus $b_i = a_i$ for each $i$

Thus each $w \in W$ can be written uniquely as a linear combination of $\{v_1, \ldots, v_n\}$

&nbsp;

**Example**: Let $W = \Span(\{\sin(x), \cos(x)\} = \{a \sin(x) + b \cos(x) \mid a, b \in R\}$

We know that $W$ is an $R$-Vector Space

$\{ \sin(x), \cos(x)\}$ is linearly independent. Otherwise $\sin(x) = r \cos(x)$ for all $x \in X$ and some $r \in R$. However, this cannot hold for when $x = \pi / 2$ since $\sin(\pi / 2) = 1 \neq r \cos(\pi / 2) = r0$

## Dimension

Let $\{v_1, \ldots, v_n\} \subseteq V$ and let $W = \Span(\{v_1, \ldots, v_n\})$

Now let $X = \{w_1, \ldots, w_m\} \subseteq W$. Then there are 2 desirable properties of $X$

- **X is Big**: $X$ spans $W$ if $\Span(X) = W$, i.e. all $w \in W$ is a linear combination of elements from $X$
- **X is Small**: $X$ is linearly independent, i.e. no element in $X$ is a linear combination of the remaining elements

**Note**: the empty set $\emptyset$ is linearly independent since no element in $\emptyset$ is a linear combination of the others. More notably, $\emptyset$ is a basis for $\{O\}$

&nbsp;

**Shrinking Lemma**: Let $X = \{w_1, \ldots, w_m\} \subseteq W$ and spans $W$ but $X$ is not linearly independent. Then $X \setminus \{w_i\}$ still spans $W$ for some $w_i \in X$

*Proof*: Since $X$ is not linearly independent, we know that some $w_i$ is a linear combination of elements in $X \setminus \{w_i\}$. Suppose
$$w_i = a_1 w_1 + \cdots + a_m w_m \quad \quad \text{ without $w_i$ occurring}$$


Then take arbitrary $u \in W$ where
$$u = b_1 w_1 + \cdots + b_m w_m$$
Replacing $w_i$ above with the previous equation, we see that $u$ is a linear combination of $X \setminus \{w_i\}$

Thus $X \setminus \{w_i\} = \Span(W)$

&nbsp;

**Shrinking Theorem**: Let $X = \{w_1, \ldots, w_m\}$ span $W$. Then for some subset $Y \subseteq X$ is a basis of $W$

*Proof*:

Case 0: If $X$ is linearly independent, then $X$ is a basis by definition

Otherwise, apply the shrinking lemma to get $X_1 = X \setminus \{w_i\}$, which spans $W$

Case 1: If $X_1$ is linearly independent, then $X_1$ is a basis

$\ldots$

Since $X$ is finite (it has $m$ elements), we will stop eventually. Either

- Some $X_i$ is linearly independent. Thus $X_i$ is a basis for $W$
- Otherwise if we hit case m: $X_m = \emptyset$, which is linearly independent, and thus $X_m$ spans $W = \{O\}$

&nbsp;

**Corollary**: If $W = \Span(\{v_1, \ldots, v_n\})$, then some subset of $\{v_1, \ldots, v_n\}$ is a basis

- **Note**: In particular, $W$ has to have a basis

&nbsp;

**Enlarging Lemma**: Suppose $X = \{w_1, \ldots, w_m\} \subseteq W$ and is linearly independent but doesn't span $W$. Then for any $w \in W \setminus \Span(X)$, $X \cup \{w\}$ is still linearly independent

*Proof*: Suppose $a_1 w_1 + \cdots + a_m w_m + bw = O$. We show that $a_1 = \cdots = a_m = b = 0$

Suppose BWOC, $b \neq 0$, then we can solve for $w$
$$w = \frac{-a_1}{b}w_1 + \cdots + \frac{-a_m}{b}w_m$$
Which means that $w \in \Span(X)$. Contradiction

Thus $b = 0$. This gives
$$a_1 w_1 + \cdots + a_m w_m + 0w = O$$
Since $X = \{w_1, \ldots, w_m\}$ is linearly independent, we also have $a_1 = \cdots = a_m = 0$

Thus $X \cup \{w\}$ is linearly independent

&nbsp;

**Main Question**: does the enlarging process above terminate? After some steps, do we get a set $\{w_1, \ldots, w_m\}$ that spans $W$?

&nbsp;

**Exchanging Lemma**: Let $X = \{v_1, \ldots, v_n\}$ be any basis for $W$. Choose any $w \in W$ but $w \notin \Span(\{v_k, \ldots, v_n\})$. Then $\exists v_i, i < k,$ such that $Y = (X \setminus \{v_i\}) \cup \{w\}$ is still a basis

- **Note**: If $k > n$, then $\{v_k, \ldots, v_n\} = \emptyset$

*Proof*: First we show that $\Span(Y) = W$. Since $X$ spans $W$, we can write
$$w = a_1 v_1 + \cdots + a_n v_n \implies v_1 = \frac{1}{a_1}w + \frac{-a_2}{a_1}v_2 + \cdots + \frac{-a_m}{a_1}v_m$$
Since $w \notin \Span(\{v_k, \ldots, v_n\})$, we must have $a_i \neq 0$ for some $i < k$

WLOG, let $a_1 \neq 0$. We show that $Y$ spans $W$

Since $X$ spans $W$, for arbitrary $u \in W$, we have
$$u = d_1 v_1 + \cdots + d_n v_n$$
Replacing $v_1$ above with the previous equation, we see that $u$ is a linear combination of elements of $Y$ and thus $u \in \Span(Y)$

Thus $\Span(Y) = W$

Next we show that $Y$ is linearly independent

Suppose we have
$$cw + b_2 v_2 + b_n v_n = O$$
We show that $c = b_2 = \cdots = b_n = 0$

- If $c = 0 \implies b_2 = \cdots = b_n = 0$ since $\{b_2, \ldots, b_n\}$ is linearly independent
- Otherwise suppose $c \neq 0$, then we can solve for $w$
$$w = \frac{-b_2}{c}v_2 + \cdots + \frac{-b_n}{c}v_n \implies v_1 = \frac{1}{a_1}(\frac{-b_2}{c}v_2 + \cdots + \frac{-b_n}{c}v_n) + \frac{-a_1}{a_1}v_2 + \cdots + \frac{-a_m}{a_1v_m}$$
Thus $v_1$ is a linear combination of $\{v_2, \ldots, v_n\}$. Contradiction since we said $X$ was linearly independent. Thus $c = 0$

&nbsp;

**Theorem**: Let $X = \{v_1, \ldots, v_n\}$ be a basis for $W$, and let $\{w_1, \ldots, w_m\} \subseteq W$ be linearly independent. Then $m \leq n$

*Proof*: If $m < n$, we are done

Now assume $m \geq n$, we show that $m = n$

Since $\{w_1, \ldots, w_m\}$ is linearly independent, we have that $w_1 \neq O = \Span(\emptyset)$

Now apply the Exchanging Lemma to the basis $X$, with $k > n$ and $w_1$ Then $\exists v_i$ such that $X_1 = (X \setminus \{v_i\}) \cup \{w_1\}$ is a basis

After reindexing, we see that $X_1$ has $n-1$ vectors from $X$ and $1$ vector from $w_1$


Now take $k = n$. Since $\{w_1, \ldots, w_m\}$ is linearly independent, $w_2 \notin \Span(\{w_1\})$

Thus applying the Exchanging Lemma again, there exists $j < k = n$ such that $X_2 = (X_1 \setminus \{v_j\}) \cup \{w_2\}$ is a basis

Reindexing again, we get that $X_2 = \{v_1, \ldots, v_{n-2}, w_1, w_2\}$ is a basis

&nbsp;

After $n$ steps, $X_n$ has no elements from $X$ and $X_n = \{w_1, \ldots, w_n\}$ is a basis

Furthermore, we see that $w_m \in \Span(\{w_1, \ldots, w_n\})$, contradicting that $\{w_1, \ldots, w_m\}$ is linearly independent

Thus $m = n$

&nbsp;

**Corollary**: If $W$ is any $K$-vector space and some basis of $W$ has $n$ elements, then every basis of $W$ has $n$ elements

&nbsp;

**Definition - Finite Dimensional**: Let $W$ be a $K$-vector space. Then $W$ is **finite dimensional** if some basis for $W$ is finite

&nbsp;

**Definition - Dimension**: Number of elements in any basis for a vector space $W$

&nbsp;

**Corollary**: Suppose $\dim(W) = n$ and $X = \{w_1, \ldots, w_n\}$ are any $n$-vectors

1. If $X$ spans $W$, then $X$ is a basis for $W$
2. If $X$ is linearly independent, then $X$ is a basis for $W$

*Proof*:

1. By Shrinking Theorem, there exists a basis $Y \subseteq X$

    However, $|Y| < n$ contradicts that $\dim(W) = n$

    Thus $Y = X$, i.e. $X$ is a basis

2. By Enlarging Lemma, we can expand $X$ to a basis $Y$

    However, $|Y| > n$ contradicts that $\dim(W) = n$

    Thus $Y = X$, i.e. $X$ is a basis

### Toolbox Corollaries and Results

The following are useful corollaries that can be used to prove additional interesting results

Let $V$ be a $K$-Vector Space with $\dim(V) = n$, i.e. $V$ has some basis with $n$ elements

1. Every basis for $V$ has $n$ elements
2. If $X \supseteq V$ and $\Span(X) = V$, then $X$ has at least $n$ elements and some subset $Y \subseteq X$ is a basis for $V$
3. If $Z \subseteq V$ is linearly independent, then $Z$ has at most $n$ elements and $Z$ can be extended to a basis $Y \supseteq Z$ for $V$

&nbsp;

**Example**: Let $V = R^3$. Since $\dim(V) = 3$, $V$ has a basis with $3$ elements

- Consider the **Standard Basis**: $B = \{(1, 0, 0), (0, 1, 0), (0, 0, 1)\}$

Suppose $X = \{v_1, v_2, v_3\} \subseteq V$ for arbitrary vectors

- If $\Span(X) = V$ then $X$ is a basis
- If $X$ is linearly independent, since $|X| = 3$, $X$ is a basis for $V$

&nbsp;

**Example**: Describe all subspaces $W \subseteq R^3$

**Note**: Since $\dim(V) = 3$, we must have $\dim(W) \leq \dim(V) = 3$

- Case 0: $\dim(W) = 0$

    Clearly $W = \{O\}$

- Case 1: $\dim(W) = 1$

    $W$ is a line going through $(0, 0, 0)$

    Thus a basis for $W$ will be $\{w\}$ for any nonzero $w \in W$

- Case 2: $\dim(W) = 2$

    $W$ is a plane containing $(0, 0, 0)$

    Thus a basis for $W$ will be any 2 element set $\{w_1, w_2\} \subseteq W$ such that

    - Neither element is $O$
    - $w_2$ is not a scalar multiple of $w_1$

- Case 3: $\dim(W) = 3$

    Only possibility is $W = V = R^3$

&nbsp;

**Examples**: Consider subspaces of $\mathcal{F}(R)$ and look at small subspaces

- $W = \Span(\{e^x\}) = \{re^x \mid r \in R\}$

    This can be thought of as a 1-dimensional subpsace of $\mathcal{F}(R)$

- $V = \Span(\{\sin(x), \cos(x)\}) = \{a \sin(x) + b \cos(x) \mid a, b \in R\}$

    Clearly $\dim(V) = 2$

    Consider $f(x) = \sin(x) \quad g(x) = \cos(x) \quad h(x) = 3 \sin(x) - 2 \cos(x)$

    Since $h = 3f + (-2)g$, $\{f, g, h\}$ is not linearly independent

    Thus $\Span(\{f, g, h\}) = \Span(\{f, g\})$

## Direct Sums

Let $V$ be a $K$-Vector Space with $\dim(V) = n$. Let $W \subseteq V$ be a subspace of $V$. Then $\dim(W) \leq n$

Now choose another subspace $U \subseteq V$

**Note**: $W \cap U \neq \emptyset$ since both must contain $O$

Thus the smallest we can make $W \cap U$ is $\{O\}$

Furthermore, it can be shown that both $U \cap W$ and $U + W$ are both subspaces of $V$

**Definition - Direct Sum**: $U \oplus W$ is called a **direct sum** if

- $U \oplus W = U + W$
- $U \cap W = \{O\}$

We often look at cases where $V = U \oplus W$

&nbsp;

**Example**: Consider $R^3$ and let $W$ be any plane containing $(0, 0, 0)$

If $U$ is any line through $(0, 0, 0)$ such that $U \notin W$, then $R^3 = W \oplus U$

&nbsp;

**Theorem**: Let $V$ be a $K$-Vector Space with $\dim(V) = n$. Let $W \subseteq V$ be any subspace of $V$. Then there exists a subspace $U \subseteq V$ such that
$$V = U \oplus W$$

*Proof*: Choose any basis $Z = \{w_1, \ldots, w_m\}$ of $W$ (we know that $m \leq n$)

Now extend $Z$ to $Y = Z \cup \{u_1, \ldots, u_r\}$, which is a basis for $V$

Let $U = \Span(\{u_1, \ldots, u_r\})$. Then $U$ is a subspace of $V$ and $\{u_1, \ldots, u_r\}$ is a basis for $U$

- Show that $U \cap W = \{O\}$

    Choose $v \in U \cap W$

    Then we have $v = a_1u_1 + \cdots + a_ru_r = b_1w_1 + \cdots + b_m w_m$

    Since $Y$ is a basis for $V$, then $\{u_1, \ldots, u_r, b_1, \ldots, b_m\}$ is linearly independent

    Thus $v-v = a_1 u_1 + \cdots + a_r u_r - b_1w_1 - \cdots - b_m w_m = O \implies a_1 = \cdots = a_r = b_1 = \cdots = b_m = 0$

    Thus $v = O$

- Show that $V = U + W$

    Choose any $v \in V$

    Since $Y$ is a basis for $V$

    $v = \underbrace{a_1 u_1 + \cdots + a_r u_r}_{u \in U} + \underbrace{b_1 w_1 + \cdots + b_m w_m}_{w \in W}$

    Thus $v = u + w \implies V = U + W$

# Matrices

**Definition - $\mathbf{m \times n}$ Matrix**: Entries $\in K$ of the form
$$A = \begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & \cdots & \cdots & a_{mn}\end{bmatrix}$$

&nbsp;

**Example**: $A = \begin{bmatrix} 4 & 0 & 2 \\ -1 & 3 & 6\end{bmatrix}$ is a $2 \times 3$ matrix with entries $\in Q$

&nbsp;

**Note**: Any $2 \times 3$ matrices can be added together componentwise or multiplied by a scalar, resulting in a $2 \times 3$ matrix

- Here the additive identity is $\begin{bmatrix} 0 & 0 & 0 \\ 0 & 0 & 0\end{bmatrix}$
- Here the additive inverse of $A$ (from previous example) is $-A = \begin{bmatrix} -4 & 0 & -2 \\ 1 & -3 & -6\end{bmatrix}$

Thus $\mat_{2 \times 3}(K)$, the set of all $2 \times 3$ matrices with entries in $K$ is a $K$-Vector Space

Here the basis is $B = \{\begin{bmatrix} 1 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}, \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 0 \end{bmatrix}, \begin{bmatrix} 0 & 0 & 1 \\ 0 & 0 & 0 \end{bmatrix}, \begin{bmatrix} 0 & 0 & 0 \\ 1 & 0 & 0 \end{bmatrix}, \begin{bmatrix} 0 & 0 & 0 \\ 0 & 1 & 0 \end{bmatrix}, \begin{bmatrix} 0 & 0 & 0 \\ 0 & 0 & 1 \end{bmatrix}\}$

- Clearly spans since any $2 \times 3$ matrix $\begin{bmatrix} a_1 & a_2 & a_3 \\ a_4 & a_5 & a_6\end{bmatrix}$ can be written as a linear combination of elements in $B$
- Clearly $B$ is linearly independent since the only way to write $O$ is to take each scalar $a_i = 0$

Thus $\dim(\mat_{2 \times 3}(K)) = 6$

&nbsp;

**Upshot**: We can generalize the discussion above to show that $\mat_{m \times n}(K)$ is a $K$-Vector Space of $\dim = m \times n$

&nbsp;

**Example**: $\{\begin{bmatrix} a & b \\ b & d\end{bmatrix}\}$, **symmetric $\mathbf{2 \times 2}$ matrices**, is a subspace of $\mat_{2 \times 2}(K)$, which has dimension $4$

&nbsp;

**Non-Example**: $\mat(K)$ is NOT a Vector Space since addition between $2 \times 2$ and $3 \times 3$ matrices is not defined

&nbsp;

**Notation**: $A_i = (a_{i1}, \ldots, a_{in})$, the $i$th row vector, is a $1 \times n$ matrix

**Notation**: $A^j = (a_{1j}, \ldots, a_{mj})$, the $j$th column vector, is a $m \times 1$ matrix

&nbsp;

**Definition - Transpose**: Given an $m \times n$ matrix $A$, the **transpose** $^t A$ is an $n \times m$ matrix that swaps the rows and columns, and vice versa

- **Note**: If $A$ is a square $n \times n$ matrix, then $^t A$ is also a square $n \times n$ matrix

&nbsp;

**Example**: $^t \begin{bmatrix} 4 & 0 & 3 \\ -1 & 3 & 0\end{bmatrix} = \begin{bmatrix} 4 & -1 \\ 0 & 3 \\ 2 & 6\end{bmatrix}$

&nbsp;

**Definition - Matrix Multiplication**: An $m \times n$ matrix $A$ can multiply with an $n \times k$ matrix $B$ where
$$C_{il} = \sum_{d=1}^{n}a_{ij} b_{d, l}$$

- **Note**: If $A, B$ are both $n \times n$ matrices, then $AB$ is an $n \times n$ matrix
- **Upshot**: Square matrices are closed under transposition and matrix multiplication

&nbsp;

**Example**: $\begin{bmatrix} 2 & 3 & 4 \\ 0 &1 & 2\end{bmatrix} \begin{bmatrix} 6 \\ 2 \\ 1\end{bmatrix} = \begin{bmatrix} 22 \\ 4\end{bmatrix}$

&nbsp;

## Linear Equations

Consider
\begin{align*}
 5x_1 + 3x_2 - 6x_3 &= 8 \\
 x_1 - 2x_2 + x_3 = 4
\end{align*}
We can represent this using
$$A = \begin{bmatrix} 5 & 3 & -6 \\ 1 & -2 & 1\end{bmatrix} \quad \quad X = \begin{bmatrix} x_1 \\ x_2 \\ x_3\end{bmatrix} \quad \quad B = \begin{bmatrix} 8 \\ 4 \end{bmatrix} \implies AX = B$$

# Mappings

**Definition - Function**: Mapping between 2 sets $D, R$ such that for each $x \in D$, there exists a unique $y \in R$ such that $f(x) = y$
$$F: D \rightarrow R$$

- **Note**: $D$ here is the **domain** of $F$ and $R$ is the **range** of $F$

&nbsp;

**Definition - Image**: $F(D) = \{F(x) \mid x \in D\} \subseteq R$

&nbsp;

**Example**: $F: R \rightarrow R \quad \quad F(x) = x^2$

- Domain($F$) = Range($F$) = $R$
- Image of $F = \{y \in R \mid y \geq 0\} = [0, \infty)$

&nbsp;

**Example**: $G[0, \infty) \rightarrow R \quad \quad G(x) = \sqrt{x}$

- Image of $G = [0, \infty)$

&nbsp;

**Example**: $\mathcal{F} =$ all functions $F: \rightarrow R$

Let $S$ be all "infinitely" differentiable functions

Let $\frac{d}{dx} : S \rightarrow S$ where $\frac{d}{dx}(f) = f'$

Thus $\frac{d}{dx}$ is a function

&nbsp;

**Example**: $t: \mat_{2 \times 3}(K) \rightarrow \mat_{3 \times 2}(K)$

Then $t(A) = ^tA$ is a function

&nbsp;

**Definition - Onto**: A function $F: D \rightarrow R$ is **onto** if Image of $F = R$

**Definition - 1-1**: A function $F: D \rightarrow R$ is **1-1** if different elements from $D$ get mapped to different elements of $R$
$$F(d) = F(e) \implies d = e$$

**Definition - Bijection**: A function that is both onto and 1-1

&nbsp;

**Definition - Inverse Function**: If $F:D \rightarrow R$ is a bijection, there exists an inverse function $F^{-1}: R \rightarrow D$ such that
\begin{align*}
\forall r, \in R, F(F^{-1}(r)) &= r\\
\forall d, \in D, F^{-1}(F(d)) &= d
\end{align*}

&nbsp;

**Definition - Linear Transformation**: For fixed $K$-Vector Spaces $V, W$, a **linear transformation** $T: V \rightarrow W$ is a function satisfying

1. $\forall v_1, v_2 \in W$, $T(v_1 + v_2) = T(v_1) + T(v_2)$
2. $\forall c \in K, v \in W$, $T(cv) = cT(v)$

&nbsp;

**Examples**

1. $F: R \rightarrow R, F(x) = x^2$

    - Not onto since $x^2$ cannot be negative
    - Not 1-1 since $1^2 = (-1)^2 = 1$
    - Not a linear transformation since $(1 + 2)^2 = 9 \neq 1^2 + 2^2$
2. $F: [0, \infty) \rightarrow R, F(x) = \sqrt{x}$

    - Not onto since $x^2$ cannot be negative
    - 1-1 since $\sqrt{x} = \sqrt{y} \implies x = y$
    - Not a linear transformation since $[0, \infty)$ isn't a Vector Space
3. Let $S$ be the set of all infinite differentiable functions. Consider $\frac{d}{dx}: S \rightarrow S$ where $\frac{d}{dx}(f) = f'$

    - Onto by the Fundamental Theorem of Calculus
    - Not 1-1 since $f$ and $f+ 5$ share the same derivative
    - Is a linear transformation by addition and scalar multiplication properties of derivatives

4. Let $C$ be the set of continuous functions on $[0, 1]$. Consider $I: C \rightarrow R, I(f) = \int_0^1 f(t) \, dt$

    - Onto since we can generate any value of $R$ by taking the integral of the constant function
    - Not 1-1 since the definite integral of $2$ functions could yield the same result
    - Is a linear transformation by additional and scalar multiplication properties of integrals

5. $I^*: G \rightarrow C, I^*(f) =  \int_0^x f(t) \, dt$

    - Not onto since not all functions of $f(0) = 0$
    - 1-1 since indefinite integral yields a unique function
    - Is a linear transformation by additional and scalar multiplication properties of integrals

6. Fix $(4, 0, 2)$ and consider $T_{(4, 0, 2)}: R^3 \rightarrow R^3, T_{(4, 0, 2)}((x, y, z)) = (x + 4, y, z + 2)$

    - Clearly onto
    - Clearly 1-1
    - Not a linear transformation since $T_{(4, 0, 2)}((0, 0, 0) + (1, 1, 1)) = (5, 0, 3) \neq T_{(4, 0, 2)}((0, 0, 0)) + T_{(4, 0, 2)}((1, 1, 1))$

7. $E_\pi: R^3 \rightarrow R^3, E_\pi((x, y, z)) = (\pi x, \pi y, \pi z)$

    - Clearly onto
    - Clearly 1-1
    - Is a linear transformation since $E_\pi((a, b, c) + (d, e, f)) = (\pi(a + d), \pi (b + e), \pi (c + f)) = E_\pi((a, b, c)) + E_\pi((d, e, f))$

## Consequences of Properties of Linear Transformations

**Proposition**:  For any linear transformation $T: V \rightarrow W$, we have that
$$T(O_V) = O_W$$
*Proof*: Let $w = T(O_V)$

Since $O_V = 0 * O_V$, we have that
$$T(O_V) = T(0 * O_V) = 0 * T(O_V) = 0 * w = O_W$$

&nbsp;

**Proposition**: $T(a_1v_1 + \cdots + a_n v_n) = a_1T(v_1) + \cdots + a_n T(v_n)$

*Proof*: Follows from linearly properties of linear transformations

- **Note**: If $x = \{v_1, \ldots, v_n\}$ is a basis for $V$ and if $w_1, \ldots, w_n$ are arbitrary vectors in $W$, then there is a unique linear transformation $T: V \rightarrow W$ such that
$$T(v_1) = w_1, \ldots, T(v_n) = w_n$$

&nbsp;

**Lemma**: $\Img(T)$ is a subspace of $W$

*Proof*: We show the necessary conditions for a subspace

- $+: w_1, w_2 \in \Img(T) \implies \exists v_1, v_2 \in V$ such that $T(v_1) = w_1$ and $T(v_2) = w_2$

    Then $w_1 + w_2 = T(v_1) + T(v_2) = T(\underbrace{v_1 + v_2}_{\in V}) \in \Img(T)$

- $\times: w \in \Img(T) \implies \exists v \in V$ such that $T(v) = w$

    Then for $c \in K$, we have $cw = c(Tv) = T(\underbrace{cv}_{\in V}) \in \Img(T)$

&nbsp;

**Definition - Pull Back**: Suppose $Y = \{w_1, \ldots, w_m\} \subseteq \Img(T)$. Then a **pull-back** is any set $\{v_1, \ldots, v_m\} \subseteq V$ such that
$$T(v_1) = w_1, \ldots, T(v_m) = w_m$$

&nbsp;

**Lemma**: If $\{w_1, \ldots, w_m\}$ is linearly independent in $\Img(T)$ (or in $W$), then any pull back $\{v_1, \ldots, v_m\} \subseteq V$ is linearly independent in $V$

*Proof*: Let $a_1v_1 + \cdots + a_m v_m = O_V$

Thus $T(a_1, v_1 + \cdots + a_m v_m = O_V) = a_1 w_1 + \cdots + a_m w_m = O_W$

Since $\{w_1, \ldots, w_m\}$ is linearly independent, we have $a_1 = \cdots = a_m = 0$ as desired

&nbsp;

**Pull Back Property**: Suppose $\{w_1, \ldots, w_m\}$ is a basis for $\Img(T)$, and let $\{v_1, \ldots, v_m\} \subseteq V$ be any pull back. Furthermore, let $S = \Span(\{v_1, \ldots, v_m\}) \subseteq V$ be a subspace. Then $\{v_1, \ldots, v_m\}$ is a basis for $S$

*Proof*: By the previous lemma, $\{v_1, \ldots, v_m\}$ is linearly independent

Furthermore, $\{v_1, \ldots, v_m\}$ spans $S$ by definition

&nbsp;

**Corollary**: If $T: V \rightarrow W$ is any linearly transformation and if $\dim(V) = n$, then $\dim(\Img(T)) \leq n$

*Proof*: BWOC, suppose $\dim(\Img(T)) > n$, thus we can create a set of $n+1$ linearly independent elements in $\Img(T)$.

By the Pull Back Property, this pulls back to $n+1$ linearly independent elements in $V$. Contradiction since $n + 1 > n = \dim(V)$

&nbsp;

**Note**: $T: V \rightarrow W$ where $T(v) = \{O_W\}$ is a linearly transformation with $\dim(\Img(T)) = 0$, regardless of the value of $\dim(V)$

## Kernel

**Definition - Kernel**: For $T: V \rightarrow W$, the **kernel** $\Ker(T) = \{v \in V \mid T(v) = O_W\}$

&nbsp;

**Proposition**: $\Ker(T)$ is a subspace of $V$

*Proof*: Clearly $O_V \in \Ker(T)$

- $+:$ For $v_1, v_2 \in \Ker(T)$, we see that $T(v_1 + v_2) = T(v_1) + T(v_2) = O_W + O_W = O_W$. Thus $v_1 + v_2 \in \Ker(T)$
- $\times:$ For $c \in K$ and $v \in \Ker(T)$, we see that $T(cv) = cT(v) = O_W$. Thus $cv \in \Ker(V)$

&nbsp;

**Proposition**: Let $T: V \rightarrow W$ be any linear transformation. For any basis $B = \{w_1, \ldots, w_m\} \subseteq \Img(T)$ and for any pullback $\{v_1, \ldots, v_m\} \subseteq V$, we have
$$V = \Ker(T) \oplus S \quad \quad S = \Span(\{v_1, \ldots, v_m\})$$

*Proof*: We need to show $V = \Ker(T) + S$ and $\Ker(T) \cap S = \{O_V\}$

- Take arbitrary $v \in V \implies T(v) \in \Img(T) = a_1 w_1 + \cdots + a_m w_m$

    Let $s = a_1 v_1 + \cdots a_m v_m \in S$.

    Then $T(s) = T(v) \implies T(v-s) = T(v) - T(s) = O_W \implies v -s \in \Ker(T)$

    Let $u = v - s \in \Ker(T)$

    Thus clearly $v = u + s$ for $u \in \Ker(T)$ and $s \in S$

- Clearly $O_V \in \Ker(T) \cap S$ since both are subspaces of $V$

    Take any arbitrary $v \in \Ker(T) \cap S$

    $v \in S \implies v= b_1 v_1 + \cdots b_m v_m \implies T(v) = b_1 w_1 + \cdots b_m w_m$

    Since $v \in \Ker(T)$, we have that $T(v) = O_W \implies b_1 = \cdots = b_m = 0$ since $\{w_1, \ldots, w_m\}$ is linearly independent

    Thus we have $v = 0v_1 + \cdots + 0 v_m = O_V \implies \Ker(T) \cap S = \{O_V\}$

Thus we have shown the necessary properties for $V = \Ker(T) \oplus S$

&nbsp;

**Theorem**: $\dim(V) = \dim(\Ker(T)) + \dim(\Img(T))$

*Proof*: Choose a basis $B = \{w_1, \ldots, w_m\}$ for $\Img(T)$ and a pullback $\{v_1, \ldots, v_m\}$

Let $S = \Span(\{v_1, \ldots, v_m\})$

Since $V = \Ker(T) \oplus S$, we have $\dim(\Ker(T)) + \dim(S) = \dim(\Ker(T)) + \dim(\Img(T)) = \dim(V)$

&nbsp;

### Consequences of Kernel

**Corollary 1**: For linear $T: R^3 \rightarrow R^4$, $T$ is NOT onto

*Proof*: $\dim(\Img(T)) \leq \dim(R^3) = 3 < 4 \implies \Img(T) \neq R^4 \implies T$ is NOT onto

&nbsp;

**Corollary 2**: For linear $T: R^4 \rightarrow R^3$, $T$ is NOT 1-1

*Proof*: $\dim(\Ker(T)) + \underbrace{\dim(\Img(T))}_{\leq 3} = \dim(R^4) = 4 \implies \dim(\Ker(T)) \geq 1$

Thus $\Ker(T)$ has something non-zero mapped to $O_W \implies T$ is NOT 1-1

&nbsp;

**Definition - Isomorphism**: $T: V \rightarrow W$ such that $T$ is linear transformation and a bijection

&nbsp;

**Corollary 3**: $\dim(V) = \dim(W)$ and $T: V \rightarrow W$ is a linear transformation and 1-1 $\implies T$ is an isomorphism (i.e. $T$ is onto)

*Proof*: $\dim(\Ker(T)) + \dim(\Img(T)) = \dim(V)$

But we know that $\dim(\Ker(T)) = 0 \implies \dim(\Img(T)) = \dim(V) = \dim(W)$

Furthermore $\Img(T)$ is a subspace of $W$ and $\dim(\Img(T)) = \dim(W) \implies T$ is onto

&nbsp;

**Corollary 4**: $\dim(V) = \dim(W)$ and $T: V \rightarrow W$ is a linear transformation and onto $\implies T$ is an isomorphism (i.e. $T$ is 1-1)

*Proof*: $\dim(\Ker(T)) + \dim(\Img(T)) = \dim(V)$

But we know that $\dim(\Img(T)) = \dim(V) \implies \dim(\Ker(T)) = 0$

## Compositions and Inverse Linear Mappings

Consider Vector Spaces $U, V, W$ and linear transformations $T: U \rightarrow V$ and $S: V \rightarrow W$

**Proposition**: $S \circ T: V \rightarrow W$ is a linear transformation

*Proof*:

- $+:$ For $u_1, u_2 \in U$ we have that
\begin{align*}
S \circ T(u_1 + u_2) &= S(T(u_1 + u_2)) \\
&= S(T(u_1) + T(u_2)) \\
&= S(T(u_1)) + S(T(u_2)) \\
&= S \circ T(u_1) + S \circ T(u_2)
\end{align*}

- $\times:$ For $u \in U$ and $c \in K$
\begin{align*}
S \circ T(cu) &= S(T(cu)) \\
&= S(cT(u)) \\
&= cS(T(u)) \\
&= c S \circ T(u)
\end{align*}

Thus $S \circ T: V \rightarrow W$ is a linear transformation

&nbsp;

**Definition - Inverse Mapping**: $T^{-1}: W \rightarrow V$ where $T^{-1}(w) =$ the unique $v \in V$ such that $T(v) = w$

&nbsp;

**Proposition**: $T^{-1}: W \rightarrow V$ is a linear transformation (and thus an isomorphism)

*Proof*:

- $+:$ Take $w_1, w_2 \in W$ such that $T(v_1) = w_1$ and $T(v_2) = w_2$ for $v_1, v_2 \in V$. Then we see that
$$T(v_1 + v_2) = T(v_1) + T(v_2) = w_1 + w_2$$
However, by definition of inverse mapping, $v_1 + v_2$ is the unique element such that $T(v_1 + v_2) = w_1 + w_2$

&nbsp; &nbsp; &nbsp; &nbsp; Thus by definition of $T^{-1}$, we have that $T^{-1}(w_1 + w_2) = v_1 + v_2 = T^{-1}(w_1) + T^{-1}(w_2)$

- $\times:$ Similar

# Linear Maps and Matrices

**Definition - $\mathbf{L_A}$**: For a $m \times n$ matrix $A$, $L_A$ determines a linear transformation from $R^n \rightarrow R^m$

&nbsp;

**Example**: Consider $L_A: R^3 \rightarrow R^2$ where $A = \displaystyle \begin{bmatrix} 2 & 3 & 1 \\ 0 & 4 & 2\end{bmatrix}$

Then we see that $A \begin{bmatrix} x \\ y \\ z\end{bmatrix} = \begin{bmatrix} 2x + 3y + z \\ 4y + 2z\end{bmatrix}$

It can be clearly shown that $L_A$ is a linear transformation (follows from logic of dot products)

## Bases, Matrices, and Linear Maps

For a given transformation $T: V \rightarrow W$, the matrix of $T$ with respect to the standard basis is given by
$$A = (T(E_1), \ldots, T(E_n))$$

&nbsp;

**Example**: $T: R^2 \rightarrow R^3 \quad \quad T(x, y) = (5x + y, x - y, x)$

$T(E_1) = (5, 1, 1) \quad \quad T(E_2) = (1, -1, 0)$

Thus we see that $A = \begin{bmatrix} 5 & 1 \\ 1 & -1 \\ 1 & 0\end{bmatrix}$

- $T(^t(3, 2)) = \begin{bmatrix} 5 & 1 \\ 1 & -1 \\ 1 & 0\end{bmatrix} \begin{bmatrix} 3 \\ 2\end{bmatrix} = ^t(17, 1, 3)$

&nbsp;

**Example**: $T: R^2 \rightarrow R^2$ where we stretch the $x$-coordinate by $2$

$T(^t(1, 0)) = ^t(2, 0) \quad \quad T(^t(0, 1)) = ^t(0, 1)$

Thus we see that $A = \begin{bmatrix} 2 & 0 \\ 0 & 1\end{bmatrix}$

&nbsp;

**Example**:  $S \circ T: R^2 \rightarrow R^2$ where we first stretch by $x$ by $3$ then stretch $y$ by $3$

$T(^t(1, 0)) = ^t(2, 0) \quad \quad T(^t(0, 1)) = ^t(0, 3)$

Thus we see that $A = \begin{bmatrix} 2 & 0 \\ 0 & 3\end{bmatrix}$

- **Note**: we see that applying functions just corresponds to matrix multiplication $\begin{bmatrix} 1 & 0 \\ 0 & 3\end{bmatrix} \begin{bmatrix} 2 & 0 \\ 0 & 1\end{bmatrix} = \begin{bmatrix} 2 & 0 \\ 0 & 3\end{bmatrix}$

&nbsp;

**Example**: Fix $\theta \in R$, then rotate by $\theta$

$R_{\theta} (^t(1, 0)) = ^t(\cos(\theta), \sin(\theta)) \quad \quad R_{\theta} (^t(0, 1)) = ^t(- \sin(\theta), \cos(\theta))$

Thus $A = \begin{bmatrix} \cos(\theta) & -\sin(\theta) \\ \sin(\theta) & \cos(\theta)\end{bmatrix}$

Thus given any $^t(x, y) \in R^2$, we see that $T_\theta(^t(x, y)) = \begin{bmatrix} x\cos(\theta) - y \sin(\theta) \\ x\sin(\theta) + y \cos(\theta)\end{bmatrix}$

&nbsp;

**Example**: Stretch $x$ by $2$, rotate by $\pi / 4$, and stretch $y$ by $3$

$A = \begin{bmatrix} 1 & 0 \\ 0 & 3\end{bmatrix} \begin{bmatrix} \sqrt{2} / 2 & - \sqrt{2} / 2 \\ \sqrt{2} / 2 & \sqrt{2} / 2\end{bmatrix} \begin{bmatrix} 2 & 0 \\ 0 & 1\end{bmatrix}$

&nbsp;

**Note**: Given $T: K^n \rightarrow K^m$, the matrix $A$ for $T$ depends on our choosing of bases for $K^n$ and $K^m$

&nbsp;

**Example**: $T: R^2 \rightarrow R^3 \quad\quad T(x, y) = (5x + y, x- y, x)$

Let $B = \{\underbrace{(1, 4)}_{v_1}, \underbrace{(3, 0)}_{v_2}\}$ be a basis for $R^2$ and $B' = \{\underbrace{(3, 0, 0)}_{w_1}, \underbrace{(0, 5, 0)}_{w_2}, \underbrace{(0, 0, 1)}_{w_3}\}$ be a basis for $R^3$

We can define a matrix of $T$ with respect to $B$ and $B'$
$$M_{B'}^B(T) = (\underbrace{T(v_1) \quad \quad T(v_2)}_{\text{in terms of } w_1, w_2, w_3})$$

$T(v_1) = T(1, 4) = (9, -3, 1) = 3w_1 - \frac{3}{5}w_2 + w_3$

$T(v_2) = T(1, 4) = (15, 3, 3) = 5w_1 + \frac{3}{5}w_2 + 3w_3$

Thus we see that $M_{B'}^B(T) = \begin{bmatrix} 3 & 5\\ -3/5 & 3/5 \\ 1 & 3\end{bmatrix}$

**Upshot**: Any vector, written in $B$ coordinates, when multiplied by this matrix, yields an answer in $B'$ coordinates. Thus for $v = a v_1 + b v_2$, we have
$$T(v) = (3a + 5b) w_1 + (-3/5 a + 3/5 b) w_2 + (a + 3b) w_3$$

- As a sanity check, for $v = (5,8) \in R^2$
  - Normal Transformation: $T(v) = (33, -3, 5)$
  - Linear Map: writing $v$ in terms of $v_1, v_2$, we get $(5,8) = a(1, 4) + b(3, 0) \implies (5, 8) = 2(1, 4) + 2 (3, 0)$

    Thus we have
    $$M^B_{B'}(T) \begin{bmatrix} a \\ b \end{bmatrix} = \begin{bmatrix} 3 & 5 \\ -3/5 & 3/5 \\ 1 & 3\end{bmatrix} \begin{bmatrix} 2 \\ 1\end{bmatrix} = \begin{bmatrix} 11 \\ -3/5 \\ 5\end{bmatrix} \implies 11(3, 0, 0) - 3/5(0, 5, 0) + 5(0, 0, 1) = (33, -3, 5)$$

&nbsp;

**Example**: Consider $P_n = \{a_0 + a_1 x + \cdots + a_n x^n \mid a_i \in R\}$

It's easily verifiable that $P_n$ is a subspace of $\mathcal{F}(R)$. Furthermore, the basis for $P_n$ is $\{1, x, \ldots, x^n\} \implies \dim(P_n) = n + 1$

Let $D: P_2 \rightarrow P_2$ be the derivative
$$D(a_0 + a_1 x + a_2 x^2 = a_1 + 2a_2 x)$$
Easily verifiable that $D$ is a linear transformation. Consider what is the matrix of $D$ with respect to $B = \{1, x, x^2\}$?
$$A = \begin{bmatrix} D(1) & D(x) & D(x^2)\end{bmatrix} = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \\ 0 & 0 & 0\end{bmatrix}$$
Thus we see that for $p(x) = 5 + 3x + 4x^2$,
$$D(p(x)) = 3 + 8x = 5(0, 0, 0) + 3(0, 1, 0) + 4(0, 2, 0)$

&nbsp;

**Upshot**: For a linear transformation $T: V \rightarrow W$, with $\dim(V) = n$ and $\dim(W) = m$, if $B = \{v_1, \ldots, v_n\}$ and $B' = \{w_1, \ldots, w_m\}$ are bases for $V, W$, then
$$M_{B'}^B(T) = \begin{bmatrix} T(v_1) & T(v_2) & \cdots & T(V_n)\end{bmatrix}$$
is a $m \times n$ matrix with column vectors containing coefficients of $T(v_1)$ WRT $B'$

Furthermore, for any $v \in V, v = x_1 v_1 + \cdots + x_n v_n$, we have
$$M_{B'}^B(T) \begin{bmatrix} x_1 \\ \cdots \\ x_n \end{bmatrix} = \begin{bmatrix} y_1 \\ \cdots \\ y_m\end{bmatrix}$$
Thus $T(v) = y_1 w_1 + \cdots + y_m w_m$ (**Note** coordinate is WRT to $B'$)

&nbsp;

**Definition - Change of Basis**: Let $B = \{v_1, \ldots, v_n\}$ and $B' = \{w_1, \ldots, w_n\}$ be basis for the same vector space $V$, and let $T:V \rightarrow V$ be the identity mapping. Then
$$M_{B'}^B(\id) = \underbrace{\begin{bmatrix} \id(v_1) & \id(v_2) & \cdots & \id(v_n)\end{bmatrix}}_{\text{WRT } B'}$$
is the **Change of Basis** matrix for $V$

&nbsp;

**Example**: Let $V = P_1 = \{a_0 + a_1 x \mid a_i \in R\}$ and let $B = \{1, x\}$ and $B' = \{3 + x, 5 + 2x\}$, which are both bases for $V$

$1 = a(3 + x) + b(5 + 2x) \implies a = 2, b = -1 \implies 1 = 2(3 + x) - (5 + 2x)$

$x = c(3 + x) + d(5 + 2x) \implies c = -5, d = 3 \implies x = -5(3 + x) + 3(5 + 2x)$

$M_{B'}^B(\id) = \underbrace{\begin{bmatrix} 2 & -5 \\ -1 & 3\end{bmatrix}}_{\text{WRT } B'}$

Furthermore, consider

$M_{B}^{B'}(\id) = \underbrace{\begin{bmatrix} \id(w_1) & \id(w_2)\end{bmatrix}}_{\text{WRT } B} = \begin{bmatrix} 3 & 5 \\ 1 & 2\end{bmatrix}$

Finally, we see that $M_{B}^{B'}(M_{B'}^B(\id)) = \id$

Thus the inverse of $M_{B'}^B$ is $M_B^{B'}$

# Scalar Products and Orthogonality

## Scalar Prodcuts

**Definition - Scalar Product:**: For a Vector Space $V$, we define $<,>: V \times V \rightarrow K$

- **Example**: Think of dot products in $R^n \times R^n \rightarrow R$

&nbsp;

**Properties of Scalar Products**

1. $<v, w> = <w, v>$
2. $<v, w_1 + w_2> = <v, w_1> + <v, w_2>$
3. $<v, cw> = c<v, w> \quad \quad <cv, w> = c<v, w>$

&nbsp;

**Consequences of Properties**

- $\forall v_1, v_2, w \in V, <v_1 + v_2, w> = <v_1, w> + <v_2, w>$

    *Proof*: Follows from applying properties $1$ and $2$

- $\forall v \in V, <v, O_v> = 0 = <O_v, v>$

  *Proof*: For any $w \in V$, we have $<v, O_V> = <v, 0w> = 0<v, w>$

&nbsp;

**Definition - Non-Degenerate**: Scalar product that satisfies $\forall v \neq 0, \exists w \in V$ such that $<v, w> \neq 0$

&nbsp;

**Example**: $\mathcal{F}([0, 1])$, all functions $f:[0,1] \rightarrow R$

Let $C([0,1])$ be the set of all continuous functions $f:[0, 1] \rightarrow R$, which is clearly an $R$ subspace

Now define $<f, g> = \int_0^1 f(x) g(x) \, dx$. We claim that this is a scalar product

*Proof*:

- $\int_0^1 f(x) g(x) \, dx = \int_0^1 g(x) f(x) \, dx$ so property $1$ holds

- $\int_0^1 f(x) (g_1(x) + g_2(x)) \, dx = \int_0^1 f(x) g_1(x) \, dx + \int_0^1 f(x) g_2(x) \, dx$ so property $2$ holds

- $\int_0^1 f(x) cg(x) \, dx = c\int_0^1 f(x) g(x)$ so property $3$ holds

We also claim that $<f, g>$ is non-degenerate since for $f \neq 0$, we have $<f, f> = \int_0^1 f(x)^2$, which is always $\geq 0$ and is continuous

&nbsp;

**Example**: $f(x) = 2x + 3 \quad \quad g(x) = x^2$

$<2x + 3, x^2> = \int_0^1 (2x + 3) x^2 \, dx = 3/2$

&nbsp;

**Defintion - Orthogonal**: Elements $v, w \in V$ are **orthogonal**, denote $v \perp w$, if $<v, w> = 0$

&nbsp;

**Definition - Orthogonal Complement**: Suppose $W \subseteq V$ is a subspace, then the **orthogonal complement** of $W$ is
$$W^{\perp} = \{v \in V \mid v \perp w\} \quad \quad \text{for } w \in W$$

- **Note**: $W^{\perp} \subseteq V$ is a subspace

&nbsp;

**Definition - Positive Definite**: Scalar product that satisfies $\forall v \neq O, <v, v> \geq 0$. Otherwise $<v, v> = 0 \implies v = O$

&nbsp;

**Definition - Length**: $\| v \| = \sqrt{<v, v>}$

- Length between $v$ and $w$: $\|v - w\|$
- $\|c\| = |c| \|v\|$
- $\|v + w\|^2 = <v + w, v + w> = <v, v> + <v, w> + <w, v> + <w, w> = \|v\|^2 - 2<v, w> + \|w\|^2$
- $v \perp w\implies <v, w> = 0 \implies \|v + w\|^2 = \|v - w\|^2 = \|v \|^2 + \|w \|^2$

&nbsp;

**Parallelogram Law**: For any $v, w \in V$, we have
$$\|v + w\|^2 + \|v - w\|^2 = 2\|v\|^2 + 2 \|w \|^2$$

*Proof*: Follows from the definition/properties of length

&nbsp;

**Definition - Unit Vector**: $v \in V$ such that $\|v \| = 1$

- If $v \neq O$, then $(\frac{1}{\|v\|}) v$ is a unit vector

&nbsp;

**Definition - Projection**: $\proj_w v$ represents $v$ as a scalar multiple of $w$ where $\proj_w v = (\frac{<v, w>}{<w, w>}) w$

- Definition comes from creating a right triangle where $v - cw \perp cw \implies <v - cw, cw> = 0$

    Thus we have $<v, cw> - <cw, cw> = c<v, w> - c^2<w, w> \implies c = \frac{<v, w>}{<w, w>}$

- Special case where $<w, w> = 1 \implies \proj_w v = <v, w> w$

&nbsp;

**Schwartz Inequality**: For any $v, w \in V$ we have
$$|<v, w>| \leq \|v\| \|w\|$$

*Proof*: If $w = O$, then $|<v, w>| \leq 0$

Otherwise, using the definition of projection, we have $cw \perp v - cw$. Thus we see
\begin{align*}
\|v\|^2 &= \|v - cw\|^2 + \|cw\|^2 \\
\implies \|cw^2\| &\leq \|v^2\| \\
c^2 \|w\|^2 &\leq \|v\|^2 \\
\frac{<v, w>^2}{<w,w>^2}\|w\|^2 &\leq \|v\|^2 \\
\implies <v, w>^2 &\leq \|v\|^2 \|w\|^2
\end{align*}

&nbsp;

**Triangle Inequality**: For $v, w \in V$, we have
$$\|v + w\| \leq \|v\| + \|w \|$$

*Proof*:
\begin{align*}
\|v + w\|^2 &= <v + w, v + w> \\
&= \|v\|^2 + 2<v, w> + \|w\|^2 \\
&\leq \|v\|^2 + 2\|v\|\|w\| + \|w\|^2 \\
&\leq (\|v\| + \|w\|)^2 \\
\implies \|v +  w \| &\leq \|v\| + \|w\|
\end{align*}



