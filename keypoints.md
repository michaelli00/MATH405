---
geometry: "left=1cm,right=1cm,top=1cm,bottom=1cm"
header-includes:
    - \pagenumbering{gobble}
    - \usepackage{amsmath}
    - \usepackage{mathrsfs}
    - \DeclareMathOperator{\lcm}{lcm}
    - \DeclareMathOperator{\Span}{span}
    - \DeclareMathOperator{\mat}{Mat}
    - \DeclareMathOperator{\range}{range}
    - \DeclareMathOperator{\Img}{Im}
    - \DeclareMathOperator{\Ker}{Ker}
    - \DeclareMathOperator{\matvect}{Mat$_{x \times n}(K)$}
    - \DeclareMathOperator{\id}{id}
    - \DeclareMathOperator{\proj}{proj}
    - \DeclareMathOperator{\Null}{Null}
    - \DeclareMathOperator{\Ann}{Ann}
    - \DeclareMathOperator{\Tr}{Tr}
    - \DeclareMathOperator{\ML}{ML}
    - \DeclareMathOperator{\rank}{rank}
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

**Inverse Mapping**: If $F: D \rightarrow R$ is a bijection, then $\exists F^{-1}:R \rightarrow D$ such that $\forall r, \in R, F(F^{-1}(r)) = r$ and $\forall d \in D, F^{-1}(F(d)) = d$

**Linear Transformation**: Function $T: V \rightarrow W$ for vector spaces $V, W$, satisfying

- $\forall v_1, v_2 \in W, T(v_1 + v_2) = T(v_1) + T(v_w) \quad \quad \forall c \in K, v \in W, T(cv) = cT(v)$

**Pull Back**: Any set $\{v_1, \ldots, v_m\} \subseteq V$ such that $T(v_1) = w_1, \ldots, T(v_m) = w_m$

- If $\{w_1, \ldots, w_m\} \subseteq \Img(T)$ is a basis, then $\{v_1, \ldots, v_m\} \subseteq V$ is a basis for $\Span(\{v_1, \ldots, v_m\})$. Thus $\dim(\Img(T)) \leq \dim(V)$

**Kernel**: $\Ker(T) = \{v \in V \mid T(v) = O_W\}$, which can be shown to be a subspace of $V$

- **Proposition** $V = \Ker(T) \oplus \Span(\{v_1, \ldots, v_m\})$ for any pullback $\{v_1, \ldots, v_m\} \subseteq V$

- **Theorem**: $\dim(V) = \dim(\Ker(T)) + \dim(\Img(T))$. Comes from $V = \Ker(T) \oplus S \implies \dim(V) = \dim(\Ker(T)) + \dim(S)$

**Upshot**: $\dim(\Ker(T)) > 0 \implies$ $T$ is NOT 1-1 $\quad \quad \dim(\Img(T)) < \dim(W) \implies T$ is NOT onto

**Isomorphism**: $T: V \rightarrow W$ such that $T$ is a linear transformation and a bijection

- If $\dim(V) = \dim(W)$ and $T: V \rightarrow W$ is a linear transformation and is 1-1 $\implies$ onto OR is onto $\implies$ is 1-1

**Inverse Mapping/Transformation**: An isomorphism $T^{-1}: W \rightarrow V$ where $T^{-1}(w)$ is the unique $v \in V$ such that $T(v) = w$

**Linear Map/Matrix**: Matrix $L_A$ that determines the LT $R^n \rightarrow R^m$, and is itself a LT (from logic of dot products)

- Transformation $T: V \rightarrow W$ WRT to bases $B = \{v_1, \ldots, v_m\} \subseteq V$ and $B' = \{w_1, \ldots, w_m\} \subseteq W$ is given by

    $M_{B'}^B = \begin{bmatrix} T(v_1) & T(v_2) & \cdots & T(v_n)\end{bmatrix}$ where $v_1$ is WRT to $B$ and the result is written in terms of coordinates of $B'$

    **Upshot**: Any vector, written in $B$ coordinates, when multiplied by this matrix, yields an answer in $B'$ coordinates

**Change of Basis**: $M_{B'}^B(\id) = \begin{bmatrix} \id(v_1) & \id(v_2) & \cdots \id(v_n)\end{bmatrix}$ with respect to bases $B, B'$ of the same vector space $V$

\newpage

**Scalar Product**: $V \times V \rightarrow K$ satisfying $\langle v, w \rangle = \langle w, v \rangle \quad \quad \langle v, c(w_1 + w_2) \rangle = c\langle v, w_1 \rangle + c \langle v, w_2 \rangle$

- **Positive Definite**: For $v \neq O, \langle v, v \rangle > 0$
- **Non-Degenerate**: For $v \neq O, \exists w \in W, \langle v, w \rangle \neq 0$
- **Non-Trivial**: $\exists v, w \in V$ such that $\langle v, w \rangle \neq 0$
- **Trivial**: $\forall v, w \in V, \langle v, w \rangle = 0$

**Orthogonal**: $v \perp w \implies \langle v, w \rangle = 0 \quad \quad$ **Orthogonal Complement**: $W^\perp = \{v \in V \mid \forall w \in W, v \perp w\} \subseteq V$

**Length**: $\| v \| = \sqrt{\langle v, v \rangle} \quad \quad$ **Projection**: For $w \in V$ and any $v \in V, \exists c \in K$ such that $v - cw \perp w \implies \proj_{w}v = \frac{\langle v, w \rangle}{\langle w, w \rangle} w$

**Pythagoras Theorem**: $v \perp w \implies \|v + w\|^2 = \|v\|^2 + \|w\|^2 \quad \quad$ **Parallelogram Law**: $\|v + w\|^2 + \|v - w\|^2 = 2\|v\|^2 + 2\|w\|^2$

**Schwartz Inequality**: $|\langle v, w \rangle| \leq \|v\|\|w\| \quad \quad$ **Triangle Inequality**: $\|v + w\| \leq \|v\| + \|w\|$

**Proposition**: $\{w_1, \ldots, w_r\}$ pairwise orthogonal $\implies \{w_1, \ldots, w_r\}$ is linearly independent

**Projection onto Subspace**: $\proj_Wv = \sum_{i=1}^{r} \proj_{w_i}w_i = \sum_{i=1}^{r} c_i w_i$. Clearly $\proj_W v \in W$

**Proposition**: $(v - \sum_{j=1}^{r}c_j w_j) \perp w_i$ for all $i \quad \quad$ **Corollary**: $(v - \sum_{j=1}^{r}c_j w_j) \perp w$ for all $w \in W$

**Geometric Interpertation**: $\proj_W v$ is the closest point to $v$ in $W$: $\|v - \proj_W v \| \leq \|v - w \|$ for any $w \in W$

**Orthonormal Basis**: $\{w_1, \ldots, w_r\}$ that is pairwise orthogonal and each $\|w_i\| = 1$

**Gram-Schmidt Process**: $u_1 = v_1 \quad \quad p_2 = v_2 - \proj_{u_1} v_2 \implies u_2 = \frac{1}{\|p_2\|} p_2 \quad \quad p_3 = v_3 - \proj_{u_1} v_3 - \proj_{u_2}v_3 \implies u_3 = \frac{1}{\|p_3\|} p_3$

**Theorem**: $V = W \oplus W^\perp \quad \quad$ **Corollary**: $\dim(V) = \dim(W) + \dim(W^\perp)$

**Rank**: $\dim(R^n) = \dim(C_A) + \dim(\Null(A)) = \dim(R_A) + \dim((R_A)^\perp) \implies \dim(R_A) = \dim(C_A)$

**Hermitian Inner Product**: For $y, z \in C^n$, $\langle y, z \rangle = y_1 \overline{z_1} + \cdots + y_n \overline{z_n}$

- **Proposition**: Positive definite since $\langle v, v \rangle = x_1 \overline{x_1} + \cdots x_n \overline{x_n} = \|x_1\|^2 + \cdots + \|x_n\|^2 \geq 0$

**Lemma**: $\forall v \in V, \langle v, v \rangle = 0 \implies \langle, \rangle$ is trivial $\quad \quad$ **Corollary**: $\forall v \in V, \langle v, v \rangle = 0 \implies$ any basis of $V$ is orthogonal

**Theorem**: If $\langle, \rangle$ is a scalar product on $V$, then $V$ has an orthogonal basis

**Dual Space**: $V^* = \mathcal{L}(V, K)$ containing linear transformations $\phi: V \rightarrow K$

- Typically we take $\phi_i$ where $\phi_i(v_j) = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases} \quad \quad$ **Proposition**: $B' = \{\phi_1, \ldots, \phi_n\}$ is a basis for $V^*$

- **Corollary** $\dim(V^*) \approx \dim(V)$. Namely $\dim(V^*) = \dim(V)$ and $\exists$ a 1-1, onto linear transformation $F: V \rightarrow V^*, F(v_i) = \phi_i$

**Annihilator**: $\Ann(W) = \{\phi \in V^* \mid \forall w \in W, \phi(w) = 0\}$. The set of linear transformations $\phi$ in $V^*$ where $W \subseteq \Ker(\phi)$

**Annihilator Theorem**: $\dim(W) + \dim(\Ann(W)) = \dim(V) = n$

**Determinate Formula**: $D(A) = (-1)^{i+1} a_{i1} \det(A_{i1}) + \cdots + (-1)^{i + n} a_{in} \det(A_{in})$

- $D(A^1, \ldots, A^n) =  \sum_{\sigma}^{}\epsilon(\sigma) a_{\sigma(1), 1} \cdots a_{\sigma(n), n}$

- Determinant is linear: $D(A^1, \ldots, C + C', \ldots, A^n) = D(A^1, \ldots, C, \ldots, A^n) + D(A^1, \ldots, C', \ldots, A^n)$

- If $2$ columns are equal, i.e. $A^j = A^i$, then $D(A) = 0$

- For the unit matrix $I$, $D(I) = 1$

- Interchanging columns changes sign: $D(A^1, \ldots, A^i, \ldots, A^j, \ldots) = - D(A^1, \ldots, A^j, \ldots, A^i, \ldots)$

- Adding a scalar multiple of a column to another column doesn't change $D(A): D(\ldots, A^k + tA^j, \ldots) = D(\ldots, A^k, \ldots)$

**Symmetric Operator**: $\langle Av , w \rangle = \langle v, Aw \rangle \implies A = ^t A$

**Hermitian Operator**: $\langle Av, w \rangle = \langle v, A^* w \rangle = \langle v, ^t \overline{A} w\rangle \implies A = ^t \overline{A}$

**Unitary**: $\langle Av , Aw \rangle = \langle v, w\rangle$

- $^t A A = I \iff$ real unitary $\quad \quad A^* A = ^t \overline{A} A = I \iff$ complex unitary
