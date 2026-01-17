**Modular arithmetic** is a system of integer arithmetic where numbers “wrap around” when
reaching a certain value.  The number at which the wrap occurs is called the **modulus**.

**How does modular arithmetic provide the computational infrastructure for algebraic types that have cryptographically useful examples of one-way functions ?**

### Congruence

Let $n \in \mathbb{N}$, $n \geq 2$ be a fixed natural number  
(called the **modulus**).

#### Congruence classes

Two integers $a$ and $b$ are **congruent modulo $n$**  
(denoted $a \equiv b \pmod{n}$) if and only if they leave the **same remainder** when divided by $n$ by Euclidean division.

In other words:

$$
a \equiv b \pmod{n} \quad\iff\quad n \mid (a - b)
$$

Equivalently:

$$
a = qn + r, \quad b = pn + r \quad \text{for some integers } q,p \text{ and the same remainder } 0 \leq r < n
$$

**Short version (most used):**

$$
a \equiv b \pmod{n} \quad\Longleftrightarrow\quad a - b \text{ is divisible by } n
$$

#### ❓ The Problem
> [!question] Statement
> Find all integers $x$ such that the congruence $x \equiv 4 \pmod{6}$ is satisfied.

> [!done]- Solution
> All numbers of the form $6k + 4$ for integer $k$ satisfy this congruence.
> 

#### Computational Rules

Let $a_1, a_2, b_1, b_2, k \in \mathbb{Z}$ and $n \geq 2$ fixed modulus.

##### 1. Compatibility with translation (adding the same number)
$$
a_1 \equiv b_1 \pmod{n} \quad\iff\quad a_1 + k \equiv b_1 + k \pmod{n}
$$

##### 2. Compatibility with scaling (multiplication by constant)
$$
a_1 \equiv b_1 \pmod{n} \quad\implies\quad k \cdot a_1 \equiv k \cdot b_1 \pmod{n}
$$

##### 3. Cancellation law (when multiplier is coprime to modulus)
$$
\gcd(k,n)=1 \quad\text{and}\quad k \cdot a_1 \equiv k \cdot b_1 \pmod{n} \quad\implies\quad a_1 \equiv b_1 \pmod{n}
$$

##### 4. Stronger cancellation (multiplication by k and modulus k·n)
$$
k \cdot a_1 \equiv k \cdot b_1 \pmod{k \cdot n} \quad\implies\quad a_1 \equiv b_1 \pmod{n}
$$

##### 5. Compatibility with addition (most used!)
$$
\begin{aligned}
&a_1 \equiv b_1 \pmod{n} \\
&a_2 \equiv b_2 \pmod{n}
\end{aligned}
\quad\implies\quad a_1 + a_2 \equiv b_1 + b_2 \pmod{n}
$$

##### 6. Compatibility with multiplication (very important!)
$$
\begin{aligned}
&a_1 \equiv b_1 \pmod{n} \\
&a_2 \equiv b_2 \pmod{n}
\end{aligned}
\quad\implies\quad a_1 \cdot a_2 \equiv b_1 \cdot b_2 \pmod{n}
$$

##### Quick Summary Card (memorize these!)

$$
\begin{array}{ll}
\text{Addition:}    & a \equiv b,\ c \equiv d \ \implies\ a+c \equiv b+d \pmod{n} \\[1ex]
\text{Multiplication:} & a \equiv b,\ c \equiv d \ \implies\ ac \equiv bd \pmod{n} \\[1ex]
\text{Scaling:}     & a \equiv b \ \implies\ ka \equiv kb \pmod{n} \\[1ex]
\text{Cancellation (coprime):} & \gcd(k,n)=1,\ ka \equiv kb \ \implies\ a \equiv b \pmod{n}
\end{array}
$$

### Fermat's Little Theorem

Let $p$ be a **prime** number.

$$
\begin{aligned}
&\text{For any integer } a, &&a^p \equiv a \pmod{p}\\[1ex]
&\text{If } p \nmid a, &&\text{then} \quad a^{p-1} \equiv 1 \pmod{p} &&\text{we can divide both sides of this congruence by a}
\end{aligned}
$$

#### ❓ The Problem
> [!question] Statement
> 1. Find all integers $x$ such that the congruence $x \equiv 4 \pmod{6}$ is satisfied.
> 2.  Find all solutions $x \in \mathbb{Z}$ to the following congruence:
$$5x + 4 \equiv 28 + 2x \pmod{13}$$ 
>3. Find all solutions $x \in \mathbb{Z}$ to the following congruence: $$69x \equiv 5 \pmod{23}$$
>4. Find all solutions $x \in \mathbb{Z}$ to the following congruence:
> $$69x \equiv 46 \pmod{23}$$
> 5. Show that for $a \equiv b \pmod{n}$ the equivalence $a^k \equiv b^k \pmod{n}$ holds.
> 6.  Let $a, n$ be integers, such that $a$ and $n$ are **not** co-prime. For which $b \in \mathbb{Z}$ does $ax \equiv b \pmod{n}$ have a solution $x$, and how does the solution set look like?

> [!done]- Solution
> 1. All numbers of the form $6k + 4$ for integer $k$ satisfy this congruence.
> 2. By reducing we find $3x \equiv 24 \pmod{13}$. We need to get rid of the 3 in $3x$, so we must multiply $3x$ by some $k$ where $3k = 1$.
> 
> Fermat's Little Theorem tells us that $3^{13 - 2} \pmod{13}$ would give us that $k$, which we find to be 9. Multiplying both sides with 9, we get $x \equiv 216 \equiv 8 \pmod{13}$.
> 
> 3. Due to mod 23, we get $0x \equiv 5 \pmod{23}$, so there are no solutions.
> 4. Due to mod 23, we get $0x \equiv 0 \pmod{23}$, so all $x$ are solutions.
> 5. It comes from "compatibility with multiplication" which is the rule that
> 
> $$
> a_1 \equiv b_1 \pmod{n} \text{ and } a_2 \equiv b_2 \pmod{n} \implies a_1a_2 \equiv b_1b_2 \pmod{n}
> $$
> 
> implying one by one the equivalences $a^i \equiv b^i \pmod{n}$ for $i = 2, 3, \ldots, k$.
> 
> You can also prove this by induction to show $a^1 \equiv b^1 \pmod{n}$ and assume $a^{k-1} \equiv b^{k-1} \pmod{n}$.
> 
> 6. The equivalence implies $ax - ny = b$. Denote $d=\gcd(a, n)$ which also implies $a = da'$ and $n = dn'$. Now, supposing that the solution exists for $ax - ny = b$ for some $x', y'$:
> 
> $$b = ax' - ny' = da'x' - dn'y' = d(a'x' - n'y')$$
> 
> Since $a', x', n', y'$ are all integers, $b / d$ must be an integer too; implying that $d \mid b$. In other words, solutions exists for $b \in \mathbb{Z}$ where $\gcd(a, n) \mid b$.
> 
> Now that we also know $b = db'$, let's rewrite the congruence:
> 
> $$da'x \equiv db' \pmod{dn'}$$
> 
> We can remove $d$ from all sides:
> 
> $$a'x \equiv b' \pmod{n'}$$
> 
> Since $\gcd(a', n') = 1$, this has only one solution. Denote this solution as $t$ where $x \equiv t \pmod{n'}$. The other solutions are the numbers from $t$ to $t + n$, with increments of $n'$. Notice that:
> 
> - $t \implies da'(t) \equiv db' \pmod{dn'}$
> - $t + n' \implies da'(t + n') = da't + a'dn' = da' \equiv db' \pmod{dn'}$
> - $t + 2n' \implies da'(t + 2n') = da't + 2a'dn' = da' \equiv db' \pmod{dn'}$
> - $\ldots$
> - $t + dn' \implies da'(t + dn') = da't + da'dn' = da' \equiv db' \pmod{dn'}$
> 
> Since $t + (d+1)n' = t + n' + dn'$ would be equivalent to $t + n'$ in modulo $n'$, we start to wrap around the solution set of $x$. That is our complete set of solutions with $d$ elements.
> 

### The Chinese Remainder Theorem

Let $n_1, n_2, \dots, n_k$ be pairwise coprime positive integers (i.e., $\gcd(n_i, n_j) = 1$ for all $i \neq j$).  
Let $a_1, a_2, \dots, a_k$ be any integers.

Then the following system of congruences

$$
\begin{cases}
x \equiv a_1 \pmod{n_1} \\
x \equiv a_2 \pmod{n_2} \\
\vdots \\
x \equiv a_k \pmod{n_k}
\end{cases}
$$

has a **unique solution modulo** $N = n_1 n_2 \cdots n_k$.  
That is, there exists a unique $x \pmod{N}$ satisfying all the congruences simultaneously.

**When to use:**  
You have a system of congruences with **pairwise coprime** moduli.

**General method:**

1. Check that the moduli $n_1, n_2, \dots, n_k$ are **pairwise coprime** ($\gcd(n_i,n_j)=1$ for $i \neq j$).
2. Compute $N = n_1 \cdot n_2 \cdot \dots \cdot n_k$
3. For each $i$, compute $N_i = N / n_i$
4. Find the inverse $y_i$ such that $N_i \cdot y_i \equiv 1 \pmod{n_i}$
5. The solution is:
   $$
   x \equiv \sum_{i=1}^k a_i N_i y_i \pmod{N}
   $$


#### ❓ The Problem
> [!question] Statement
$\textbf{Problem: Solve the system: }$
$$\begin{cases} 
x \equiv 2 \pmod 3 \\
x \equiv 3 \pmod 4 \\
x \equiv 1 \pmod 5
\end{cases}$$

> [!done]- Solution
> 
> $\textbf{1. Total Modulus:}$ $N = 3 \times 4 \times 5 = 60$.
> 
> $\textbf{2. Table of Values:}$
> 
> | $a_i$ | $n_i$ | $N_i = N/n_i$ | $N_i \pmod{n_i}$ | Inverse $y_i$ ($N_i y_i \equiv 1$) |
> | :--- | :--- | :--- | :--- | :--- |
> | 2 | 3 | 20 | $20 \equiv 2$ | $2 \cdot 2 = 4 \equiv 1 \implies \mathbf{2}$ |
> | 3 | 4 | 15 | $15 \equiv 3$ | $3 \cdot 3 = 9 \equiv 1 \implies \mathbf{3}$ |
> | 1 | 5 | 12 | $12 \equiv 2$ | $2 \cdot 3 = 6 \equiv 1 \implies \mathbf{3}$ |
> 
> $\textbf{3. Calculation:}$
> $$
> \begin{aligned}
> x &= \sum (a_i \cdot N_i \cdot y_i) \\
> x &= (2 \cdot 20 \cdot 2) + (3 \cdot 15 \cdot 3) + (1 \cdot 12 \cdot 3) \\
> x &= 80 + 135 + 36 = 251
> \end{aligned}
> $$
> 
> $\textbf{4. Final Reduction:}$
> $$ x \equiv 251 \pmod{60} \implies x \equiv 11 \pmod{60} $$


### Residue Class Representation

**Definition:**
For an integer $n > 0$, the **residue class** of an integer $a$, denoted $[a]_n$, is the set of all integers that share the same remainder as $a$ when divided by $n$.

$$
[a]_n = \{ x \in \mathbb{Z} : x \equiv a \pmod{n} \}
$$

**The Set $\mathbb{Z}_n$:**
The collection of all distinct residue classes modulo $n$ forms the set of integers modulo $n$:
$$
\mathbb{Z}_n = \{ [0], [1], \dots, [n-1] \}
$$

**Properties:**
1.  **Equality:** $[a] = [b]$ if and only if $a \equiv b \pmod n$.
2.  **Partition:** These classes split the integers ($\mathbb{Z}$) into $n$ disjoint sets.
3.  **Representative:** Any $x \in [a]$ can "represent" the class, but usually we choose the smallest $r \ge 0$.

**Example ($\mathbb{Z}_3$):**
* $[0] = \{ \dots, -3, 0, 3, 6, \dots \}$
* $[1] = \{ \dots, -2, 1, 4, 7, \dots \}$
* $[2] = \{ \dots, -1, 2, 5, 8, \dots \}$

From the properties of Euclidean Division that there are exactly $n$ different
remainder classes for every modulus $n$.

**Disjoint Sets**

**Definition:**
Two sets $A$ and $B$ are **disjoint** if they have no elements in common.
$$A \cap B = \emptyset$$

**Pairwise Disjoint:**
A collection of sets $\{S_1, S_2, \dots, S_n\}$ is pairwise disjoint if, for every distinct pair $i \neq j$:
$$S_i \cap S_j = \emptyset$$

**Example:**
* $A = \{1, 2, 3\}$
* $B = \{4, 5, 6\}$
* $A \cap B = \emptyset \implies$ **Disjoint**

**Relation to Residue Classes:**
The residue classes modulo $n$ ($\mathbb{Z}_n$) form a **partition** of the integers because they are pairwise disjoint and their union is all of $\mathbb{Z}$.

#### ❓ The Problem
> [!question] Statement
> Define $\mathbb{Z}_{13}$ as the arithmetic modulo 13. Consider the following equation:
> $$5x + 4 \equiv 28x +2x \pmod{13}$$
> Rewrite this in $\mathbb{Z}_{13}$.

> [!done]- Solution
> We have:
> 
> $$5x + 4 \equiv 2 + 2x \pmod{13}$$
> $$3x + 2 \equiv 0 \pmod{13}$$
> $$3x \equiv 11 \pmod{13}$$
> 
> Now, which integers $x \in \mathbb{Z}_{13}$ give $11 \pmod{13}$ when multiplied by 3? Instead of asking that, here I can ask what is the inverse of 3 in modulo 13, that is, which number when multiplied by 3 gives 1?
> 
> We know that $3 \times 9 = 27 \equiv 1 \pmod{13}$, so I can multiply both sides with 9.
> 
> $$x \equiv 99 \equiv 8 \pmod{13}$$
> 
> Meaning that all integers of the form $13k+8, k \in \mathbb{N}$ solve this equation.

### Modular Inverses

**Definition:** Let $S$ be our set that has some notion $a \cdot b$ of multiplication and a **neutral element** $1 \in S$, such that $1 \cdot a = a$ for all elements $a \in S$. Then a **multiplicative inverse** $a^{-1}$ of an element $a \in S$ is defined as follows:

$$
a \cdot a^{-1} = 1 \tag{3.22}
$$

**Definition.** Let $S$ be a set equipped with an operation $+$ (addition) and a **neutral element** $0 \in S$, such that $0 + a = a = a + 0$ for all $a \in S$. Then an **additive inverse** of an element $a \in S$, denoted as $-a$, is defined as follows:

$$
a + (-a) = 0
$$


#### Connection: Extended Euclidean Algorithm & Modular Inverse

**The Goal:** Find the multiplicative inverse of $r$ modulo $n$.
(This implies finding a number $t$ such that $t \cdot r \equiv 1 \pmod n$).

**The Condition:** The inverse exists if and only if $\gcd(n, r) = 1$.

**The Logic:**

1.  **Bézout's Identity:**
    Since $\gcd(n, r) = 1$, the Extended Euclidean Algorithm guarantees we can find integers $s$ and $t$ satisfying:
    $$
    s \cdot n + t \cdot r = 1
    $$

2.  **Apply Modulo $n$:**
    Take the operation $\pmod n$ on both sides of the equation:
    $$
    (s \cdot n + t \cdot r) \equiv 1 \pmod n
    $$

3.  **The "Magic" Step:**
    Since $s \cdot n$ is a multiple of $n$, it becomes $0$ in modulo $n$:
    $$
    0 + t \cdot r \equiv 1 \pmod n
    $$

**Conclusion:**
$$
t \cdot r \equiv 1 \pmod n
$$
Therefore, **$t \pmod n$ is the multiplicative inverse of $r$**.


#### ❓ The Problem
> [!question] Statement
> Find Inverse of $5 \pmod 6$

> [!done]- Solution
> 
> 
> We want to find $x$ such that:
> 
> $$5x \equiv 1 \pmod 6$$
> 
> **Step 1: Euclidean Algorithm (Forward)**
> 
> We divide the modulus (6) by the number (5) to find the greatest common divisor (GCD).
> 
> $$6 = 1 \cdot 5 + 1$$
> 
> Since the remainder is already **1**, we stop here. This confirms that $\gcd(6, 5) = 1$, so an inverse exists.
> 
>  **Step 2: Extended Algorithm (Backward)**
> 
> We need to write **1** as a linear combination of **6** and **5**. From the equation above, we rearrange it:
> 
> $$1 = 6 - (1 \cdot 5)$$
> 
> **Step 3: Apply Modulo 6**
> 
> Now we look at this equation in the world of modulo 6.
> 
> $$1 \equiv 6 - (1 \cdot 5) \pmod 6$$
> 
> Since $6 \equiv 0 \pmod 6$, the term $6$ vanishes:
> 
> $$1 \equiv 0 - 1 \cdot 5 \pmod 6 \\ 1 \equiv -1 \cdot 5 \pmod 6$$
> 
> **Step 4: Identify the Inverse**
> 
> We have found that the inverse is **-1**. However, we usually want the positive representative in the range $[0, 5]$.
> 
> $$-1 \equiv 5 \pmod 6$$
> 
> **Conclusion:** The multiplicative inverse of 5 modulo 6 is **5**.
> 
> Check: $5 \cdot 5 = 25$.
> 
> $25 = 4 \cdot 6 + 1$, so $25 \equiv 1 \pmod 6$. (Correct).
> 


#### Non-Unique Solutions in Modular Arithmetic

**The Phenomenon:**
In standard algebra, linear equations like $ax = b$ usually have 1 solution. In modular arithmetic $\mathbb{Z}_n$, if $\gcd(a, n) = d > 1$, the equation might have **$d$ distinct solutions** (or none at all).

**Example in $\mathbb{Z}_6$:**
Equation: $3x + 3 = 0 \implies 3x \equiv 3 \pmod 6$.

1.  **The Problem:** $\gcd(3, 6) = 3 \neq 1$.
    * We cannot calculate $3^{-1}$.
    * We cannot "divide" to isolate $x$.
2.  **The Result:** instead of 1 solution, we have **3 solutions** (matching the GCD).
    * $x_1 = 1$
    * $x_2 = 3$
    * $x_3 = 5$

**Verification:**
$$
\begin{aligned}
3(1) &\equiv 3 \\
3(3) &= 9 \equiv 3 \\
3(5) &= 15 \equiv 3
\end{aligned}
$$
All three values satisfy $3x \equiv 3 \pmod 6$.

#### ❓ The Problem
> [!question] Statement
> Which of the integers 7, 1, 0, 805, -4255 have multiplicative inverses in modular 24 arithmetic?

> [!done]- Solution
> First let's get rid of the trivial cases:
> 
> - 1 is always it's own inverse.
> - 0 never has a multiplicative inverse.
> 
> We can check GCD for the remaining numbers:
> 
> 
> ```python
> from sage.all import gcd
> gcd(7, 24), gcd(805, 24), gcd(-4255, 24)
> ```
> 
> 
> 
> 
>     (1, 1, 1)
> 
> 
> 
> 
> Apparently, all of these are coprime to 24. We can perhaps use Extended Euclidean Algorithm, which is implemented in Sage already. Using `xgcd(a, b)` where `a >= b` we can find:
> 
> $$
> \gcd(a, b) = s \times a + t \times b
> $$
> 
> First, let's treat all numbers in mod 24, so $805 \equiv 13 \pmod{24}$ and $-4255 \equiv 17 \pmod{24}$. Then, let's use `xgcd` as follows:
> 
> 
> ```python
> from sage.all import xgcd
> print(xgcd(24, 7))  # (1, -2, 7)
> print(xgcd(24, 13)) # (1, 6, -11)
> print(xgcd(24, 17)) # (1, 5, -7)
> ```
> 
>     (1, -2, 7)
>     (1, 6, -11)
>     (1, 5, -7)
> 
> 
> 
> To interpret these results:
> 
> - $7^{-1} \equiv 7 \pmod{24}$
> - $13^{-1} \equiv -11 \equiv 13 \pmod{24}$
> - $17^{-1} \equiv -7 \equiv 17 \pmod{24}$
> 
> These numbers all are their own inverses, nice!

#### ❓ The Problem
> [!question] Statement
> Find the set of all solutions to the congruence $17(2x + 5) - 4 \equiv 2x + 4 \pmod{5}$. Then, project the congruence into $\mathbb{Z}_5$ and solve the resulting equation in $\mathbb{Z}_5$.

> [!done]- Solution
> Due to mod 5, we find:
> 
> $$
> 2(2x) + 1 \equiv 2x + 4 \pmod{5}
> $$
> 
> $$
> 2x \equiv 3 \pmod{5}
> $$
> 
> We have $2^{-1} \equiv 2^{5-2} \pmod{5}$ which is 3. Multipyling both sides with 3 we find:
> 
> $$
> x \equiv 4 \pmod{5}
> $$
> 

#### ❓ The Problem
> [!question] Statement
> Find the set of all solutions to the congruence $17(2x + 5) - 4 \equiv 2x + 4 \pmod{6}$. Then, project the congruence into $\mathbb{Z}_6$ and _try to solve_ the resulting equation in $\mathbb{Z}_6$.

> [!done]- Solution
> Due to mod 6 we find:
> 
> $$
> 5(2x + 5) + 2 \equiv 2x + 4 \pmod{6}
> $$
> 
> $$
> 8x + 23 \equiv 0 \pmod{6}
> $$
> 
> $$
> 2x \equiv 1 \pmod{6}
> $$
> 
> This has no solutions. One way to think about it is that for something to be 1 in mod 6, it has to be an odd number. The left-hand side of this congruence will always be an even number.
> 

