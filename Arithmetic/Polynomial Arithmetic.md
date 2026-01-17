### Univariate Polynomials

**Definition:**
A **univariate polynomial** $P(x)$ is an expression defined as:

$$
P(x) := \sum_{j=0}^{m} a_j x^j = a_m x^m + a_{m-1} x^{m-1} + \dots + a_1 x + a_0
$$



**Key Terminology:**
* **Variable:** The symbol $x$.
* **Coefficients:** The values $a_j$. If the coefficients come from a set $R$, the set of all such polynomials is denoted **$R[x]$**.
* **Constant Term:** The term $a_0$, also written as $P(0)$.

**Special Polynomials:**
* **Zero Polynomial:** A polynomial where **all** coefficients are zero.
* **One Polynomial:** A polynomial where the constant term is $1$ and all other coefficients are zero.

**Degree ($deg(P)$):**
The degree is the non-negative integer $m$ corresponding to the highest power of $x$ with a non-zero coefficient.
* **Special Case:** The degree of the **zero polynomial** is defined as $-\infty$.
    * Property: $-\infty + m = -\infty$ and $-\infty < m$ for all integers $m \ge 0$.

> [!done]- Why is $\deg(0) = -\infty$?
> **The Logic:**
> The zero polynomial ($P(x)=0$) has no non-zero coefficients, so it has no natural degree. We define it as $-\infty$ to satisfy the **Degree Formula for Products**:
> 
> $$\deg(P \cdot Q) = \deg(P) + \deg(Q)$$
> 
> **Proof of Necessity:**
> Let $P(x) = 0$ and $Q(x)$ be any polynomial with degree $m$.
> 1.  The product $P(x) \cdot Q(x)$ is always $0$.
> 2.  Therefore, $\deg(P \cdot Q) = \deg(0)$.
> 3.  Applying the formula:
>     $$\deg(0) = \deg(0) + m$$
> 4.  The only "number" that remains unchanged when you add $m$ to it is $-\infty$ (or conceptually zero in a multiplicative sense, which maps to $-\infty$ in logarithms/exponents).
> 
> **Properties used:**
> * $-\infty + m = -\infty$ (Preserves multiplication rule)
> * $-\infty < m$ (Preserves addition rule: $\deg(P+Q) = \max(\deg P, \deg Q)$)

**Leading Coefficient ($Lc(P)$):**
The coefficient of the term with the highest degree ($a_m$).

$$
Lc(P) := a_m
$$


We write **$R_{\ge m}[x]$** for the set of all polynomials with a degree less than or equal to $m$.

**(Integer Polynomials)** : The coefficients of a polynomial must all have the same
type. The set of polynomials with integer coefficients is written as $\mathbb{Z}[x]$.

$$
\begin{align*}
P_1(x) &= 2x^2 - 4x + 17 && \# \text{ with } deg(P_1) = 2 \text{ and } Lc(P_1) = 2 \\
P_2(x) &= x^{23} && \# \text{ with } deg(P_2) = 23 \text{ and } Lc(P_2) = 1 \\
P_3(x) &= x && \# \text{ with } deg(P_3) = 1 \text{ and } Lc(P_3) = 1 \\
P_4(x) &= 174 && \# \text{ with } deg(P_4) = 0 \text{ and } Lc(P_4) = 174 \\
P_5(x) &= 1 && \# \text{ with } deg(P_5) = 0 \text{ and } Lc(P_5) = 1 \\
P_6(x) &= 0 && \# \text{ with } deg(P_6) = -\infty \text{ and } Lc(P_6) = 0 \\
P_7(x) &= (x - 2)(x + 3)(x - 5)
\end{align*}
$$

**(Polynomials over $\mathbb{Z_6}$)** :The set of all polynomials with indeterminate x and coefficients in $\mathbb{Z_6}$ is symbolized as $\mathbb{Z_6}[x]$.

$$\begin{align*}
(x - 2)(x + 3)(x - 5) &= (x + 4)(x + 3)(x + 1) && \# \text{ additive inverses in } \mathbb{Z}_6 \\
&= (x^2 + 4x + 3x + 3 \cdot 4)(x + 1) && \# \text{ bracket expansion} \\
&= (x^2 + 1x + 0)(x + 1) && \# \text{ computation in } \mathbb{Z}_6 \\
&= x^3 + x^2 + x^2 + x && \# \text{ bracket expansion} \\
&= x^3 + 2x^2 + x
\end{align*}$$

To be more precise, let $P \in R[x]$, with $P(x) = \sum_{j=0}^m a_j x^j$ be a polynomial with a coefficient of type $R$ and let $b \in R$ be an element of that type. Then the **evaluation** of $P$ at $b$ is given as follows:

$$
P(b) = \sum_{j=0}^m a_j b^j \tag{3.28}
$$

#### ❓ The Problem
> [!question] Statement
> Compare both expansions of $P_7$ from $\mathbb{Z}[x]$ in example 18 and from $\mathbb{Z}_6[x]$ in example 19. Can you see how definition of $P_7$ over $\mathbb{Z}$ projects to the definition over $\mathbb{Z}_6$, if you consider the residue classes of $\mathbb{Z}_6$?

> [!done]- Solution
> 
> Our polynomial is $P_7(x) = (x-2)(x+3)(x-5)$, which is projected to be:
> 
> $$
> P_7 \in \mathbb{Z}[x] = x^3 - 4x^2 - 11x + 30
> $$
> 
> $$
> P_7 \in \mathbb{Z}_6[x] = x^3 + 2x^2 + x
> $$
> 
> We can compute the result in $\mathbb{Z}$ and then project the coefficients, that is equal to doing everything in $\mathbb{Z}_6$ in the first place!
> 

### Polynomial arithmetic


To be more precise, let $\sum_{n=0}^{m_1} a_n x^n$ and $\sum_{n=0}^{m_2} b_n x^n$ be two polynomials from $R[x]$. Then the $\textbf{sum}$ and the $\textbf{product}$ of these polynomials is defined as follows:

$$\begin{align}
\sum_{n=0}^{m_1} a_n x^n + \sum_{n=0}^{m_2} b_n x^n &= \sum_{n=0}^{\max(\{m_1, m_2\})} (a_n + b_n)x^n \tag{3.29} \\[1em]
\left(\sum_{n=0}^{m_1} a_n x^n\right) \cdot \left(\sum_{n=0}^{m_2} b_n x^n\right) &= \sum_{n=0}^{m_1 + m_2} \sum_{i=0}^{n} a_i b_{n-i} x^n \tag{3.30}
\end{align}$$

**Goal:** Multiply $(1 + 2x)$ and $(3 + 4x)$.

**Formula:** $c_n = \sum_{i=0}^n a_i b_{n-i}$

1.  **$n=0$ ($x^0$):** $a_0 b_0 = 1 \cdot 3 = \mathbf{3}$
2.  **$n=1$ ($x^1$):** $a_0 b_1 + a_1 b_0 = (1 \cdot 4) + (2 \cdot 3) = 4 + 6 = \mathbf{10}$
3.  **$n=2$ ($x^2$):** $a_0 b_2 + a_1 b_1 + a_2 b_0 = (1 \cdot 0) + (2 \cdot 4) + (0 \cdot 3) = \mathbf{8}$

**Result:** $3 + 10x + 8x^2$

### Euclidean Division with polynomials

The arithmetic of polynomials shares a lot of properties with the arithmetic of integers. As a consequence, the concept of Euclidean Division and the algorithm of long division is also defined for polynomials. Recalling the Euclidean Division of integers, we know that, given two integers $a$ and $b \neq 0$, there is always another integer $m$ and a natural number $r$ with $r < |b|$ such that $a = m \cdot b + r$ holds.

We can generalize this to polynomials whenever the leading coefficient of the dividend polynomial has a notion of multiplicative inverse. In fact, given two polynomials $A$ and $B \neq 0$ from $R[x]$ such that $Lc(B)^{-1}$ exists in $R$, there exist two polynomials $Q$ (the quotient) and $P$ (the remainder), such that the following equation holds and $deg(P) < deg(B)$:

$$
A = Q \cdot B + P \tag{3.31}
$$

Similarly to integer Euclidean Division, both $Q$ and $P$ are uniquely defined by these relations.

$\textit{Notation and Symbols}$ : Suppose that the polynomials $A, B, Q$ and $P$ satisfy equation 3.31. We often use the following notation to describe the quotient and the remainder polynomials of the Euclidean Division:

$$
A \text{ div } B := Q, \quad A \text{ mod } B := P \tag{3.32}
$$

We also say that a polynomial $A$ is divisible by another polynomial $B$ if $A \text{ mod } B = 0$ holds. In this case, we also write $B|A$ and call $B$ a $\textit{factor}$ of $A$.


#### ❓ The Problem
> [!question] Statement
> Show that the polynomial $B(x) = 2x^4 -3x +4 \in \mathbb{Z}_5[x]$ is a factor of the polynomial $A(x) = x^7 + 4x^6 + 4x^5 + x^3 + 2x^2 + 2x + 3 \in \mathbb{Z}_5[x]$.

> [!done]- Solution
> The important thing here is to realize that you need to invert the leading coefficient. In the case of $B(x)$, that is 2. We need to find the inverse of 2, which we can via Fermat's Little Theorem as $2^{5-2} \bmod 5 = 3$. By doing the calculations by hand, I've found:
> 
> - $Q(x) = 3x^3 + 2x^2 + 2x + 2$
> 
> Let's verify from Sage:
> 
> 
> ```python
> from sage.all import Integers
> 
> # Univariate Polynomial Ring in x
> # over Ring of integers modulo 5
> Z5x = Integers(5)['x']
> 
> # x^7 + 4*x^6 + 4*x^5 + x^3 + 2*x^2 + 2*x + 3
> A = Z5x([3, 2, 2, 1, 0, 4, 4, 1])
> # 2*x^4 - 3*x + 4
> B = Z5x([4, -3, 0, 0, 2])
> 
> # expected result
> # 3*x^3 + 2*x^2 + 2*x + 2
> Q = Z5x([2, 2, 2, 3])
> 
> assert Q == A / B
> ```

### Prime Factors

The polynomial analog to a prime number is a so-called irreducible polynomial, which is
defined as a polynomial that cannot be factored into the product of two non-constant polynomials using Euclidean Division. Irreducible polynomials are to polynomials what prime numbers are to integers: they are the basic building blocks from which all other polynomials can be constructed.

To be more precise, let $P \in R[x]$ be any polynomial. Then there always exist irreducible polynomials $F_1, F_2, \dots, F_k \in R[x]$, such that the following holds:

$$
P = F_1 \cdot F_2 \cdot \dots \cdot F_k \tag{3.34}
$$

This representation is unique (except for permutations in the factors) and is called the **prime factorization** of $P$. Moreover, each factor $F_i$ is called a **prime factor** of $P$.

**Definition (Roots)**  : Points where a polynomial evaluates to zero are called $\textbf{roots}$ of the polynomial. To be more precise, let $P \in R[x]$ be a polynomial. Then a root is a point $x_0 \in R$ with $P(x_0) = 0$ and the set of all roots of $P$ is defined as follows:

$$
R_0(P) := \{ x_0 \in R \mid P(x_0) = 0 \} \tag{3.35}
$$

**Connection to Factors** : If $x_0$ is a root of $P$, then the linear polynomial $F(x) = (x - x_0)$ is a $\textbf{prime factor}$ of $P$.

**Multiplicity**:  A root $x_0$ of a polynomial $P$ is said to have a \textbf{multiplicity} of $k$ if the polynomial $(x - x_0)^k$ is a factor of $P$. That is, if there is a polynomial $Q$ such that we can write $P$ as:

$$
P(x) = (x - x_0)^k \cdot Q(x) \tag{3.36}
$$

**Theorem (Bound on Roots)** :  If $m$ is the degree of a polynomial $P$, then $P$ cannot have more than $m$ roots.

> [!done]-  Theorem: Roots imply Prime Factors
> **The Statement:**
> If $P(x_0) = 0$, then $(x - x_0)$ is a prime factor of $P(x)$.
> 
> **Proof (Factor Theorem):**
> 1.  By Euclidean Division: $P(x) = (x - x_0)Q(x) + R$.
> 2.  Evaluate at $x_0$: $P(x_0) = 0 \cdot Q(x_0) + R = R$.
> 3.  Since $x_0$ is a root, $P(x_0) = 0$, implying $R = 0$.
> 4.  Thus $P(x) = (x - x_0)Q(x)$.
> 
> **Why "Prime"?**
> Suppose $F(x) = A(x) \cdot B(x)$. By the degree sum formula:
$$ \deg(A) + \deg(B) = \deg(F) = 1 $$
Since degrees are non-negative integers, the only solution is $\{1, 0\}$.
Thus, one factor must be degree 0 (a constant). Since it cannot be split into two non-constant polynomials, $F(x)$ is irreducible.

#### ❓ The Problem
> [!question] Statement
> Show that if a polynomial $P \in \mathbb{R}[X]$ of degree $\deg(P) = m$ has less than $m$ roots, it must have a prime factor $F$ such that $\deg(F) > 1$.

> [!done]- Solution
>  **Proposition.** If $P \in \mathbb{R}[x]$ with $\deg(P)=m$ has fewer than $m$ real roots, it contains a prime factor of degree $> 1$. 
> 
> **Or** : Let $P \in \mathbb{R}[x]$ be a polynomial of degree $m$. If the sum of the multiplicities of its real roots is strictly less than $m$, then $P$ must contain a prime factor $F$ with $\deg(F) > 1$.
> 
> **Proof.**
>  Suppose that $P$ has $k$ roots $\{z_1, z_2, \ldots, z_k\}$ such that $k < m$. Then, we know that:
> $$
> P(x) = (x - z_1)(x - z_2)\ldots(x - z_k)Q(x)
> $$
> From this, we can see that $P(x) = (x^k + \ldots)Q(x)$, meaning that $Q(x)$ must have degree $m - k$. $Q(x)$ itself may be reducible; however, none of it's factors may be linear because that would imply the existence of another root. So, $Q(x)$ must have at least one prime factor that is not linear (i.e. degree greater than 1), which implies $P(x)$ such a factor.
> 

#### ❓ The Problem
> [!question] Statement
> Consider $P = x^7 + 3x^6 + 3x^5 + x^4 - x^3 - 3x^2 - 3x - 1$ in $\mathbb{Z}_6[X]$. Find the set of all roots $R_0(P)$ and then compute the prime factorization of $P$.

> [!done]- Solution
> Let's use Sage to find the roots:
> 
> ```python
> Z6 = Integers(6)
> Z6x = Z6['x']
> # x^7 + 3*x^6 + 3*x^5 + x^4 - x^3 - 3*x^2 - 3*x - 1
> P = Z6x([-1, -3, -3, -1, 1, 3, 3, 1])
> 
> # find roots
> roots = P.roots(multiplicities=False)
> print("Roots:", roots)
> # [1, 5]
> ```
> 
>     Roots: [1, 5]
> 
> 
> To find factors, we can divide $x - r$ for each root $r$ until the quotient does not have $r$ as a root anymore. Once we are done with all roots, if the remaining result is not $1$ we can also include that as a factor.
> 
> 
> ```python
> factors = []
> Q = P
> for r in roots:
>   R = Z6x([-r, 1])
>   count = 1
>   while True:
>     Q = Q // R
>     if r not in Q.roots(multiplicities=False):
>       break
>     count += 1
>   factors.append((R, count))
> 
> if Q != Z6x(1):
>   factors.append((Q, 1))
> 
> print("Factors:", factors)
> # [(x + 5, 1), (x + 1, 4), (x^2 + 1, 1)]
> ```
> 
>     Factors: [(x + 5, 1), (x + 1, 4), (x^2 + 1, 1)]
> 
> 
> Note that the same factor can appear a few times, so the `factors` here is a list of tuples where the first item of a tuple is the factor, and the second item is the number of time it appears.
> 
> After finding the factors, we can test to see if we get back the original polynomial when we multiply all these factors.
> 
> 
> ```python
> PP = Z6x(1)
> for f in factors:
>   assert(f[1] > 0)
>   for _ in range(f[1]):
>     PP = PP * f[0]
> 
> assert P == PP
> ```

### Lagrange Interpolation

One particularly useful property of polynomials is that a polynomial of degree $m$ is completely determined on $m+1$ evaluation points, which implies that we can uniquely derive a polynomial of degree $m$ from a set $S$:

$$
S = \{ (x_0, y_0), (x_1, y_1), \dots, (x_m, y_m) \mid x_i \neq x_j \text{ for all indices i and j} \} \tag{3.37}
$$
Polynomials therefore have the property that $m + 1$ pairs of points $(x_i, y_i)$ for $xi \ne x_j$ are enough to determine the set of pairs $(x, P(x))$ for all $x ∈ R$.

If the coefficients of the polynomial we want to find *have a notion of multiplicative inverse*,
it is always possible to find such a polynomial using a method called **Lagrange Interpolation**.

*"Given m+1 points with distinct x-values, Lagrange Interpolation constructs the **unique** polynomial of degree **at most m** that passes through them."*

We need uniqueness because it turns a set of random-looking dots into a **rigid, lock-and-key definition**. Without uniqueness, a set of points would be a "suggestion" rather than a definition.


**Example :**  Let us consider the set $S = \{(0,4), (-2,1), (2,3)\}$. Our task is to compute a polynomial of degree $2$ in $\mathbb{Q}[x]$ with coefficients from the set of rational numbers $\mathbb{Q}$. Since $\mathbb{Q}$ has multiplicative inverses, we can use method of Lagrange Interpolation to compute the polynomial:

$$\begin{align*}
l_0(x) &= \frac{x-x_1}{x_0-x_1} \cdot \frac{x-x_2}{x_0-x_2} = \frac{x+2}{0+2} \cdot \frac{x-2}{0-2} = - \frac{(x+2)(x-2)}{4} \\
&= -\frac{1}{4}(x^2 - 4) \\[1em]
l_1(x) &= \frac{x-x_0}{x_1-x_0} \cdot \frac{x-x_2}{x_1-x_2} = \frac{x-0}{-2-0} \cdot \frac{x-2}{-2-2} = \frac{x(x-2)}{8} \\
&= \frac{1}{8}(x^2 - 2x) \\[1em]
l_2(x) &= \frac{x-x_0}{x_2-x_0} \cdot \frac{x-x_1}{x_2-x_1} = \frac{x-0}{2-0} \cdot \frac{x+2}{2+2} = \frac{x(x+2)}{8} \\
&= \frac{1}{8}(x^2 + 2x) \\[1em]
P(x) &= 4 \cdot (-\frac{1}{4}(x^2-4)) + 1 \cdot \frac{1}{8}(x^2-2x) + 3 \cdot \frac{1}{8}(x^2+2x) \\
&= -x^2 + 4 + \frac{1}{8}x^2 - \frac{1}{4}x + \frac{3}{8}x^2 + \frac{3}{4}x \\
&= -\frac{1}{2}x^2 + \frac{1}{2}x + 4
\end{align*}$$

And, indeed, evaluation of $P$ on the $x$-values of $S$ gives the correct points, since $P(0) = 4$, $P(-2) = 1$ and $P(2) = 3$. 

#### ❓ The Problem
> [!question] Statement
> Consider modular 5 arithmetic, and set $S = \{(0, 0), (1, 1), (2, 2), (3, 2)\}$. Find a polynomial $P \in \mathbb{Z}_5[x]$ such that $P(x_i) = y_i$ for all $(x_i, y_i) \in S$.

> [!done]- Solution
> We need to do lagrange interpolation for this. We could do by hand, but let's just use Sage for this one!
> 
> 
> ```python
> Integers(5)["x"].lagrange_polynomial([(0, 0), (1, 1), (2, 2), (3, 2)])
> # 4*x^3 + 3*x^2 + 4*x
> ```
> 
> 
> 
> 
>     4*x^3 + 3*x^2 + 4*x
> 
> 
> 
> Apparently, $4x^3 + 3x^2 + 4x$ does the job.
> 


#### ❓ The Problem
> [!question] Statement
>  Consider the same set $S = \{(0, 0), (1, 1), (2, 2), (3, 2)\}$. Why is it not possible to do Lagrange interpolation for these points in $\mathbb{Z}_6[x]$?

> [!done]- Solution
> **The Constraint:**
> For Lagrange interpolation to work in a ring $R$, the difference between every pair of distinct x-coordinates $(x_j - x_i)$ must be a **unit** (invertible element) in $R$.
> 
> **Example Failure:**
> Set $S = \{(0, 0), (1, 1), (2, 2), (3, 2)\}$ in $\mathbb{Z}_6$.
> * **Coordinate Pair:** $x_2=2, x_0=0$
> * **Difference:** $2 - 0 = 2$
> * **Invertibility Check:** $2 \times k \equiv 1 \pmod 6$ has no solution.
> * **Result:** The term $\frac{1}{x_2 - x_0}$ is undefined, preventing the construction of the basis polynomial $L_2(x)$.

