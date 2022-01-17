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
output: pdf_document
---

# Vector Spaces

## $R^n$ and $C^n$

**Definition - Complex Numbers**: ordered pairs $(a, b)$ where $a, b \in R$, denoted $a + bi$ where $i = \sqrt{-1}$

The set of all complex numbers is denoted $C = \{a + bi \mid a,b \in R\}$
- Addition is defined as $(a + bi) + (c + di) = (a + c) + (b + d)i$
- Multiplication is defined as $(a + bi)(c + di) = (ac - bd) + (ad + bc)i$

&nbsp;

**1.3 - Properties of Complex Arithmetic** (for $\alpha, \beta, \lambda \in C$):

- **Commutativity**: $\alpha + \beta = \beta + \alpha$ and $\alpha \beta = \beta \alpha$
- **Associativity**: $(\alpha + \beta) + \lambda = \alpha + (\beta + \lambda)$ and $(\alpha \beta) \lambda = \alpha (\beta \lambda)$
- **Identities**: $\lambda + 0 = \lambda$ and $\lambda 1 = \lambda$
- **Additive Inverse**: $\forall \alpha \in C$, there eixsts a unique $\beta \in C$ such that $\alpha + \beta = 0$
- **Multiplicative Inverse**: $\forall \alpha \in C$, with $\alpha \neq 0$, there exists a unique $\beta \in C$ such that $\alpha \beta = 1$
- **Distributive Property**: $\lambda(\alpha + \beta) = \lambda \alpha + \lambda \beta$

&nbsp;

**1.5 - Additive Inverse, Subtraction, Multiplicative Inverse, Division** (for $\alpha, \beta \in C$)

- **Additive Inverse** of $\alpha$ is denoted $- \alpha$, where $\alpha + (- \alpha) = 0$
- **Subtraction** on $C$ is defined by $\beta - \alpha = \beta + (-\alpha)$
- **Multiplicative Inverse** of $\alpha \neq 0$ is denoted $1/ \alpha$, where $\alpha (1/\alpha) = 1$
- **Division** on $C$ is defined by $\beta / \alpha = \beta (1/\alpha)$

&nbsp;

**ASIDE on Fields**: both $R$ and $C$ are known as **fields**. Elements of $F$ are called **scalars** and all of the work in linear algebra can be abstracted into dealing with fields

- For $\alpha \in F$ and $m \in Z^{+}$, $\alpha^m  = \underbrace{\alpha \cdots \alpha}_{\text{m times}}$
- $(\alpha^m)n = \alpha^{mn}$
- $(\alpha \beta)^m = \alpha^m \beta^m$

&nbsp;

**Definition - Lists**: A **list** of length $n$ is an ordered collection of $n$ elements that looks like $(x_1, \ldots, x_n)$

- 2 lists are equal if and only if they have the same length and the same elements in the same order

&nbsp;

**Definition - $\mathbf{F^n}$**: The set of all lists of length $n$ of elements of $F$, denoted $F^n = \{(x_1, \ldots, x_n) \mid x_i \in F\}$

- Here $x_i$ is known as the **ith coordinate** of the list
- Addition is defined by adding corresponding coordinates: $(x_1, \ldots, x_n) + (y_1, \ldots, y_n) = (x_1 + y_1, \ldots, x_n + y_n)$ and short handed as $x + y$

&nbsp;

Properties for $F^n$ similar to that of $C$ can be seen:

- Clearly addition in $F^n$ is commutative: $x + y = y + x$
- There is a $0$ element whose coordinates are all $0$ such that $x + 0 = x$ for all $x \in F^n$
- $\forall x \in F^n$, there exists a unique $-x$ such that $x + (-x) = 0$ known as the **additive inverse**
- **NOTE**: multiplication in $F^n$ between $2$ lists is not particular useful. Instead we look at **scalar multiplication**. Take $\lambda \in F$ and vector $x \in F^n$ then
$$\lambda(x_1, \ldots, x_n) = (\lambda x_1, \ldots, \lambda x_n)$$

## Definition of Vector Space

**Definition - Vector Space**: A set $V$ with addition and scalar multiplication on $V$ over $F$, for $u, v, w \in V$ and $a, b \in F$, satisfying

- **Commutativity**: $u + v = v + u$
- **Associativity**: $(u + v) + w = u + (v + w)$ and $(ab)v = a(bv)$
- **Additive Identity**: $\exists 0 \in V$ such that $v + 0 = v$ for all $v \in V$
- **Additive Inverse**: $\forall v \in V, \exists w \in V$ such that $v + w = 0$
- **Multiplicative Identity**: $1v = v$ for all $v \in V$
- **Distributive Properties**: $a(u + v) = au + av$ and $(a + b)v = av + bv$

**Definition - Vectors**: Elements of a vector space

&nbsp;

An interesting vector space to consider is $\mathbf{F^S}$: the set of functions from $S$ to $F$

- For $f, g \in F^S$, $f + g \in F^S$ is defined by $(f + g)(x) = f(x) + g(x)$ for all $x \in S$
- For $f \in F^S$ and $\lambda \in F$, the product $\lambda f \in F^S$ is defined by $(\lambda f)(x) = \lambda f(x)$ for all $x \in S$
- **Example**: If $S = [0,1]$ and $F = R$, then $R^{[0, 1]}$ is the set of real-valued functions on the interval $[0, 1]$

  - Clearly addition and scalar multiplication is well defined for $F^S$
  - Additive identity of $F^S$ is $0(x) = 0$ for all $x \in S$
  - Additive inverse of $f \in F^S$ is $(-f)(x) = -f(x)$ for all $x \in S$
- **NOTE**: we can treat $F^n$ as $F^{\{1, 2, \ldots, n\}}$

### Properties of Vector Spaces

**1.25 - Unique Additive Identity**: Vector spaces have a unique additive identity

*Proof*: Suppose $0$ and $0'$ are both additive identities for a vector space $V$. Then
$$0' = 0' + 0 = 0 + 0' = 0$$

&nbsp;

**1.26 - Unique Additive Inverses**: Each element in $V$ has a unique additive inverse

*Proof*: Suppose $w$ and $w'$ are both additive inverses of $v$. Then
$$w = w + 0 = w + (w' + v) = (w + v) + w' = 0 + w' = w'$$

&nbsp;

**1.29 - $\mathbf{0}$ Times a Vector**: For every $v \in V$, $0v = 0$ (**note** $0$ here is a scalar)

*Proof*: $0v = (0 + 0)v = 0v + 0v$. Then adding the inverse of $0v$ to both sides, we get $0 = 0v$

&nbsp;

**1.30 - A Number Times the $\mathbf{0}$ Vector**: For every $a \in F, a0 = 0$ (**note** $0$ here is a vector)

*Proof*: $a0 = a(0 + 0) = a0 + a0$. Then adding the inverse of $a0$ to both sides, we get $0 = a0$

&nbsp;

**1.31 - $\mathbf{-1}$ Times a Vector**: For every $v \in V$, $(-1)v = -v$

*Proof*: $v + (-1)v = (1 + (-1)) v = 0v = 0$. Thus $(-1)v$ is the additive inverse of $v$

## Subspaces

**Definition - Subspace**: A subset $U$ of $V$ is also a vector space under the same addition and scalar multiplication of $V$

- **Example**: $\{(x_1, x_2, 0 \mid x_1, x_2 \in F\}$ is a subspace of $F^3$

&nbsp;

**1.34 - Conditions for a Subspace**: $U \subseteq V$ is a subspace of $V$ if and only if $U$ satisfies the following conditions

1. **Additive Identity**: $0 \in U$
2. **Closed under Addition**: $u, w \in U \implies u + w \in U$
3. **Closed under Scalar Multiplication**: $a \in F$ and $U \in U \implies au \in U$

*Proof*: $\implies$ if $U$ is a subspace of $V$ then $U$ satisfies the 3 conditions above by the definition of vector space

$\impliedby$ suppose $U$ satisfies the 3 conditions above

- Associativity and commutativity are automatically satisfied since $U \subseteq V$
- The first condition ensures that the additive identity of $V$ is in $U$
- The second condition ensures that addition on $U$ makes sense
- The third condition ensures that scalar multiplication makes since on $U$, helping show that the additive inverse $(-1)u$ and that the distributive properties hold

&nbsp;

**Definition - Sum of Subsets**: Suppose $U_1, \ldots, U_m$ are subsets of $V$. The **sum** of $U_1, \ldots, U_m$, denoted $U_1 + \cdots + U_m$, is the set of all possible sums of elements of $U_1, \ldots, U_m$
$$U_1 + \cdots + U_m = \{u_1 + \cdots + u_m \mid u_i \in U_i\}$$

- **Example**: Let $U$ be the set of elements of $F^3$ whose second and third coordinates are $0$, and $W$ be the set of elements of $F^3$ whose first and third coordinates are $0$. Then
$$U = \{(x, 0, 0) \in F^3 \mid x \in F\} \quad \quad W = \{(0, y, 0) \in F^3 \mid y \in F\} \quad \quad U + W = \{(x, y, 0) \mid x, y \in F\}$$

&nbsp;

**1.39 - Sum of Subspaces is the Smallest Containing Subspace**: Suppose $U_1, \ldots, U_m$ are subspaces of $V$. Then $U_1 + \cdots + U_m$ is the smallest subspace of $V$ containing $U_1, \ldots, U_m$

*Proof*: Clearly $0 \in U_1 + \cdots + U_m$ and addition is and scalar multiplication is closed. Thus $U_1 + \cdots + U_m$ is a subspace of $V$

Furthermore, clearly $U_1, \cdots, U_m$ are contained in $U_1 + \cdots + U_m$.

Conversely, all subspaces containing $U_1, \ldots, U_m$ contain $U_1 + \cdots + U_m$ (subspaces contain all finite sums of their elements)

Thus $U_1 + \cdots + U_m$ is the smallest subspace of $V$ containing $U_1, \ldots, U_m$

&nbsp;

Suppose $U_1, \ldots, U_m$ are subspaces of $V$. Then every element of $U_1 + \cdots + U_m$ can be written in the form
$$u_1 + \cdots + u_m \quad \quad u_j \in U_j$$

**Definition - Direct Sum**: If each element of $U_1 + \cdots + U_m$ can be written in only one way as a sum of $u_1 + \cdots u_m$ then the sum $U_1 + \cdots + U_m$ is called a **direct sum**. Denoted
$$U_1 \oplus \cdots \oplus U_m$$

- **Example**: Let $U$ be the subspace of $F^3$ of vectors whose last coordinate is $0$ and $W$ be the subspace of $F^3$ of vectors whose first 2 coordinates are $0$
$$U = \{(x, y, 0)\} \quad \quad W = \{(0, 0, z)\} \quad \quad F^3 = U \oplus W$$
- **Non-Example**: Let
$$U_1 = \{(x, y, 0)\} \quad \quad U_2 = \{(0, 0, z)\} \quad \quad \{(0, y, y)\}$$
&nbsp; &nbsp; &nbsp; &nbsp; Then $U_1 + U_2 +U_3$ is NOT a direct sum since we have
$$(0, 0, 0) = (0, 1, 0)+(0, 0, 1) + (0, -1, -1) = (0, 0, 0) + (0, 0, 0) + (0, 0, 0)$$

&nbsp;

**1.44 - Condition for a Direct Sum**: Suppose $U_1, \ldots, U_m$ are subspaces of $V$. Then $U_1 + \cdots + U_m$ is a direct sum if and only if the only way to write $0$ as a sum is by taking each $u_j = 0$

*Proof*: $\implies$ Suppose $U_1 + \cdots + U_m$ is a direct sum. Then clearly there is a unique way writing $0$ as the sum of $u_1 + \cdots + u_m$

$\impliedby$ Suppose that the only way to write $0$ as the sum of $u_1 + \cdots + u_m$ is by taking each $u_j = 0$.

By contradiction, to show that $U_1 + \cdots + U_m$ is a direct sum, let $v \in U_1 + \cdots + U_m$ where
$$v = v_1 + \cdots + v_m = w_1 + \cdots + w_m$$
Then we have
$$0 = (v_1 - w_1) + \cdots + (v_m - w_m)$$
Thus $v_j = w_j$ and each vector in $U_1 + \cdots + U_m$ has a unique representation

&nbsp;

**1.45 - Direct Sum of 2 Subspaces**: Suppose $U$ and $W$ are subspaces of $V$. Then $U + W$ is a direct sum if and only if $U \cap W = \{0\}$

*Proof*: $\implies$ Suppose $U + V$ is a direct sum. If $v \in U \cap W$, then $0 = v + (-v)$.

By the unique representation of $0$ as the sum of vectors in $U$ and $W$, we must have $v = 0$. Thus $U \cap W = \{0\}$

$\impliedby$ Suppose $U \cap W = \{0\}$ and suppose $0 = u + w$. We show that $u = w = 0$

$0 = u + w \implies u = -w \implies u \in W \implies u \in U \cap W$. Thus $u = 0 = w$

# Finite-Dimensional Vector Spaces

## Span and Linear Independence

**Definition - Linear Combination**: Let $v_1, \ldots, v_m$ be a list of vectors in $V$. Then vectors of the form
$$v = a_1v_1 + \cdots + a_m v_m \quad \quad a_i \in F$$
are said to be a **linear combination** of the vectors $v_1, \ldots, v_m$

&nbsp;

**Definition - Span**: set of all linear combinations of vectors $v_1, \ldots, v_m$ in $V$. Denoted
$$\Span(v_1, \ldots, v_m) = \{a_1v_1 + \cdots + a_m v_m \mid a_i \in F$$

- If $\Span(v_1, \ldots, v_m) = V$ then $v_1, \ldots, v_m$ **spans** $V$

&nbsp;

**2.7 - Span is the Smallest Containing Subspace**: the span of a list of vectors is the smallest subspace of $V$ containing all vectors in the list

*Proof*: Clearly $\Span(v_1, \ldots, v_m)$ is a subspace of $V$

- $0 = 0v_1 + \cdots + 0v_m \in \Span(v_1, \ldots, v_m)$
- $(a_1v_1 + \cdots + a_m v_m) + (b_1 v_1 \cdots + b_m v_m) = (a_1 + b_1)v_1 + \cdots + (a_m + b_m)v_m$ so closed under addition
- $\lambda(a_1v_1 + \cdots + a_mv_m) = \lambda a_1 v_1 + \cdots + \lambda a_m v_m$ so closed under scalar multiplication

Clearly each $v_j$ can be written as a linear combination of $v_1, \ldots, v_m$. Thus each $v_j \in \Span(v_1, \ldots, v_m)$

Conversely, every subspace containing $v_1, \ldots, v_m$ contains $\Span(v_1, \ldots, v_m)$ be closure under addition and scalar multiplication

Thus $\Span(v_1, \ldots, v_m)$ is the smallest subspace of $V$ containing all vectors $v_1, \ldots, v_m$

&nbsp;

**Definition - Finite Dimensional Vector Space**: Vector space with a finite list of vectors that span the space

&nbsp;

**Definition - $\mathbf{\mathcal{P}(F)}$**: Set of all polynomial functions $p: F \rightarrow F$ with coefficients in $F$
$$p(z) = a_0 + a_1z + a_2z^2 + \cdots + a_m z^m \quad \quad z, a_i \in F$$

- $P(F)$ is clearly a subspace of $F^F$ (has additive inverse $0(x)$ and is closed under addition and scalar multiplication)
- The coefficients of a polynomial unique determined by the polynomial

&nbsp;

**Definition - Degree of a Polynomial**: A polynomial $p \in \mathcal{P}(F)$ has **degree** $m$ if there exists scalars $a_0, \ldots, a_m \in F$ with $a_m \neq 0$ such that
$$p(z) = a_0 + a_1 z + \cdots + a_m z^m \quad \quad z, a_i \in F$$

- **NOTE**: Polynomial that is identically $0$ is said to have degree $- \infty$
- $\mathcal{P}_m(F)$ denotes the set of all polynomials with coefficients in $F$ and degree at most $m$

&nbsp;

**Definition - Linear Independence**: List of vectors $v_1, \ldots, v_m$ is **linearly independent** if the only choice of $a_1, \ldots, a_m \in F$ that satisfies $a_1 v_1 + \cdots + a_m v_m = 0$ is $a_1 = \cdots = a_m = 0$

- Thus $v_1, \ldots, v_m$ is linearly independent if and only if each vector in $\Span(v_1, \ldots, v_m)$ has only one representation as a linear combination of $v_1, \ldots, v_m$
- **NOTE**: If some vectors are removed from a linearly independent list, the remaining list is also linearly independent

&nbsp;

**Definition - Linear Dependence**: List of vectors $v_1, \ldots, v_m$ is **linearly dependent** if there exists $a_1, \ldots, a_m \in F$, not all $0$, such that $a_1 v_1 + \cdots + a_m v_m = 0$

- **NOTE**: If some vector in the list of vectors is a linear combination of the other vectors, the list is linearly dependent
- Every list of vectors containing the $0$ vector is linearly dependent

&nbsp;

**2.21 - Linear Dependence Lemma**: Suppose $v_1, \ldots, v_m$ is linearly dependent. Then one of the $j \in \{1, \ldots, m\}$ satisfies

- $v_j \in \Span(v_1, \ldots, v_{j-1})$
- If the jth term is removed, the span of the remaining list equals $\Span(v_1, \ldots, v_m)$

*Proof*:

- Since $v_1, \ldots, v_m$ is linearly dependent, there exists $a_1, \ldots, a_m \in F$ not all $0$ such that
$$a_1 v_1 + \cdots + a_m v_m = 0$$
Let $j$ be the largest in $\{1, \ldots, m\}$ such that $a_j \neq 0$ then we have
$$v_j = - \frac{a_1}{a_j}v - \cdots - \frac{a_{j-1}}{a_j}v_{j-1}$$

- Suppose $u \in \Span(v_1, \ldots, v_m)$ then there exists $c_1, \ldots, c_m \in F$ such that
$$u = c_1 v_1 + \cdots + c_m v_m$$
From the previous bullet point, we can replace $v_j$ with a linear combination of $v_1, \ldots, v_{j-1}$.

&nbsp; &nbsp; &nbsp; &nbsp;Thus we have shown that $u$ is the span of the list obtained from removing the jth term from $v_1, \ldots, v_m$

&nbsp;

**2.23 - Length of Linearly Independent List $\leq$ Length of Spanning List**

*Proof*: Suppose $u_1, \ldots, u_m$ are linearly independent and suppose $w_1, \ldots, w_n$ spans $V$.

We show that $m \leq n$ through a multistep process where we add one of u's and remove one of the w's

- Step 1: Let $B$ be the list $w_1, \ldots, w_n$ that spans $V$. Adjoining any vectors in $V$ to this list produces a linearly dependent list. Thus by the Linear Dependence Lemma, if we add $u_1$ to this list, we can remove $w_j$ from the list to form a new list of length $n$ that spans $V$
- Step $j$: Let $B$ be the list of length $n$ from $j-1$ that spans $V$. If we add $u_j$ to $B$, the list becomes linearly dependent. But since $u_1, \ldots, u_{j-1}$ is linearly independent, we need to remove one of the w's to make $B$ independent again

After $m$ steps, we have added all u's to the list and the process stops. Thus we have $m \leq n$

&nbsp;

**Examples**:

- $(1, 2, 3), (4, 5, 8), (9, 6, 7), (-3, 2, 8)$ is NOT linearly independent in $R^3$. Since $(1, 0, 0), (0, 1, 0), (0, 0, 1)$ span $R^3$ and is a list of length $3$, no linearly independent list in $R^3$ has length $> 3$
- $(1, 2, 3, 5), (4, 5, 8, 1), (4,6 , 7, -1)$ does NOT span $R^4$. Since $(1, 0, 0, 0), (0, 1, 0, 0), (0, 0, 1, 0), (0, 0, 0, 1)$ is linearly indepdent in $R^4$, no list of length $< 4$ spans $R^4$

&nbsp;

**2.26 - Finite-Dimensional Subspaces are Finite-Dimensional**: Every subspace of a finite-dimensional vector space is finite-dimensional

*Proof*: Suppose $U$ is a subspace of a finite-dimensional subspace $V$. We show $U$ is finite-dimensional by construction

- Step 1: If $U= \{0\}$ then clearly $U$ is finite-dimensional. Otherwisen we choose a nonzero vector $v_1 \in U$
- Step $j$: If $U = \Span(v_1, \ldots, v_{j-1})$, then $U$ is finite-dimensional and we are done. Otherwise, take $v_j \notin \Span(v_1, \ldots, v_j)$ and add it to $U$

After each step, we have constructed a list of independent vectors that cannot have length longer than the spanning list of $V$.

Thus the process eventually terminates and $U$ is finite-dimensional

## Bases

**Definition - Bases**: List of vectors in $V$ that is linearly independent and spans $V$

- $(1, 0, \ldots, 0), (0, 1, 0, \ldots, 0), \ldots, (0, \ldots, 0, 1)$ is the **standard basis** of $F^n$

&nbsp;

**2.29 - Criterion for Basis**: A list $v_1, \ldots, v_n$ of vectors is a basis of $V$ if and only if every $v \in V$ can be written uniquely in the form
$$v = a_1 v_1 + \cdots + a_n v_n \quad \quad a_i \in F$$

*Proof*: $\implies$ Suppose $v_1, \ldots, v_n$ is a basis of $V$ and let $v \in V$.

Since $v_1, \ldots, v_n$ spans $V$, $v$ can be written linear combination of the basis vectors with $a_1, \ldots, a_n \in F$

To show this representation is unique, suppose $v$ can also be written as a linear combination using $b_1, \ldots, b_n$. Then
$$0 = (a_1 - b_1)v_1 + \cdots + (a_n - b_n)v_n$$
Since $v_1, \ldots, v_n$ are linearly independent, we have $a_1 = b_1, \ldots, a_n = b_n$

$\impliedby$ Suppose every $v \in V$ can be written uniquely as a linear combination using $a_1, \ldots, a_n$

By definition this means that $v_1, \ldots, v_n$ spans $V$

Looking at the unique representation of
$$0 = a_1v_1 + \cdots + a_n v_n$$
We must have $a_1 = \cdots = a_n = 0$. Thus $v_1, \ldots, v_n$ are linearly independent and a basis of $V$

&nbsp;

**2.31 - Spanning List Contains a Basis**: Every spanning list can be reduced to a basis of the vector space

*Proof*: Suppose $B = v_1, \ldots, v_n$ spans $V$. We can remove vectors using the following steps

- Step 1: if $v_1 = 0$, delete $v_1$ from $B$. Otherwise leave $B$ unchanged
- Step $j$: If $v_j \in \Span(v_1, \ldots, v_{j-1})$, delete $v_j$ from $B$. Otherwise leave $B$ unchanged

Once $B$ is of length $n$, stop. This list $B$ spans $V$ because the original list spanned $V$ and we only discarded extraneous vectors

This process ensures no vector in $B$ is in the span of the previous ones. Thus $B$ is linearly independent

Thus $B$ is a basis of $V$

&nbsp;

**2.32 - Basis of Finite-Dimensional Vector Space**: Every finite-dimensional vector space has a basis

*Proof*: Since a finite-dimensional vector space has a spanning list, the previous result shows us the list can be reduced to a basis

&nbsp;

**2.33 - Linearly independent List Can be Extended to a Basis**: Every linearly independent list of vectors in a finite-dimensional vector space can be extended to a basis

*Proof*: Suppose $u_1, \ldots, u_m$ is linearly independent and $w_1, \ldots, w_n$ be a basis of $V$. Forming the list
$$u_1, \ldots, u_m, w_1, \ldots, w_n$$
Clearly spans $V$. Then removing the extraneous vectors from this list produces a basis of $V$

However, none of the u's will be removed since they are already linearly independent so we only remove w's from the list

&nbsp;

**2.34 - Every Subspace of $\mathbf{V}$ is Part of a Direct Sum Equal to V**: Suppose $U$ is a subspace of a finite-dimensional $V$. Then there is a subspace $W$ of $V$ such that $V = U \oplus W$

*Proof*: Since $V$ is finite-dimensional, so is $U$.

Thus there is a basis $u_1, \ldots, u_m$ of $U$ that can be extended to a basis $u_1, \ldots, u_m, w_1, \ldots, w_n$ of $V$

Let $W = \Span(w_1, \ldots, w_n)$. To show $V = U \oplus W$, we need
$$V = U + W \quad \quad U \cap W = \{0\}$$

- Since $u_1, \ldots, u_m, w_1, \ldots, w_n$ spans $V$, any vector $v \in V$ can be written as
$$v = u + w \quad \quad u \in U, w \in W$$
Thus we have $v \in U + W \implies V = U + W$

- Let $v \in U \cap W$. Then there exists scalars $a_1, \ldots, a_m, b_1, \ldots, b_n \in F$ such that
$$v = a_1 u_1 + \cdots + a_m u_m = b_1 w_1 + \cdots + b_n w_n$$
Then we must have
$$a_1u_1 + \cdots + a_m u_m - b_1 w_1 - \cdots - b_n w_n = 0$$
Since these vectors are linearly independent, we must have $a_1 = \cdots = a_m = b_1 = \cdots = b_n = 0$

&nbsp; &nbsp; &nbsp; &nbsp;Thus $v = 0$ and $U \cap W = \{0\}$

## Dimension

**2.35 - Bases Have the Same Length**

*Proof*: Suppose $B_1$ and $B_2$ are bases of a finite-dimensional $V$

Since both $B_1$ and $B_2$ are linearly independent and span $V$, length $B_1 = \text{ length } B_2$

&nbsp;

**Definition - Dimension $\dim{V}$**: length of any basis of a vector space

&nbsp;

**2.38 - Dimension of a Subspace**: Let $U$ be a subspace of a finite-dimensional $V$. Then $\dim{U} \leq \dim{V}$

*Proof*: Basis of $U$ has length $\leq$ the length of the basis of $V$. Thus $\dim{U} \leq \dim{V}$

&nbsp;

**2.39 - Linearly Independent List of the Correct Length is a Basis**

*Proof*: Suppose $\dim{V} = n$ and $v_1, \ldots, v_n$ is linearly independent.

We know that this list can be extended to a basis of $V$, but since the basis is of length $n$, there is nothing to extend

Thus $v_1, \ldots, v_n$ is the basis of $V$ we desire

&nbsp;

**2.42 - Spanning List of the Right Length is a Basis**: Every spanning list of vectors in $V$ with length $\dim{V}$ is a basis of $V$

*Proof*: Suppose $v_1, \ldots, v_n$ spans $V$. This list can be reduced to a basis of $V$.

However, every basis of $V$ has length $n$, so this reduction is trivial and thus $v_1, \ldots, v_n$ is a basis of $V$

&nbsp;

**2.43 - Dimension of a Sum**: If $U_1, U_2$ are finite-dimensional vector spaces, then
$$\dim(U_1 + U_2) = \dim{U_1} + \dim{U_2} - \dim(U_1 \cap U_2)$$

*Proof*: Let $u_1, \ldots, u_m$ be a basis of $U_1 \cap U_2$ (thus $\dim(U_1 \cap U_2) = m$)

Note that this list is linearly independent in $U_1$ and $U_2$.

Thus we can extend the list to a basis $u_1, \ldots, u_m, v_1, \ldots, v_j$ of $U_1$ with $\dim{U_1} = m + j$

And extend the list to a basis $u_1, \ldots, u_m, w_1, \ldots, w_k$ of $U_2$ with $\dim{U_2} = m + k$

Clearly $\Span(u_1, \ldots, u_m, v_1, \ldots, v_j, w_1, \ldots, w_k)$ contains $U_1$ and $U_2$, and thus equals $U_1 + U_2$

We now show that this list is linearly independent. We need
$$a_1 u_1 + \cdots + a_m u_m + b_1 v_1 + \cdots + b_j v_j + c_1 w_1 + \cdots + c_k w_k = 0$$
This can be rewritten as
$$c_1 w_1 + \cdots + c_k w_k = -a_1 u_1 - \cdots - a_m u_m - b_1v_1 - \cdots - b_jv_j \in U_1$$
Since all w's are in $U_2$, this means that $c_1w_1 + \cdots + c_k w_k \in U_1 \cap U_2$ and thus
$$c_1 w_1 + \cdots c_k w_k = d_1 u_1 + \cdots + d_m u_m$$
However, we know that $u_1, \ldots, u_m, w_1, \ldots, w_k$ is linearly independent. Thus $c_1 = \cdots = c_k = d_1 = \cdots = d_m = 0$
Thus the original equation becomes
$$a_1 u_1 + \cdots + a_m u_m + b_1 v_1 + \cdots + b_j v_j = 0$$
But $u_1, \ldots, u_m, v_1, \ldots, v_j$ is linearly independent. Thus $a_1 = \cdots = a_m = b_1 = \cdots = b_j = 0$

Thus $\dim(U_1 + U_2) = (m + j) + (m + k) - m = \dim{U_1} + \dim{U_2} - \dim(U_1 \cap U_2)$

# Linear Maps

## Vector Space of Linear Maps

**Definition - Linear Map**: Function $T: V \rightarrow W$ satisfying

- **Additivity**: $T(u + v) = Tu + Tv \quad \quad \forall u, v \in V$
- **Homogeneity**: $T(\lambda v) = \lambda (Tv) \quad \quad \forall \lambda \in F \quad \forall v \in V$

&nbsp;

**Definition - $\mathbf{\mathcal{L}(V, W)}$**: set of all linear maps from $V \rightarrow W$

&nbsp;

**Examples**:

- $0 \in \mathcal{L}(V, W)$: takes any vector in $V$ and maps it to the additivity identity in $W$. Denoted $0v = 0 \quad \quad \forall v \in V$
- $I \in \mathcal{L}(V, V)$: identity mapping that takes any vector in $V$ and maps it to itself. Denoted $Iv = v \quad \quad \forall v \in V$
- $T \in \mathcal{L}(R^3, R^2)$: defined by $T(x, y, z) = (2x - y + 3z, 7x + 5y - 6z)$
- $T \in \mathcal{L}(F^n, F^m)$: define by $T(x_1, \ldots, x_n) = (A_{1,1} x_1 + \cdots + A_{1, n} x_n, \ldots, A_{m, 1} x_1 + \cdots + A_{m, n} x_n)$ for $A_{j, k} \in F$

&nbsp;

**3.5 - Linear Maps and Basis of Domain**: Let $v_1, \ldots, v_n$ be a basis of $V$ and $w_1, \ldots, w_n \in W$. Then there exists a unique linear map $T: V \rightarrow W$ such that
$$Tv_{j} = w_j \quad \quad j \in \{1, \ldots, n\}$$

*Proof*: First we show existence of such an equation. Define $T: V \rightarrow W$ by
$$T(c_1 v_1 + \cdots + c_nv_n) = c_1 w_1 + \cdots + c_n w_n \quad \quad c_i \in F$$

Since $v_1, \ldots, v_n$ is a basis of $V$, the equation above is a function $T: V \rightarrow W$ since each element of $V$ can be uniquely written in the form $c_1v_1 + \cdots + c_n v_n$

For each $j$, take $c_j = 1$ and all other $c_i = 0$. Then clearly $Tv_j = w_j$

Next we show that this function is a linear map.

- For $u, v \in V$ we have
\begin{align*}
T(u + v) &= T((a_1 + c_1)v_1 + \cdots + (a_n + c_n) v_n) \\
&= (a_1 + c_1) w_1 + \cdots + (a_n + c_n) w_n \\
&= Tu + Tv
\end{align*}
- For $\lambda \in F$ and $v \in V$, we have
\begin{align*}
T(\lambda v) &= T(\lambda c_1 v_1 + \cdots + \lambda c_n v_n) \\
&= \lambda (c_1 w_1 + \cdots + c_n w_n) \\
&= \lambda Tv
\end{align*}

Finally we show that this linear mapping is unique. Let $T \in \mathcal{L}(V, W)$ and $Tv_j = w_j$ for $j \in \{1, \ldots, n\}$

- Homogeneity implies that $T(c_j v_j) = c_j w_j$
- Additivity implies $T(c_1v_1 + \cdots + c_n v_n) = c_1w_1 + \cdots + c_n w_n$

Thus $T$ is uniquely determined by $\Span(v_1, \ldots, v_n)$. Since $v_1, \ldots, v_n$ is a basis, $T$ is uniquely determined on $V$

## Algebraic Operations on $\mathbf{\mathcal{L}(V, W)}$

**Definition - Addition and Scalar Multiplication on $\mathbf{\mathcal{L}(V, W)}$**: Let $S, T \in \mathcal{L}(V, W)$ and $\lambda \in F$. Then

- **Sum**: $(S + T)(v) = Sv + Tv$
- **Product**: $(\lambda T) (v) = \lambda (Tv)$

&nbsp;

**3.7 - $\mathbf{\mathcal{L}(V, W)}$ is a Vector Space**: Under the operations of addition and scalar multiplication defined above, $\mathcal{L}(V, W)$ is a vector space

*Proof*: Let $S, T, U \in \mathcal{L}(V, W)$ and $a, b \in F$

- **Commutativity**: $S + T = T + S$ holds
- **Associativity**: $(S + T) + U = S + (T + U)$ and $(ab) S = a(bS)$
- **Additivity Identity**: $S + 0 = S$
- **Multiplicative Identity** $1S = S$
- **Distributive Property**: $a(S + T) = aS + aT)$ and $(a + b)S = aS + bS$

&nbsp;

**Definition - Product of Linear Maps**: For $T \in \mathcal{L}(U, V)$ and $S \in \mathcal{L}(V, W)$, the **product** $ST \in \mathcal{L}(U, W)$ is defined by $(ST)(u) = S(T u)$ for $u \in U$


- **NOTE**: this is identical to the usual composition of functions $S \circ T$

&nbsp;

**3.9 - Algebraic Properties of Products of Linear Maps**: For products of linear maps $T, T_1, T_2, T_3, S, S_1, S_2$ where the domains of the mappings make sense, the following properties hold

- **Associativity**: $(T_1 T_2) T_3 = T_1 (T_2 T_3)$
- **Identity**: $TI = IT = T$

  - First $I$ is the identity map on $V$ and second $I$ is the identity map on $W$
- **Distributive Properties**: $(S_1 + S_2)T = S_1T + S_2T$ and $S(T_1 + T_2) = ST_1 + S T_2$

&nbsp;

**NOTE**: Product of linear maps aren't commutative, so it's not always true that $ST = TS$

**Example**: Let $D \in \mathcal{L}(\mathcal{P}(R), \mathcal{P}(R))$ be the differentiation map and $T \in \mathcal{L}(\mathcal{P}(R), \mathcal{P}(R))$ be the multiplication by $x^2$ map

Clearly $((TD)p)(x) = x^2 p'(x) \neq x^2 p'(x) + 2xp(x) = ((DT)p)(x)$

&nbsp;

**3.11 - Linear Maps Take $\mathbf{0}$ to $\mathbf{0}$**: Let $T$ be a linear map from $V$ to $W$. Then $T(0) = 0$

*Proof*: By additivity, we have that $T(0) = T(0 + 0) = T(0) + T(0)$

Then adding the additive inverse of $T(0)$ to both sides gives us $T(0) = 0$

## Null Spaces and Ranges

### Null Space and Injectivity

**Definition - Null Space**: For $T \in \mathcal{L}(V, W)$, $\Null T$, is a subset of $V$ consisting of vectors that $T$ maps to $0$
$$\Null T = \{v \in V \mid Tv = 0\}$$

&nbsp;

**Examples**

- If $T$ is the zero map from $V$ to $W$, then $\Null T = V$
- Let $D \in \mathcal{L}(\mathcal{P}(R), \mathcal{P}(R))$ be the differentiation map defined by $Dp = p'$. Then $\Null D$ is the set of constant functions
- Let $T \in \mathcal{L}(\mathcal{P}(R), \mathcal{P}(R))$ be the multiplication by $x^2$ map defined by $(Tp)(x) = x^2 p(x)$. Then $\Null T = \{0\}$

&nbsp;

**3.14 - Null Space is a Subspace**: For $T \in \mathcal{L}(V, W)$, $\Null T$ is a subspace of $V$

*Proof*: Since $T$ is a linear mapping, we have $T(0) = 0 \implies 0 \in \Null T$

If we take $u, v \in \Null T$, then $T(u + v) = Tu + Tv = 0$. Thus $\Null T$ is closed under addition

If we take $\lambda \in F$ and $v \in \Null T$, then $T(\lambda u) = \lambda T u = \lambda 0 = 0$. Thus $\Null T$ is closed under scalar multiplication

Thus we have satisfied all criterion for $\Null T$ to be a subspace of $V$

&nbsp;

**Definition - Injective**: A function $T: V \rightarrow W$ is **injective** if $Tu = Tv \implies u = v$

&nbsp;

**3.16 Injectivity is Equivalent if Null Space is $\mathbf{\{0\}}$**: If $T \in \mathcal{L}(V, W)$, then $T$ is injective if and only if $\Null T = \{0\}$

*Proof*: $\implies$ Suppose $T$ is injective. Clearly $0 \subseteq \Null T$. To show the other way around, take $v \in \Null T \implies T(v) = 0 = T(0)$

Since $T$ is injective, we must have $v = 0 \implies \Null T = \{0\}$

$\impliedby$ Suppose $\Null T = \{0\}$ and suppose there are $u, v \in V$ such that $Tu = Tv$

Then we have $0 = Tu - Tv = T(u - v) \implies u - v \in \Null T = \{0\} \implies u = v$

## Range and Surjectivity

**Definition - Range**: For $T \in \mathcal{L}(V, W)$, $\range T$ is a subset of $W$ such that
$$\range T = \{Tv \mid v \in V\}$$

&nbsp;

**Examples**:

- If $T$ is the zero map from $V$ to $W$, so $\forall v \in V$, $Tv = 0$, then $\range T = \{0\}$
- Let $T \in \mathcal{L}(R^2, R^3)$ for $T(x, y) = (2x, 5y, x + y)$. Then $\range T = \{2x, 5y, x + y \mid x, y \in R\}$
- Let $D \in \mathcal{L}(\mathcal{P}(R), \mathcal{P}(R))$ be the differentiation map defined by $Dp = p'$. Then $\range D = \mathcal{P}(R)$

&nbsp;

**3.19 - Range is a Subspace**: For $T \in \mathcal{L}(V, W)$, we have $\range T$ is a subspace of $W$

*Proof*: Clearly $T(0) = 0 \implies 0 \in \range T$

For $w_1, w_2 \in \range T$, there exists $v_1, v_2 \in V$ such that $Tv_1 = w_1$ and $T v_2 = w_2$. Thus
$$T(v_1 + v_2) = Tv_1 + Tv_2 = w_1 + w_2 \in \range T$$
Thus $\range T$ is closed under addition

For $w \in \range T$ and $\lambda \in F$, there exists $v \in V$ such that $Tv = w$. Thus
$$T(\lambda v) = \lambda Tv = \lambda w \in \range T$$
Thus $\range T$ is closed under scalar multiplication

&nbsp;

**Definition - Surjective**: $T: V \rightarrow W$ is **surjective** if $\range T = W$

### Fundamental Theorem of Linear Maps

**3.22 - Fundamental Theorem of Linear Maps**: Suppose $V$ is finite-dimensional and $T \in \mathcal{L}(V, W)$. Then $\range T$ is finite-dimensional and
$$\dim V = \dim \Null T + \dim \range T$$

*Proof*: Let $u_1, \ldots, u_m$ be a basis of $\Null T \implies \dim \Null T = m$

This list can be extended into a basis of $V$: $u_1, \ldots, u_m , v_1, \ldots, v_n \implies \dim V = m + n$

We show that $\dim \range T = n$ by proving that $Tv_1, \ldots, Tv_n$ is a basis of $\range T$

Take $v \in V$. Since $u_1, \ldots, u_m, v_1, \ldots, v_n$ spans $V$, we can write
$$v = a_1 u_1 = \cdots + a_m u_m + b_1 v_1 + \cdots + b_n v_n \quad \quad a_i, b_i \in F$$
Applying $T$ to both sides gives
$$Tv = b_1 T v_2 + \cdots + b_n T v_n$$
Which implies that $Tv_1, \ldots T v_n$ spans $\range T$.

To show $T v_1, \ldots, Tv_n$ is linearly independent, suppose $c_1, \ldots c_n \in F$ such that
$$c_1 T v_1 + \cdots + c_n T v_n = T(c_1v_1 + \cdots + c_n + v_n) = 0 \implies c_1 v_1 + \cdots + c_n v_n \in \Null T$$
Since $u_1, \ldots, u_m$ spans $\Null T$, we have
$$c_1 v_1 + \cdots + c_n v_n = d_1 u_1 + \cdots d_m u_m \quad \quad d_i \in F$$
Since $u_1, \ldots, u_m, v_1, \ldots v_n$ is linearly independent, we must have $c_j = d_i = 0$ and thus $Tv_1, \ldots, T v_n$ is linearly independent

Thus we must have $T v_1, \ldots, Tv_n$ is a basis of $\range T$ and clearly $\dim \range T = n$

Thus $\dim V = \dim \Null T + \dim \range T$

&nbsp;

**3.23 - Map to a Smaller Dimensional Space is not Injective**: Suppose $V, W$ are finite-dimensional vector spaces where $\dim V > \dim W$. Then no linear map from $V \rightarrow W$ is injective

*Proof*: Let $T \in \mathcal{L}(V, W)$. Then
\begin{align*}
\dim \Null T &= \dim V - \dim \range T\\
&\geq \dim V - \dim W\\
&> 0
\end{align*}
Thus $\Null T$ contains vectors other than $0$ and $T$ is not injective

&nbsp;

**3.24 - Map to a Larger Dimensional Space is not Surjective**: Suppose $V, W$ are finite-dimensional vector spaces where $\dim V < \dim W$. Then no linear map from $V \rightarrow W$ is surjective

*Proof*: Let $T \in \mathcal{L}(V, W)$. Then
\begin{align*}
\dim \range T &= \dim V - \dim \Null T \\
&\leq \dim V \\
&< \dim W
\end{align*}
Thus $\range T$ cannot equal $W$ and $T$ is not surjective

&nbsp;

**3.26 Homogeneous System of Linear Equations**: Homogeneous system of equations with more variables than equations has nonzero solutions

*Proof*: Define $T: F^n \rightarrow F^m$ by
$$T(x_1, \ldots, x_n) = (\sum_{k = 1}^n A_{1, k} x_k, \ldots, \sum_{k = 1}^n A_{m, k} x_k)$$
Since $n > m$, clearly $T$ is not injective and thus the homogenous system of equations has nonzero solutions

&nbsp;

**3.29 - Inhomogenous System of Linear Equations**: Inhomogenous system of equations with more equations than variables has no solutions

*Proof*: Define $T: F^n \rightarrow F^m$ by
$$T(x_1, \ldots, x_n) = (\sum_{k = 1}^n A_{1, k} x_k, \ldots, \sum_{k = 1}^n A_{m, k} x_k)$$
Since $n < m$, clearly $T$ is not surjective and thus the homogenous system of equations has no solution

## Matrices

**Definition - Matrix of a Linear Map $\mathbf{\mathcal{M}(T)}$**: Let $T \in \mathcal{L}(V, W)$ and $v_1, \ldots, v_n$ be a basis of $V$ and $w_1, \ldots, w_m$ be a basis of $W$. Then the **matrix** of $T$, denoted $\mathcal{M}(T)$, has entries $A_{j, k}$ defined by
$$Tv_k = A_{1, k} w_1 + \cdots + A_{m, k} w_m$$

- **NOTE**: Unless stated otherwise, assume the bases between $F^n \rightarrow F^m$ are dealing with standard bases

&nbsp;

**Example**: Suppose $T \in \mathcal{L}(F^2, F^3)$ is defined by $T(x, y) = (x + 3y, 2x + 5y, 7x + 9y)$.

Since $T(1, 0) = (1, 2, 7)$ and $T(0,1) = (3, 5, 9)$, we have $\mathcal{M}(T) = \begin{bmatrix}1 & 3 \\ 2 & 5 \\ 7 & 9 \end{bmatrix}$

&nbsp;

&nbsp;

**3.36 Matrix of Sum of Linear Maps**: Suppose $S, T \in \mathcal{L}(V, W)$. Then $\mathcal{M}(S + T) = \mathcal{M}(S) + \mathcal{M}(T)$

*Proof*: Follows from matrix addition

&nbsp;

**3.38 Matrix of Scalar Times a Linear Map**: Suppose $\lambda \in F$ and $T \in \mathcal{L}(V, W)$. Then $\mathcal{M}(\lambda T) = \lambda \mathcal{M}(T)$

*Proof*: Follows from matrix scalar multiplication

&nbsp;


**Definition - $\mathbf{F^{m, n}}$**: Set of all $m$-by-$n$ matrices with entries in $F$

&nbsp;

**3.40 - $\mathbf{\dim F^{m,n } = mn}$**

*Proof*: First show that $F^{m, n}$ is a vector space

- Commutativity: Matrix addition is commutative
- Associativity: Matrix addition and scalar multiplication is associative
- Additivity Identity: Matrix with all zeros is the additive identity
- Multiplicative Identity $1 \in F$ is the multiplicative identity
- Distributive Property: Scalar multiplication clearly distributes over matrix addition

Next we show that the basis of $F^{m,n}$ is of length $mn$.

Clearly the list of $m$-by-$n$ matrices with $0$ in all entries except for a $1$ in one entry form a basis of $F^{m, n}$.

There are $mn$ such matrices. Thus $\dim F^{m, n} = mn$

&nbsp;

**3.43 Matrix of the Product of Linear Map**: Let $T \in \mathcal{L}(U, V)$ and $S \in \mathcal{L}(V, W)$. Then $\mathcal{M}(ST) = \mathcal{M}(S) \mathcal{M}(T)$

*Proof*: Follows from matrix multiplication

&nbsp;

**Notation - $\mathbf{A_{j, \cdot}, A_{\cdot, k}}$**: For a $m$-by-$n$ matrix $A$

- $A_{j, \cdot}$ denotes row $j$ of $A$
- $A_{\cdot, k}$ denotes column $k$ of $A$

&nbsp;

**3.47 - Entry of Matrix Product Equals Row Times Column**: Let $M$ be an $m$-by-$n$ matrix and $C$ be an $n$-by-$p$ matrix. Then
$$(AC)_{j, k} = A_{j, \cdot} C_{\cdot, k}$$

&nbsp;

**3.49 - Column of Matrix Product Equals Matrix Times Column**: Let $M$ be an $m$-by-$n$ matrix and $C$ be an $n$-by-$p$ matrix. Then
$$(AC)_{\cdot, k} = AC_{\cdot, k}$$

**Example**: $\begin{bmatrix} 1 & 2 \\ 3 & 4 \\ 5 & 6 \end{bmatrix} = \begin{bmatrix} 5 \\ 1\end{bmatrix} = \begin{bmatrix} 7 \\ 19 \\ 31\end{bmatrix}$

&nbsp;

**3.52 - Linear Combination of Columns**: Suppose $A$ is an $m$-by-$n$ matrix and $c$ is an $m$-by-$1$ matrix. Then
$$Ac = c_1 A_{\cdot, 1} + \cdots + c_n A_{\cdot, n}$$

**Example**: $\begin{bmatrix}7 \\ 19 \\ 31 \end{bmatrix} = 5 \begin{bmatrix} 1 \\ 3 \\ 5\end{bmatrix} + 1 \begin{bmatrix} 2 \\ 4 \\ 6 \end{bmatrix}$

## Invertibility and Isomoprhic Vector Spaces

### Invertible Linear Maps

**Definition - Invertible**: $T \in \mathcal{L}(V, W)$ is **invertible** if there exists $S \in \mathcal{L}(W, V)$ such that $ST = I$ on $V$ and $%S = I$ on $W$

&nbsp;

**Definition - Inverse**: $S \in \mathcal{L}(W, V)$ satisfying $ST = I$ and $TS = I$ is called an **inverse** of $T$, denoted $T^{-1}$

&nbsp;

**3.54 - Inverse is Unique**: An invertible linear map has a unique inverse

*Proof*: Let $T \in \mathcal{L}(V, W)$ and $S_1, S_2$ be inverses of $T$. Then we have
$$S_1 = S_1 I = S_1 (TS_2) = (S_1 t) S_2 = I S_2 = S_2$$

&nbsp;

**3.56 - Invertibility is Equivalent to Injectivity and Surjectvitiy**: $T \in \mathcal{L}(V, W)$ is invertible if and only if it is injective and surjective

*Proof*: $\implies$ Suppose $T$ is invertible

- Injective: Let $u, v \in V$ such that $Tu = Tv$. Then $u = T^{-1}(Tu) = T^{-1}(Tv) = v$
- Surjective: Let $w \in W$ where $w = T(T^{-1}w) \implies w \in \range T$. Thus $\range T = W$

$\impliedby$ Assume $T$ is injective and surjective and let $S \in \mathcal{L}(W, V)$.

For each $w \in W$, let $Sw$ to be the unique element of $V$ such that $T(Sw) = w$ (this follows from surjectivity and injectivity of $T$).

Clearly $T \circ S$ is the identity mapping on $W$

To show that $S \circ T$ equals the identity mapping on $V$, take $v \in V$. Then
$$T((S \circ T) v) = (T \circ S)(Tv) = I(Tv) = Tv$$
Thus $(S \circ T) v = v \implies S \circ T$ is the identity mapping on $V$

Finally we show that $S$ is linear. Suppose $w_1, w_2 \in W$. Then
$$T(S(w_1 + w_2)) = T(Sw_1 + Sw_2) = T(Sw_1) + T(Sw_2) = w_1 + w_2$$
Thus $S(w_1 + w_2) = Sw_1 + Sw_2$

Suppose $w \in W$ and $\lambda \in F$. Then
$$T(S(\lambda w)) = T(\lambda S w) = \lambda T(Sw) = \lambda w$$
Thus $S(\lambda w) = \lambda Sw$

### Isomorphic Vector Spaces

**Definition - Isomorphism**: An invertible linear map

&nbsp;

**Definition - Isomorphic**: 2 vector spaces are **isomorphic**: if there is an isomorphism from one vector space onto the other

&nbsp;

**3.59 - Dimension Shows Whether Vector Spaces are Isomorphic**: 2 finite-dimensional vector spaces over $F$ are isomorphic if and only if they have the same dimension

*Proof*: $\implies$ Suppose $V, W$ are isomorphic finite-dimensional vector spaces, meaning that there is an isomorphism $T: V \rightarrow W$.

Since $T$ is invertible, $\Null T = \{ 0\} \implies \dim \Null T = 0$ and $\range T = W \implies \dim \range T = \dim W$

Thus $\dim V = \dim \Null T + \dim \range T = \dim W$

$\impliedby$ Suppose $V, W$ are finite-dimensional vector spaces with the same dimension and let $v_1, \ldots w_n$ and $w_1, \ldots, w_n$ be bases of $V$ and $W$. Let $T \in \mathcal{L}(V, W)$ be defined by
$$T(c_1v_1 + \cdots + c_n v_n) = c_1 w_1 + \cdots + c_n w_n$$
$T$ is well-defined because $v_1, \ldots, v_n$ is a basis of $V$ and thus each $v \in V$ can be uniquely represented as a LC of $v_1, \ldots, v_n$

- $T$ is surjective because $w_1, \ldots, w_n$ spans $W$

- $\Null T = \{0\}$ since $w_1, \ldots, w_n$ is linearly independent. Thus $T$ is injective

Since $T$ is both injective and surjective, $T$ is an isomorphism and $V, W$ are isomorphic

&nbsp;

**3.60 - $\mathbf{\mathcal{L}(V, W)}$ and $\mathbf{F^{m, n}}$ are Isomorphic**: Let $v_1, \ldots, v_n$ and $w_1, \ldots, w_m$ be bases of $V, W$ respectively. Then $\mathcal{M}$ is an isomorphism between $\mathcal{L}(V, W)$ and $F^{m, n}$

*Proof*: Note that for each $T \in \mathcal{L}(V, W)$, we have a matrix $\mathcal{T} \in F^{m, n}$. Thus $\mathcal{M}$ is a function from $\mathcal{L}(V, W) \rightarrow F^{m, n}$

We know that $\mathcal{M}$ is a linear map since additivity and homogeneity hold.

To show that $\mathcal{M}$ is invertible

- If $\mathcal{M}(T) = 0$, then $Tv_k = 0$ for $k \in \{1, \ldots, n\}$. Since $v_1, \ldots, v_n$ is a basis of $V$, we must have $T = 0$. Thus $\mathcal{M}$ is injective
- Let $A \in F^{m, n}$ and $\displaystyle Tv_k = \sum_{j = 1}^m A_{j, k} w_j$. Clearly $\mathcal{M}(T) = A$. Thus $\range \mathcal{M} = F^{m,n}$

&nbsp;

**3.61 - $\mathbf{\dim \mathcal{L}(V, W) = (\dim V)(\dim W)}$**: Let $V, W$ be finite-dimensional. Then $\mathcal{L}(V, W)$ is finite-dimensional and
$$\dim \mathcal{L}(V, W) = (\dim V)(\dim W)$$

*Proof*: We know that $\mathcal{L}(V, W)$ is isomorphic to $F^{m, n}$

Thus they must have the same dimension as $F^{m, n}$

We know that $F^{m,n}$ has dimension $mn = (\dim V) (\dim W)$

### Linear Maps as Matrix Multiplication

**Definition - Matrix of a Vector $\mathbf{\mathcal{M}(v)}$**: Suppose $v \in V$ and $v_1, \ldots, v_n$ is a basis of $V$. Then the **matrix** of $V$ with respect to this basis is
$$\mathcal{M}(v) = \begin{bmatrix} c_1 \\ \vdots \\ c_n\end{bmatrix}$$
Where $c_1, \ldots, c_n$ are scalars such that
$$v = c_1v_1 + \cdots + c_n v_n$$

- **NOTE**: Once a basis is chosen, the function $\mathcal{M}$ that takes $v \in V$ to $\mathcal{M}(v)$ is an isomorphism $V \rightarrow F^{n,1}$

&nbsp;

**3.64 - $\mathbf{\mathcal{M}(T)_{\cdot, k} = \mathcal{M}(v_k)}$**: Suppose $T \in \mathcal{L}(V, W)$ and $v_1, \ldots, v_n$ is a basis of $V$ and $w_1, \ldots, w_m$ is a basis of $W$. Then the kth column of $\mathcal{M}(T)$ is equal to $\mathcal{M}(v_k)$

&nbsp;

**3.65 - Linear Maps Act Like Matrix Multiplication**: Suppose $T \in \mathcal{L}(V, W)$ and $v \in V$, and suppose $v_1, \ldots, v_n$ and $w_1, \ldots, w_m$ are bases of $V$ and $W$ respectively. Then
$$\mathcal{M}(Tv) = \mathcal{M}(T) \mathcal{M}(v)$$

*Proof*: Suppose $v = c_1v_1 + \cdots + c_n v_n$ Then
$$Tv = c_1 Tv_1 + \cdots + c_n T v_n$$
Thus we have
\begin{align*}
 \mathcal{M}(Tv)  &= c_1 \mathcal{M}(Tv_1) + \cdots + c_n \mathcal{M}(T_n)\\
 &= c_1 \mathcal{M}(T)_{\cdot, 1} + \cdots + c_n \mathcal{M}(T)_{\cdot, n}\\
 &= \mathcal{M}(T)\mathcal{M}(v)
\end{align*}

### Operators

**Definition - Operator $\mathbf{\mathcal{L}(V)}$**: Linear map from a vector space to itself

&nbsp;

**3.69 - Injectivity is Equivalent to Surjectivity in Finite Dimensions**: Suppose $V$ is finite-dimensional and $T \in \mathcal{L}(V)$. Then the following are equivalent:

- $T$ is invertible
- $T$ is injective
- $T$ is surjective

*Proof*: Clearly $T$ invertible $\implies T$ is injective

Now suppose $T$ is injective (thus $\Null T = \{0\}$) and thus we have
\begin{align*}
\dim \range T &= \dim V - \dim \Null T \\
&= \dim V
\end{align*}
Thus $\range T = V$ and thus $T$ is surjective

Finally, suppose that $T$ is surjective, meaning that $\range T = V$. Then we have
\begin{align*}
\dim \null T &= \dim V - \dim \range T \\
&= 0
\end{align*}
Thus $\Null T = \{0\}$ and thus $T$ is injective and surjective, meaning $T$ is invertible

## Products and Quotients of Vector Spaces

### Products of Vector Spaces

**Definition - Product of Vector Spaces**: Suppose $V_1, \ldots, V_m$ are vector spaces over $F$. The **product** $V_1 \times \cdots \times V_m$ is defined by
$$V_1 \times \cdots \times V_m = \{(v_1, \ldots, v_m) \mid v_1 \ldots, v_m \in V_m\}$$
- Addition is defined by
$$(u_1, \ldots, u_m) + (v_1, \ldots, v_m) = (u_1 + v_1, \ldots, u_m + v_m)$$
- Scalar multiplication is defined by
$$\lambda (v_1, \ldots, v_m) = (\lambda v_1, \ldots, \lambda v_m)$$

&nbsp;

**3.73 - Product of Vector Spaces is a Vector Space**: Suppose $V_1, \ldots, V_m$ are vector spaces over $F$. Then $V_1 \times \cdots \times V_m$ is a vector space over $F$

*Proof*: Necessary properties of commutative, associativity, identities, additive inverse, and distributivity all hold

&nbsp;

**3.76 - Dimension of a Product is the Sum of Dimensions**: Suppose $V_1, \ldots, V_m$ are vector spaces over $F$. Then $V_1 \times \cdots \times V_m$ is finite-dimensional and
$$\dim (V_1 \times \cdots \times V_m) = \dim V_1 + \cdots + \dim V_m$$
*Proof*: Choose a basis of each $V_j$. For each basis vector of each $V_j$, consider the element of $V_1 \times \cdots \times V__m$ such that

- has the appropriate basis vector in the jth slot
- $0$ in all other slots
This list is clearly linearly independent and spans $V_1 \times \cdots \times V_m$ and thus is a basis of $V_1 \times \cdots \times V_m$

The length of this basis is $\dim V_1 + \cdots + \dim V_m$

### Products and Direct Sums

**3.77 - Products and Direct Sums**: Suppose $U_1, \ldots, U_m$ are subspaces of $V$. Define a linear map $\Tau$
























<!-- # Introduction -->

<!-- For these notes, we will use Roman letters $(a, b, c)$ for vectors and Greek letters $(\alpha, \beta, \gamma)$ for elements of $F$ (*scalars*) -->

<!-- **Field**: a nonempty set $F$ with operations: addition and multiplication that assigns pairs of elements $\alpha, \beta \in F$ to $\alpha + \beta$ and $\alpha \beta \in F$ and satisfies the following properties for $\alpha, \beta, \gamma \in F$ -->

<!-- 1. $\alpha + \beta = \beta + \alpha$ and $\alpha \beta = \beta \alpha \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad$ (commutative law) -->
<!-- 2. $\alpha + (\beta + \gamma) = (\alpha + \beta) + \gamma$ and $(\alpha \beta) \gamma = \alpha (\beta \gamma) \quad \quad$ (associativity law) -->
<!-- 3. $\alpha (\beta + \gamma) = \alpha \beta + \alpha \gamma \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad$ (distributive law) -->
<!-- 4. $\exists 0 \in F$ such that $\forall \alpha \in F, \alpha + 0 = \alpha$ -->
<!-- 5. $\forall \alpha \in F, \exists -a \in F$ such that $\alpha + (-\alpha) = 0$ -->
<!-- 6. $\exists 1 \in F$ such that $1 \neq 0$ and $\forall \alpha \in F, \alpha \cdot 1 = \alpha$ -->
<!-- 7. $\forall \alpha \in F, \alpha \neq 0, \exists a^{-1} \in F$ such that $aa^{-1} = 1$ -->

<!-- - **Example**: $R$ is a field under normal addition and multiplication. $Z$ is NOT a field since $2 \in Z$ but $2^{-1} \notin Z$ -->

<!-- **Subfield** is a nonempty set $F_0 \subseteq F$ that is closed under the operations defined by $F$ and satisfies the axioms relative to the operation $(\alpha, \beta \in F_0 \implies \alpha + \beta, \alpha \beta \in F_0)$ -->

<!-- - **Example**: $Q$ is a subfield of $R$ -->

<!-- **Ordered Fields**: Fields that contain a subset $P$ called the positive elements that satisfies -->

<!-- 1. $\alpha, \beta \in P \implies \alpha + \beta, \alpha \beta \in P$ -->
<!-- 2. $\forall \alpha \in F$ only one of the following holds -->

<!--     - $\alpha \in P$ -->
<!--     - $\alpha = 0$ -->
<!--     - $-\alpha \in P$ -->

<!-- - **Example**: both $Q$ and $R$ are ordered fields -->
<!-- - **Example**: $C$ is not an ordered field. It is defined as the set of all pairs of reals $(\alpha, \beta)$ for $\alpha, \beta \in R$ -->

<!--     2 pairs $(\alpha, \beta)$ and $(\alpha', \beta')$ are equal if and only if $\alpha = \alpha'$ and $\beta = \beta'$ -->

<!--     Operations are defined as -->
<!-- \begin{align*} -->
<!-- (\alpha, \beta) + (\alpha', \beta') &= (\alpha + \alpha', \beta + \beta') \\ -->
<!-- (\alpha, \beta) (\alpha', \beta') &= (\alpha \alpha' - \beta \beta', \alpha \beta' + \beta \alpha') -->
<!-- \end{align*} -->

<!--     If we consider all complex numbers of the form $\{\alpha, 0) \mid \alpha \in R\}$ then -->
<!-- \begin{align*} -->
<!-- (\alpha, 0) + (\beta, 0) &= (\alpha + \beta, 0) \\ -->
<!-- (\alpha, 0) (\beta, 0) &= (\alpha \beta, 0) -->
<!-- \end{align*} -->

<!--     This forms a subfield $R'$ of $C$ and a rule that maps $\alpha \in R \longleftrightarrow (\alpha, 0) \in R' \subset C$. This an **isomorphism** that satisfies -->

<!--     1. $(\alpha, 0) = (\alpha', 0)$ if and only if $\alpha = \alpha'$ -->
<!--     2. Preserves operations in the respective number systems -->

<!--     Finally, we can see the following relationship between number systems -->
<!--     $$Z \subset Q \subset R \subset C$$ -->

<!-- # Vector Spaces and Systems of Linear Equations -->

<!-- ## Vector Spaces -->

<!-- **Vector**: tuple of reals $u = (\alpha, \beta, \gamma, \delta)$ that operate under -->
<!-- \begin{align*} -->
<!-- u + u' &= (\alpha + \alpha', \beta + \beta', \gamma + \gamma', \delta + \delta')\\ -->
<!-- \lambda u &= (\lambda \alpha, \lambda \beta, \lambda \gamma, \lambda \delta) -->
<!-- \end{align*} -->
<!-- Two vectors $u = (\alpha, \beta, \gamma, \delta)$ and $u' = (\alpha', \beta', \gamma', \delta')$ are equal if and only if $\alpha = \alpha', \beta = \beta', \gamma = \gamma', \delta = \delta'$ -->

<!-- Vectors satisfy the following properties -->

<!-- 1. $u + u' = u' + u \quad \quad \quad \quad \quad \quad \quad \quad$ (commutative law) -->
<!-- 2. $(u + u') + u'' = u + (u' + u'') \quad \quad$ (associativity law) -->
<!-- 3. $\exists \vec{0}$ such that $u + \vec{0} = u$ for all vectors $u$ -->
<!-- 4. For all vectors $u$, $\exists -u$ such that $u + (-u) = \vec{0}$ -->
<!-- 5. $\alpha(\beta u) = (\alpha \beta)u$ for all vectors $u$ and for all $\alpha, \beta \in R$ -->
<!-- 6. $(\alpha + \beta)u = \alpha u + \beta u$ for all vectors $u$ and for all $\alpha, \beta \in R$ -->
<!-- 7. $\alpha (u + u') = \alpha u + \alpha u'$ for vectors $u$ and $u'$ and for all $\alpha \in R$ -->
<!-- 8. $\bar{1} \cdot u = u$ for all vectors $u$ -->

<!-- **n-tuple**: assigns each positive integer $i \in \{1, \ldots n\}$ a real number $\alpha_i$ -->
<!-- Two n-tuples $\langle \alpha_1, \ldots, \alpha_n\rangle$ and $\langle \beta_1, \ldots, \beta_n\rangle$ are equal if and only if $\forall i, \alpha_i = \beta_i$ -->

<!-- **Vector Space $R_n$**: Consists of n-tuples (called **vectors**) $\langle \alpha_1, \ldots, \alpha_n\rangle$ with $\alpha_i \in R$ (called **components**) that operate under addition and scalar multiplication -->
<!-- \begin{align*} -->
<!-- a + b &= \langle \alpha_1 + \beta_1, \ldots, \alpha_n + \beta_n \rangle \\ -->
<!-- \lambda a &= \langle \lambda \alpha_1, \ldots, \lambda \alpha_n \rangle -->
<!-- \end{align*} -->
<!-- Two vectors $\langle \alpha_1, \ldots, \alpha_n\rangle$ and $\langle \beta_1, \ldots, \beta_n\rangle$ are equal if and only if $\forall i, \alpha_i = \beta_i$ -->

<!-- **Vector Space $F_n$**: Set of n-tuples $a = \langle \alpha_1, \ldots, \alpha_n\rangle$ where each $\alpha_i \in F$ with operations identical to that of $R_n$ -->

<!-- **Vector Space of Functions on the Real Line**: Let $\mathscr{F}(R)$ be the set of all real-valued functions defined on $R$. Then $\mathscr{F}(R)$ becomes a vector space defined over -->
<!-- \begin{align*} -->
<!-- (f + g)(x) &= f(x) + g(x), \quad \quad \quad x\in R, \quad f, g \in \mathscr{F}(R) \\ -->
<!-- (\alpha f)(x) &= \alpha f(x), \quad \quad \quad \quad \quad \quad \, \, x, \alpha \in R, \quad f \in \mathscr{F}(R) -->
<!-- \end{align*} -->
<!-- **Theorem 3.5**: Let $V$ be a vector space over a field $F$. Then the following hold -->

<!-- 1. $u + v = u + w \implies v = w$ for all $u, v, w \in V$ -->
<!-- 2. $u + x = v$ has a unique solution $v- u = v + (-u)$ -->
<!-- 3. $-(-u) = u$ for all $u \in V$ -->
<!-- 4. $\bar{0} \cdot u = 0$ for all $u \in V$ -->
<!-- 5. $-(\alpha u) = (-\alpha)u = \alpha(-u)$ for all $\alpha \in F$ and $u \in V$ -->
<!-- 6. $(- \alpha)(-u) = \alpha u$ for all $\alpha \in F$ and $u \in V$ -->
<!-- 7. For $\alpha \neq 0, \alpha u = \alpha v$, $\implies u = v$ for all $u, v \in V$ -->

<!-- Finally, from commutative and associativity, we see that -->
<!-- \begin{align*} -->
<!-- \sum_{i = 1}^n a_i + \sum_{i = 1}^n b_i &= \sum_{i = 1}^n (a_i + b_i) \\ -->
<!-- (\sum_{i = 1}^n \lambda_i ) a &= \sum_{i = 1}^n \lambda_i a \\ -->
<!-- \lambda (\sum_{i = 1}^n a_i) &= \sum_{i = 1}^n \lambda a_i \\ -->
<!-- (\sum_{i = 1}^n \lambda_i a_i) + (\sum_{i = 1}^n \mu_i a_i) &=  \sum_{i = 1}^n (\lambda_i + \mu_i)a_i -->
<!-- \end{align*} -->

<!-- ## Subspaces and Linear Dependence -->

<!-- **Subspace** $S$ of a vector space $V$ is a nonempty set of vectors in $V$ such that -->

<!-- 1. $a, b \in S \implies a + b \in S$ -->
<!-- 2. $a \in S, \lambda \in F \implies \lambda a \in S$ -->

<!-- - **Example**: -->
<!-- \begin{align*} -->
<!-- x + 2y - 3z + t &= 0\\ -->
<!-- x - y + z + t &= 0 -->
<!-- \end{align*} -->

<!-- &nbsp; &nbsp; &nbsp; &nbsp; Suppose $u, u'$ are solutions to the system above. Then so are $u + u'$ and $\lambda u$ -->

<!-- &nbsp; &nbsp; &nbsp; &nbsp; Thus the solutions to the system of homogenous equations above form a subspace of $R_4$ -->

<!-- - **Example**: The following are subspaces of $\mathscr{F}(R)$ -->

<!--     - $C(R)$ set of continuous real functions -->
<!--     - $D(R)$ set of differential real valued functions -->
<!--     - $P(R)$ set of polynomial functions of the form $\alpha_0 + \alpha_1 + x + \cdots + \alpha_n x^n$ with $x , \alpha_i \in R$ -->

<!-- **Linear Combination**: Let $\{a_1, \ldots, a_m\}$ be a set of vectors in $V$. Then $a \in V$ is a linear combination of $\{a_1, \ldots, a_m\}$ if there exists $\lambda_1, \ldots, \lambda_m \in F$ such that -->
<!-- $$a = \lambda_1 a_1 + \cdots + \lambda_m a_m$$ -->

<!-- **Proposition 4.4**: if $S$ is a subspace of $V$ containing vectors $a_1, \ldots, a_m$, then every linear combination of $a_1, \ldots, a_m$ belongs to $S$ -->

<!-- &nbsp; *Proof by Induction*: -->

<!-- &nbsp; Base case: clearly the statement holds for $m = 1$ by the definition of a subspace -->

<!-- &nbsp; IH: Suppose any linear combination of $m-1$ vectors in $S$ belongs to $S$ -->

<!-- &nbsp; IS: Consider $a = \lambda_1 a_1 + \cdots + \lambda_m a_m$ where each $a_i \in S$ -->

<!-- &nbsp; &nbsp; If we let $a' = \lambda_2 a_2 + \cdots + \lambda_m a_m$, then we have $a = \lambda_1 a_1 + a' \in S$ by IH and definition of subspace -->

<!-- **Proposition 4.5**: Let $\{a_1, \ldots, a_m\}$ be a set of vectors in $V$ for $m \geq 1$. Then the set of linear combinations of vectors $a_1 , \ldots, a_m$ form a subspace $S = S(a_1, \ldots, a_m)$. Furthermore, $S$ is the smallest subspace containing $\{a_1, \ldots, a_m\}$ -->

<!-- &nbsp; *Proof*: Let $a = \sum_{i = 1}^m \lambda_i a_i$, $b = \sum_{i = 1}^m \mu_i a_i$, and $\lambda \in F$. Then -->
<!-- \begin{align*} -->
<!-- a +b &= \sum_{i = 1}^m (\lambda_i + \mu_i) a_i \in S \\ -->
<!-- \lambda a &= \sum_{i = 1}^m (\lambda \lambda_i)a_i \in S -->
<!-- \end{align*} -->

<!-- &nbsp; Thus we have shown that $S$ is a subspace -->

<!-- &nbsp; The fact that $S$ is the smallest subspace comes from the previous proposition -->

<!-- **Generator**: The subspace $S = S(a_1, \ldots, a_m)$ is the subspace **generated by** $a_1, \ldots, a_m$, called the **generators** of $S$ -->


<!-- - Subspace $S$ is **finitely generated** if there exists vectors $s_1, \ldots, s_k \in S$ such that $S = S(s_1, \ldots, s_k)$ -->


<!-- To find a description of the solutions to a system of equations, we need to -->

<!-- 1. Show $S$ is finitely generated -->
<!-- 2. Find a set of generators of $S$ -->

<!-- Suppose $S$ is finitely generated subspace of a vector space $V$ over $F$ generated by $\{a_1, \ldots, a_m\}$. This set of linear combinations will be useful if none of the $a_i$ are **superfluous** (no $a_i$ can be expressed as a linear combination of the remaining vectors) -->

<!-- Otherwise if $a_i$ is a linear combination of $a_1, \ldots, a_{i-1}, a_{i+1}, \ldots, a_m$, there exists $\lambda_1, \ldots, \lambda_{i-1}, \lambda_{i+1}, \lambda_m \in F$ such that -->
<!-- \begin{align*} -->
<!-- a_1 &= \lambda_1 a_1 + \cdots + \lambda_{i-1} a_{i-1} + \lambda_{i+1} a_{i+1} + \cdots + \lambda_m a_m \\ -->
<!-- 0 &= \lambda_1 a_1 + \cdots + \lambda_{i-1} a_{i-1} + (-1)a_i + \lambda_{i+1} a_{i+1} + \cdots + \lambda_m a_m -->
<!-- \end{align*} -->

<!-- Thus there exists elements $\mu_1, \ldots, \mu_m \in F$, not all equal to zero, such that -->
<!-- $$\mu_1 a_1 + \ldots + \mu_m a_m = 0$$ -->

<!-- Conversely, suppose $\sum_{i=1}^m \mu_i a_i = 0$ where not all $\mu_i$ are equal to zero. Then we show some $a_j$ is a linear combination of the remaining vectors -->

<!-- Suppose $\mu_j \neq 0$, then since $-\mu_j^{-1} \in F$ -->
<!-- \begin{align*} -->
<!-- -\mu_j a_j &= \mu_1 a_1 + \cdots + \mu_{j-1} a_{j-1} + \mu_{j+1} a_{j+1} + \cdots + \mu_m a_m \\ -->
<!-- a_j &= -\mu_j^{-1}a_1 + \cdots + -\mu_j^{-1} \mu_{j-1} a_{j-1} + -\mu_{j}^{-1} \mu_{j+1} a_{j+1} + \cdots + -\mu_{j} \mu_{m} a_{m} -->
<!-- \end{align*} -->

<!-- **Theorem 4.9**: Let $\{a_1, \ldots, a_m\}$ be a set of vectors in $V$. Some vector $a_i$ can be expressed as a linear combination of the other vectors if and only if $\exists \lambda_1, \ldots, \lambda_m \in F$, not all equal to zero, such that -->
<!-- $$\lambda a_1 + \cdots + \lambda_m a_m = 0$$ -->

<!-- &nbsp; *Proof*: follows from the discussion above -->

<!-- **Linearly Dependent**: Let $\{a_1, \ldots, a_m\}$ be an arbitrary finite set of vectors in $V$. This set is **linearly dependent** if there exists $\lambda _1, \ldots, \lambda_m \in F$, not all zero, such that $\sum_{i = 1}^m \lambda_i a_i = 0$. -->

<!-- Otherwise the set is **linearly independent** if and only if $\sum_{i = 1}^n \lambda_i a_i = 0 \implies \lambda_i = 0$ -->

<!-- - **Example**: $\{0\}$ is linearly dependent and $\{a\}, a \neq 0$, is linearly independent -->

<!-- **Proposition 4.11**: $\{a, b\}$ is linearly dependent if and only if $a = \lambda b$ or $b = \lambda' a$ for some $\lambda, \lambda' \in F$ -->

<!-- &nbsp; *Proof*: $\implies$ Let $a = \lambda b$. Then $a + [-(\lambda b)] = 0 \implies 1\cdot a + (-\lambda)b = 0$ -->

<!-- &nbsp; $1 \neq 0 \implies -\lambda \neq 0 \implies \{a, b\}$ are linearly dependent -->

<!-- &nbsp; Similar proof shows that $b = \lambda' a \implies \{a, b\}$ are linearly dependent -->

<!-- &nbsp; $\impliedby$ suppose $\alpha a + \beta b = 0$ where either $\alpha$ or $\beta \neq 0$ -->

<!-- &nbsp; If $\alpha \neq 0$ then $\alpha a = (-\beta)b \implies a = (-\alpha^{-1} \beta)b$ as desired -->

<!-- &nbsp; Otherwise let $\alpha = 0$ and $\beta \neq 0$. Then we must have $b = 0 \implies b = \lambda' a \implies \lambda' = 0$ as desired -->

<!-- - **Example**: Take $a = \langle 1, -1 \rangle$ in $R_2$. Then $\{a, b\}$ -->

<!--     - is linearly independent if $b = \langle 1, 1 \rangle$ or $b = \langle 1, 0\rangle$ -->
<!--     - is linearly dependent if $b = \langle -2, 2 \rangle$ or $b = \langle 0, 0 \rangle$ -->

<!-- - **Example**: Consider $a = \langle 1, -1 \rangle, b = \langle 1, 1 \rangle, c = \langle 2, 1 \rangle$ -->

<!--     Is $\{a, b, c\}$ linearly dependent? Consider the equation $\alpha a + \beta b + \gamma c = 0 = \langle \alpha + \beta + 2\gamma, -\alpha + \beta + \gamma \rangle$ -->

<!--     Then we need -->
<!-- \begin{align*} -->
<!-- \alpha + \beta + 2\gamma &= 0 \\ -->
<!-- -\alpha + \beta + \gamma &= 0 -->
<!-- \end{align*} -->
<!-- Clearly we can solve for these variables by holding one constant (e.g. $\gamma = 1$). Thus these vectors are linearly dependent -->

<!-- - **Example**: Describe the set of all solutions to $x_1 + 2x_2 - x_3 = 0$ -->

<!--     Solution is a vector $\langle \alpha_1, \alpha_2, \alpha_3 \rangle \in R_3$ and the set of all solution is a subspace $S$ of $R_3$ -->

<!--     Let $x_3 = 0 \implies u_1 = \langle 1, -1/2, 0\rangle \in S$ -->

<!--     Let $x_1 = 0 \implies u_2 = \langle 0, 1, 2 \rangle \in S$ -->

<!--     We show that $S = S(u_1, u_2)$. Suppose $u = \langle \alpha, \beta, \gamma \rangle$ is another solution -->

<!--     - If $\alpha = \beta = \gamma = 0$, then clearly $u \in S$ -->

<!--     - Otherwise $\alpha \neq 0 \implies u - \alpha u_1 = \langle 0, \beta + \alpha / 2, \gamma \rangle = \langle 0, \gamma /2, \gamma \rangle = \frac{\gamma}{2} u_2 \in S$, since we said $\alpha + 2\beta - \gamma = 0$ is a solution -->

<!--     - Otherwise $\alpha = 0$ and $\beta \neq 0 \implies 2\beta - \gamma = 0$ and then we have $u = \langle 0, \beta, \gamma \rangle = \beta u_2 \in S$ -->

<!--     Thus $u_1, u_2$ generate $S$. Clearly $u_1, u_2$ are linearly independent so by Theorem 4.4, $S = S(u_1, u_2)$ and neither $u_1, u_2$ can be omitted from the solution -->

<!--     Thus any solution $u$ to $x_1 + 2x_2 - x_3 = 0$ has the form $u = \lambda_1 u_1 + \lambda_2 u_2$ where -->

<!--     - $u_1 = \langle 1, -1/2, 0 \rangle$ -->

<!--     - $u_2 = \langle 0, 1, 2 \rangle$ -->

<!-- # Basis and Dimension -->

<!-- Using the previous example, we show that no single vector $u$ generates $S$. Suppose by contradiction that $S$ were generated by $u$ -->

<!-- Since $u_1 \neq 0, u_2 \neq 0$, we have $u_1 = \alpha u$ and $u_2 = \beta u$ for $\alpha \neq 0$ and $\beta \neq 0$ -->

<!-- Thus we have $\beta u_1 - \alpha u_2 = 0$, showing that $u_1, u_2$ are linearly dependent. But this is a contradiction since we showed that they are linearly independent. Thus no single vector $u$ generates $S$ -->

<!-- **Theorem 5.1**: Let $S$ be a subspace of a vector space $V$ over a field $F$ such that $S$ is generated by $\{a_1, \ldots, a_n \}$. Suppose $\{b_1, \ldots, b_m\}$ are vectors in $S$ with $m > n$. Then $\{b_1, \ldots, b_m\}$ are linearly dependent -->

<!-- &nbsp; *Proof by Induction*: Base case: for $n = 1 \implies S= S(a)$, so we must have $b_1 = \lambda_1 a, \ldots, b_m = \lambda_m a$ for $\lambda_i \in F$ -->

<!-- &nbsp; At least one of the $\lambda_i$ is non zero. Otherwise we'd have $b_1 = b_2 = \cdots = b_m  = 0 \implies b_1 - b_2 = 0$ is a linear dependence -->

<!-- &nbsp; Now assume $\lambda_j \neq 0 \implies \lambda_j b_1 + 0 \cdot b_2 + \cdots + (-\lambda_1)b_j + 0 \cdot b_{j+1} + \cdots + 0 \cdot b_m = \lambda_j \lambda_1 a - \lambda_1 \lambda_j a = 0$ -->

<!-- &nbsp; Since $\lambda_j \neq 0$, we have shown that $\{b_1, \ldots, b_m\}$ are linearly dependent -->

<!-- &nbsp; IH: assume the theorem holds for subspaces generated by $n-1$ vectors -->

<!-- &nbsp; IS: $m$ distinct vectors $\{b_1, \ldots, b_m\}$ contained in $S = S(a_1, \ldots, a_n)$ where $m > n$. Then we have -->
<!-- \begin{align*} -->
<!-- b_1 &= \lambda_{11} a_1 + \cdots + \lambda_{1n} a_n \\ -->
<!-- b_2 &= \lambda_{21} a_1 + \cdots + \lambda_{2n} a_n \\ -->
<!-- & \quad \quad \quad \quad \cdots \\ -->
<!-- b_m &= \lambda_{m1} a_1 + \cdots + \lambda_{mn} a_n \\ -->
<!-- \end{align*} -->
<!-- &nbsp; Some $\lambda_{i1}$ must be nonzero, otherwise the terms involving $a_1$ are missing so $\{b_1, \ldots, b_m\}$ belong to $S(a_2, \ldots, a_m)$ -->

<!-- &nbsp; which by IH shows that $\{b_1, \ldots, b_m\}$ are linearly dependent -->

<!-- &nbsp; Assume some $\lambda_{i1} \neq 0$ and rename $b_i$ to $b_1$. Now we can assume that $\lambda_{11} \neq 0$ -->

<!-- &nbsp; So the coefficient of $a_1$ in $b_2 - \lambda_{21} \lambda_{11}^{-1} b_1$ is $\lambda_{21} - \lambda_{21} \lambda_{11}^{-1} \cdot \lambda_{11} = 0$ -->

<!-- &nbsp; Thus we have that -->
<!-- $$b_2 - \lambda_{21} \lambda_{11}^{-1} b_1 = \lambda_{22}' a_2 + \cdots + \lambda_{2n}' a_n$$ -->

<!-- Similarly, we have -->
<!-- \begin{align*} -->
<!-- b_3 - \lambda_{31} \lambda_{11}^{-1} b_1 &= \lambda_{32}' a_2 + \cdots + \lambda_{3n}' a_n\\ -->
<!-- b_m - \lambda_{m1} \lambda_{11}^{-1} b_1 &= \lambda_{m2}' a_2 + \cdots + \lambda_{mn}' a_n -->
<!-- \end{align*} -->

<!-- &nbsp; Thus the $m-1$ vectors above $\{b_2 - \lambda_{21} \lambda_{11}^{-1}b_1, \ldots, b_m - \lambda_{m1} \lambda_{11}^{-1}b_1\}$ all belong to the subspace $S(a_2, \ldots, a_n)$ with $n-1$ generators -->

<!-- &nbsp; Thus by IH, these vectors are linearly dependent and we have for elements $\mu_2, \ldots, \mu_m \in F$, which are not all zero -->
<!-- $$\mu_2(b_2 - \lambda_{21}\lambda_{11}^{-1}b_1) + \cdots + \mu_m(b_m - \lambda_{m1}\lambda_{11}^{-1}b_1) = 0$$ -->

<!-- &nbsp; Now if we rewrite this expression as a linear combination of $\{b_1, \ldots, b_m\}$ we get -->
<!-- $$((-\lambda_{21}\lambda_{11}^{-1}b_1) + \cdots + (- \lambda_{m1}\lambda_{11}^{-1}))b_1 + \mu_2 b_2 + \cdots + \mu_m b_m = 0$$ -->

<!-- &nbsp; Where one of $\{\mu_2, \ldots, \mu_m\}$ is nonzero. Thus $\{b_1, \ldots, b_m\}$ are linearly dependent in the subspace $S = S(a_1, \ldots, a_n)$ -->

<!-- - **Example**: Suppose $S = S(a_1, a_2)$ and -->
<!-- \begin{align*} -->
<!-- b_1 &= 2a_1 + a_2\\ -->
<!-- b_2 &= -a_1 + a_2\\ -->
<!-- b_3 &= a_1 -->
<!-- \end{align*} -->

<!-- &nbsp; &nbsp; &nbsp; &nbsp; We can subtract multiples of $b_1$ from $b_2$ and $b_3$ to make the coefficient of $a_1 = 0$ to get -->
<!-- \begin{align*} -->
<!-- b_2 + \frac{1}{2}b_1 &= \frac{3}{2}a_2 \\ -->
<!-- b_3 - \frac{1}{2}b_1 &= - \frac{1}{2}a_2 -->
<!-- \end{align*} -->
<!-- &nbsp; &nbsp; &nbsp; &nbsp; Now we have 2 vectors in the space $S(a_2)$ and we have -->
<!-- $$b_2 + \frac{1}{2}b_1 + 3[b_3 - \frac{1}{2}b_1] = 0$$ -->

<!-- &nbsp; &nbsp; &nbsp; &nbsp; Rewriting it as a linaer combination of $b_1, b_2, b_3$, we get -->

<!-- $$-b_1 + b_2 + 3b_3 = 0$$ -->

<!-- &nbsp; &nbsp; &nbsp; &nbsp; Thus $\{b_1, b_2, b_3\}$ are linearly dependent -->

<!-- **Theorem 5.3**: Let $S$ be a subspace of a vector space $V$ and suppose $\{a_1, \ldots, a_m\}$ and $\{b_1, \ldots, b_n\}$ both generate $S$, which are linearly independent. Then $n = m$ -->

<!-- &nbsp; *Proof*: View $\{b_1, \ldots, b_n\}$ as vectors in $S(a_1, \ldots, a_m)$. Since $\{b_1, \ldots, b_n\}$ are linearly independent, we must have $n \leq m$ -->

<!-- &nbsp; Similarly, view $\{a_1, \ldots, a_m\}$ as vectors in $S(b_1, \ldots, b_n)$. Since $\{a_1, \ldots, a_m\}$ are linearly independent, we must have $m \leq n$ -->

<!-- &nbsp; Thus we must have that $n = m$ -->

<!-- **Basis**: a finite set of vectors $\{b_1, \ldots, b_k\}$ are a basis for $V$ if the set is a linearly independent set of generators of $V$ -->

<!-- **Dimension**: Suppose $V$ is a vector space with basis $\{b_1, \ldots, b_k\}$. Then the unique number of basis vectors, $k$, is called the **dimension** of the vector space $V$. Denoted $\dim V = k$ -->

<!-- - **Example**: Let $n$ be a fixed positive integer. We see that -->
<!-- \begin{align*} -->
<!-- e_1 &= \langle 1, 0, \ldots, 0\rangle\\ -->
<!-- e_2 &= \langle 0, 1, 0, \ldots, 0 \rangle\\ -->
<!-- & \quad \quad \ldots \\ -->
<!-- e_n &= \langle 0, 0, \ldots, 0, 1 \rangle -->
<!-- \end{align*} -->
<!-- The vectors $\{e_i\}$ (called the **unit vectors**) form a basis of $R_n$ -->

<!-- &nbsp; &nbsp; &nbsp; &nbsp; Clearly these vectors are linearly independent since $\sum \lambda_i e_i = 0$ if and only if all $\lambda_i = 0$ -->

<!-- &nbsp; &nbsp; &nbsp; &nbsp; Furthermore, any vector $a \in R_n$ can be generated by $\langle \alpha_1, \alpha_2, \ldots, \alpha_n \rangle = \alpha_1 e_1 + \cdots + \alpha_n e_n$ -->

<!-- ## Row Equivalence of Matrices -->

<!-- **Matrix**: Ordered set $\{r_1, \ldots, r_m\}$ of $m$ vectors from $R_n$ is a $m \times n$ **Matrix** where vectors $\{r_1, \ldots, r_m\}$ are called **rows** -->

<!-- - **Example**: $r_1 = \langle -3, 2, 1, 4 \rangle, r_2 = \langle 4, 1, 0, 2\rangle, r_3 = \langle -10, 3, 2, 6 \rangle$ is represented by -->
<!-- $$A = \begin{bmatrix} -3 & 2 & 1 & 4 \\ 4 & 1 & 0 & 2\\ -10 & 3 & 2 & 6 \end{bmatrix}$$ -->

<!-- We can use **elementary row operations** to obtain matrices $A = A_1, A-2 \ldots, A_s = A'$. These operations preserve the subspace corresponding to the rows unchanged. Thus $S(a', b', c') = S(a, b, c)$ -->

<!-- Thus to find a basis for $S(a, b, c)$ we apply row operations to the original matrix $A$ until we find vectors $\{a', b', c'\}$ where it is easy to test for linear independence -->

<!-- One way to do this is using **Gaussian elimination**. Using the example matrix above, we get -->
<!-- $$A = \begin{bmatrix} -3 & 2 & 1 & 4 \\ 4 & 1 & 0 & 2\\ -10 & 3 & 2 & 6 \end{bmatrix} \sim \begin{bmatrix} -3 & 2 & 1 & 4 \\ 0 & 11/3 & 4/3 & 22/3 \\ 0 & 0 & 0 & 0\end{bmatrix}$$ -->

<!-- Thus we can conclude that $S(a,b,c) = S(a', b')$ where -->
<!-- \begin{align*} -->
<!-- a' &= -3e_1 &+ 2e_2 &+ e_3 &+ 4e_4\\ -->
<!-- b' &= & \frac{11}{3}e_2 & \frac{4}{3}e_3 &+ \frac{22}{3}e_4 -->
<!-- \end{align*} -->

<!-- To show that $a', b'$ are linear independent, suppose that $\lambda a' + \mu b' = 0$ then $-3 \lambda e_1 + (\ldots)e_1 + (\ldots)e_3 + (\ldots)e_4 = 0 \implies \lambda = 0$ since $\{e_1, \ldots, e_4\}$ are linearly independent -->

<!-- Thus we then have $\mu b' = 0 \implies \mu = 0$ since $b' \neq 0$ -->

<!-- **Row Equivalent**: an $m \times n$ matrix $A$ is **row equivalent** to another $m \times n$ matrix $A'$ (denoted $A \sim A'$) if there exist $m \times n$ matrices $A_0, A_1, \ldots A_s$ such that -->
<!-- $$A_0 = A, \quad \quad \quad A_s = A'$$ -->

<!-- Where each $A_i$, for $1 \leq i \leq s$ is obtained by applying an elementary row operation to $A_{i-1}$ -->

<!-- **NOTE**: row equivalence creates an equivalence relationship -->

<!-- - $A \sim A$ -->
<!-- - $A \sim A' \implies A' \sim A$ -->
<!-- - $A \sim A'$ and $A' \sim A''\implies A \sim A''$ -->

<!-- **Theorem 6.11**: Let $V$ be a vector space with a finite bases $\{a_1, \ldots, a_n\}$. Let $\{b_1, \ldots, b_m\}$ be vectors in $V$ where -->

<!-- \begin{align*} -->
<!-- b_1 = \lambda_{11}a_1 + \cdots + \lambda_{1n}a_n \\ -->
<!-- \cdots \\ -->
<!-- b_m = \lambda_{m1}a_1 + \cdots + \lambda_{mn}a_n -->
<!-- \end{align*} -->

<!-- Furthermore, let -->
<!-- $$A' = \begin{bmatrix} \lambda_{11}' & \cdots & \lambda_{1n}' \\ \cdots & \cdots & \cdots \\ \lambda_{m1}' & \cdots & \lambda_{mn}' \end{bmatrix}$$ -->

<!-- By the $m \times n$ matrix which is row equivalent to the coefficient matrix. Then $S(b_1, \ldots, b_m) = S(b'_1, \ldots b'_m)$ -->

<!-- Where -->
<!-- \begin{align*} -->
<!-- b_1' = \lambda_{11}'a_1 + \cdots + \lambda_{1n}'a_n \\ -->
<!-- \cdots \\ -->
<!-- b_m' = \lambda_{m1}'a_1 + \cdots + \lambda_{mn}'a_n -->
<!-- \end{align*} -->

<!-- &nbsp; *Proof*: Sufficient to prove that $A'$ can be obtained by $A$ through elementary row operations -->

<!-- **Echelon Form**: A collection of vectors $\{b_1, \ldots, b_p\}$ is in **echelon form** if each $b_i \neq 0$ and the position of the first non-zero entry of $b_i$ is to the left of the first non-zero entry of $b_{i+1}$ -->

<!-- **Lemma 6.14**: Let $A$ be a coefficient matrix of vectors $\{b_1, \ldots, b_m\}$ on basis $\{a_1, \ldots, a_n\}$. Furthermore, suppose that rows $r_1, \ldots r_m$ are in echelon form, then $\{b_1, \ldots, b_m\}$ are linearly independent -->

<!-- &nbsp; *Proof by Induction*: Clearly for $m = 1$, by the definition of echelon form, $b_1 \neq 0 \implies \{b_i\}$ is linearly independent -->

<!-- &nbsp; IH: assume the lemma holds for $m-1$ rows -->

<!-- &nbsp; IS: suppose $\beta_1 b_1 + \cdots + \beta_m b_m = 0$. We show that $\beta_1 = 0$ -->

<!-- &nbsp; Let $\lambda_{1i}$ be the first non-zero entry of row $r_1$. Then by definition of echelon form, when $r_1$ is expressed in terms of the -->

<!-- &nbsp; basis vectors $\{a_1, \ldots, a_n\}$, the coefficient of $a_1$ is $\lambda_{1i} \beta_1$. We need $\lambda_{1i} \beta_1 = 0$ but since $\lambda_{1i} \neq 0$, we must have $\beta_1 = 0$ -->

<!-- &nbsp; Now considering the vectors $\{b_2, \ldots, b_n\}$, these are in echelon form so by IH, these are linearly independent so $\beta_2 = \cdots = \beta_m = 0$ -->

<!-- &nbsp; Thus we $\beta_1 = \beta_2 = \cdots = \beta_m = 0$ and the Lemma holds -->

<!-- **Theorem 6.16**: Let $A$ be a coefficient matrix expressing the set of vectors $\{b_1, \ldots, b_m\}$ as a linear combinination of a given set of basis vectors. Then the following statements hold -->

<!-- 1. $\exists A' \sim A$ such that either $A' = 0$ or there is a unique integer $k$, with $1 \leq k \leq m$, such that the first $k$ rows of $A'$ are in echelon form, the remaining rows are all zero -->

<!-- 2. Vectors $\{b_1', \ldots, b_k'\}$ corresponding to the first $k$ rows of $A'$ form a basis for $S(b_1, \ldots, b_k)$ -->

<!-- 3. The original vectors $\{b_1, \ldots, b_m\}$ are linearly independent if and only if $m = k$ -->

<!-- &nbsp; *Proof*: First show that $A' \sim A$ such that the first $k$ rows are in row echelon form by induction on the number of rows -->

<!-- &nbsp; &nbsp; Base case: when the number of rows is $1$, clearly $A'$ is already in echelon form -->

<!-- &nbsp; &nbsp; IH: Suppose that the statement holds for an matrix $A$ with $m- 1$ rows -->

<!-- &nbsp; &nbsp; IS: By interchanging 2 rows, we may assume that the first row $r_1$ of $A$ is different from zero -->

<!-- &nbsp; &nbsp; Consider the nonzero entry as far to the left as possible in $r_1$ -->

<!-- &nbsp; &nbsp; By adding multiples of the first row to the remaining rows, we obtain a matrix equivalent to -->
<!-- $$A_1 = \begin{bmatrix} 0 & \cdots & 0 & \lambda_{1i} & \cdots \\ 0 & \cdots & 0 & 0 & \cdots \\ \cdots & \cdots & \cdots & \cdots & \cdots\\ 0 & \cdots & 0 & 0 & \cdots\end{bmatrix}$$ -->

<!-- &nbsp; &nbsp; By IH, we can apply elementary row operations to the last $m-1$ rows of $A_1$ to obtain $A'$ -->

<!-- &nbsp; &nbsp; where $\{r'_2, \ldots, r_k'\}$ are in echelon form and the remaining rows are zero -->

<!-- &nbsp; Thus by definition of echelon form, all nonzero rows of $A'$ are in echelon form -->

<!-- &nbsp; Let $\{b_1', \ldots b_k'\}$ be the vector corresponding to the first $k$ rows of $A'$. By Theorem 6.11, $S(b_1, \ldots, b_m) = S(b_1', \ldots, b_k')$ -->

<!-- &nbsp; &nbsp; and by Lemma 6.14, $\{b_1', \ldots, b_k'\}$ are linearly independent and are the basis for $S(b_1, \ldots, b_m)$ -->

<!-- &nbsp; Vectors $\{b_1, \ldots, b_n\}$ are linearly independent if and only if $m$ is the number of basis vectors of $S(b_1, \ldots, b_m)$. -->

<!-- &nbsp; &nbsp; Clearly this only happens when $m = k$ -->

<!-- - **Example**: Find the basis for subspace $R_3$ generated by $\langle 1, 3, 4 \rangle, \langle 4, 0, 1 \rangle, \langle 3, 1, 2 \rangle$ -->

<!--     We can create the coefficient matrix -->
<!--     $$A = \begin{bmatrix}1 & 3 & 4 \\ 4 & 0 & 1 \\ 3 & 1 & 2\end{bmatrix} \sim A' = \begin{bmatrix}1 & 3 & 4 \\ 0 & 1 & 5/4 \\ 0 & 0 & 0 \end{bmatrix}$$ -->

<!--     Thus the basis for $S(b_1, b_2, b_3)$ is -->
<!-- \begin{align*} -->
<!-- b'_1 &= e_1 + 3 e_2 + 4 e_3\\ -->
<!-- b'2 &= 0e_1 + e_2 + \frac{5}{4} e_3 -->
<!-- \end{align*} -->
<!-- And thus the original vectors are linearly dependent -->


