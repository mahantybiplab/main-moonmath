- $\mathbb{N} = \{1,2,3,\ldots\}$ - a set of natural numbers.
- $\mathbb{N}_0 := \{0,1,2,3,\ldots\}$ - a set of all non-negative integers.
- $\mathbb{Z} = \{0, \pm 1, \pm 2, \pm 3, \ldots\}$ - a set of integers.
- $\mathbb{Q} = \{\frac{n}{m} : n \in \mathbb{Z}, m \in \mathbb{N}\}$ - a set of rational numbers.
- $\mathbb{R}$ - a set of real numbers. Examples: $2.2, -3.90.12, 1.4, -6.7, \ldots$
- $\mathbb{R}_{>0}$ - a set of positive real numbers. Examples: $2.6, 10.4, 100.2$.
- $\mathbb{C}$ - a set of complex numbers$^1$. Examples: $1 + 2i, 5i, -7 - 5.7i, \ldots$

**Key Sage Notations:**
- `ZZ` - Integer Ring ($\mathbb{Z}$)
- `NN` - Non-negative integer semiring ($\mathbb{N}_0$)
- `QQ` - Rational Field ($\mathbb{Q}$)
- `RR` - Real Field ($\mathbb{R}$)
- `CC` - Complex Field ($\mathbb{C}$)

We use $\mathbb{P}$ for the set of all prime numbers and $\mathbb{P}_{\ge 3}$ for the set of all odd prime numbers.

### Fundamental Theorem of Arithmetic

> [!done]- **Theorem: Fundamental Theorem of Arithmetic**
> Every integer $n > 1$ can be represented as the product of prime numbers in a way that is **unique** (up to the order of the factors).
> 
> $$
> n = p_1^{e_1} \cdot p_2^{e_2} \cdots p_k^{e_k} = \prod_{i=1}^{k} p_i^{e_i}
> $$
> 
> Where:
> * $p_i$ are distinct prime numbers.
> * $e_i \ge 1$ are positive integers (exponents).


$$
\begin{align}
\textbf{Polynomial Time (P)}: \quad & T(n) = O(n^k) \quad \text{where } k \text{ is a constant.} \\
& \text{Examples: } O(n), O(n^2), O(n \log n) \\
\ \\
\textbf{Non-Polynomial Time}: \quad & T(n) = O(k^n) \quad \text{or} \quad O(n!) \\
& \text{Examples: } O(2^n), O(3^n), O(n!)
\end{align}
$$


#### ❓ The Problem
> [!question] Statement
> For $2x^3 - x^2 - 2x = -1$, compute the set of all solutions for $x$ under the alternative assumptions:
> - equation is defined over set of natural numbers
> - equation is defined over set of integers
> - equation is defined over set of rational numbers

> [!done]- Solution
> With a quick manipulation, we can see that $(2x)(x^2 - 1) = x^2 - 1$. With this form $x=1$ and $x=-1$ is a solution.
> 
> We can also find an $x$ such that $|x| \ne 1$ by dividing both sides by $x^2 - 1$, and obtain $2x=1$ to find $x=1/2$. The sets of solutions are thus:
> 
> - $\{1\} \in \mathbb{N}$
> - $\{1, -1\} \in \mathbb{Z}$
> - $\{1, -1, 1/2\} \in \mathbb{Q}$

### **Euclidean Division**
Let $a \in \mathbb{Z}$ and $b \in \mathbb{Z}$ be two integers with $b \neq 0$. Then there is always another integer $m \in \mathbb{Z}$ and a non negative integer $r \in \mathbb{N}_0$, with $0 \leq r < |b|$ such that the following holds:
$$
a = m \cdot b + r \tag{3.7}
$$

This decomposition of *a* given *b* is called **Euclidean Division**, where *a* is called the **dividend**,
*b* is called the **divisor**, *m* is called the **quotient** and *r* is called the **remainder**.

$$−17 = −5·4+3$$
$$−17 = 5 · (−4) + 3$$


Let $a, b \in \mathbb{Z}$ with $b \neq 0$. We say that $b$ divides $a$, written as $b \mid a$, if there exists an integer $m \in \mathbb{Z}$ such that: $$ a = b \cdot m $$
a div b $:=$ m, a mod b $:=$ r 

If we look at the equation $a=b⋅m$ :
- **b** is the **Divisor** (or Factor).
- **m** (which is $a$ *div* $b$) is the **Cofactor**.

#### ❓ The Problem
> [!question] Statement
> Find an $m \in \mathbb{Z}$ and an $r \in \mathbb{N}$ with $0 \leq r < |b|$ such that $a = mb + r$ holds for the following pairs:
>
> 1. $(a, b) = (27, 5)$
> 2. $(a, b) = (-27, 5)$
> 3. $(a, b) = (127, 0)$
> 4. $(a, b) = (-1687, 11)$
> 5. $(a, b) = (0, 7)$
>
> In which cases are your solutions unique?

> [!done]- Solution
> 
> 1. $m = 5, r = 2$
> 2. $m = -5, r = 2$
> 3. No solutions possible because we get $0 \leq r < 0$ due to $b = 0$.
> 4. $m = -154, r = 7$, which we find by solving for $(1687, 11)$ first.
> 5. $m = 0, r = 0$.
> 
> All solutions are unique.
> 


```rust
fn int_long_division(dividend: i64, divisor: i64) -> (i64, u64) {
    if divisor == 0 {
        panic!("Division by zero");
    }

    let mut carry: i64 = 0;
    let mut quotient: i64 = 0;

    for digit in dividend.to_string().chars().map(|c| c.to_digit(10).unwrap() as i64) {
        carry = carry * 10 + digit;
        quotient *= 10;
        
        while carry >= divisor {
            carry -= divisor;
            quotient += 1;
        }
    }

    (quotient, carry as u64)
}
```

```rust
fn main () {
    let mut rng = rand::thread_rng();
    let numbers: Vec<u64> = (0..100).map(|_| rng.gen_range(1..10000000)).collect();

    for dividend in numbers {
        let divisor = rng.gen_range(1..10000000);
        let (q,r) = int_long_division(dividend as i64, divisor as i64);
        
        println!("{} / {} = {} with reminder {}", dividend, divisor, q, r);
        
        assert_eq!(dividend as i64, q * divisor as i64 + r as i64);
    }
}
```

```rust
fn binary_rep(n: i32) -> String {
    let mut n = n;
    let mut digits = Vec::new();

    if n == 0 {
        return "0".to_string();
    }

    while n > 0 {
        digits.push((n & 1).to_string()); // n % 2
        n >>= 1; // n / 2
    }

    digits.reverse()
    digits.join("")
}
```

### The Extended Euclidean Algorithm

Extended Euclidean Algorithm, which is a method for calculating the greatest common divisor of two natural numbers $a$ and $b \in \mathbb{N}$, as well as two additional integers $s, t \in \mathbb{Z}$, such that the following equation holds:

$$\gcd(a,b) = s \cdot a + t \cdot b \tag{3.12}$$


 **Definition: Coprime Numbers**

Let $a, b \in \mathbb{Z}$. We say that $a$ and $b$ are **coprime** (or **relatively prime**) if:

$$\gcd(a,b) = 1$$
We write $a \perp b$ to denote that $a$ and  $b$ are coprime.

**Notation:** $a \perp b \iff \gcd(a,b) = 1$ ; 


#### ❓ The Problem
> [!question] Statement
>Find all numbers $k \in \mathbb{N}$ with $0 \leq k \leq 100$ such that $\gcd(100, k) = 5$.

> [!done]- Solution
> We begin by reducing the GCD:
> 
> $$
> \gcd(5 \times 20, 5 \times k') = 5 \implies \gcd(20, k') = 1
> $$
> 
> From this, we simply list out all the coprimes with 20:
> 
> $$
> k' \in \{19, 17, 13, 11, 9, 7, 3, 1\}
> $$
> 
> Our solutions for $k$ is therefore these numbers multiplied by 5:
> 
> $$
> k \in \{95, 85, 65, 55, 45, 35, 15, 5\}
> $$
> 
> 

#### ❓ The Problem

> [!question] Statement
>  Show that $\gcd(n, m) = \gcd(n + m, m)$ for all $n, m \in \mathbb{N}$.

> [!done]- Solution
> **Theorem:** For all $n, m \in \mathbb{N}$, prove that $\gcd(n, m) = \gcd(n + m, m)$.
> 
> **Proof:**
> 
> Let $g = \gcd(n, m)$. By the definition of GCD:
> 1. $g \mid n$ and $g \mid m$.
> 2. We can write $n = g n'$ and $m = g m'$, where $\gcd(n', m') = 1$.
> 
> Now, substitute these into the expression for $\gcd(n + m, m)$:
> 
> $$
> \begin{aligned}
> \gcd(n + m, m) &= \gcd(g n' + g m', g m') \\
> &= \gcd(g(n' + m'), g m') \\
> &= g \cdot \gcd(n' + m', m') \quad \text{(Distributive property)}
> \end{aligned}
> $$
> 
> **Lemma:** If $\gcd(n', m') = 1$, then $\gcd(n' + m', m') = 1$.
> 
> *Proof of Lemma:*
> Let $d = \gcd(n' + m', m')$.
> * By definition, $d \mid (n' + m')$ and $d \mid m'$.
> * It follows that $d$ divides their difference: $(n' + m') - m' = n'$.
> * So, $d$ is a common divisor of $n'$ and $m'$.
> * Since we know $\gcd(n', m') = 1$, the only common divisor is $1$.
> * Therefore, $d = 1$.
> 
> Returning to the main equation:
> 
> $$
> \begin{aligned}
> \gcd(n + m, m) &= g \cdot \gcd(n' + m', m') \\
> &= g \cdot 1 \\
> &= g \\
> &= \gcd(n, m)
> \end{aligned}
> $$

> [!done]- **Theorem (Distributive Property of GCD):**
> For integers $k, a, b$, prove that $\gcd(ka, kb) = |k| \gcd(a, b)$.
> 
> **Proof:**
> 
> Let $g = \gcd(a, b)$.
> By definition, we can write $a$ and $b$ as multiples of $g$:
> 1. $a = g x$
> 2. $b = g y$
> 3. Where $\gcd(x, y) = 1$ (they share no other factors).
> 
> Now, substitute these into the expression $\gcd(ka, kb)$:
> 
> $$
> \begin{aligned}
> \gcd(ka, kb) &= \gcd(k(gx), k(gy)) \\
> &= \gcd(kg \cdot x, kg \cdot y)
> \end{aligned}
> $$
> 
> We are looking for the greatest common divisor of $(kg)x$ and $(kg)y$.
> * We can see that $kg$ is a **common divisor** of both terms.
> * The remaining parts are $x$ and $y$.
> * Since $\gcd(x, y) = 1$, there are no *other* common factors hiding inside $x$ and $y$ that we missed.
> 
> Therefore, the **greatest** common divisor is exactly $kg$.
> 
> $$
> \begin{aligned}
> \gcd(ka, kb) &= kg \\
> &= k \cdot \gcd(a, b)
> \end{aligned}
> $$
> 


### Integer Representations

**decimal positional system** : $\left\{0,1,2,\dots,9\right\}$
**binary positional system** : represents every integer as a sequence of elements from the set of binary digits (or bits) $\{0, 1\}$ .

### Binary Representation of Non-negative Integers

The **binary positional system** (binary representation) expresses every non-negative integer as a sequence of binary digits (bits) from the set $\{0, 1\}$. 

More precisely:
Let $n \in \mathbb{N}_0$ be a non-negative integer (in decimal) and let $b = b_{k-1} b_{k-2} \dots b_1 b_0$ be a finite sequence of bits $b_j \in \{0,1\}$ for some positive integer $k \in \mathbb{N}$.

Then $b$ is called the **binary representation** of $n$ if and only if

$$
n = \sum_{j=0}^{k-1} b_j \cdot 2^j \tag{3.13}
$$

In this case we write

$$
\operatorname{Bits}(n) := b_{k-1}b_{k-2}\dots b_1 b_0
$$

and say that $n$ is a **$k$-bit number**.

The number $k$ is called the **bit length** (or binary length) of $n$ and is commonly denoted

$$
k := |n|_2
$$

#### Most common modern notation summary

$$
\begin{aligned}
n &\in \mathbb{N}_0 \\
b_j &\in \{0,1\} \\
n &= \sum_{j=0}^{k-1} b_j \, 2^j \\
k &= |n|_2 = \lfloor \log_2 (n+1) \rfloor \quad \text{(or } \lfloor \log_2 n \rfloor + 1 \text{ for } n > 0\text{)}
\end{aligned}
$$

**Note:** The notation $|n|_2$ for bit length is very common in theoretical computer science and algorithm analysis.

We call $b_0$ the **least significant bit** and $b_{k−1}$ the **most significant bit** and define the **Hamming weight** of an integer as the number of *1s* in its binary representation.

### Hexadecimal positional system

**Hexadecimal positional system** :  which represents every integer as a sequence of elements from a set of 16 digits usually written as $\{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, a, b, c, d, e, f\}$.

### Positional Number System – Quick Reference

Base / Radix:          $k$

Digit set:             $\{0, 1, \dots, k-1\}$

Number in base $k$:    $d_h d_{h-1} \dots d_1 d_0$

Decimal value:  
$$
n = \sum_{i=0}^{h} d_i \cdot k^i \tag{3.14}
$$

Most important compact forms:

$$
n = d_h k^h + d_{h-1} k^{h-1} + \cdots + d_1 k + d_0
$$

$$
n = \sum_{i=0}^{h} d_i \, k^i \qquad d_i \in \{0,1,\dots,k-1\}
$$

Special cases:

- Binary ($k=2$):          $d_i \in \{0,1\}$
- Decimal ($k=10$):        $d_i \in \{0,1,\dots,9\}$
- Hex ($k=16$):            $d_i \in \{0,1,\dots,9,A,\dots,F\}$

Rightmost digit = units ($k^0$), leftmost = highest power ($k^h$)
