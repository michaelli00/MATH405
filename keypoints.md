---
geometry: "left=1cm,right=1cm,top=1cm,bottom=1cm"
header-includes:
    - \pagenumbering{gobble}
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
output: pdf_document
---

**Subspace**: $W \subseteq V$ that is  $K$-vector space itself satisfying

- $w_1, w_2, \in W \implies w_1 + w_2 \in W$ $\quad \quad \forall c \in K, w \in W \implies cw \in W \quad \quad O \in W$

**Span**: $\Span(\{v_1, \ldots, v_n\})$ is a subspace of $V$ consisting of all linear combinations of $\{v_1, \ldots v_n\}$

- If $W = \Span(\{v_1, \ldots, v_n\})$, then every $w \in W$ is a linear combination of $\{v_1, \ldots, v_n\}$

**Linear Independent**: occurs when $a_1 v_1 + \cdots + a_n v_n = 0 \implies a_1 = \cdots = a_n = 0$

- $\{v_1, \ldots, v_n\}$ is linearly independent if and only if for each $i, v_i \notin \Span(\{v_1, \ldots, v_n\} \setminus \{v_i\})$

**Basis**: $\{v_1, \ldots, v_n\}$ that spans $W$ and is linearly independent. **Note**: The empty set $\emptyset$ is a basis for $\{O\}$

**Shrinking Lemma**: Let $X = \{w_1, \ldots, w_m\} \subseteq W$ span $W$ but not be LI. Then $X \setminus \{w_i\}$ still spans $W$ for some $w_i \in X$

- **Shrinking Theorem**: Some $Y \subseteq X$ is a basis of $W$ (must stop eventually when we get $\emptyset$ basis for $\{O\}$)

**Enlarging Lemma**: let $X = \{w_1, \ldots, w_m\} \subseteq W$ be LI but not span $W$. Then for any $w \in W \setminus \Span(X), X \cup \{w\}$ is still LI

**Exchanging Lemma**: Let $X = \{v_1, \ldots, v_n\}$ be a basis for $W$. Take $w \in W$ where $w \in \Span(\{v_1, \ldots, v_n\})$. Then for $i < k$, $Y = (X \setminus \{v_i\}) \cup \{w\}$ is still a basis

- Can be used to show that if $\{w_1, \ldots, w_m\} \subseteq W$ is linearly independent, then $m \leq n$. Thus any basis of $W$ has $n$ elements

**Finite Dimensional**: $W$ with some basis. **Dimension** of $W$ is the number of elements in the basis

- Any set of vectors that spans $W$, with the correct dimension, is a basis by the Shrinking Theorem
- Any set of vectors that is linearly independent, with the correct dimension, is a basis by the Enlarging Lemma

**Direct Sum**: $U \oplus W$ such that $U \oplus W = U + W$ AND $U \cap W = \{O\}$

- **Note**: $U \cap W$ and $U + W$ are subspaces of $V$
- **Theorem**: For subpsace $W \subseteq V$, there exists a subspace $U \subseteq V$ such that $V = U \oplus W$.

**Mat$\mathbf{_{m \times n}(K)}$**: $K$-Vector Space of all $m \times n$ matrices with entries in $K$

- Basis here is $\bigcup E_{ij}$ where $E_{ij}$ has the the $ij$ entry is $1$ and all other entries as $0$, which clearly has dimension $m \times n$

**Symmetric $\mathbf{2 \times 2}$ Matrices** come in the form of $\begin{bmatrix} a & b \\ b & c\end{bmatrix}$ and is a subspace of $\mat_{2 \times 2}(K)$

**Image**: $F(D) = \{F(x) \mid x \in D\} \subseteq R$ for the mapping $F: D \rightarrow R$

- **Onto** if $F(D) = R \quad \quad$ **1-1** if $F(d) = F(e) \implies d= e \quad \quad$ **Bijection** if both onto and 1-1

**Inverse Mapping**: If $F: D \rightarrow D$ is a bijection, then $\exists F^{-1}:R \rightarrow D$ such that $\forall r, \in R, F(F^{-1}(r)) = r$ and $\forall d \in D, F^{-1}(F(d)) = d$

**Linear Transformation**: Function $T: V \rightarrow W$ for vector spaces $V, W$, satisfying

- $\forall v_1, v_2 \in W, T(v_1 + v_2) = T(v_1) + T(v_w) \quad \quad \forall c \in K, v \in W, T(cv) = cT(v)$

**Pull Back**: Any set $\{v_1, \ldots, v_m\} \subseteq V$ such that $T(v_1) = w_1, \ldots, T(v_m) = w_m$

- If $\{w_1, \ldots, w_m\} \subseteq \Img(T)$ is a basis, then $\{v_1, \ldots, v_m\} \subseteq V$ is a basis for $\Span(\{v_1, \ldots, v_m\})$. Thus $\dim(\Img(T)) \leq \dim(V)$

**Kernel**: $\Ker(T) = \{v \in V \mid T(v) = O_W\}$, which can be shown to be a subspace of $V$

- **Proposition** $V = \Ker(T) \oplus \Span(\{v_1, \ldots, v_m\})$ for any pullback $\{v_1, \ldots, v_m\} \subseteq V$

- **Theorem**: $\dim(V) = \dim(\Ker(T)) + \dim(\Img(T))$. Comes from $V = \Ker(T) \oplus S \implies \dim(V) = \dim(\Ker(T)) + \dim(S)$

**UPSHOT**: $\dim(\Ker(T)) > 0 \implies$ $T$ is NOT 1-1 $\quad \quad \dim(\Img(T)) < \dim(W) \implies T$ is NOT onto

**Isomorphism**: $T: V \rightarrow W$ such that $T$ is a linear transformation and a bijection

- If $\dim(V) = \dim(W)$ and $T: V \rightarrow W$ is a linear transformation and is 1-1 $\implies$ onto OR is onto $\implies$ is 1-1

**Inverse Mapping/Transformation**: An isomorphism $T^{-1}: W \rightarrow V$ where $T^{-1}(w)$ is the unique $v \in V$ such that $T(v) = w$

**Linear Map/Matrix**: Matrix $L_A$ that determines the LT $R^n \rightarrow R^m$, and is itself a LT (from logic of dot products)

- Transformation $T: V \rightarrow W$ WRT to bases $B = \{v_1, \ldots, v_m\} \subseteq V$ and $B' = \{w_1, \ldots, w_m\} \subseteq W$ is given by

    $M_{B'}^B = \begin{bmatrix} T(v_1) & T(v_2) & \cdots & T(v_n)\end{bmatrix}$ where the result is written in terms of coordinates of $B'$

    **Upshot**: Any vector, written in $B$ coordinates, when multiplied by this matrix, yields an answer in $B'$ coordinates

**Change of Basis**: $M_{B'}^B(\id) = \begin{bmatrix} \id(v_1) & \id(v_2) & \cdots \id(v_n)\end{bmatrix}$ with respect to bases $B, B'$ of the same vector space $V$
