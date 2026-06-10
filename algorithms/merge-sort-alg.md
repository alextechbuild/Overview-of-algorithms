
Definition of the left-truncation function (fonction de troncature à gauche) $\pi^{[L]}_{1, \dots, m}$ :


$$
\begin{array}{l}
\forall n \in \mathbb{N}_{\geq 2}, \quad
\forall m \in \{1, \dots, max(1, n - 1)\}, \quad
\forall (x_{1}, \dots, x_{n}) \in \mathbb{R}^{n}, \quad
\pi^{[L]}_{1, \dots, m} : \mathbb{R}^{n} \to \mathbb{R}^{m}, \quad
(x_{1}, \dots, x_{n}) \mapsto \pi^{[L]}_{1, \dots, m}(x_{1}, \dots, x_{n}), \quad
\pi^{[L]}_{1, \dots, m}(x_{1}, \dots, x_{n})
:=
(x_{1}, \dots, x_{m})
\end{array}
$$




Definition of the right-truncation function (fonction de troncature à droite) $\pi^{[R]}_{m, \dots, n}$ :


$$
\begin{array}{l}
\forall n \in \mathbb{N}_{\geq 2}, \quad
\forall m \in \{2, \dots, n\}, \quad
\forall (x_{1}, \dots, x_{n}) \in \mathbb{R}^{n}, \quad
\pi^{[R]}_{m, \dots, n} : \mathbb{R}^{n} \to \mathbb{R}^{n - m + 1}, \quad
(x_{1}, \dots, x_{n}) \mapsto \pi^{[R]}_{m, \dots, n}(x_{1}, \dots, x_{n}), \quad
\pi^{[R]}_{m, \dots, n}(x_{1}, \dots, x_{n})
:=
(x_{m}, \dots, x_{n})
\end{array}
$$




Definition of the concatenation function of two $n$-tuples of real numbers $cat$ :


$$
\begin{array}{l}
\forall n, m \in \mathbb{N}_{\geq 1}, \quad
\forall (a_{1}, \dots, a_{n}) \in \mathbb{R}^{n}, \quad
\forall (b_{1}, \dots, b_{m}) \in \mathbb{R}^{m}, \quad
cat : \mathbb{R}^{n} \times \mathbb{R}^{m} \to \mathbb{R}^{n + m}, \quad
cat\Big(
(a_{1}, \dots, a_{n}), 
(b_{1}, \dots, b_{m})
\Big)
:=
(a_{1}, \dots, a_{n}, b_{1}, \dots, b_{m})
\end{array}
$$




Definition of the properties of the merge sort algorithm :




- If $\lfloor \frac{\gamma}{2^{s}} \rfloor$ is even, then the number of blocks of size $2^{s}$ is even

- If $\lfloor \frac{\gamma}{2^{s}} \rfloor$ is odd, then the number of blocks of size $2^{s}$ is odd

- More generally, if $\lfloor \frac{\gamma}{2^{s - 1}} \rfloor = 2 \xi + 1$ (= if the number of blocks of size $2^{s - 1}$ is odd), then :
	
	- $\lfloor \frac{\gamma}{2^{s - 1}} \rfloor$ denotes the index of the last block of size $2^{s-1}$ that has not been paired with the penultimate block of size $2^{s-1}$ (since all other blocks of size $2^{s-1}$ 
	  (with the exception of the last block of size $2^{s-1}$) have already been paired between themselves two by two)
	
	- $\lfloor \frac{\gamma}{2^{s}} \rfloor$ denotes the index of the last block of size $2^{s}$ that has been paired with the penultimate block of size $2^{s}$ (meaning that all other blocks of size $2^{s}$ 
	  are paired between themselves two by two)

    (See "Diagram 1 of part 26 to 28" and "Diagram 1 of part 29 and 31")




$$
\begin{array}{l}
\begin{cases}
\text{def } Merge(T_{1}, T_{2}) :
\\[1em]
\quad
n := Card\Big(
\Big\{
a_{(1)}, 
a_{(2)}, 
\dots, 
a_{(n - 1)}, 
a_{(n)}
\Big\}
\Big)
\\[1em]
\quad
m := Card\Big(
\Big\{
b_{(1)}, 
b_{(2)}, 
\dots, 
b_{(m - 1)}, 
b_{(m)}
\Big\}
\Big)
\\[1em]
\quad
S_{4} := \emptyset
\\[1em]
\quad
T_{4} := ()
\\[1em]
\quad
\alpha := 1
\\[1em]
\quad
\beta := 1
\\[1em]
\quad
\text{while } \alpha \leq n \text{ and } \beta \leq m :
\\[1em]
\quad
\quad \quad
\text{If } a_{(\alpha)} \leq b_{(\beta)} :
\\[1em]
\quad
\quad \quad \quad \quad
S_{4} := S_{4} \ \cup \ \{ a_{(n)} \}
\\[1em]
\quad
\quad \quad \quad \quad
T_{4} := cat(T_{4}, (a_{(n)}))
\\[1em]
\quad
\quad \quad \quad \quad
\alpha := \alpha + 1
\\[1em]
\quad
\quad \quad
\text{Else} :
\\[1em]
\quad
\quad \quad \quad \quad
S_{4} := S_{4} \ \cup \ \{ b_{(m)} \}
\\[1em]
\quad
\quad \quad \quad \quad
T_{4} := cat(T_{4}, (b_{(m)}))
\\[1em]
\quad
\quad \quad \quad \quad
\beta := \beta + 1
\\[1em]
\quad
S_{4}
:=
S_{4}
\ \cup \
\{ a_{(\alpha)}, \dots, a_{(n)} \}
\ \cup \
\{ b_{(\beta)}, \dots, b_{(m)} \}
\\[1em]
\quad
T_{4}
:=
cat\Big(
cat\Big(
T_{4}, (a_{(\alpha)}, \dots, a_{(n)})
\Big)
, 
(b_{(\beta)}, \dots, b_{(m)})
\Big)
\\[1em]
\quad
\text{return } (S_{4}, T_{4})
\\[2em]
T_{1}
:=
\Big(
a_{(1)}, 
a_{(2)}, 
\dots, 
a_{(n - 1)}, 
a_{(n)}
\Big)
\\[1em]
T_{2}
:=
\Big(
b_{(1)}, 
b_{(2)}, 
\dots, 
b_{(m - 1)}, 
b_{(m)}
\Big)
\\[1em]
Merge(T_{1}, T_{2})
\end{cases}
\\[1em]
\hspace{700pt}
\end{array}
$$




Algorithm main properties :


- Each notation of the type $(P1)$, $(P2)$, etc., refers to one property of the algorithm

$$
\begin{array}{l}
\begin{cases}
(P1) \quad
\left(
\begin{cases}
\ \
\forall n, m \in \mathbb{N}_{\geq 1}, \quad
\exists! {\iota}_{max_{(1)}} \in \mathbb{N}, \quad
\forall {\iota}_{(1)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\alpha : \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\} \to S_{3}(n, m), \quad
{\iota}_{(1)} \mapsto \alpha({\iota}_{(1)}), \quad
{\alpha}^{-1} : S_{3}(n, m) \to \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\alpha \mapsto {\iota}_{(1)}(\alpha), \quad
\\[1em]
\quad
\exists! {\iota}_{max_{(2)}} \in \mathbb{N}, \quad
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\beta : \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\} \to S_{3}(n, m), \quad
{\iota}_{(2)} \mapsto \beta({\iota}_{(2)}), \quad
{\beta}^{-1} : S_{3}(n, m) \to \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\beta \mapsto {\iota}_{(2)}(\beta), \quad
\\[1em]
\quad
V : S_{3}(n, m) \to S_{3}(n, m), \quad
(\alpha, \beta) \mapsto V(\alpha, \beta), \quad
G : S_{3}(n, m) \to S_{3}(n, m), \quad
(\alpha, \beta) \mapsto G(\alpha, \beta), \quad
\boxed{
\Bigg(
\ \
V(\alpha, \beta)
=
max\Big(
0, 
min\Big(
\lfloor n + 1 - \alpha \rfloor, \ 
\lfloor m + 1 - \beta \rfloor
\Big)
\Big)
\ \
\Bigg)
}
\land
\Bigg(
\ \
\Bigg(
\bigg(
G(\alpha, \beta)
=
min\Big(
-\alpha, -\beta
\Big)
\bigg)
\iff
\bigg(
\Big(
G(\alpha, \beta) \leq -\alpha
\land
G(\alpha, \beta) \leq -\beta
\Big)
\land
\Big(
G(\alpha, \beta) = -\alpha
\lor
G(\alpha, \beta) = -\beta
\Big)
\bigg)
\Bigg)
\Rightarrow
\boxed{
\Bigg(
G \text{ is linear}
\Bigg)
}
\ \
\Bigg)
\land
\Bigg(
\ \
V(\alpha, \beta)
\in
\underbrace{
\Big\{
V(\alpha, \beta)
\ \Big| \
\Big(
\exists \gamma \in \mathbb{R}_{>0}, \quad
\exists \alpha_{(0)}, \beta_{(0)} \in \mathbb{N}_{>0}, \quad
\forall \alpha \geq \alpha_{(0)}, \quad
\forall \beta \geq \beta_{(0)}, \quad
|V(\alpha, \beta)|
\leq
\gamma
\times
|G(\alpha, \beta)|
\Big)
\Big\}
}_{\boxed{\mathcal{O}(|G(\alpha, \beta)|) \ = \ \mathcal{O}(|min(-\alpha, -\beta)|)}}
\bigg)
\ \
\Bigg)
\end{cases}
\right)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P2) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists d_{(1)}, d_{(2)}, \dots, d_{(\gamma - 1)}, d_{(\gamma)} \in \mathbb{R}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists B_{s}, R_{s} \subseteq S_{5}, \quad
\forall \zeta \in \{1, \dots, \lfloor \frac{\gamma}{2^{s}} \rfloor\}, \quad
\exists B_{(\zeta, s)} \subset S_{5}, \quad
\bigg(
0 \leq \gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s} < 2^{s}
\bigg)
\land
\left(
S_{5}
=
\Big\{
d_{(1)}, 
\dots,  
d_{(\gamma)}
\Big\}
=
\underbrace{
\Big\{
d_{(1)}, \dots, d_{\boxed{(\lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s})}}
\Big\}
}_{\boxed{B_{s}}}
\ \cup \
\underbrace{
\Big\{
d_{\boxed{(\lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s} + 1)}}, \dots, d_{(\gamma)}
\Big\}
}_{\boxed{R_{s}}}
=
\left(
\overset{ \boxed{\lfloor \frac{\gamma}{2^{s}} \rfloor} }{\underset{\zeta = 1}{\bigcup}}{
\underbrace{
\left(
\overset{2^{s}}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot 2^{s} + \tau)}
\Big\}
}
\right)
}_{
\boxed{
B_{(\zeta, s)}
}
}
}
\right)
\ \cup \
\left(
\overset{ \boxed{\gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s}} }{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{\boxed{(\lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s} + \phi)}}
\Big\}
}
\right)
=
\underbrace{
\left(
\overset{ \boxed{\lfloor \frac{\gamma}{2^{s}} \rfloor} }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, s)}
}
\right)
}_{
\boxed{B_{s}}
}
\ \cup \
R_{s}
\right)
\right)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P3) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! (q, r) \in \mathbb{N}^{2}, \quad
\bigg(
q
=
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
\bigg)
\land
\bigg(
L
=
\boxed{
2^{s}
}
\bigg)
\land
\overbrace{
\bigg(
\gamma
=
\underbrace{
L + L + \dots + L
}_{q \text{ times}}
+
r
=
q \cdot L + r
\bigg)
\land
\bigg(
0 \leq r < |L|
\bigg)
}^{
\forall x \in \mathbb{Z}, \quad
\forall n \in \mathbb{Z}_{>0}, \quad
\exists! (q,r) \in \mathbb{Z}^{2}, \quad
\big(
x = q \times n + r
\big)
\land
\big(
0 \leq r < |n|
\big)
\text{ form}
}
\land
\bigg(
r
=
\gamma
-
q \cdot 2^{s}
\bigg)
\right)
\\[1em]
(P4) \quad
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! (q, r) \in \mathbb{N}^{2}, \quad
\exists B_{s}, R_{s} \subseteq S_{5}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\exists B_{(\zeta, s)} \subset S_{5}, \quad
\bigg(
Card(B_{s}) = q \cdot L
\bigg)
\land
\bigg(
Card(B_{(\zeta, s)}) = L
\bigg)
\land
\bigg(
0 \leq Card(R_{s}) < L
\bigg)
\land
\bigg(
Card(R_{s}) = r
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P5) \quad
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall \mu \in \{1, \dots, \underbrace{\lfloor \frac{\gamma}{2^{0}} \rfloor}_{\boxed{\gamma}} \}, \quad
\exists d_{(\mu)} \in \mathbb{R}, \quad
\exists! \lambda_{(\mu, 0)} \in \mathbb{R}^{1}, \quad
\exists! \Lambda_{0} \in \mathbb{R}^{0}, \quad
\bigg(
\lambda_{(\mu, 0)}
=
(d_{(\mu)})
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{0}
:=
()
\bigg)
}_{
\substack{
{
\text{Trivially sorted } 0 \text{-tuple}
}
\\
{
\text{associated to } R_{0}
}
}
}
\Bigg)
\\[1em]
(P6) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\forall \Omega \in \{1, \dots, \varrho\}, \quad
\forall \varphi \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{(\Omega)}} \rfloor} \}, \quad
\exists! \zeta \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{(\Omega)}} \rfloor} \}, \quad
\boxed{\exists! \lambda_{(\zeta, \quad \Omega)} \in \mathbb{R}^{\boxed{2^{(\Omega)}}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{(\Omega)} - 1\}, \quad
\boxed{\exists! \Lambda_{(\Omega)} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{(\Omega)}) < 2^{(\Omega)}
}
, \quad
\exists B_{\Omega} \subseteq S_{5}, \quad
\begin{cases}
\Bigg(
\bigg(
B_{\Omega}
\neq
\emptyset
\bigg)
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{(\Omega) - 1}} \rfloor
=
\boxed{
2 \xi
}
\bigg)
\Bigg)
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\lambda_{(\zeta, \quad \Omega)}
=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega - 1)}, \lambda_{(2 \varphi, \quad \Omega - 1)})
\Big)
\bigg)
}_{
\text{Sorted } (2^{(\Omega)}) \text{-tuple}
}
\land
\underbrace{
\bigg(
\Lambda_{(\Omega)}
=
\Lambda_{(\Omega - 1)}
\bigg)
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{(\Omega)} - 1
}
\Bigg)
\\[1em]
\Bigg(
\bigg(
B_{\Omega}
\neq
\emptyset
\bigg)
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{(\Omega) - 1}} \rfloor
=
\boxed{
2 \xi + 1
}
\bigg)
\Bigg)
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\lambda_{(\zeta, \quad \Omega)}
=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega - 1)}, \lambda_{(2 \varphi, \quad \Omega - 1)})
\Big)
\bigg)
}_{
\text{Sorted } (2^{(\Omega)}) \text{-tuple}
}
\land
\underbrace{
\bigg(
\Lambda_{(\Omega)}
=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{(\Omega - 1)}} \rfloor, \quad \Omega - 1)}}}, \Lambda_{(\Omega - 1)})
\Big)
\bigg)
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{(\Omega)} - 1
}
\Bigg)
\end{cases}
\right)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P7) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\forall \Omega \in \{1, \dots, \varrho\}, \quad
\exists! \lambda_{(1, \quad \Omega)}, \lambda_{(2, \quad \Omega)}, \dots, \lambda_{(\lfloor \frac{\gamma}{2^{\Omega}} \rfloor, \quad \Omega)} \in \mathbb{R}^{\boxed{2^{(\Omega)}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{(\Omega)} - 1\}, \quad
\boxed{\exists! \Lambda_{(\Omega)} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{(\Omega)}) < 2^{(\Omega)}
}
, \quad
\Bigg(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega)}
, 
\lambda_{(2, \quad \Omega)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega}} \rfloor}, \quad \Omega)}
}
,
\Lambda_{\Omega}
\Big\}
\quad
\text{ contains sorted tuples}
\Bigg)
\land
\Bigg(
\varrho
=
min\Big(
\Big\{
s
\ \Big| \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Big\}
\Big)
\Bigg)
\right)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P8) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\exists! \lambda_{(\zeta, \quad \varrho - 1)} \in \mathbb{R}^{\boxed{2^{(\varrho - 1)}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{(\varrho - 1)} - 1\}, \quad
\boxed{\exists! \Lambda_{(\varrho - 1)} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{(\varrho - 1)}) < 2^{(\varrho - 1)}
}
, \quad
\exists! \Gamma \in \mathbb{R}^{Card(S_{5})}, \quad
\exists! \Gamma_{1}, \dots, \Gamma_{(\gamma)} \in S_{5}, \quad
\boxed{
\Bigg(
\Gamma
=
\pi^{[R]}_{2, \dots, 2}\bigg(
Merge\Big(
\lambda_{(1, \quad \varrho - 1)}, \Lambda_{(\varrho - 1)}
\Big)
\bigg)
=
(
\Gamma_{1}, \dots, \Gamma_{(\gamma)}
)
\Bigg)
}
\land
\boxed{
\Bigg(
\Gamma
\text{ is the tuple representing the sorted version of the set } S_{5}
\Bigg)
}
\land
\Bigg(
\varrho
=
min\Big(
\Big\{
s
\ \Big| \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Big\}
\Big)
\Bigg)
\right)
\end{cases}
\end{array}
$$




Proof of the algorithm properties :

Part 1 :

- From part 1 to part 12, we build (first by recurrence and then by algorithm) a "final sorted tuple" (sorted in ascending order) from two already sorted tuples (sorted in ascending order). 
  This "final sorted tuple" is composed of all the elements of the two already sorted tuples. 
  Then, we examine the function $G$ associated to the growth rate $\mathcal{O}(G(N))$ of the algorithm. If $G$ is linear, then, in the following parts, we will examine if the principle of building such 
  a "final sorted tuple" (with such a growth rate) can be reused. Indeed, if $G$ is linear, then the total number of operations is linear and makes the algorithm efficient

	- From part 1 to part 9, we build (by recurrence) the $\boxed{\text{first version}}$ of the "final sorted tuple" from the two already sorted tuples :

		- 1. We take the leftmost element of $T_{1}$ (which we will call "EG1") that has not yet been examined, and the leftmost element of $T_{2}$ (which we will call "EG2") that has not yet been 
		  examined

		- 2. If "EG1" is exactly less than "EG2", then "EG1" is added to the very right in $T_{4}$ (using the concatenation function $cat$), and :

			- this "EG1" is no longer examined
			- $T_{1}$ is called the “current starting tuple”
			- We move on directly to the step 4

		- 3. If "EG2" is greater than or equal to "EG1", then "EG2" is added to the very right in $T_{4}$ (using the concatenation function $cat$), and :

			- this "EG2" is no longer examined
			- $T_{2}$ is called the “current starting tuple”
			- We move on directly to the step 4

		- 4. In the "current starting tuple", we start again from step 1 until there are no more elements to examine in $T_{1}$ or $T_{2}$ 


		- " until there are no more elements to examine in $T_{1}$ or $T_{2}$ " is equivalent to " as long as there are elements to examine in $T_{1}$ or $T_{2}$ "


- $T_{1}$ and $T_{2}$ are the two initial sorted tuples used to build the "final sorted tuple"

- $T_{4}$ is the "final sorted tuple" that is built from $T_{1}$ and $T_{2}$ 


- For illustrative purposes, we can also examine, in the comments in the following parts, the indices of the arguments of the min function when $c_{(1)} = a_{(1)}$ 
  (and $c_{(1)} = a_{(1)}$ will be arbitrary referred to as "branch 1")

- For $c_{1}$, since there is an unique combination of arguments for the $min$ function (see "Summary" in this part), we can generalize it into a general pair $(\alpha_{(1)}, \beta_{(1)})$ 

$$
\begin{array}{l}
\forall n, m \in \mathbb{N}_{\boxed{\geq 1}}, \quad
\exists a_{(1)}, a_{(2)}, \dots, a_{(n - 1)}, a_{(n)}, b_{(1)}, b_{(2)}, \dots, b_{(m - 1)}, b_{(m)} \in \mathbb{R}, \quad
\exists! S_{1}, S_{2}, S_{3} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\exists! T_{1} \in \mathbb{R}^{n}, \quad
\exists! T_{2} \in \mathbb{R}^{m}, \quad
\exists! T_{4} \in \mathbb{R}^{n + m}, \quad
\Bigg(
\bigg(
S_{1}
:=
\Big\{
a_{(1)}, 
a_{(2)}, 
\dots, 
a_{(n - 1)}, 
a_{(n)}
\Big\}
\bigg)
\land
\bigg(
T_{1}
:=
(
a_{(1)}, 
a_{(2)}, 
\dots, 
a_{(n - 1)}, 
a_{(n)}
)
\bigg)
\land
\bigg(
a_{(1)}
<
a_{(2)}
<
\dots
<
a_{(n - 1)}
<
a_{(n)}
\bigg)
\land
\bigg(
S_{2}
:=
\Big\{
b_{(1)}, 
b_{(2)}, 
\dots, 
b_{(m - 1)}, 
b_{(m)}
\Big\}
\bigg)
\land
\bigg(
T_{2}
:=
(
b_{(1)}, 
b_{(2)}, 
\dots, 
b_{(m - 1)}, 
b_{(m)}
)
\bigg)
\land
\bigg(
b_{(1)}
<
b_{(2)}
<
\dots
<
b_{(m - 1)}
<
b_{(m)}
\bigg)
\land
\underbrace{
\bigg(
\ \
S_{3}(n, m)
:=
\begin{cases}
m < n
\Rightarrow
S_{3}(n, m)
=
\{1, \dots, m\}
\\[1em]
m \geq n
\Rightarrow
S_{3}(n, m)
=
\{1, \dots, n\}
\end{cases}
\ \
\bigg)
}_{
\text{We sort only on all the length of the shorter set (which is either } S_{1} \text{ or } S_{2} \text{ )}
}
\land
\bigg(
T_{4}
:=
()
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\eta_{0} := 1
\Bigg)
\\[1em]
\Rightarrow
\left(
\exists c_{1} \in \mathbb{R}, \quad
\left(
\ \
c_{(1)}
:=
\begin{cases}
\bigg(
a_{(1)} < b_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(1)} = a_{(1)}
\bigg)
\\[1em]
\bigg(
a_{(1)} \geq b_{(1)}
\iff
b_{(1)} \leq a_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(1)} = b_{(1)}
\bigg)
\end{cases}
\ \
\right)
\Rightarrow
\underbrace{
\left(
\ \
c_{(1)}
=
min\Big(
\underbrace{
a_{(1)}, b_{(1)}
}_{
\text{Unique combination}
}
\Big)
=
\begin{cases}
\bigg(
a_{(1)} < b_{(1)}
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(1)} = a_{(1)}
}
=
min\Big(
\boxed{
a_{(1)}, b_{(1)}
}
\Big)
\bigg)
\\[1em]
\bigg(
b_{(1)} \leq a_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(1)} = b_{(1)}
=
min\Big(
a_{(1)}, b_{(1)}
\Big)
\bigg)
\end{cases}
\ \
\right)
}_{
\boxed{
\text{Summary}
}
}
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(1)}, \beta_{(1)} \in S_{3}(n, m), \quad
\boxed{
\bigg(
c_{(1)}
=
min\Big(
a_{(\alpha_{(1)})}, 
b_{(\beta_{(1)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < \dots < a_{(n)}
\land
c_{(1)} < \dots < b_{(m)}
\bigg)
\land
\bigg(
T_{4}
:=
cat\Big(
(), 
(c_{(1)})
\Big)
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 1 :

$$
\begin{array}{l}
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m < n
\\[1em]
\hline
a_{(1)} & < & a_{(2)} & < & a_{(3)} & < & \dots & < & a_{(m - 1)} & < & a_{(m)} & < & \dots & < & a_{(n)}
\\[2em]
< &  & < &  & < &  & \dots &  & < &  & <
\\[2em]
b_{(1)} & < & b_{(2)} & < & b_{(3)} & < & \dots & < & b_{(m - 1)} & < & b_{(m)}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m \geq n
\\[1em]
\hline
a_{(1)} & < & a_{(2)} & < & a_{(3)} & < & \dots & < & a_{(n - 1)} & < & a_{(n)}
\\[2em]
< &  & < &  & < &  & \dots &  & < &  & <
\\[2em]
b_{(1)} & < & b_{(2)} & < & b_{(3)} & < & \dots & < & b_{(n - 1)} & < & b_{(n)} & < & \dots & < & b_{(m)}
\\[1em]
\hline
\end{array}
\end{array}
$$

Diagram 2 of part 1 :

$$
\begin{array}{l}
\begin{array}{|c|c|}
\hline
/ & m < n
\\[1em]
\hline
c_{(1)} = a_{(1)}
&
\begin{array}{l}
\boxed{a_{(1)}} < a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
\boxed{a_{(1)}} < b_{(1)} < b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(1)} = b_{(1)}
&
\begin{array}{l}
\boxed{b_{(1)}} \leq a_{(1)} < a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
\boxed{b_{(1)}} < b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|c|c|}
\hline
/ & m \geq n
\\[1em]
\hline
c_{(1)} = a_{(1)}
&
\begin{array}{l}
\boxed{a_{(1)}} < a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
\boxed{a_{(1)}} < b_{(1)} < b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(1)} = b_{(1)}
&
\begin{array}{l}
\boxed{b_{(1)}} \leq a_{(1)} < a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
\boxed{b_{(1)}} < b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Diagram 3 of part 1 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
m < n
\\[1em]
\hline
\begin{array}{l}
\boxed{c_{(1)}} < \dots < a_{(n)}
\\[1em]
\boxed{c_{(1)}} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|c|}
\hline
m \geq n
\\[1em]
\hline
\begin{array}{l}
\boxed{c_{(1)}} < \dots < a_{(n)}
\\[1em]
\boxed{c_{(1)}} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Part 2 :

- Starting from "branch 1" and examining the indices of the arguments of the min function when $c_{(2)} = a_{(2)}$ ($c_{(2)} = a_{(2)}$ will be arbitrary referred to as "branch 1 of branch 1"), 
  we observe that an index progression takes place in $S_{1}$ (because it goes from $a_{(1)}$ (when $c_{(1)} = a_{(1)}$) to $a_{(2)}$ (when $c_{(2)} = a_{(2)}$) ) and we observe that an index stagnation takes place in $S_{2}$ 
  (because it goes from $b_{(1)}$ (when $c_{(1)} = a_{(1)}$) to $b_{(1)}$ (when $c_{(2)} = a_{(2)}$) )

- For $c_{2}$, since there are several possible combinations of arguments for the $min$ function (see "Summary" in this part), we generalize all these combinations (we "group them together") 
  into a general pair $(\alpha_{(2)}, \beta_{(2)})$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\exists c_{2} \in \mathbb{R}, \quad
\left(
\ \
c_{(2)}
:=
\begin{cases}
\overbrace{
\bigg(
\Big(
c_{(1)} = a_{(1)}
\Big)
\land
\Big(
a_{(2)} < b_{(1)}
\Big)
\bigg)
}^{
\text{Case 1}
}
\Rightarrow
\overbrace{
\bigg(
\boxed{
c_{(2)} = a_{(2)}
}
\bigg)
}^{
\text{Result for the case 1}
}
\\[1em]
\overbrace{
\bigg(
\Big(
c_{(1)} = a_{(1)}
\Big)
\land
\Big(
a_{(2)} \geq b_{(1)}
\iff
b_{(1)} \leq a_{(2)}
\Big)
\bigg)
}^{
\text{Case 2}
}
\Rightarrow
\bigg(
c_{(2)} = b_{(1)}
\bigg)
\\[1em]
\overbrace{
\bigg(
\Big(
c_{(1)} = b_{(1)}
\Big)
\land
\Big(
b_{(2)} < a_{(1)}
\Big)
\bigg)
}^{
\text{Case 3}
}
\Rightarrow
\bigg(
c_{(2)} = b_{(2)}
\bigg)
\\[1em]
\overbrace{
\bigg(
\Big(
c_{(1)} = b_{(1)}
\Big)
\land
\Big(
b_{(2)} \geq a_{(1)}
\iff
a_{(1)} \leq b_{(2)}
\Big)
\bigg)
}^{
\text{Case 4}
}
\Rightarrow
\bigg(
c_{(2)} = a_{(1)}
\bigg)
\end{cases}
\ \
\right)
\Rightarrow
\left(
\ \
c_{(2)}
=
\begin{cases}
\overbrace{
\bigg(
c_{(1)} = a_{(1)}
\land
a_{(2)} < b_{(1)}
\bigg)
}^{
\text{First case}
}
\Rightarrow
\overbrace{
\bigg(
a_{(1)} < b_{(1)}
\bigg)
}^{
\text{Property extracted from } c_{(1)} \text{ for the case 1}
}
\Rightarrow
\overbrace{
\bigg(
\boxed{
c_{(2)} = a_{(2)}
}
=
min\Big(
\boxed{
a_{(2)}, b_{(1)}
}
\Big)
\bigg)
}^{
\text{Result for the case 1}
}
\\[1em]
\bigg(
c_{(1)} = a_{(1)}
\land
b_{(1)} \leq a_{(2)}
\bigg)
\Rightarrow
\bigg(
a_{(1)} < b_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(2)} = b_{(1)}
=
min\Big(
a_{(2)}, b_{(1)}
\Big)
\bigg)
\\[1em]
\bigg(
c_{(1)} = b_{(1)}
\land
b_{(2)} < a_{(1)}
\bigg)
\Rightarrow
\bigg(
b_{(1)} \leq a_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(2)} = b_{(2)}
=
min\Big(
a_{(1)}, b_{(2)}
\Big)
\bigg)
\\[1em]
\bigg(
c_{(1)} = b_{(1)}
\land
a_{(1)} \leq b_{(2)}
\bigg)
\Rightarrow
\bigg(
b_{(1)} \leq a_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(2)} = a_{(1)}
=
min\Big(
a_{(1)}, b_{(2)}
\Big)
\bigg)
\end{cases}
\ \
\right)
\Rightarrow
\underbrace{
\left(
\ \
c_{(2)}
=
\begin{cases}
\underbrace{
\bigg(
c_{(1)} = a_{(1)}
\bigg)
}_{
\text{Current possible element of } T_{4}
}
\Rightarrow
\bigg(
c_{(2)}
=
min\Big(
\underbrace{
a_{(2)}, b_{(1)}
}_{
\text{Combination 1}
}
\Big)
\bigg)
\\[1em]
\underbrace{
\bigg(
c_{(1)} = b_{(1)}
\bigg)
}_{
\text{Current possible element of } T_{4}
}
\Rightarrow
\bigg(
c_{(2)}
=
min\Big(
\underbrace{
a_{(1)}, b_{(2)}
}_{
\text{Combination 2}
}
\Big)
\bigg)
\end{cases}
\ \
\right)
}_{
\boxed{
\text{Summary}
}
}
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(2)}, \beta_{(2)} \in S_{3}(n, m), \quad
\boxed{
\bigg(
c_{(2)}
=
min\Big(
a_{(\alpha_{(2)})}, 
b_{(\beta_{(2)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} < \dots < a_{(n)}
\land
c_{(1)} < c_{(2)} < \dots < b_{(m)}
\bigg)
\land
\bigg(
T_{4}
:=
cat\Big(
(c_{(1)}), 
(c_{(2)})
\Big)
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 2 :

$$
\begin{array}{l}
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m < n
\\[1em]
\hline
a_{(1)} & < & a_{(2)} & < & a_{(3)} & < & \dots & < & a_{(m - 1)} & < & a_{(m)} & < & \dots & < & a_{(n)}
\\[2em]
< &  & < &  & < &  & \dots &  & < &  & <
\\[2em]
b_{(1)} & < & b_{(2)} & < & b_{(3)} & < & \dots & < & b_{(m - 1)} & < & b_{(m)}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m \geq n
\\[1em]
\hline
a_{(1)} & < & a_{(2)} & < & a_{(3)} & < & \dots & < & a_{(n - 1)} & < & a_{(n)}
\\[2em]
< &  & < &  & < &  & \dots &  & < &  & <
\\[2em]
b_{(1)} & < & b_{(2)} & < & b_{(3)} & < & \dots & < & b_{(n - 1)} & < & b_{(n)} & < & \dots & < & b_{(m)}
\\[1em]
\hline
\end{array}
\end{array}
$$

Diagram 2 of part 2 :

$$
\begin{array}{l}
\begin{array}{|c|c|}
\hline
/ & m < n
\\[1em]
\hline
c_{(2)} = a_{(2)}
&
\begin{array}{l}
a_{(1)} < \boxed{a_{(2)}} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
a_{(1)} < \boxed{a_{(2)}} < b_{(1)} < b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(2)} = b_{(1)}
&
\begin{array}{l}
a_{(1)} < \boxed{b_{(1)}} \leq a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
a_{(1)} < \boxed{b_{(1)}} < b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(2)} = b_{(2)}
&
\begin{array}{l}
b_{(1)} < \boxed{b_{(2)}} < a_{(1)} < a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
b_{(1)} < \boxed{b_{(2)}} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(2)} = a_{(1)}
&
\begin{array}{l}
b_{(1)} \leq \boxed{a_{(1)}} < a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
b_{(1)} \leq \boxed{a_{(1)}} \leq b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|c|c|}
\hline
/ & m \geq n
\\[1em]
\hline
c_{(2)} = a_{(2)}
&
\begin{array}{l}
a_{(1)} < \boxed{a_{(2)}} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
a_{(1)} < \boxed{a_{(2)}} < b_{(1)} < b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(2)} = b_{(1)}
&
\begin{array}{l}
a_{(1)} < \boxed{b_{(1)}} \leq a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
a_{(1)} < \boxed{b_{(1)}} < b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(2)} = b_{(2)}
&
\begin{array}{l}
b_{(1)} < \boxed{b_{(2)}} < a_{(1)} < a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
b_{(1)} < \boxed{b_{(2)}} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(2)} = a_{(1)}
&
\begin{array}{l}
b_{(1)} \leq \boxed{a_{(1)}} < a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
b_{(1)} \leq \boxed{a_{(1)}} \leq b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Diagram 3 of part 2 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
m < n
\\[1em]
\hline
\begin{array}{l}
\boxed{c_{(1)}} < \boxed{c_{(2)}} < \dots < a_{(n)}
\\[1em]
\boxed{c_{(1)}} < \boxed{c_{(2)}} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|c|}
\hline
m \geq n
\\[1em]
\hline
\begin{array}{l}
\boxed{c_{(1)}} < \boxed{c_{(2)}} < \dots < a_{(n)}
\\[1em]
\boxed{c_{(1)}} < \boxed{c_{(2)}} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Part 3 :

- Starting from "branch 1 of branch 1" and examining the indices of the arguments of the min function when $c_{(3)} = a_{(3)}$ ($c_{(3)} = a_{(3)}$ will be arbitrary referred to as "branch 1 of branch 1 of 
  branch 1"), we observe that an index progression takes place in $S_{1}$ (because it goes from $a_{(2)}$ (when $c_{(2)} = a_{(2)}$) to $a_{(3)}$ (when $c_{(3)} = a_{(3)}$) ) and we observe that an index stagnation takes 
  place in $S_{2}$ (because it goes from $b_{(1)}$ (when $c_{(2)} = a_{(2)}$) to $b_{(1)}$ (when $c_{(3)} = a_{(3)}$) )

- We can suppose that, starting from one specific branch, for each $c$ (= $c_{1}$, etc.), index progression takes place in one specific tuple and that index stagnation takes place in the other. 
  Indeed, the index progression is associated to an index which indexes the leftmost element (that has not yet been examined) of the tuple $T_{1}$ or $T_{2}$ (tuple which we will call the "current tuple"), 
  and the index stagnation is associated to another index which indexes the leftmost element (that has not yet been examined) of a tuple which is not the "current tuple" 
  (see commentaries of part 1 for details)

- For $c_{3}$, since there are several possible combinations of arguments for the $min$ function (see "Summary" in this part), we generalize all these combinations (we "group them together") 
  into a general pair $(\alpha_{(3)}, \beta_{(3)})$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\exists c_{3} \in \mathbb{R}, \quad
\left(
\ \
c_{(3)}
:=
\begin{cases}
\overbrace{
\bigg(
c_{(1)} = a_{(1)}
\land
c_{(2)} = a_{(2)}
\land
a_{(3)} < b_{(1)}
\bigg)
}^{
\text{Case 1}
}
\Rightarrow
\overbrace{
\bigg(
a_{(1)} < b_{(1)}
\land
a_{(2)} < b_{(1)}
\bigg)
}^{
\text{Property extracted from } c_{(1)} \text{ for the case 1}
}
\Rightarrow
\overbrace{
\bigg(
\boxed{
c_{(3)} = a_{(3)}
}
=
min\Big(
\boxed{
a_{(3)}, b_{(1)}
}
\Big)
\bigg)
}^{
\text{Result for the case 1}
}
\\[1em]
\overbrace{
\bigg(
c_{(1)} = a_{(1)}
\land
c_{(2)} = b_{(1)}
\land
a_{(2)} < b_{(2)}
\bigg)
}^{
\text{Case 2}
}
\Rightarrow
\bigg(
a_{(1)} < b_{(1)}
\land
b_{(1)} \leq a_{(2)}
\bigg)
\Rightarrow
\bigg(
c_{(3)} = a_{(2)}
=
min\Big(
a_{(2)}, b_{(2)}
\Big)
\bigg)
\\[1em]
\overbrace{
\bigg(
c_{(1)} = b_{(1)}
\land
c_{(2)} = b_{(2)}
\land
b_{(3)} < a_{(1)}
\bigg)
}^{
\text{Case 3}
}
\Rightarrow
\bigg(
b_{(1)} \leq a_{(1)}
\land
b_{(2)} < a_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(3)} = b_{(3)}
=
min\Big(
a_{(1)}, b_{(3)}
\Big)
\bigg)
\\[1em]
\overbrace{
\bigg(
c_{(1)} = b_{(1)}
\land
c_{(2)} = a_{(1)}
\land
b_{(2)} \leq a_{(2)}
\bigg)
}^{
\text{Case 4}
}
\Rightarrow
\bigg(
b_{(1)} \leq a_{(1)}
\land
a_{(1)} \leq b_{(2)}
\bigg)
\Rightarrow
\bigg(
c_{(3)} = b_{(2)}
=
min\Big(
a_{(2)}, b_{(2)}
\Big)
\bigg)
\\[2em]
\overbrace{
\bigg(
c_{(1)} = a_{(1)}
\land
c_{(2)} = a_{(2)}
\land
b_{(1)} \leq a_{(3)}
\bigg)
}^{
\text{Case 5}
}
\Rightarrow
\bigg(
a_{(1)} < b_{(1)}
\land
a_{(2)} < b_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(3)} = b_{(1)}
=
min\Big(
a_{(3)}, b_{(1)}
\Big)
\bigg)
\\[1em]
\overbrace{
\bigg(
c_{(1)} = a_{(1)}
\land
c_{(2)} = b_{(1)}
\land
b_{(2)} \leq a_{(2)}
\bigg)
}^{
\text{Case 6}
}
\Rightarrow
\bigg(
a_{(1)} < b_{(1)}
\land
b_{(1)} \leq a_{(2)}
\bigg)
\Rightarrow
\bigg(
c_{(3)} = b_{(2)}
=
min\Big(
a_{(2)}, b_{(2)}
\Big)
\bigg)
\\[1em]
\overbrace{
\bigg(
c_{(1)} = b_{(1)}
\land
c_{(2)} = b_{(2)}
\land
a_{(1)} \leq b_{(3)}
\bigg)
}^{
\text{Case 7}
}
\Rightarrow
\bigg(
b_{(1)} \leq a_{(1)}
\land
b_{(2)} < a_{(1)}
\bigg)
\Rightarrow
\bigg(
c_{(3)} = a_{(1)}
=
min\Big(
a_{(1)}, b_{(3)}
\Big)
\bigg)
\\[1em]
\overbrace{
\bigg(
c_{(1)} = b_{(1)}
\land
c_{(2)} = a_{(1)}
\land
a_{(2)} < b_{(2)}
\bigg)
}^{
\text{Case 8}
}
\Rightarrow
\bigg(
b_{(1)} \leq a_{(1)}
\land
a_{(1)} \leq b_{(2)}
\bigg)
\Rightarrow
\bigg(
c_{(3)} = a_{(2)}
=
min\Big(
a_{(2)}, b_{(2)}
\Big)
\bigg)
\end{cases}
\ \
\right)
\Rightarrow
\underbrace{
\left(
\ \
c_{(3)}
=
\begin{cases}
\underbrace{
\bigg(
c_{(1)} = a_{(1)}
\land
c_{(2)} = a_{(2)}
\bigg)
}_{
\text{Current possible element of } T_{4}
}
\Rightarrow
\bigg(
c_{(3)}
=
min\Big(
\underbrace{
a_{(3)}, b_{(1)}
}_{
\text{Combination 1}
}
\Big)
\bigg)
\\[1em]
\underbrace{
\bigg(
c_{(1)} = a_{(1)}
\land
c_{(2)} = b_{(1)}
\bigg)
}_{
\text{Current possible element of } T_{4}
}
\Rightarrow
\bigg(
c_{(3)}
=
min\Big(
\underbrace{
a_{(2)}, b_{(2)}
}_{
\text{Combination 2}
}
\Big)
\bigg)
\\[1em]
\underbrace{
\bigg(
c_{(1)} = b_{(1)}
\land
c_{(2)} = b_{(2)}
\bigg)
}_{
\text{Current possible element of } T_{4}
}
\Rightarrow
\bigg(
c_{(3)}
=
min\Big(
\underbrace{
a_{(1)}, b_{(3)}
}_{
\text{Combination 3}
}
\Big)
\bigg)
\\[1em]
\underbrace{
\bigg(
c_{(1)} = b_{(1)}
\land
c_{(2)} = a_{(1)}
\bigg)
}_{
\text{Current possible element of } T_{4}
}
\Rightarrow
\bigg(
c_{(3)}
=
min\Big(
\underbrace{
a_{(2)}, b_{(2)}
}_{
\text{Combination 4}
}
\Big)
\bigg)
\end{cases}
\ \
\right)
}_{
\boxed{
\text{Summary}
}
}
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(3)}, \beta_{(3)} \in S_{3}(n, m), \quad
\boxed{
\bigg(
c_{(3)}
=
min\Big(
a_{(\alpha_{(3)})}, 
b_{(\beta_{(3)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} < c_{(3)} < \dots < a_{(n)}
\land
c_{(1)} < c_{(2)} < c_{(3)} < \dots < b_{(m)}
\bigg)
\land
\bigg(
T_{4}
:=
cat\Big(
(c_{(1)}, c_{(2)}), 
(c_{3})
\Big)
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 3 :

$$
\begin{array}{l}
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m < n
\\[1em]
\hline
a_{(1)} & < & a_{(2)} & < & a_{(3)} & < & \dots & < & a_{(m - 1)} & < & a_{(m)} & < & \dots & < & a_{(n)}
\\[2em]
< &  & < &  & < &  & \dots &  & < &  & <
\\[2em]
b_{(1)} & < & b_{(2)} & < & b_{(3)} & < & \dots & < & b_{(m - 1)} & < & b_{(m)}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m \geq n
\\[1em]
\hline
a_{(1)} & < & a_{(2)} & < & a_{(3)} & < & \dots & < & a_{(n - 1)} & < & a_{(n)}
\\[2em]
< &  & < &  & < &  & \dots &  & < &  & <
\\[2em]
b_{(1)} & < & b_{(2)} & < & b_{(3)} & < & \dots & < & b_{(n - 1)} & < & b_{(n)} & < & \dots & < & b_{(m)}
\\[1em]
\hline
\end{array}
\end{array}
$$

Diagram 2 of part 3 :

$$
\begin{array}{l}
\begin{array}{|c|c|}
\hline
/ & m < n
\\[1em]
\hline
c_{(3)} = a_{(3)}
&
\begin{array}{l}
a_{(1)} < a_{(2)} < \boxed{a_{(3)}} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
a_{(1)} < a_{(2)} < \boxed{a_{(3)}} < b_{(1)} < b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = a_{(2)}
&
\begin{array}{l}
a_{(1)} < b_{(1)} \leq \boxed{a_{(2)}} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
a_{(1)} < b_{(1)} < \boxed{a_{(2)}} < b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = b_{(3)}
&
\begin{array}{l}
b_{(1)} < b_{(2)} < \boxed{b_{(3)}} < a_{(1)} < a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
b_{(1)} < b_{(2)} < \boxed{b_{(3)}} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = b_{(2)}
&
\begin{array}{l}
b_{(1)} \leq a_{(1)} \leq \boxed{b_{(2)}} \leq a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
b_{(1)} \leq a_{(1)} \leq \boxed{b_{(2)}} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = b_{(1)}
&
\begin{array}{l}
a_{(1)} < a_{(2)} < \boxed{b_{(1)}} \leq a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
a_{(1)} < a_{(2)} < \boxed{b_{(1)}} < b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = b_{(2)}
&
\begin{array}{l}
a_{(1)} < b_{(1)} \leq \boxed{b_{(2)}} \leq a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
a_{(1)} < b_{(1)} < \boxed{b_{(2)}} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = a_{(1)}
&
\begin{array}{l}
b_{(1)} < b_{(2)} < \boxed{a_{(1)}} < a_{(2)} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
b_{(1)} < b_{(2)} < \boxed{a_{(1)}} \leq b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = a_{(2)}
&
\begin{array}{l}
b_{(1)} \leq a_{(1)} < \boxed{a_{(2)}} < a_{(3)} < \dots < a_{(m - 1)} < a_{(m)} < \dots < a_{(n)}
\\[1em]
b_{(1)} \leq a_{(1)} \leq \boxed{a_{(2)}} \leq b_{(2)} < b_{(3)} < \dots < b_{(m - 1)} < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|c|c|}
\hline
/ & m \geq n
\\[1em]
\hline
c_{(3)} = a_{(3)}
&
\begin{array}{l}
a_{(1)} < a_{(2)} < \boxed{a_{(3)}} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
a_{(1)} < a_{(2)} < \boxed{a_{(3)}} < b_{(1)} < b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = a_{(2)}
&
\begin{array}{l}
a_{(1)} < b_{(1)} \leq \boxed{a_{(2)}} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
a_{(1)} < b_{(1)} < \boxed{a_{(2)}} < b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = b_{(3)}
&
\begin{array}{l}
b_{(1)} < b_{(2)} < \boxed{b_{(3)}} < a_{(1)} < a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
b_{(1)} < b_{(2)} < \boxed{b_{(3)}} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = b_{(2)}
&
\begin{array}{l}
b_{(1)} \leq a_{(1)} \leq \boxed{b_{(2)}} \leq a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
b_{(1)} \leq a_{(1)} \leq \boxed{b_{(2)}} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = b_{(1)}
&
\begin{array}{l}
a_{(1)} < a_{(2)} < \boxed{b_{(1)}} \leq a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
a_{(1)} < a_{(2)} < \boxed{b_{(1)}} < b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = b_{(2)}
&
\begin{array}{l}
a_{(1)} < b_{(1)} \leq \boxed{b_{(2)}} \leq a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
a_{(1)} < b_{(1)} < \boxed{b_{(2)}} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = a_{(1)}
&
\begin{array}{l}
b_{(1)} < b_{(2)} < \boxed{a_{(1)}} < a_{(2)} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
b_{(1)} < b_{(2)} < \boxed{a_{(1)}} \leq b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
c_{(3)} = a_{(2)}
&
\begin{array}{l}
b_{(1)} \leq a_{(1)} < \boxed{a_{(2)}} < a_{(3)} < \dots < a_{(n - 1)} < a_{(n)}
\\[1em]
b_{(1)} \leq a_{(1)} \leq \boxed{a_{(2)}} \leq b_{(2)} < b_{(3)} < \dots < b_{(n - 1)} < b_{(n)} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Diagram 3 of part 3 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
m < n
\\[1em]
\hline
\begin{array}{l}
\boxed{c_{(1)}} < \boxed{c_{(2)}} < \boxed{c_{(3)}} < \dots < a_{(n)}
\\[1em]
\boxed{c_{(1)}} < \boxed{c_{(2)}} < \boxed{c_{(3)}} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|c|}
\hline
m \geq n
\\[1em]
\hline
\begin{array}{l}
\boxed{c_{(1)}} < \boxed{c_{(2)}} < \boxed{c_{(3)}} < \dots < a_{(n)}
\\[1em]
\boxed{c_{(1)}} < \boxed{c_{(2)}} < \boxed{c_{(3)}} < \dots < b_{(m)}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Diagram 4 of part 3 :

$$
\begin{array}{l}
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m < n
\\[1em]
\hline
a_{(1)} & < & a_{(2)} & < & a_{(3)} & < & \dots & < & a_{(m - 1)} & < & a_{(m)} & < & \dots & < & a_{(n)}
\\[2em]
< &  & < &  & < &  & \dots &  & < &  & <
\\[2em]
b_{(1)} & < & b_{(2)} & < & b_{(3)} & < & \dots & < & b_{(m - 1)} & < & b_{(m)}
\\[1em]
\hline
\end{array}
\quad \quad
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m \geq n
\\[1em]
\hline
a_{(1)} & < & a_{(2)} & < & a_{(3)} & < & \dots & < & a_{(n - 1)} & < & a_{(n)}
\\[2em]
< &  & < &  & < &  & \dots &  & < &  & <
\\[2em]
b_{(1)} & < & b_{(2)} & < & b_{(3)} & < & \dots & < & b_{(n - 1)} & < & b_{(n)} & < & \dots & < & b_{(m)}
\\[1em]
\hline
\end{array}
\end{array}
$$

Part 4 :

- Since the recurrence is performed until there are no more elements to examine in $T_{1}$ or $T_{2}$, the sorting (= the computation of each element (indexed by $\eta$ ) of $T_{4}$) is performed either 
  on all the length of $T_{1}$, or on all the length of $T_{2}$. It means that the index $\eta$ varies either on all the length of $T_{1}$ or on all the length of $T_{2}$ 

  To cover the two cases simultaneously, we can add the length of $T_{1}$ (represented by $Card(S_{1})$ ) and the length of $T_{2}$ (represented by $Card(S_{2})$ ). 
  We can thus generalize by assuming that $\eta$ varies between $1$ and $\boxed{Card(S_{1}) + Card(S_{2}) = n + m}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\mathcal{P}(\eta) :
\Bigg(
\bigg(
\Big(
\underline{1 \leq \eta \leq n + m}
\Big)
\Rightarrow
\Big(
\exists \alpha_{(\eta)}, \beta_{(\eta)} \in S_{3}(n, m), \quad
\boxed{
\Big(
c_{(\eta)}
=
min\big(
a_{(\alpha_{(\eta)})}, 
b_{(\beta_{(\eta)})}
\big)
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(\eta - 1)} < c_{(\eta)} \leq a_{(n)}
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(\eta - 1)} < c_{(\eta)} \leq b_{(m)}
\Big)
}
\Big)
\bigg)
\Bigg)
\Bigg)
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
k = 1
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(n_{0}) :
\Bigg(
\bigg(
\Big(
\exists \alpha_{(1)}, \beta_{(1)} \in S_{3}(n, m), \quad
\Big(
c_{(1)}
=
min\big(
a_{(\alpha_{(1)})}, 
b_{(\beta_{(1)})}
\big)
\Big)
\land
\Big(
c_{(1)} \leq a_{(n)}
\Big)
\land
\Big(
c_{(1)} \leq b_{(m)}
\Big)
\Big)
\bigg)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(1)}, \beta_{(1)} \in S_{3}(n, m), \quad
\boxed{
\bigg(
c_{(1)}
=
min\Big(
a_{(\alpha_{(1)})}, 
b_{(\beta_{(1)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} \leq a_{(n)}
\bigg)
\land
\bigg(
c_{(1)} \leq b_{(m)}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(n_{0})
\Bigg)
}
\end{cases}
\end{array}
$$

Part 5 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
k = 2
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(k = 2) :
\Bigg(
\exists \alpha_{(2)}, \beta_{(2)} \in S_{3}(n, m), \quad
\bigg(
c_{(2)}
=
min\Big(
a_{(\alpha_{(2)})}, 
b_{(\beta_{(2)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} \leq a_{(n)}
\land
\bigg(
c_{(1)} < c_{(2)} \leq b_{(m)}
\bigg)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(2)}, \beta_{(2)} \in S_{3}(n, m), \quad
\boxed{
\bigg(
c_{(2)}
=
min\Big(
a_{(\alpha_{(2)})}, 
b_{(\beta_{(2)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} \leq a_{(n)}
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} \leq b_{(m)}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(k = 2)
\Bigg)
}
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
k = 3
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(k = 3) :
\Bigg(
\exists \alpha_{(3)}, \beta_{(3)} \in S_{3}(n, m), \quad
\bigg(
c_{(3)}
=
min\Big(
a_{(\alpha_{(3)})}, 
b_{(\beta_{(3)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} < c_{(3)} \leq a_{(n)}
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} < c_{(3)} \leq b_{(m)}
\bigg)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(3)}, \beta_{(3)} \in S_{3}(n, m), \quad
\boxed{
\bigg(
c_{(3)}
=
min\Big(
a_{(\alpha_{(3)})}, 
b_{(\beta_{(3)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} < c_{(3)} \leq a_{(n)}
\bigg)
\land
\bigg(
c_{(1)} < c_{(2)} < c_{(3)} \leq b_{(m)}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(k = 3)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 6 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
k \curvearrowright k + 1
\Bigg)
\\[1em]
\Rightarrow
\begin{cases}
\mathcal{P}(k) :
\Bigg(
\bigg(
\Big(
\underline{1 \leq k \leq n + m}
\Big)
\Rightarrow
\Big(
\exists \alpha_{(k)}, \beta_{(k)} \in S_{3}(n, m), \quad
\boxed{
\Big(
c_{(k)}
=
min\big(
a_{(\alpha_{(k)})}, 
b_{(\beta_{(k)})}
\big)
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(k - 1)} < c_{(k)} \leq a_{(n)}
\land
\Big(
c_{(1)} < \dots < c_{(k - 1)} < c_{(k)} \leq b_{(m)}
\Big)
}
\Big)
\bigg)
\Bigg)
\\[1em]
\mathcal{H}(k) :
\Bigg(
\forall k \in \mathbb{N}, \quad
\Bigg(
k \geq n_{0}
\land
\mathcal{P}(k)
\Bigg)
\Rightarrow
\Bigg(
\mathcal{P}(k + 1) :
\Bigg(
\bigg(
\Big(
\underline{1 \leq k + 1 \leq n + m}
\Big)
\Rightarrow
\Big(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\boxed{
\Big(
c_{(k + 1)}
=
min\big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\big)
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(k)} < c_{(k + 1)} \leq a_{(n)}
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(k)} < c_{(k + 1)} \leq b_{(m)}
\Big)
}
\Big)
\bigg)
\Bigg)
\Bigg)
\end{cases}
\end{cases}
\end{array}
$$

Part 7 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\exists \alpha_{(k)}, \beta_{(k)} \in S_{3}(n, m), \quad
\bigg(
c_{(k)}
=
min\Big(
a_{(\alpha_{(k)})}, 
b_{(\beta_{(k)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < \dots < c_{(k - 1)} < c_{(k)} \leq a_{(n)}
\bigg)
\land
\bigg(
c_{(1)} < \dots < c_{(k - 1)} < c_{(k)} \leq b_{(m)}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\underbrace{
\Bigg(
a_{(\alpha_{(k)})}
<
b_{(\beta_{(k)})}
\Bigg)
}_{\text{Case } 1}
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
a_{(\alpha_{(k)})}
<
b_{(\beta_{(k)})}
\bigg)
\Rightarrow
\boxed{
\bigg(
c_{(k)}
=
a_{(\alpha_{(k)})}
\bigg)
}
\Rightarrow
\bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\boxed{
\Big(
\underbrace{
\alpha_{(k + 1)}
=
\alpha_{(k)} + 1
}_{
\text{Index progression}
}
\land
\underbrace{
b_{(\beta_{(k + 1)})}
=
b_{(\beta_{(k)})}
}_{
\text{Same index}
}
\Big)
}
\because
\Big(
\text{Here, index progression takes place in } T_{1} \text{ and index stagnation takes place in } T_{2}
\Big)
\bigg)
\Rightarrow
\boxed{
\bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
c_{(k + 1)}
=
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\underline{
\bigg(
a_{(\alpha_{(k)})}
<
a_{(\alpha_{(k + 1)})}
\bigg)
\land
\bigg(
a_{(\alpha_{(k)})}
<
b_{(\beta_{(k)})}
\bigg)
\iff
\bigg(
c_{(k)}
<
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\bigg)
}
\iff
\boxed{
\bigg(
c_{(k)}
<
c_{(k + 1)}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\underbrace{
\overbrace{
\bigg(
\Big(
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\leq
a_{(\alpha_{(k + 1)})}
\Big)
\land
\Big(
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\leq
b_{(\beta_{(k + 1)})}
\Big)
\bigg)
}^{
\boxed{
\text{Property of a minimum}
}
}
}_{
\boxed{
\Big(
\forall \alpha,\beta \in \mathbb{R}, \quad
\big(
min(\alpha, \beta)
\leq
\alpha
\big)
\land
\big(
min(\alpha, \beta)
\leq
\beta
\big)
\Big)
\text{ form}
}
}
\iff
\boxed{
\bigg(
\Big(
c_{(k + 1)}
\leq
a_{(\alpha_{(k + 1)})}
\Big)
\land
\Big(
c_{(k + 1)}
\leq
b_{(\beta_{(k + 1)})}
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\underline{
\bigg(
\Big(
c_{(k)}
<
c_{(k + 1)}
\leq
a_{(\alpha_{(k + 1)})}
\leq
a_{(n)}
\Big)
\land
\Big(
c_{(k)}
<
c_{(k + 1)}
\leq
b_{(\beta_{(k + 1)})}
\leq
b_{(m)}
\Big)
\bigg)
}
\Rightarrow
\underbrace{
\bigg(
\Big(
c_{(1)}
<
\dots
<
c_{(k - 1)}
<
c_{(k)}
<
c_{(k + 1)}
\leq
a_{(\alpha_{(k + 1)})}
\leq
a_{(n)}
\Big)
\land
\Big(
c_{(1)}
<
\dots
<
c_{(k - 1)}
<
c_{(k)}
<
c_{(k + 1)}
\leq
b_{(\beta_{(k + 1)})}
\leq
b_{(m)}
\Big)
\bigg)
}_{
\boxed{
\text{Using the recurrence hypothesis}
}
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
a_{(\alpha_{(k)})}
<
b_{(\beta_{(k)})}
\bigg)
\Rightarrow
\bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\Big(
c_{(k + 1)}
=
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(k)} < c_{(k + 1)} \leq a_{(n)}
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(k)} < c_{(k + 1)} \leq b_{(m)}
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 8 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\underbrace{
\Bigg(
a_{(\alpha_{(k)})}
\geq
b_{(\beta_{(k)})}
\iff
b_{(\beta_{(k)})}
\leq
a_{(\alpha_{(k)})}
\Bigg)
}_{\text{Case } 2}
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
b_{(\beta_{(k)})}
\leq
a_{(\alpha_{(k)})}
\bigg)
\Rightarrow
\boxed{
\bigg(
c_{(k)}
=
b_{(\beta_{(k)})}
\bigg)
}
\Rightarrow
\bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\boxed{
\Big(
\underbrace{
\alpha_{(k + 1)}
=
\alpha_{(k)}
}_{
\text{Same index}
}
\land
\underbrace{
b_{(\beta_{(k + 1)})}
=
b_{(\beta_{(k)})} + 1
}_{
\text{Index progression}
}
\Big)
}
\because
\Big(
\text{Here, index progression takes place in } T_{2} \text{ and index stagnation takes place in } T_{1}
\Big)
\bigg)
\Rightarrow
\boxed{
\bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
c_{(k + 1)}
=
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\underline{
\bigg(
b_{(\beta_{(k)})}
<
b_{(\beta_{(k + 1)})}
\bigg)
\land
\bigg(
b_{(\beta_{(k)})}
\leq
a_{(\alpha_{(k)})}
\bigg)
\iff
\bigg(
c_{(k)}
<
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\bigg)
}
\iff
\boxed{
\bigg(
c_{(k)}
<
c_{(k + 1)}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\underbrace{
\overbrace{
\bigg(
\Big(
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\leq
a_{(\alpha_{(k + 1)})}
\Big)
\land
\Big(
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\leq
b_{(\beta_{(k + 1)})}
\Big)
\bigg)
}^{
\boxed{
\text{Property of a minimum}
}
}
}_{
\boxed{
\Big(
\forall \alpha,\beta \in \mathbb{R}, \quad
\big(
min(\alpha, \beta)
\leq
\alpha
\big)
\land
\big(
min(\alpha, \beta)
\leq
\beta
\big)
\Big)
\text{ form}
}
}
\iff
\boxed{
\bigg(
\Big(
c_{(k + 1)}
\leq
a_{(\alpha_{(k + 1)})}
\Big)
\land
\Big(
c_{(k + 1)}
\leq
b_{(\beta_{(k + 1)})}
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\underline{
\bigg(
\Big(
c_{(k)}
<
c_{(k + 1)}
\leq
a_{(\alpha_{(k + 1)})}
\leq
a_{(n)}
\Big)
\land
\Big(
c_{(k)}
<
c_{(k + 1)}
\leq
b_{(\beta_{(k + 1)})}
\leq
b_{(m)}
\Big)
\bigg)
}
\Rightarrow
\underbrace{
\bigg(
\Big(
c_{(1)}
<
\dots
<
c_{(k - 1)}
<
c_{(k)}
<
c_{(k + 1)}
\leq
a_{(\alpha_{(k + 1)})}
\leq
a_{(n)}
\Big)
\land
\Big(
c_{(1)}
<
\dots
<
c_{(k - 1)}
<
c_{(k)}
<
c_{(k + 1)}
\leq
b_{(\beta_{(k + 1)})}
\leq
b_{(m)}
\Big)
\bigg)
}_{
\boxed{
\text{Using the recurrence hypothesis}
}
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
b_{(\beta_{(k)})}
\leq
a_{(\alpha_{(k)})}
\bigg)
\Rightarrow
\bigg(
\exists \alpha_{(k + 1)}, \beta_{(k + 1)} \in S_{3}(n, m), \quad
\Big(
c_{(k + 1)}
=
min\Big(
a_{(\alpha_{(k + 1)})}, 
b_{(\beta_{(k + 1)})}
\Big)
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(k)} < c_{(k + 1)} \leq a_{(n)}
\Big)
\land
\Big(
c_{(1)} < \dots < c_{(k)} < c_{(k + 1)} \leq b_{(m)}
\Big)
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(k+1)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 9 :

- We have : $c_{\boxed{(\eta)}} = min\Big( a_{(\alpha_{\boxed{(\eta)}})}, b_{(\beta_{\boxed{(\eta)}})} \Big)$

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \eta \in \{1, \dots, n + m\}, \quad
\exists \alpha_{(\eta)}, \beta_{(\eta)} \in S_{3}(n, m), \quad
\boxed{
\bigg(
c_{(\eta)}
=
min\Big(
a_{(\alpha_{(\eta)})}, 
b_{(\beta_{(\eta)})}
\Big)
\bigg)
\land
\bigg(
c_{(1)} < \dots < c_{(\eta - 1)} < c_{(\eta)} \leq a_{(n)}
\bigg)
\land
\bigg(
c_{(1)} < \dots < c_{(\eta - 1)} < c_{(\eta)} \leq b_{(m)}
\bigg)
}
\Bigg)
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\mathcal{P}(\eta) \curvearrowright P_{i}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\forall \eta \in \{1, \dots, n + m\}, \quad
\underbrace{
\bigg(
T_{4}
:=
cat\Big(
cat\Big(
\dots
cat\Big(
(), 
(c_{(1)})
\Big)
\dots
\Big)
,
(c_{(\eta)})
\Big)
=
(c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)})
\bigg)
}_{
\text{Tuple sorted in ascending order}
}
\land
\bigg(
c_{(1)} < \dots < c_{(\eta - 1)} < c_{(\eta)}
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 10 :

- In this part, we build (by recurrence) the $\boxed{\text{final version}}$ of the "final sorted tuple" from the two already sorted tuples
	
	- According to the step 1 of part 1 :
	  " *We take the leftmost element of $T_{1}$ (which we will call "EG1") that has not yet been examined, and the leftmost element of $T_{2}$ (which we will call "EG2") that has not yet been examined* "
		
		
		- Thus, at each step of the recurrence, we take the "leftmost element" of a tuple that has not yet been examined
		
		- It means that as long as the "leftmost element" of a given tuple has not yet been examined, we do not skip this "leftmost element" to examine the element immediately to the right 
		  of this "leftmost element" in the same tuple. 
		  Therefore, for $c_{(n)} = a_{(n)}$, we needed to add in $T_{4}$ the elements $a_{(1)}, \dots, a_{(n-1)}$ from $T_{1}$ 
		
		- Each step of the recurrence corresponds to the adding of an element (from $T_{1}$ or $T_{2}$) to $T_{4}$ (at an unique position in $T_{4}$) until there are no more elements to examine in $T_{1}$ or $T_{2}$ 
		
		- " until there are no more elements to examine in $T_{1}$ or $T_{2}$ " is also equivalent to " $\boxed{\text{until either } a_{(n)} \text{ or } b_{(m)} \text{ (not both) is added to } T_{4}}$ "
		
		- " until either $a_{(n)}$ or $b_{(m)}$ (not both) is added to $T_{4}$ " is equivalent to " as long as $a_{(n)}$ or $b_{(m)}$ (not both) has not been added to $T_{4}$ "
		
		
		- For example, if $n = 5$ and $m = 7$, we can potentially have :
		
			Note :
			
			*Until there are no more elements to examine in $T_{1}$ or $T_{2}$ , the following instruction is repeated :*
			*Instruction : "As long as the "right value" is greater than the "left value", the "right value" is compared again each time"*
			*Since $\forall \eta \in \{1, \dots, n + m\}, \quad \exists \alpha_{(\eta)}, \beta_{(\eta)} \in S_{3}(n, m), \quad c_{(\eta)} = min\Big( a_{(\alpha_{(\eta)})}, b_{(\beta_{(\eta)})} \Big)$, then the "left value" can also be viewed as $a_{(\alpha_{(\eta)})}$ and the "right value" can be viewed as $b_{(\beta_{(\eta)})}$*

$$
\begin{array}{l}
\text{Example ( } n = 5 \text{ and } m = 7 \text{ ) (See step 2 for final result) :}
\\[1em]
\text{Step 1 : }
\\[1em]
\begin{array}{|c|}
\hline
\begin{array}{l}
S_{1}
:=
\underbrace{
\{ a_{(1)}, a_{(2)}, a_{(3)}, a_{(4)}, a_{\boxed{(5)}} \}
}_{
\boxed{
\large{
\substack{
{
\text{We sort only on all the length of the shorter set}
}
\\
{
\text{(here is it } S_{1} \text{ because } Card(S_{1}) < Card(S_{2}) \iff 5 < 7 \text{ ).}
}
\\
{
\text{Here, it means that the recurrence will stop when } a_{(5)} \text{ is added to } S_{4}
}
}
}
}
}
\\[1em]
S_{2}
:=
\{ b_{(1)}, b_{(2)}, b_{(3)}, b_{(4)}, b_{(5)}, b_{(6)}, b_{\boxed{(7)}} \}
\\[1em]
T_{1} := (a_{(1)}, a_{(2)}, a_{(3)}, a_{(4)}, a_{(5)})
\\[1em]
T_{2} := (b_{(1)}, b_{(2)}, b_{(3)}, b_{(4)}, b_{(5)}, b_{(6)}, b_{(7)})
\\[1em]
T_{4}
:=
(
\underbrace{
a_{(1)}
}_{
\boxed{
\substack{
{
\text{Start of the}
}
\\[0.5em]
{
\text{recurrence}
}
\\[0.5em]
{
\text{Step } k = 1
}
}
}
}
, 
\overbrace{
a_{(2)}
}^{
\text{Step } k = 2
}
, 
\overbrace{
b_{(4)}
}^{
\text{Step } k = 3
}
, 
\overbrace{
a_{(4)}
}^{
\text{Step } k = 4
}
, 
\overbrace{
b_{(3)}
}^{
\text{Step } k = 5
}
, 
\overbrace{
b_{(1)}
}^{
\text{Step } k = 6
}
, 
\overbrace{
b_{(2)}
}^{
\text{Step } k = 7
}
, 
\overbrace{
a_{(3)}
}^{
\text{Step } k = 8
}
, 
\underbrace{
a_{(5)}
}_{
\boxed{
\substack{
{
\text{End of the}
}
\\[0.5em]
{
\text{recurrence}
}
\\[0.5em]
{
\text{Step } k = 9
}
}
}
}
,
b_{(5)}, b_{(6)}, b_{(7)}
)
\\[1em]
\begin{array}{|cccccccccccccc|}
\hline
& & & & & & m \geq n
\\[1em]
\hline
\underbrace{
a_{(1)}
}_{
\boxed{
\substack{
{
\text{Start of the}
}
\\[0.5em]
{
\text{recurrence}
}
\\[0.5em]
{
\text{Step } k = 1
}
}
}
}
 & < & 
\overbrace{
a_{(2)}
}^{
\text{Step } k = 2
}
 & < & 
\overbrace{
a_{(3)}
}^{
\text{Step } k = 4
}
 & < & 
\overbrace{
a_{(4)}
}^{
\text{Step } k = 8
}
 & < & 
\underbrace{
a_{\boxed{(n = 5)}}
}_{
\boxed{
\substack{
{
\text{End of the}
}
\\[0.5em]
{
\text{recurrence}
}
\\[0.5em]
{
\text{Step } k = 9
}
}
}
}
\\[2em]
\overbrace{
b_{(1)}
}^{
\text{Step } k = 3
}
 & < & 
\overbrace{
b_{(2)}
}^{
\text{Step } k = 5
}
 & < & 
\overbrace{
b_{(3)}
}^{
\text{Step } k = 6
}
 & < & 
\overbrace{
b_{(4)}
}^{
\text{Step } k = 7
}
 & < & b_{(5)} & < & b_{(6)} & < & b_{\boxed{(m = 7)}}
\\[1em]
\hline
\end{array}
\\[1em]
b_{(5)}, b_{(6)} \text{ and } b_{(m = 7)}
\text{ will not be compared since the recurrence has stopped}
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\small{
\begin{array}{|c|}
\hline
\begin{array}{l}
\Bigg(
\bigg(
\underbrace{a_{(1)}}_{\text{Left value}} < \overbrace{\underline{b_{(1)}}}^{\text{Right value}}
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(1)} = a_{(1)}
}
\bigg)
\Bigg)
\\[1em]
\Bigg(
\bigg(
\Big(
c_{(1)} = a_{(1)}
\Big)
\land
\Big(
\underbrace{a_{(2)}}_{\text{Left value}} < \overbrace{\underline{b_{(1)}}}^{\text{Right value}}
\Big)
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(2)} = a_{(2)}
}
\bigg)
\Bigg)
\\[1em]
\Bigg(
\bigg(
\Big(
c_{(2)} = a_{(2)}
\Big)
\land
\Big(
\underbrace{a_{(3)}}_{\text{Left value}} \centernot{<} \overbrace{\underline{b_{(1)}}}^{\text{Right value}}
\iff
a_{(3)} \geq b_{(1)}
\iff
b_{(1)} \leq \underline{a_{(3)}}
\Big)
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(3)} = b_{(1)}
}
\bigg)
\Bigg)
\\[1em]
\Bigg(
\bigg(
\Big(
c_{(3)} = b_{(1)}
\Big)
\land
\Big(
\underbrace{b_{(2)}}_{\text{Left value}} \centernot{<} \overbrace{\underline{a_{(3)}}}^{\text{Right value}}
\iff
b_{(2)} \geq a_{(3)}
\iff
a_{(3)} \leq \underline{b_{(2)}}
\Big)
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(4)} = a_{(3)}
}
\bigg)
\Bigg)
\\[1em]
\Bigg(
\bigg(
\Big(
c_{(4)} = a_{(3)}
\Big)
\land
\Big(
\underbrace{a_{(4)}}_{\text{Left value}} \centernot{<} \overbrace{\underline{b_{(2)}}}^{\text{Right value}}
\iff
a_{(4)} \geq b_{(2)}
\iff
b_{(2)} \leq \underline{a_{(4)}}
\Big)
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(5)} = b_{(2)}
}
\bigg)
\Bigg)
\\[1em]
\Bigg(
\bigg(
\Big(
c_{(5)} = b_{(2)}
\Big)
\land
\Big(
\underbrace{b_{(3)}}_{\text{Left value}} < \overbrace{\underline{a_{(4)}}}^{\text{Right value}}
\Big)
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(6)} = b_{(3)}
}
\bigg)
\Bigg)
\\[1em]
\Bigg(
\bigg(
\Big(
c_{(6)} = b_{(3)}
\Big)
\land
\Big(
\underbrace{b_{(4)}}_{\text{Left value}} < \overbrace{\underline{a_{(4)}}}^{\text{Right value}}
\Big)
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(7)} = b_{(4)}
}
\bigg)
\Bigg)
\\[1em]
\Bigg(
\bigg(
\Big(
c_{(7)} = b_{(4)}
\Big)
\land
\Big(
\underbrace{b_{(5)}}_{\text{Left value}} \centernot{<} \overbrace{\underline{a_{(4)}}}^{\text{Right value}}
\iff
b_{(5)} \geq a_{(4)}
\iff
a_{(4)} \leq \underline{b_{(5)}}
\Big)
\bigg)
\Rightarrow
\bigg(
\boxed{
c_{(8)} = a_{(4)}
}
\bigg)
\Bigg)
\\[1em]
\Bigg(
\bigg(
\Big(
c_{(8)} = a_{(4)}
\Big)
\land
\Big(
\underbrace{a_{(5)}}_{\text{Left value}} < \overbrace{\underline{b_{(5)}}}^{\text{Right value}}
\Big)
\bigg)
\Rightarrow
\underbrace{
\bigg(
\boxed{
c_{(9)} = a_{(n = 5)}
}
\bigg)
}_{
a_{(\alpha_{(\eta)})}
=
a_{(n)}
=
a_{(5)}
}
\Bigg)
\end{array}
\\[1em]
\hline
\end{array}
}
\end{array}
$$

$$
\begin{array}{l}
\text{Step 2 : }
\\[1em]
\begin{array}{|c|}
\hline
\Bigg(
a_{(\alpha_{(\eta)})}
=
a_{(n)}
=
a_{(5)}
\land
b_{(\beta_{(\eta)})}
=
b_{(5)}
\Bigg)
\Rightarrow
\Bigg(
\{ a_{(6)}, \dots, a_{(5)} \}
=
\emptyset
\land
\{ b_{(5)}, \dots, b_{(7)} \}
\neq
\emptyset
\Bigg)
\Rightarrow
\Bigg(
T_{4}
:=
cat\Big(
(c_{(1)}, \dots c_{(9)}), 
(b_{(5)}, b_{(6)}, b_{(7)})
\Big)
=
(c_{(1)}, \dots c_{(9)}, b_{(5)}, b_{(6)}, b_{(7)})
\Bigg)
\\[1em]
\hline
\end{array}
\end{array}
$$

- We observe that $a_{(1)}, \dots, a_{(n)}$ can be widely spaced apart, and that the steps of the recurrence do not always produce $a_{(1)}$, followed immediately by $a_{(2)}$, followed immediately 
  by $a_{(3)}$, and so on (in that order) 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
c_{(\eta)}
=
min\Big(
a_{(\alpha_{(\eta)})}, 
b_{(\beta_{(\eta)})}
\Big)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
c_{(\eta)}
=
min\Big(
a_{(\alpha_{(\eta)})}, 
b_{(\beta_{(\eta)})}
\Big)
=
\begin{cases}
a_{(\alpha_{(\eta)})} \leq b_{(\beta_{(\eta)})} \Rightarrow min(a_{(\alpha_{(\eta)})}, b_{(\beta_{(\eta)})}) = a_{(\alpha_{(\eta)})} \\
b_{(\beta_{(\eta)})} < a_{(\alpha_{(\eta)})} \Rightarrow min(a_{(\alpha_{(\eta)})}, b_{(\beta_{(\eta)})}) = b_{(\beta_{(\eta)})}
\end{cases}
\Big)
\land
\boxed{
\Big(
c_{(\eta)}
=
a_{(\alpha_{(\eta)})}
\Big)
}
\land
\boxed{
\Big(
a_{(\alpha_{(\eta)})}
=
a_{(n)}
\Big)
}
\bigg)
\Rightarrow
\bigg(
\underbrace{
\Big(
\{ a_{(n + 1)}, \dots, a_{(n)} \}
= 
\emptyset
\Big)
}_{
\substack{
{
\text{Since } a_{(n)} \text{ is the last element of } S_{1} \text{ that was the result of the min,}
}
\\
{
\text{then there is no element present just to the right of } a_{(n)} \text{ (which means}
}
\\
{
\text{that there are no elements with a position greater than } n \text{)}
}
}
}
\land
\underbrace{
\Big(
\{ b_{(\beta_{(\eta)})}, \dots, b_{(m)} \}
\neq 
\emptyset
\Big)
}_{
\substack{
{
\text{Thus, } b_{(\beta_{(\eta)})}, \dots, b_{(m)} \text{ remain, and they will not be}
}
\\
{
\text{compared with the element present just to the right of } a_{n}
}
\\
{
\text{(since no such element is present)}
}
}
}
\bigg)
\Rightarrow
\bigg(
\Big(
S_{4}
:=
\{ c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)} \}
\ \cup \
\emptyset
\ \cup \
\{ b_{(\beta_{(\eta)})}, \dots, b_{(m)} \}
=
\{ c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)} \}
\ \cup \
\{ b_{(\beta_{(\eta)})}, \dots, b_{(m)} \}
=
\{ c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)}, b_{(\beta_{(\eta)})}, \dots, b_{(m)} \}
\Big)
\land
\Big(
Card(S_{4})
=
Card(S_{1}) + Card(S_{2})
=
n + m
\Big)
\bigg)
\Rightarrow
\underbrace{
\bigg(
T_{4}
:=
cat\Big(
(c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)}), 
(b_{(\beta_{(\eta)})}, \dots, b_{(m)})
\Big)
=
(c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)}, b_{(\beta_{(\eta)})}, \dots, b_{(m)})
\bigg)
}_{
(c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)}, b_{(\beta_{(\eta)})}, \dots, b_{(m)})
\text{ is the sorted tuple formed by the tuples } T_{1} \text{ and } T_{2}
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
c_{(\eta)}
=
min\Big(
a_{(\alpha_{(\eta)})}, 
b_{(\beta_{(\eta)})}
\Big)
=
\begin{cases}
a_{(\alpha_{(\eta)})} \leq b_{(\beta_{(\eta)})} \Rightarrow min(a_{(\alpha_{(\eta)})}, b_{(\beta_{(\eta)})}) = a_{(\alpha_{(\eta)})} \\
b_{(\beta_{(\eta)})} < a_{(\alpha_{(\eta)})} \Rightarrow min(a_{(\alpha_{(\eta)})}, b_{(\beta_{(\eta)})}) = b_{(\beta_{(\eta)})}
\end{cases}
\Big)
\land
\boxed{
\Big(
c_{(\eta)}
=
b_{(\beta_{(\eta)})}
\Big)
}
\land
\boxed{
\Big(
b_{(\beta_{(\eta)})}
=
b_{(m)}
\Big)
}
\bigg)
\Rightarrow
\bigg(
\underbrace{
\Big(
\{ b_{(m + 1)}, \dots, b_{(m)} \}
= 
\emptyset
\Big)
}_{
\substack{
{
\text{Since } b_{(m)} \text{ is the last element of } S_{2} \text{ that was the result of the min,}
}
\\
{
\text{then there is no element present just to the right of } b_{(m)} \text{ (which means}
}
\\
{
\text{that there are no elements with a position greater than } m \text{)}
}
}
}
\land
\underbrace{
\Big(
\{ a_{(\alpha_{(\eta)})}, \dots, a_{(n)} \}
\neq
\emptyset
\Big)
}_{
\substack{
{
\text{Thus, } a_{(\alpha_{(\eta)})}, \dots, a_{(n)} \text{ remain, and they will not be}
}
\\
{
\text{compared with the element present just to the right of } b_{m}
}
\\
{
\text{(since no such element is present)}
}
}
}
\bigg)
\Rightarrow
\bigg(
\Big(
S_{4}
:=
\{ c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)} \}
\ \cup \
\{ a_{(\alpha_{(\eta)})}, \dots, a_{(n)} \}
\ \cup \
\emptyset
=
\{ c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)} \}
\ \cup \
\{ a_{(\alpha_{(\eta)})}, \dots, a_{(n)} \}
=
\{ c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)}, a_{(\alpha_{(\eta)})}, \dots, a_{(n)} \}
\Big)
\land
\Big(
Card(S_{4})
=
Card(S_{1}) + Card(S_{2})
=
n + m
\Big)
\bigg)
\Rightarrow
\underbrace{
\bigg(
T_{4}
:=
cat\Big(
(c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)}), 
(a_{(\alpha_{(\eta)})}, \dots, a_{(n)})
\Big)
=
(c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)}, a_{(\alpha_{(\eta)})}, \dots, a_{(n)})
\bigg)
}_{
(c_{(1)}, \ \dots, \ c_{(\eta - 1)}, \ c_{(\eta)}, a_{(\alpha_{(\eta)})}, \dots, a_{(n)})
\text{ is the sorted tuple formed by the tuples } T_{1} \text{ and } T_{2}
}
\Bigg)
\end{cases}
\end{array}
$$

Part 11 :

- From part 11 to part 12, we build (by algorithm) the $\boxed{\text{final version}}$ of the "final sorted tuple" from the two already sorted tuples
	
	- To obtain the "final sorted tuple" from $T_{1}$ and $T_{2}$, and using $T_{4}$ , we can implement the algorithm which describes the recurrence (recurrence from part 1 to part 10)

$$
\begin{array}{l}
\begin{cases}
\text{def } Merge(T_{1}, T_{2}) :
\\[1em]
\quad
n := Card\Big(
\Big\{
a_{(1)}, 
a_{(2)}, 
\dots, 
a_{(n - 1)}, 
a_{(n)}
\Big\}
\Big)
\\[1em]
\quad
m := Card\Big(
\Big\{
b_{(1)}, 
b_{(2)}, 
\dots, 
b_{(m - 1)}, 
b_{(m)}
\Big\}
\Big)
\\[1em]
\quad
S_{4} := \emptyset
\\[1em]
\quad
T_{4} := ()
\\[1em]
\quad
\alpha := 1
\\[1em]
\quad
\beta := 1
\\[1em]
\quad
\text{while } \alpha \leq n \text{ and } \beta \leq m :
\\[1em]
\quad
\quad \quad
\text{If } a_{(\alpha)} \leq b_{(\beta)} :
\\[1em]
\quad
\quad \quad \quad \quad
S_{4} := S_{4} \ \cup \ \{ a_{(n)} \}
\\[1em]
\quad
\quad \quad \quad \quad
T_{4} := cat(T_{4}, (a_{(n)}))
\\[1em]
\quad
\quad \quad \quad \quad
\alpha := \alpha + 1
\\[1em]
\quad
\quad \quad
\text{Else} :
\\[1em]
\quad
\quad \quad \quad \quad
S_{4} := S_{4} \ \cup \ \{ b_{(m)} \}
\\[1em]
\quad
\quad \quad \quad \quad
T_{4} := cat(T_{4}, (b_{(m)}))
\\[1em]
\quad
\quad \quad \quad \quad
\beta := \beta + 1
\\[1em]
\quad
S_{4}
:=
S_{4}
\ \cup \
\{ a_{(\alpha)}, \dots, a_{(n)} \}
\ \cup \
\{ b_{(\beta)}, \dots, b_{(m)} \}
\\[1em]
\quad
T_{4}
:=
cat\Big(
cat\Big(
T_{4}, (a_{(\alpha)}, \dots, a_{(n)})
\Big)
, 
(b_{(\beta)}, \dots, b_{(m)})
\Big)
\\[1em]
\quad
\text{return } (S_{4}, T_{4})
\\[2em]
T_{1}
:=
\Big(
a_{(1)}, 
a_{(2)}, 
\dots, 
a_{(n - 1)}, 
a_{(n)}
\Big)
\\[1em]
T_{2}
:=
\Big(
b_{(1)}, 
b_{(2)}, 
\dots, 
b_{(m - 1)}, 
b_{(m)}
\Big)
\\[1em]
Merge(T_{1}, T_{2})
\end{cases}
\\[1em]
\hspace{700pt}
\end{array}
$$

Part 12 :

- In this part, we examine some cases in the algorithm and we compute the loop variant $V$ of the algorithm. Then, we show that the function $G$ associated to the growth rate $\mathcal{O}(G(N))$ of 
  the algorithm is linear

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\ \
\Bigg(
\underbrace{
\bigg(
\alpha = n + 1
\land
\beta \leq m
\bigg)
}_{
\boxed{
m > n
}
}
\Rightarrow
\bigg(
\Big(
\{ a_{(\alpha)}, \dots, a_{(n)} \}
=
\emptyset
\Big)
\because
\Big(
\alpha = n + 1
\Big)
\bigg)
\Rightarrow
\bigg(
S_{4}
=
S_{4}
\ \cup \
\emptyset
\ \cup \
\{ b_{(\beta)}, \dots, b_{(m)} \}
=
S_{4}
\ \cup \
\{ b_{(\beta)}, \dots, b_{(m)} \}
\bigg)
\Bigg)
\\[1em]
\quad
\oplus
\Bigg(
\underbrace{
\bigg(
\alpha \leq n
\land
\beta = m + 1
\bigg)
}_{
\boxed{
m < n
}
}
\Rightarrow
\bigg(
\Big(
\{ b_{(\beta)}, \dots, b_{(m)} \}
=
\emptyset
\Big)
\because
\Big(
\beta = m + 1
\Big)
\bigg)
\Rightarrow
\bigg(
S_{4}
=
S_{4}
\ \cup \
\{ a_{(\alpha)}, \dots, a_{(n)} \}
\ \cup \
\emptyset
=
S_{4}
\ \cup \
\{ a_{(\alpha)}, \dots, a_{(n)} \}
\bigg)
\Bigg)
\\[1em]
\quad
\oplus
\Bigg(
\underbrace{
\bigg(
\alpha = n + 1
\land
\beta = m + 1
\bigg)
}_{
\boxed{
m = n
}
}
\Rightarrow
\bigg(
\Big(
\{ a_{(\alpha)}, \dots, a_{(n)} \}
=
\emptyset
\Big)
\because
\Big(
\alpha = n + 1
\Big)
\bigg)
\Rightarrow
\bigg(
S_{4}
=
S_{4}
\ \cup \
\emptyset
\ \cup \
\emptyset
=
S_{4}
\bigg)
\Bigg)
\ \
\Bigg)
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\forall n, m \in \mathbb{N}_{\geq 1}, \quad
\exists! {\iota}_{max_{(1)}} \in \mathbb{N}, \quad
\forall {\iota}_{(1)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\alpha : \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\} \to S_{3}(n, m), \quad
{\iota}_{(1)} \mapsto \alpha({\iota}_{(1)}), \quad
{\alpha}^{-1} : S_{3}(n, m) \to \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\alpha \mapsto {\iota}_{(1)}(\alpha), \quad
\\[1em]
\quad
\exists! {\iota}_{max_{(2)}} \in \mathbb{N}, \quad
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\beta : \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\} \to S_{3}(n, m), \quad
{\iota}_{(2)} \mapsto \beta({\iota}_{(2)}), \quad
{\beta}^{-1} : S_{3}(n, m) \to \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\beta \mapsto {\iota}_{(2)}(\beta), \quad
\\[1em]
\quad
V : S_{3}(n, m) \to S_{3}(n, m), \quad
(\alpha, \beta) \mapsto V(\alpha, \beta), \quad
G : S_{3}(n, m) \to S_{3}(n, m), \quad
(\alpha, \beta) \mapsto G(\alpha, \beta), \quad
\boxed{
\bigg(
V(\alpha, \beta)
:=
max\Big(
0, 
min\Big(
\lfloor n + 1 - \alpha \rfloor, \ 
\lfloor m + 1 - \beta \rfloor
\Big)
\Big)
\bigg)
}
\land
\boxed{
\bigg(
G(\alpha, \beta)
:=
min\Big(
-\alpha, -\beta
\Big)
\bigg)
}
\land
\bigg(
V(\alpha, \beta)
\in
\underbrace{
\Big\{
V(\alpha, \beta)
\ \Big| \
\Big(
\exists \gamma \in \mathbb{R}_{>0}, \quad
\exists \alpha_{(0)}, \beta_{(0)} \in \mathbb{N}_{>0}, \quad
\forall \alpha \geq \alpha_{(0)}, \quad
\forall \beta \geq \beta_{(0)}, \quad
|V(\alpha, \beta)|
\leq
\gamma
\times
|G(\alpha, \beta)|
\Big)
\Big\}
}_{\boxed{\mathcal{O}(|G(\alpha, \beta)|) \ = \ \mathcal{O}(|min(-\alpha, -\beta)|)}}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\ \
\Bigg(
\bigg(
G(\alpha, \beta)
=
min\Big(
-\alpha, -\beta
\Big)
\bigg)
\iff
\bigg(
\Big(
G(\alpha, \beta) \leq -\alpha
\land
G(\alpha, \beta) \leq -\beta
\Big)
\land
\Big(
G(\alpha, \beta) = -\alpha
\lor
G(\alpha, \beta) = -\beta
\Big)
\bigg)
\Bigg)
\Rightarrow
\Bigg(
G \text{ is linear}
\Bigg)
\ \
\Bigg)
}
\end{cases}
\end{array}
$$

Part 13 :

- In the following parts, we will examine if the principle of building such a "final sorted tuple" (with such a growth rate) can be reused. 
  Indeed, if $G$ is linear, then the total number of operations is linear and makes the algorithm efficient


	- (English) Since a set (which we will call $S_{5}$) can be viewed as the union of its singletons, since each singleton is sorted, and since each singleton can be viewed as a $1$-tuple, then 
	  we can use the function $Merge()$ by providing these 1-tuple as arguments two by two. 
	  We thus obtain sorted tuples of size $2^{1}$, with possibly a remainder (a tuple of size less than $2^{1}$). Here we say we are at "iteration 1"

	- (English) We can then generalize this process at any iteration (which we will call iteration "$s$") :

		- 1. If the number of sorted tuples of size $2^{s}$ is even, then all the sorted tuples of size $2^{s}$ are paired up in pairs. We then reuse the $Merge()$ function by 
	      providing each pair as an argument. We thus obtain sorted tuples of size $2^{s + 1}$ 

			- 1.1. If a remainder from the previous iteration is present, then this remainder is preserved as is (= this remainder is not provided as an argument with a sorted tuple of size $2^{s}$ 
			  to the $Merge()$ function). We then proceed directly to step 3

			- 1.2. If no remainder from the previous iteration is present, then we proceed directly to step 3


		- 2. If the number of sorted tuples of size $2^{s}$ is odd, then all sorted tuples of size $2^{s}$ (except the last sorted tuple of size $2^{s}$) are paired up in pairs. 
          We then reuse the $Merge()$ function by providing each pair as an argument. We thus obtain sorted tuples of size $2^{s + 1}$ 

			- 2.1. If a remainder from the previous iteration is present, then this remainder is paired with the last sorted tuple of size $2^{s}$ (since the last sorted tuple of size $2^{s}$ is not  
              paired with another sorted tuple of size $2^{s}$). 
              We then reuse the $Merge()$ function by providing this specific pair as an argument. We thus obtain a sorted tuple of size between $0$ and $2^{s} - 1$. 
              We then proceed directly to step 3

			- 2.2. If a remainder from the previous iteration is not present, then the last sorted tuple of size $2^{s}$ becomes the remainder of the current iteration. 
              We then proceed directly to step 3


		- 3. We start again from step 1 until we obtain an unique sorted tuple, possibly accompanied by a remainder. The size of this single sorted tuple is a power of $2$, and the 
          “length” (in this context) of this unique sorted tuple must be as large as possible without exceeding the cardinality (= the “size”) of the set $S_{5}$. 
          1 iteration corresponds to 1 execution of step 3. In other words, each repetition of step 3 corresponds to 1 iteration

            - 3.1. If this unique sorted tuple is accompanied by a remainder, then this unique sorted tuple is paired with the remainder. We then reuse the $Merge()$ function by providing 
              this specific pair as an argument. We thus obtain a “final sorted tuple” which has the same “length” (in this context) as the set $S_{5}$. This “final sorted tuple” is the “sorted version” 
              of the set $S_{5}$.
              Step 3.2 is skipped
		
			- 3.2. If this unique sorted tuple is not accompanied by a remainder, then this unique sorted tuple is the ‘final sorted tuple’ which has the same ‘length’ (in this context) as 
              the set $S_{5}$. This "final sorted tuple" is the "sorted version" of the set $S_{5}$ 




	- (French) Comme un ensemble (qu'on appelera $S_{5}$) peut être vu comme l'union de ses singletons, comme chaque singleton est trié, et comme chaque singleton peut être vu comme un
	  1-uplet, alors on peut utiliser la fonction $Merge()$ en mettant en argument ces 1-uplets deux à deux. 
      On obtient ainsi des tuples triés de taille $2^{1}$, avec éventuellement un reste (un tuple de taille inférieure à $2^{1}$). On dit qu'on est ici à "l'itération 1"


	- (French) On peut ensuite généraliser ce processus à une itération quelconque (qu'on appellera itération quelconque "$s$") :


		- 1. Si le nombre de tuples triés de taille $2^{s}$ est pair, alors tous les tuples triés de taille $2^{s}$ sont appariés deux à deux. On utilise ensuite la fonction $Merge()$ en mettant en 
		  argument chaque paire. On obtient ainsi des tuples triés de taille $2^{s + 1}$ 

			- 1.1. Si un reste de l'itération précédente est présent, alors ce reste est conservé tel quel (= ce reste n'est pas mis en argument avec un tuple trié de taille $2^{s}$ dans la fonction 
			  $Merge()$ ). On passe ensuite directement à l'étape 3
			
			- 1.2. Si un reste de l'itération précédente n'est pas présent, alors on passe directement à l'étape 3


		- 2. Si le nombre de tuples triés de taille $2^{s}$ est impair, alors tous les tuples triés de taille $2^{s}$ (sauf le dernier tuple trié de taille $2^{s}$) sont appariés deux à deux. 
		  On réutilise ensuite la fonction $Merge()$ en mettant en argument chaque paire. On obtient ainsi des tuples triés de taille $2^{s + 1}$ 

			- 2.1. Si un reste de l'itération précédente est présent, alors ce reste est apparié avec le dernier tuple trié de taille $2^{s}$ (car le dernier tuple trié de taille $2^{s}$ ne peut 
			  pas être apparié avec un autre tuple trié de taille $2^{s}$). 
              On réutilise ensuite la fonction $Merge()$ en mettant en argument cette paire spécifique. On obtient ainsi un tuple trié de taille comprise entre $0$ et $2^{s} - 1$. 
              On passe ensuite directement à l'étape 3

			- 2.2. Si un reste de l'itération précédente n'est pas présent, alors le dernier tuple trié de taille $2^{s}$ devient le reste de l'itération actuelle. 
			  On passe ensuite directement à l'étape 3


		- 3. On recommence à partir de l'étape 1 jusqu'à obtenir un unique tuple trié, accompagné éventuellement d'un reste. La taille de cet unique tuple trié est une puissance de $2$, et la 
		  "longueur" (dans ce contexte) de cet unique tuple trié a besoin d'être la plus grande possible sans dépasser le cardinal (= la "taille") de l'ensemble $S_{5}$. 
		  1 itération correspond à 1 exécution de l'étape 3. Autrement dit, chaque répétition de l'étape 3 constitue 1 itération

			- 3.1. Si cet unique tuple trié est accompagné d'un reste, alors cet unique tuple trié est apparié avec le reste. On réutilise ensuite la fonction $Merge()$ en mettant en argument 
			  cette paire spécifique. On obtient ainsi un "tuple trié final" qui a la même "longueur" (dans ce contexte) que l'ensemble $S_{5}$. Ce "tuple trié final" est la "version triée" 
			  de l'ensemble $S_{5}$.
			  L'étape 3.2 est ignorée
		
			- 3.2. Si cet unique tuple trié n'est pas accompagné d'un reste, alors cet unique tuple trié est le "tuple trié final" qui a la même "longueur" (dans ce contexte) que 
			  l'ensemble $S_{5}$. Ce "tuple trié final" est la "version triée" de l'ensemble $S_{5}$ 


- In general, and by applying the process described above to sets, a tuple of size $2^{s}$ and a subset (from $S_{5}$) of cardinality $2^{s}$ can both be viewed as a " block of size $2^{s}$ " (or a "block")




- From parts 13 to 40, we choose to automatize the steps 1 to 3 described above so that they can be applied to any starting set $S_{5}$ 
  (a starting set that can potentially contain several million elements) :


- We summarize all the information we have so far below :
	
	- The $Merge()$ function can be called multiple times
	
	- The $Merge()$ function takes exactly two sorted tuples as arguments on each call
	
	- For each of the two sorted tuples passed as arguments to the $Merge()$ function, the function needs to manipulate indexed elements to produce a new sorted tuple. 
	  This means that on each call to the $Merge()$ function, for each tuple passed as an argument, the indices of its elements (= elements of the tuple) need to be between two 
	  calculated bounds
	
	- any set (generally speaking) has a cardinal number (a "size") that can be manipulated directly, contrary to a tuple
	
	- any set (generally speaking) can be manipulated using "native operators that are directly built in", contrary to a tuple
	
	- the starting set $S_{5}$ is first partitioned into singletons (singletons being represented as 1-tuples), thus guaranteeing that each "starting unit" is already sorted
	
	- steps 1 to 3 can be viewed as a “subdivision process” that uses the structure of powers of $2$ to partition the starting set $S_{5}$ into subset(s) 
	  (subset(s) being represented as tuple) via indices at each iteration $s$ 
	
	- this "subdivision process" systematically merges (= passes as an argument to the $Merge()$ function (to produce the result)) pairs of subsets of size $2^{s}$ (already sorted) 
	  to produce one or more subsets of size $2^{s + 1}$, while preserving a potential subset (the "remainder") whose size is between 0 and $2^{s} - 1$ 




- We therefore have the following objectives :

	- 1. to show that any starting set $S_{5}$ and all its possible subsets follow this "subdivision process"
	
	- 2. to identify the bounds and indices of the elements of the starting set $S_{5}$ and all its possible subsets
	
	- 3. to express the tuples concerned from the starting set $S_{5}$ and all its possible subsets and show that these tuples follow this “subdivision process”
	
	  Identifying the bounds and the indices of the elements of the starting set $S_{5}$ and all its possible subsets can show that for any pair of tuples 
	  (tuples being expressed from these sets), any call to the Merge() function does indeed produce a new sorted tuple
	
	  In other words, by identifying the bounds and the indices of the elements of the starting set $S_{5}$ and all its possible subsets, we also "indirectly" identify the bounds 
	  and the indices of the elements of these tuples (because a tuple can be expressed from a starting set or a subset)


- To fill objectives 1 and 2, a first approach consists of finding a general formula describing this "subdivision process" at any iteration $s$ from the starting set $S_{5}$. If such a general formula is 
  found, then, using this formula, we will examine if we can identify bounds and indices of the elements of the starting set $S_{5}$ and of all its possible subsets. 
  More generally, we therefore need to focus on building such a general formula




- Parts 13 to 21 will focus on objectives 1 and 2

- Parts 25 to 40 will focus on objective 3




- In this part, since $S_{5}$ needs to be decomposed into blocks of $2^s$ (with potentially a "remainder") to follow the "subdivision process" at iteration $s$, then we express 
  the index of the last element $\gamma$ of the starting set $S_{5}$ as blocks of size $2^{s}$ (potentially accompanied by a block (the "remainder") whose size is between 0 and $2^{s - 1} - 1$ )
	
	- $s$ is the current iteration (see steps 1 to 3 of part 13) and is also the exponent of a block ($s$ is a naturel number, since a block do not have a "negative size")
	
	- $L = 2^{s}$ (the divisor $L$) is the number of elements of $S_{5}$ in one individual block. In other words, $L$ is the size of one individual block
	
	- Moreover, $L = \underbrace{2^{s}}_{\in \mathbb{N}} \iff \lfloor 1 \cdot 2^{s} \rfloor \iff \boxed{1 \ll_{2} s}$ (we thus have a bitwise left-shift which corresponds to 1 CPU cycle (which is optimal) )
	
	- $q = \lfloor \frac{\gamma}{2^{s}} \rfloor$ (the quotient $q$) represents the number of blocks of size $2^{s}$ that can be formed using $\gamma$ elements from the set $S_{5}$ 
	
	- $r = \gamma - q \cdot 2^{s}$ (the remainder $r$) represents all the remaining elements (elements of the set $S_{5}$) that form a block whose size is between $0$ and $2^{s} - 1$ 
	
	- $q \cdot L$ is the number of elements of $S_{5}$ in $q$ blocks. In other words, $q \cdot L$ is the size of the $q$ blocks

	- For example, if we have $\gamma = 10$ and $2^s = 4$, then :
		
		$q = 2$ (we can form 2 blocks of size $2^{s}$ using 10 elements from the set $S_{5}$)
		$q \cdot 2^s = 8$ (there are 8 elements of $S_{5}$ in the 2 blocks)
		$r = 2$ (there are 2 elements remaining that form a block whose size is between $0$ and $2^{s} - 1$)

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists d_{(1)}, d_{(2)}, \dots, d_{(\gamma - 1)}, d_{(\gamma)} \in \mathbb{R}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\boxed{
S_{5}
:=
\Big\{
d_{(1)}, 
d_{(2)}, 
\dots, 
d_{(\gamma - 1)}, 
d_{(\gamma)}
\Big\}
}
=
\Big\{
d_{\boxed{(1)}}, 
d_{(2)}, 
\dots, 
d_{(\gamma - 1)}, 
d_{\boxed{(\gamma)}}
\Big\}
\Bigg)
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\boxed{
\underbrace{
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! (q, r) \in \mathbb{N}^{2}, \quad
\bigg(
L
:=
\boxed{
2^{s}
}
\bigg)
\land
\bigg(
\gamma
=
\underbrace{
L + L + \dots + L
}_{\boxed{q \text{ times}}}
+
r
\bigg)
\land
\bigg(
0 \leq r < |L|
\bigg)
\Bigg)
}_{
\forall x \in \mathbb{Z}, \quad
\forall n \in \mathbb{Z}_{>0}, \quad
\exists! (q,r) \in \mathbb{Z}^{2}, \quad
\big(
x = q \times n + r
\big)
\land
\big(
0 \leq r < |n|
\big)
\text{ form}
}
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
\gamma
=
\underbrace{
L + L + \dots + L
}_{q \text{ times}}
+
r
\Big)
\land
\Big(
0 \leq r < \underbrace{|L|}_{\boxed{> 0}}
\Big)
\bigg)
\iff
\underline{
\bigg(
\Big(
\gamma
=
q \cdot L + r
\Big)
\land
\Big(
0 \leq r < L
\Big)
\bigg)
}
\iff
\bigg(
\boxed{
\Big(
\gamma
=
q \cdot 2^{s} + r
\Big)
}
\land
\Big(
0 \leq r < 2^{s}
\Big)
\bigg)
\iff
\bigg(
\Big(
\frac{\gamma}{2^{s}}
=
\frac{q \cdot 2^{s} + r}{2^{s}}
\Big)
\land
\Big(
0 \leq \frac{r}{2^{s}} < \frac{2^{s}}{2^{s}}
\Big)
\bigg)
\iff
\bigg(
\Big(
\frac{\gamma}{2^{s}}
=
q
+
\frac{r}{2^{s}}
\Big)
\land
\Big(
0 \leq \frac{r}{2^{s}} < 1
\Big)
\bigg)
\\[1em]
\quad
\iff
\bigg(
\Big(
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
=
\lfloor
\underbrace{q}_{\boxed{\in \mathbb{N}}}
+
\underbrace{\frac{r}{2^{s}}}_{\boxed{\in \mathbb{R}}}
\rfloor
\Big)
\land
\boxed{
\Big(
0 \leq \frac{r}{2^{s}} < 1
\Big)
}
\bigg)
\iff
\bigg(
\Big(
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
=
q
+
\lfloor
\frac{r}{2^{s}}
\rfloor
\Big)
\land
\boxed{
\Big(
\lfloor
\frac{r}{2^{s}}
\rfloor
=
0
\Big)
}
\bigg)
\iff
\boxed{
\bigg(
\Big(
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
=
q
\Big)
\land
\Big(
\lfloor
\frac{r}{2^{s}}
\rfloor
=
0
\Big)
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Part 14 :

- In this part, since we know that $\gamma = q \cdot L + r$, we examine if the set of the indices of all the elements of $S_{5}$ can be viewed as the "union of the set of the indices of all the elements 
  (elements of $S_{5}$) of the $q$ blocks (where each of these blocks is exactly of size $L$) and of the set of the indices of all the remaining elements (elements of $S_{5}$) of the block 
  whose size is between $0$ and $2^{s} - 1$ ". 
  This shows if the relation between each of these sets is coherent with the "subdivision process" from the perspective of the indices
	
	- $\mathcal{I}_{T}$ is the set of the indices of all the elements of $S_{5}$ 
	
	- $\mathcal{I}_{B}$ is the set of the indices of all the elements (elements of $S_{5}$) of the $q$ blocks (where each of these blocks is exactly of size $L$)
	
	- $\mathcal{I}_{R}$ is the set of the indices of all the remaining elements (elements of $S_{5}$) of the block whose size is between $0$ and $2^{s} - 1$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! (q, r) \in \mathbb{N}^{2}, \quad
\bigg(
\Big(
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
=
q
\Big)
\land
\Big(
r
=
\gamma - q \cdot \boxed{L}
\Big)
\land
\Big(
q \cdot \boxed{L} + r
\Big)
\land
\Big(
0 \leq r < \boxed{L}
\Big)
\bigg)
\iff
\bigg(
\Big(
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
=
q
\Big)
\land
\Big(
r
=
\gamma - q \cdot \boxed{2^{s}}
\Big)
\land
\Big(
\gamma
=
q \cdot \boxed{2^{s}} + r
\Big)
\land
\Big(
0 \leq r < \boxed{2^{s}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\{
1, \dots, \gamma
\}
=
\{
1, \dots, \boxed{q \cdot 2^{s} + r}
\}
\bigg)
\iff
\bigg(
\{
1, \dots, \gamma
\}
=
\{
1, \dots, q \cdot 2^{s} + \boxed{0}, \quad q \cdot 2^{s} + \boxed{1}, \dots, q \cdot 2^{s} + \boxed{r}
\}
\bigg)
\iff
\boxed{
\bigg(
\{
1, \dots, \gamma
\}
=
\{
1, \dots, q \cdot 2^{s}, \quad q \cdot 2^{s} + 1, \dots, q \cdot 2^{s} + r
\}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
Card(
\{
1, \dots, q \cdot 2^{s}
\}
)
=
q \cdot 2^{s} - 1 + 1
=
q \cdot 2^{s}
\bigg)
}
\land
\bigg(
\Big(
Card(
\{
q \cdot 2^{s} + 1, \dots, q \cdot 2^{s} + r
\}
)
=
q \cdot 2^{s} + r
-
(
q \cdot 2^{s} + 1
)
+
1
\Big)
\iff
\Big(
Card(
\{
q \cdot 2^{s} + 1, \dots, q \cdot 2^{s} + r
\}
)
=
q \cdot 2^{s} + r
-
q \cdot 2^{s} - 1
+
1
\Big)
\iff
\boxed{
\Big(
Card(
\{
q \cdot 2^{s} + 1, \dots, q \cdot 2^{s} + r
\}
)
=
r
\Big)
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underline{
\bigg(
\{
1, \dots, \gamma
\}
=
\{
1, \dots, q \cdot 2^{s}, \quad q \cdot 2^{s} + 1, \dots, q \cdot 2^{s} + r
\}
\bigg)
\iff
\bigg(
\{
1, \dots, \gamma
\}
=
\{
1, \dots, q \cdot 2^{s}
\}
\ \cup \
\{
q \cdot 2^{s} + 1, \dots, q \cdot 2^{s} + r
\}
\bigg)
}
\iff
\boxed{
\bigg(
\Big(
\{
1, \dots, \gamma
\}
=
\{
1, \dots, q \cdot 2^{s}
\}
\ \cup \
\{
q \cdot 2^{s} + 1, \dots, \gamma
\}
\Big)
\because
\Big(
\gamma
=
q \cdot 2^{s} + r
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! \mathcal{I}_{T} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists \mathcal{I}_{B}, \mathcal{I}_{R} \subseteq \mathcal{I}_{T}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\boxed{
\bigg(
\mathcal{I}_{T}
:=
\{
1, \dots, \gamma
\}
\bigg)
\land
\bigg(
\mathcal{I}_{B}
:=
\{
1, \dots, q \cdot L
\}
\bigg)
\land
\bigg(
Card(\mathcal{I}_{B})
=
q \cdot 2^{s}
\bigg)
\land
\bigg(
\mathcal{I}_{R}
:=
\{
q \cdot L + 1, \dots, \gamma
\}
\bigg)
\land
\bigg(
Card(\mathcal{I}_{R})
=
r
\bigg)
\land
\bigg(
0 \leq Card(\mathcal{I}_{R}) < 2^{s}
\bigg)
\land
\bigg(
\mathcal{I}_{T}
=
\mathcal{I}_{B}
\ \cup \
\mathcal{I}_{R}
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Part 15 :

- In this part, we examine if $\mathcal{I}_{B}$ can be viewed as the "union of all the sets being each the set of the indices of all the elements (elements of $S_{5}$) of one individual block of size $2^{s}$. 
  This shows if the relation between each of these sets and $\mathcal{I}_{B}$ is coherent with the "subdivision process" from the perspective of the indices
	
	- $\mathcal{I}_{(\zeta)}$ is the set of the indices of all the elements (elements of $S_{5}$) of the $\zeta$-th block of size $2^{s}$ 

	- It is possible to have multiple $\mathcal{I}_{B}, \mathcal{I}_{R}$ and $\mathcal{I}_{(\zeta)}$, because each iteration $s$ has its own subsets

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\mathcal{I}_{B}
=
\Big\{
1, \dots, q \cdot L
\Big\}
\Bigg)
}
\\[1em]
\Rightarrow
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\exists! \vartheta \in \mathcal{I}_{B}, \quad
\left(
\mathcal{I}_{B}
=
\Big\{
1, \dots, \boxed{q \cdot L}
\Big\}
=
\underbrace{
\overbrace{
\Big\{
1, \dots, \boxed{1 \cdot L}
\Big\}
}^{
\boxed{
\mathcal{I}_{(1)}
}
}
}_{
\boxed{
Card\Big(
\Big\{
1, \dots, 1 \cdot L
\Big\}
\Big)
=
L
=
2^{s}
}
}
\ \cup \
\underbrace{
\overbrace{
\Big\{
1 \cdot L + 1, \dots, \boxed{2 \cdot L}
\Big\}
}^{
\boxed{
\mathcal{I}_{(2)}
}
}
}_{
Card\Big(
\Big\{
1 \cdot L + 1, \dots, 2 \cdot L
\Big\}
\Big)
=
\boxed{L}
}
\ \cup \
\underbrace{
\overbrace{
\Big\{
2 \cdot L + 1, \dots, \boxed{3 \cdot L}
\Big\}
}^{
\boxed{
\mathcal{I}_{(3)}
}
}
}_{
Card\Big(
\Big\{
2 \cdot L + 1, \dots, 3 \cdot L
\Big\}
\Big)
=
\boxed{L}
}
\ \cup \
\dots
\ \cup \
\boxed{
\underbrace{
\overbrace{
\Big\{
\vartheta, \dots, \boxed{q \cdot L}
\Big\}
}^{
\boxed{
\mathcal{I}_{(q)}
}
}
}_{
Card\Big(
\Big\{
\vartheta, \dots, q \cdot L
\Big\}
\Big)
=
\boxed{L}
}
}
\right)
\land
\left(
\underbrace{
\boxed{
\vartheta
}
:=
q \cdot 2^{s}
-
Card\Big(
\Big\{
\vartheta, \dots, q \cdot L
\Big\}
\Big)
+
1
=
q \cdot 2^{s}
-
2^{s} + 1
=
(q - 1) \cdot 2^{s} + 1
=
\boxed{
(q - 1) \cdot L + 1
}
}_{
\ \because \
Card\big(
\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}
\big)
=
(\text{endingIndex} - \text{startingIndex}) + 1
}
\right)
\right)
\\[1em]
\Rightarrow
\underline{
\Bigg(
\mathcal{I}_{B}
=
\Big\{
1, \dots, q \cdot L
\Big\}
=
\Big\{
1, \dots, 1 \cdot L
\Big\}
\ \cup \
\Big\{
1 \cdot L + 1, \dots, 2 \cdot L
\Big\}
\ \cup \
\Big\{
2 \cdot L + 1, \dots, 3 \cdot L
\Big\}
\ \cup \
\dots
\ \cup \
\Big\{
(q - 1) \cdot L + 1, \dots, q \cdot L
\Big\}
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\forall \zeta \in \{1, \dots, q\}, \quad
\exists! \vartheta_{(\zeta)} \in \mathcal{I}_{B}, \quad
\boxed{
\bigg(
\mathcal{I}_{(\zeta)}
:=
\Big\{
\vartheta_{(\zeta)}, \dots, \zeta \cdot L
\Big\}
\bigg)
}
\land
\bigg(
Card\Big(
\mathcal{I}_{(\zeta)}
\Big)
=
L
=
\boxed{
2^{s}
}
\bigg)
\land
\bigg(
\underbrace{
\boxed{
\vartheta_{(\zeta)}
}
:=
\zeta \cdot 2^{s}
-
Card\Big(
\Big\{
\vartheta_{(\zeta)}, \dots, \zeta \cdot L
\Big\}
\Big)
+
1
=
\zeta \cdot 2^{s}
-
2^{s} + 1
=
(\zeta - 1) \cdot 2^{s} + 1
=
\boxed{
(\zeta - 1) \cdot L + 1
}
}_{
\ \because \
Card\big(
\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}
\big)
=
(\text{endingIndex} - \text{startingIndex}) + 1
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \zeta \in \{1, \dots, q\}, \quad
\boxed{
\bigg(
\mathcal{I}_{(\zeta)}
=
\Big\{
(\zeta - 1) \cdot L + 1, \dots, \zeta \cdot L
\Big\}
\bigg)
}
\land
\bigg(
\boxed{
\mathcal{I}_{(\zeta = 1)}
}
=
\Big\{
1, \dots, 1 \cdot L
\Big\}
=
\boxed{
\mathcal{I}_{(1)}
}
\bigg)
\land
\bigg(
\boxed{
\mathcal{I}_{(\zeta = 2)}
}
=
\Big\{
1 \cdot L + 1, \dots, 2 \cdot L
\Big\}
=
\boxed{
\mathcal{I}_{(2)}
}
\bigg)
\land
\bigg(
\boxed{
\mathcal{I}_{(\zeta = 3)}
}
=
\Big\{
2 \cdot L + 1, \dots, 3 \cdot L
\Big\}
=
\boxed{
\mathcal{I}_{(3)}
}
\bigg)
\land
\dots
\land
\bigg(
\boxed{
\mathcal{I}_{(\zeta = q)}
}
=
\Big\{
(q - 1) \cdot L + 1, \dots, q \cdot L
\Big\}
=
\boxed{
\mathcal{I}_{(q)}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \zeta \in \{1, \dots, q\}, \quad
\boxed{
\mathcal{I}_{B}
=
\Big\{
1, \dots, q \cdot L
\Big\}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\Big\{
(\zeta - 1) \cdot L + 1, \dots, \zeta \cdot L
\Big\}
}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\mathcal{I}_{(\zeta)}
}
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! \mathcal{I}_{T} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists \mathcal{I}_{B}, \mathcal{I}_{R} \subseteq \mathcal{I}_{T}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\exists \mathcal{I}_{(\zeta)} \subset \mathcal{I}_{T}, \quad
\boxed{
\bigg(
\mathcal{I}_{T}
=
\mathcal{I}_{B}
\ \cup \
\mathcal{I}_{R}
\bigg)
\iff
\bigg(
\mathcal{I}_{T}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\mathcal{I}_{(\zeta)}
}
\ \cup \
\mathcal{I}_{R}
\bigg)
\iff
\bigg(
\mathcal{I}_{T}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\Big\{
(\zeta - 1) \cdot L + 1, \dots, \zeta \cdot L
\Big\}
}
\ \cup \
\Big\{
q \cdot L + 1, \dots, \gamma
\Big\}
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Part 16 :

- In this part, we rewrite the last index $\zeta \cdot L$ of the set $\mathcal{I}_{(\zeta)}$ in the same form as the first index, in order to standardize the index format. Then, we show that the intersection any two 
  different sets (each being specifically the set of the indices of all the elements (elements of $S_{5}$) of one distinct block of size $2^{s}$) have no element in common

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\bigg(
\mathcal{I}_{(\zeta)}
=
\Big\{
(\zeta - 1) \cdot L + 1, \dots, \zeta \cdot L
\Big\}
\bigg)
\land
\bigg(
\mathcal{I}_{T}
=
\Big\{
1, \dots, \gamma
\Big\}
\bigg)
\land
\bigg(
\mathcal{I}_{B}
=
\Big\{
1, \dots, q \cdot L
\Big\}
\bigg)
\land
\bigg(
\mathcal{I}_{R}
=
\Big\{
q \cdot L + 1, \dots, \gamma
\Big\}
\bigg)
\land
\bigg(
\mathcal{I}_{T}
=
\mathcal{I}_{B}
\ \cup \
\mathcal{I}_{R}
\bigg)
\land
\bigg(
S_{5}
=
\Big\{
d_{(1)}, 
d_{(2)}, 
\dots, 
d_{(\gamma - 1)}, 
d_{(\gamma)}
\Big\}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\mathcal{I}_{(\zeta)}
}
=
\Big\{
(\zeta - 1) \cdot L + 1, \dots, \zeta \cdot L
\Big\}
=
\Big\{
(\zeta - 1) \cdot L + 1, \dots, \boxed{(\zeta - 1) \cdot L + L}
\Big\}
\bigg)
\because
\bigg(
\underbrace{
\boxed{
\zeta \cdot L
}
=
\Big(
Card\Big(
\mathcal{I}_{(\zeta)}
\Big)
+
(\zeta - 1) \cdot L + 1
\Big)
- 1
=
L + (\zeta - 1) \cdot L + 1 - 1
=
\boxed{
(\zeta - 1) \cdot L + L
}
}_{
\text{endingIndex}
=
Card\big(
\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}
\big)
+
\text{startingIndex} - 1
\text{ form}
}
\bigg)
\Bigg)
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
P :
\Bigg(
\exists \zeta' \in \{1, \dots, q\}, \quad
\exists \zeta'' \in \{1, \dots, q\}, \quad
\bigg(
\zeta'
\neq
\zeta''
\bigg)
\land
\bigg(
\underbrace{
\Big\{
(\zeta' - 1) \cdot L + 1, \dots, \zeta' \cdot L
\Big\}
}_{
\mathcal{I}_{(\zeta')}
}
\ \cap \
\underbrace{
\Big\{
(\zeta'' - 1) \cdot L + 1, \dots, \zeta'' \cdot L
\Big\}
}_{
\mathcal{I}_{(\zeta'')}
}
\neq
\emptyset
\bigg)
\Bigg)
\Bigg)
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
P
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \zeta' \in \{1, \dots, q\}, \quad
\exists \zeta'' \in \{1, \dots, q\}, \quad
\bigg(
\zeta'
\neq
\zeta''
\bigg)
\land
\bigg(
\exists \mathcal{X} \in \mathcal{I}_{T}, \quad
\mathcal{X} \in
\Big\{
(\zeta' - 1) \cdot L + 1, \dots, \zeta' \cdot L
\Big\}
\land
\mathcal{X} \in
\Big\{
(\zeta'' - 1) \cdot L + 1, \dots, \zeta'' \cdot L
\Big\}
\neq
\emptyset
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
(\zeta' - 1) \cdot L + 1
\leq
\mathcal{X}
\leq
\zeta' \cdot L
\bigg)
\land
\bigg(
(\zeta'' - 1) \cdot L + 1
\leq
\mathcal{X}
\leq
\zeta'' \cdot L
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\zeta' < \zeta''
\bigg)
\Rightarrow
\bigg(
\Big(
\zeta' \leq \zeta'' - 1
\Big)
\iff
\Big(
\zeta' \cdot L \leq (\zeta'' - 1) \cdot L
\Big)
\iff
\Big(
\mathcal{X} \leq \zeta' \cdot L \leq (\zeta'' - 1) \cdot L < (\zeta'' - 1) \cdot L + 1 \leq \mathcal{X}
\Big)
\iff
\Big(
\mathcal{X} < \mathcal{X}
\Big)
\bigg)
\Rightarrow
\bigg(
\bot
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\neg P
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\forall \zeta' \in \{1, \dots, q\}, \quad
\forall \zeta'' \in \{1, \dots, q\}, \quad
\bigg(
\zeta'
\neq
\zeta''
\bigg)
\Rightarrow
\bigg(
\Big\{
(\zeta' - 1) \cdot L + 1, \dots, \zeta' \cdot L
\Big\}
\ \cap \
\Big\{
(\zeta'' - 1) \cdot L + 1, \dots, \zeta'' \cdot L
\Big\}
=
\emptyset
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 17 :

- In this part, since $Card\Big(\Big\{d_{((\zeta - 1) \cdot L + 1)}, \dots, d_{(\zeta \cdot L)}\Big\}\Big)=Card\Big(\mathcal{I}_{(\zeta)}\Big)$ (i.e. the number of indices corresponds to the number of elements), then we examine if we can build the 
  set of all the elements (elements of $S_{5}$) of the $\zeta$-th block of size $2^{s}$ (at iteration $s$) by also reusing the properties of $\mathcal{I}_{(\zeta)}$ 
  (in order to be consistent with the "subdivision process" from the perspective of the "blocks")

	- $\mathcal{B}_{(\zeta, s)}$ is the set of all the elements (elements of $S_{5}$) of the $\zeta$-th block of size $2^{s}$ (at iteration $s$)

	- $\mathcal{B}_{(\zeta, s)} = \overset{L}{\underset{\tau = 1}{\bigcup}}{\Big\{d_{((\zeta - 1) \cdot L + \tau)}\Big\}}$ means that $\mathcal{B}_{(\zeta, s)}$ can be viewed as the union of all its own singletons $\{d_{((\zeta - 1) \cdot L + 1)}\}, \dots, \{d_{((\zeta - 1) \cdot L + L)}\}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\bigg(
Card\Big(
\Big\{
d_{((\zeta - 1) \cdot L + 1)}, \dots, d_{(\zeta \cdot L)}
\Big\}
\Big)
=
Card\Big(
\mathcal{I}_{(\zeta)}
\Big)
\bigg)
}
\Rightarrow
\bigg(
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\boxed{
B_{(\zeta, s)}
:=
\Big\{
d_{((\zeta - 1) \cdot L + 1)}, \dots, d_{(\zeta \cdot L)}
\Big\}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\exists B_{(\zeta, s)} \subset S_{5}, \quad
\Bigg(
B_{(\zeta, s)}
=
\Big\{
d_{((\zeta - 1) \cdot L + 1)}, \dots, d_{(\zeta \cdot L)}
\Big\}
\Bigg)
\iff
\Bigg(
B_{(\zeta, s)}
=
\Big\{
d_{((\zeta - 1) \cdot L + 1)}, \ \ 
d_{((\zeta - 1) \cdot L + 2)}, \ \ 
d_{((\zeta - 1) \cdot L + 3)}, \ \ 
\dots, \ \ 
d_{(\zeta \cdot L)}
\Big\}
\Bigg)
\iff
\Bigg(
B_{(\zeta, s)}
=
\Big\{
d_{((\zeta - 1) \cdot L + 1)}
\Big\}
\ \cup \
\Big\{
d_{((\zeta - 1) \cdot L + 2)}
\Big\}
\ \cup \
\Big\{
d_{((\zeta - 1) \cdot L + 3)}
\Big\}
\ \cup \
\dots
\ \cup \
\Big\{
d_{(\zeta \cdot L)}
\Big\}
\Bigg)
\iff
\Bigg(
B_{(\zeta, s)}
=
{\underset{\psi \in \mathcal{I}_{(\zeta)}}{\bigcup}}{
\Big\{
d_{(\psi)}
\Big\}
}
\Bigg)
\\[1em]
\quad
\iff
\Bigg(
B_{(\zeta, s)}
=
\Big\{
d_{((\zeta - 1) \cdot L + 1)}, \ \ 
d_{((\zeta - 1) \cdot L + 2)}, \ \ 
d_{((\zeta - 1) \cdot L + 3)}, \ \ 
\dots, \ \ 
d_{\boxed{(\zeta \cdot L)}}
\Big\}
\Bigg)
\iff
\boxed{
\Bigg(
B_{(\zeta, s)}
=
\Big\{
d_{((\zeta - 1) \cdot L + \boxed{1})}, \ \ 
d_{((\zeta - 1) \cdot L + \boxed{2})}, \ \ 
d_{((\zeta - 1) \cdot L + \boxed{3})}, \ \ 
\dots, \ \ 
d_{((\zeta - 1) \cdot L + \boxed{L})}
\Big\}
\Bigg)
}
\iff
\boxed{
\Bigg(
B_{(\zeta, s)}
=
\overset{L}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot L + \boxed{\tau})}
\Big\}
}
\Bigg)
}
\ \
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
B_{(\zeta = 1, s = s)}
}
=
\Big\{
d_{(1)}, 
\dots, 
d_{(1 \cdot L)}
\Big\}
\bigg)
\land
\bigg(
\boxed{
B_{(\zeta = 2, s = s)}
}
=
\Big\{
d_{(1 \cdot L + 1)}, 
\dots, 
d_{(2 \cdot L)}
\Big\}
\bigg)
\land
\bigg(
\boxed{
B_{(\zeta = 3, s = s)}
}
=
\Big\{
d_{(2 \cdot L + 1)}, 
\dots, 
d_{(3 \cdot L)}
\Big\}
\bigg)
\land
\dots
\land
\bigg(
\boxed{
B_{(\zeta = q, s = s)}
}
=
\Big\{
d_{((q - 1) \cdot L + 1)}, 
\dots, 
d_{(q \cdot L)}
\Big\}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 18 :

- In this part, since $Card\Big(\Big\{d_{(1)}, \dots, d_{(q \cdot L)}\Big\}\Big)=Card\Big(\mathcal{I}_{B}\Big)$ (i.e. the number of indices corresponds to the number of elements), then we examine if we can build the set of all the elements 
  (elements of $S_{5}$) of the $q$ blocks (where each of these blocks is exactly of size $L$) (at iteration $s$) 
  (in order to be consistent with the "subdivision process" from the perspective of the "blocks")

	- $B_{s}$ is the set of all the elements (elements of $S_{5}$) of the $q$ blocks (where each of these blocks is exactly of size $L$) (at iteration $s$)

	- $B_{s}=\overset{q}{\underset{\zeta = 1}{\bigcup}}{B_{(\zeta, s)}}$ means that $B_{s}$ can be viewed as the union of all the sets $\mathcal{B}_{(1, s)}, \dots, \mathcal{B}_{(q, s)}$ 

	- $B_{s}=\overset{q}{\underset{\zeta = 1}{\bigcup}}{\left({\underset{\psi \in \mathcal{I}_{(\zeta)}}{\bigcup}}{\Big\{d_{(\psi)}\Big\}}\right)}=\overset{q}{\underset{\zeta = 1}{\bigcup}}{\left(\overset{L}{\underset{\tau = 1}{\bigcup}}{\Big\{d_{((\zeta - 1) \cdot L + \tau)}\Big\}}\right)}$ means that $B_{s}$ can also be viewed as the union of all the sets $\mathcal{B}_{(1, s)}, \dots, \mathcal{B}_{(q, s)}$, each 
	  being the union of all its own singletons $\{d_{((\zeta - 1) \cdot L + 1)}\}, \dots, \{d_{((\zeta - 1) \cdot L + L)}\}$ 

	- $\mathcal{I}_{(\zeta)}=\Big\{(\zeta - 1) \cdot L + 1, \dots, \zeta \cdot L\Big\}=\Big\{(\zeta - 1) \cdot L + 1, \dots, (\zeta - 1) \cdot L + L\Big\}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\bigg(
Card\Big(
\Big\{
d_{(1)}, \dots, d_{(q \cdot L)}
\Big\}
\Big)
=
Card\Big(
\mathcal{I}_{B}
\Big)
\bigg)
}
\Rightarrow
\bigg(
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\boxed{
B_{s}
:=
\Big\{
d_{(1)}, \dots, d_{(q \cdot L)}
\Big\}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists B_{s} \subseteq S_{5}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\exists B_{(\zeta, s)} \subset S_{5}, \quad
\Bigg(
B_{s}
=
\Big\{
d_{(1)}, \dots, d_{(q \cdot L)}
\Big\}
\Bigg)
\iff
\boxed{
\Bigg(
B_{s}
=
\underbrace{
\Big\{
d_{(1)}, 
\dots, 
d_{(1 \cdot L)}
\Big\}
}_{
\boxed{
B_{(\boxed{\zeta = 1}, s = s)}
}
}
\ \cup \
\underbrace{
\Big\{
d_{(1 \cdot L + 1)}, 
\dots, 
d_{(2 \cdot L)}
\Big\}
}_{
\boxed{
B_{(\boxed{\zeta = 2}, s = s)}
}
}
\ \cup \
\underbrace{
\Big\{
d_{(2 \cdot L + 1)}, 
\dots, 
d_{(3 \cdot L)}
\Big\}
}_{
\boxed{
B_{(\boxed{\zeta = 3}, s = s)}
}
}
\ \cup \
\dots
\ \cup \
\underbrace{
\Big\{
d_{((q - 1) \cdot L + 1)}, 
\dots, 
d_{(q \cdot L)}
\Big\}
}_{
\boxed{
B_{(\boxed{\zeta = q}, s = s)}
}
}
\Bigg)
}
\\[1em]
\quad
\iff
\Bigg(
B_{s}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot L + 1)}, \ \ 
d_{((\zeta - 1) \cdot L + 2)}, \ \ 
d_{((\zeta - 1) \cdot L + 3)}, \ \ 
\dots, \ \ 
d_{(\zeta \cdot L)}
\Big\}
}
\Bigg)
\iff
\Bigg(
B_{s}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, s)}
}
\Bigg)
\iff
\left(
B_{s}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\left(
{\underset{\psi \in \mathcal{I}_{(\zeta)}}{\bigcup}}{
\Big\{
d_{(\psi)}
\Big\}
}
\right)
}
\right)
\\[1em]
\quad
\iff
\boxed{
\Bigg(
B_{s}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot L + \boxed{1})}, \ \ 
d_{((\zeta - 1) \cdot L + \boxed{2})}, \ \ 
d_{((\zeta - 1) \cdot L + \boxed{3})}, \ \ 
\dots, \ \ 
d_{((\zeta - 1) \cdot L + \boxed{L})}
\Big\}
}
\Bigg)
}
\iff
\boxed{
\Bigg(
B_{s}
=
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\ \
\underbrace{
\left(
\overset{L}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot L + \boxed{\tau})}
\Big\}
}
\right)
}_{
\boxed{
B_{(\zeta, s)}
}
}
\ \
}
\Bigg)
}
\ \
\Bigg)
\end{cases}
\end{array}
$$

Part 19 :

- In this part, since $Card\Big(\Big\{d_{(q \cdot L + 1)}, \dots, d_{(\gamma)}\Big\}\Big)=Card\Big(\mathcal{I}_{R}\Big)$ (i.e. the number of indices corresponds to the number of elements), then we examine if we can build the set of all the 
  remaining elements (elements of $S_{5}$) of the block whose size is between $0$ and $2^{s} - 1$ (at iteration $s$) 
  (in order to be consistent with the "subdivision process" from the perspective of the "blocks")

	- $R_{s}$ is the set of all the remaining elements (elements of $S_{5}$) of the block whose size is between $0$ and $2^{s} - 1$ (at iteration $s$)

	- $R_{s}=\overset{r}{\underset{\phi = 1}{\bigcup}}{\Big\{d_{(q \cdot L + \phi)}\Big\}}$ means that $R_{s}$ can be viewed as the union of all its own singletons $\{d_{(q \cdot L + 1)}\}, \dots, \{d_{(q \cdot L + r)}\}$ 

	- $\gamma = q \cdot L + r$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\bigg(
Card\Big(
\Big\{
d_{(q \cdot L + 1)}, \dots, d_{(\gamma)}
\Big\}
\Big)
=
Card\Big(
\mathcal{I}_{R}
\Big)
\bigg)
}
\Rightarrow
\bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\boxed{
R_{s}
:=
\Big\{
d_{(q \cdot L + 1)}, \dots, d_{(\gamma)}
\Big\}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
0 \leq Card(R_{s}) < 2^{s}
\bigg)
}
\because
\bigg(
\Big(
0 \leq \underbrace{\gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s}}_{r} < 2^{s}
\Big)
\land
\Big(
Card(R_{s})
=
r
=
\gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists R_{s} \subseteq S_{5}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! (q, r) \in \mathbb{N}^{2}, \quad
\Bigg(
R_{s}
=
\Big\{
d_{(q \cdot L + 1)}, \dots, d_{(\gamma)}
\Big\}
\Bigg)
\iff
\Bigg(
R_{s}
=
\Big\{
d_{(q \cdot L + 1)}, \ \ 
d_{(q \cdot L + 2)}, \ \ 
d_{(q \cdot L + 3)}, \ \ 
\dots, \ \ 
d_{(\gamma)}
\Big\}
\Bigg)
\iff
\Bigg(
R_{s}
=
\Big\{
d_{(q \cdot L + 1)}
\Big\}
\ \cup \
\Big\{
d_{(q \cdot L + 2)}
\Big\}
\ \cup \
\Big\{
d_{(q \cdot L + 3)}
\Big\}
\ \cup \
\dots
\ \cup \
\Big\{
d_{(\gamma)}
\Big\}
\Bigg)
\iff
\Bigg(
R_{s}
=
{\underset{\Upsilon \in \mathcal{I}_{(R)}}{\bigcup}}{
\Big\{
d_{(\Upsilon)}
\Big\}
}
\Bigg)
\\[1em]
\quad
\iff
\Bigg(
R_{s}
=
\Big\{
d_{(q \cdot L + \boxed{1})}, \ \ 
d_{(q \cdot L + \boxed{2})}, \ \ 
d_{(q \cdot L + \boxed{3})}, \ \ 
\dots, \ \ 
d_{\boxed{(\gamma)}}
\Big\}
\Bigg)
\iff
\boxed{
\Bigg(
R_{s}
=
\Big\{
d_{(q \cdot L + \boxed{1})}, \ \ 
d_{(q \cdot L + \boxed{2})}, \ \ 
d_{(q \cdot L + \boxed{3})}, \ \ 
\dots, \ \ 
d_{(q \cdot L + \boxed{r})}
\Big\}
\Bigg)
}
\iff
\boxed{
\Bigg(
R_{s}
=
\overset{r}{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{(q \cdot L + \boxed{\phi})}
\Big\}
}
\Bigg)
}
\ \
\Bigg)
\end{cases}
\end{array}
$$

Part 20 :

- In this part, since $Card\Big(\Big\{d_{(1)}, \dots, d_{(\gamma)}\Big\}\Big)=Card\Big(\mathcal{I}_{T}\Big)$ (i.e. the number of indices corresponds to the number of elements), then we examine if $S_{5}$ can be expressed in terms of 
  $B_{(\zeta, s)}$ and $R_{s}$ (in order to be consistent with the "subdivision process" from the perspective of the "blocks")

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\bigg(
Card\Big(
\Big\{
d_{(1)}, \dots, d_{(\gamma)}
\Big\}
\Big)
=
Card\Big(
\mathcal{I}_{T}
\Big)
\bigg)
}
\Rightarrow
\bigg(
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\boxed{
S_{5}
=
B_{s}
\ \cup \
R_{s}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! q \in \mathbb{N}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\Bigg(
S_{5}
=
\Big\{
d_{(1)}, 
d_{(2)}, 
\dots, 
d_{(\gamma - 1)}, 
d_{(\gamma)}
\Big\}
\Bigg)
\iff
\boxed{
\Bigg(
S_{5}
=
B_{s}
\ \cup \
R_{s}
\Bigg)
}
\iff
\left(
S_{5}
=
\left(
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\left(
{\underset{\psi \in \mathcal{I}_{(\zeta)}}{\bigcup}}{
\Big\{
d_{(\psi)}
\Big\}
}
\right)
}
\right)
\ \cup \
\left(
{\underset{\Upsilon \in \mathcal{I}_{(R)}}{\bigcup}}{
\Big\{
d_{(\Upsilon)}
\Big\}
}
\right)
\right)
\\[1em]
\quad
\iff
\left(
S_{5}
=
\left(
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, s)}
}
\right)
\ \cup \
\left(
{\underset{\Upsilon \in \mathcal{I}_{(R)}}{\bigcup}}{
\Big\{
d_{(\Upsilon)}
\Big\}
}
\right)
\right)
\iff
\boxed{
\left(
S_{5}
=
\left(
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, s)}
}
\right)
\ \cup \
R_{s}
\right)
}
\iff
\left(
S_{5}
=
\left(
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot L + 1)}, \ \ 
d_{((\zeta - 1) \cdot L + 2)}, \ \ 
d_{((\zeta - 1) \cdot L + 3)}, \ \ 
\dots, \ \ 
d_{(\zeta \cdot L)}
\Big\}
}
\right)
\ \cup \
\bigg(
\Big\{
d_{(q \cdot L + 1)}, \ \ 
d_{(q \cdot L + 2)}, \ \ 
d_{(q \cdot L + 3)}, \ \ 
\dots, \ \ 
d_{(\gamma)}
\Big\}
\bigg)
\right)
\ \
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists d_{(1)}, d_{(2)}, \dots, d_{(\gamma - 1)}, d_{(\gamma)} \in \mathbb{R}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists B_{s}, R_{s} \subseteq S_{5}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! (q, r) \in \mathbb{N}^{2}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\bigg(
q
=
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
\bigg)
\land
\bigg(
L
=
2^{s}
\bigg)
\land
\bigg(
0 \leq r < |L|
\bigg)
\land
\bigg(
r
=
\gamma
-
q \cdot 2^{s}
\bigg)
\land
\left(
\ \
S_{5}
=
\Big\{
d_{(1)}, 
d_{(2)}, 
\dots, 
d_{(\gamma - 1)}, 
d_{(\gamma)}
\Big\}
=
\left(
\overset{q}{\underset{\zeta = 1}{\bigcup}}{
\left(
\overset{L}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot L + \tau)}
\Big\}
}
\right)
}
\right)
\ \cup \
\left(
\overset{r}{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{(q \cdot L + \phi)}
\Big\}
}
\right)
\ \
\right)
\right)
}
\end{cases}
\end{array}
$$

Part 21 :

- In this part, from the extracted formula of $S_{5}$ in part 20, we show the general formula describing the "subdivision process" (as mentioned in in part 13) at any iteration $s$ from the starting set $S_{5}$ 


- The formula $S_{5}$ represents the partition of the set $S_{5}$ into a disjoint union of "blocks" $B_{(\zeta, s)}$ of "size" $2^{s}$ and a potential block (the “remainder”) (whose "size" is between $0$ and $2^{s} - 1$) at 
  each iteration $s$ of the "subdivision process"

- $S_{5}$ is expressed in terms of $B_{s}$ and $R_{s}$, and $B_{s}, B_{(\zeta, s)}$ and $R_{s}$ represent all the possible subsets of $S_{5}$ 

- It is possible to have multiple $B_{s}, R_{s}$ and $B_{(\zeta, s)}$, because each iteration $s$ has its own subsets

- Thus, any starting set $S_{5}$ and all its possible subsets follow the "subdivision process"


- Moreover, we have also shown that any index of $B_{s}$ is varying between $1$ and $\lfloor \frac{\gamma}{2^{s}} \rfloor$, and that any index of $R_{s}$ is varying between $1$ and $\gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s}$, and that any index of $S_{5}$ is varying 
  between $1$ and $\gamma$, and that the bounds of each possible individual block of size $2^{s}$ are respectively $(\zeta - 1) \cdot 2^{s} + 1$ and $(\zeta - 1) \cdot 2^{s} + 2^{s}$ 

- Thus, we have identified the bounds and indices of the elements of the starting set $S_{5}$ and all its possible subsets


- The objectives $1$ and $2$ are filled

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists d_{(1)}, d_{(2)}, \dots, d_{(\gamma - 1)}, d_{(\gamma)} \in \mathbb{R}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists B_{s}, R_{s} \subseteq S_{5}, \quad
\forall \zeta \in \{1, \dots, \lfloor \frac{\gamma}{2^{s}} \rfloor\}, \quad
\exists B_{(\zeta, s)} \subset S_{5}, \quad
\bigg(
0 \leq \gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s} < 2^{s}
\bigg)
\land
\left(
S_{5}
=
\Big\{
d_{(1)}, 
\dots,  
d_{(\gamma)}
\Big\}
=
\left(
\overset{ \lfloor \frac{\gamma}{2^{s}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
\underbrace{
\left(
\overset{2^{s}}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot 2^{s} + \tau)}
\Big\}
}
\right)
}_{
\boxed{
B_{(\zeta, s)}
}
}
}
\right)
\ \cup \
\left(
\overset{\gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s}}{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{(\lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s} + \phi)}
\Big\}
}
\right)
=
\underbrace{
\left(
\overset{ \lfloor \frac{\gamma}{2^{s}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, s)}
}
\right)
}_{
B_{s}
}
\ \cup \
R_{s}
\right)
\right)
}
\end{cases}
\end{array}
$$

Part 22 :

- From part 22 to 24, we examine the bounds of $s$ 

	- Since in step 3.1 or 3.2, the unique sorted tuple of size $2^{s}$ was merged with a potential remainder to form a "final sorted tuple" that has the same length as the initial set $S_{5}$, 
	  then it means that at this step, no more blocks of size $2^{s}$ are present
	
	- And since we know that $q$ represents the number of blocks of size $2^{s}$ that can be formed using $\gamma$ elements from the set $S_{5}$, then it means that at this step, $q = 0$
	
	- Moreover, $\gamma$ is fixed during the entire subdivision process and s is variable (because it is an iteration) ; this means that $s$ has a specific value such that $q = \lfloor \frac{\gamma}{2^{s}} \rfloor = 0$
	
	
	- In this part, starting from $q = \lfloor \frac{\gamma}{2^{s}} \rfloor = 0$, we will extract $s$ to find a first relation, and we will also show that if $q = \lfloor \frac{\gamma}{2^{s}} \rfloor = 0$, then the result is indeed representative of this step

		- We have $s > \frac{\ln(\gamma)}{\ln(2)}$

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\boxed{
\bigg(
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\bigg)
}
\Rightarrow
\bigg(
\boxed{
B_{s}
}
=
\overset{ \boxed{ \lfloor \frac{\gamma}{2^{s}} \rfloor } }{\underset{\zeta = 1}{\bigcup}}{
\underbrace{
\Big(
\overset{2^{s}}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot 2^{s} + \tau)}
\Big\}
}
\Big)
}_{
\boxed{
B_{(\zeta, s)}
}
}
}
=
\overset{ \boxed{ 0 } }{\underset{\zeta = \boxed{1}}{\bigcup}}{
\underbrace{
\Big(
\overset{2^{s}}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot 2^{s} + \tau)}
\Big\}
}
\Big)
}_{
\boxed{
B_{(\zeta, s)}
}
}
}
=
\boxed{
\emptyset
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
\lfloor \underbrace{\frac{\gamma}{2^{s}}}_{\boxed{\in \mathbb{R}}} \rfloor = 0
\bigg)
}
\iff
\bigg(
\lfloor 0 \rfloor
\leq
\frac{\gamma}{2^{s}}
<
\lfloor 0 \rfloor
+ 1
\bigg)
\iff
\bigg(
0
\leq
\frac{\gamma}{2^{s}}
<
0
+ 1
\bigg)
\iff
\bigg(
\Big(
0
\leq
\frac{\gamma}{2^{s}}
<
1
\Big)
\iff
\boxed{
\underbrace{
\Big(
0
\leq
\gamma
<
2^{s}
\Big)
}_{
\ \because \
2^{s} > 0
}
}
\bigg)
\iff
\bigg(
0
\leq
1
<
\frac{2^{s}}{\gamma}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
\frac{2^{s}}{\gamma} > 1
\bigg)
}
\iff
\boxed{
\bigg(
2^{s} > \gamma
\bigg)
}
\iff
\bigg(
\ln(\underbrace{2^{s}}_{> 0}) > \ln(\underbrace{\gamma}_{> 0})
\bigg)
\iff
\bigg(
s \cdot \ln(2) > \ln(\gamma)
\bigg)
\iff
\boxed{
\bigg(
s
>
\frac{\ln(\gamma)}{\ln(2)}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\bigg(
s
>
\frac{\ln(\gamma)}{\ln(2)}
\bigg)
\Rightarrow
\bigg(
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\bigg)
\Rightarrow
\bigg(
B_{s}
=
\emptyset
\bigg)
\Bigg)
}
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\boxed{
\bigg(
s
>
\frac{\ln(\gamma)}{\ln(2)}
\bigg)
}
\Rightarrow
\bigg(
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\bigg)
\Rightarrow
\bigg(
S_{5}
=
\overset{ \boxed{ \lfloor \frac{\gamma}{2^{s}} \rfloor } }{\underset{\zeta = 1}{\bigcup}}{
\Big(
\overset{2^{s}}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot 2^{s} + \tau)}
\Big\}
}
\Big)
}
\ \cup \
\Big(
\overset{\gamma - \boxed{ \lfloor \frac{\gamma}{2^{s}} \rfloor } \cdot 2^{s}}{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{(\boxed{ \lfloor \frac{\gamma}{2^{s}} \rfloor } \cdot 2^{s} + \phi)}
\Big\}
}
\Big)
\iff
S_{5}
=
\emptyset
\ \cup \
\Big(
\overset{\gamma - 0 \cdot 2^{s}}{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{(0 \cdot 2^{s} + \phi)}
\Big\}
}
\Big)
\iff
S_{5}
=
\emptyset
\ \cup \
\Big(
\overset{\gamma}{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{(\phi)}
\Big\}
}
\Big)
\iff
S_{5}
=
\overset{\gamma}{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{(\phi)}
\Big\}
}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 23 :

- In this part, we show that the specific value (which we will call $\varrho$) taken by $s$ such that $q = \lfloor \frac{\gamma}{2^{s}} \rfloor = 0$ can be expressed using the $min$ function, and we examine if this specific value 
  is the maximum value that $s$ can take

- if this specific value is the maximum value that $s$ can take, then we will examine if we can extract any relation 

	- The relation extracted is $2^{(\varrho - 1)} \leq \gamma < 2^{(\varrho)}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\bigg(
\varrho
:=
min\Big(
\Big\{
s
\ \Big| \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Big\}
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
0
\leq
\gamma
<
2^{(\varrho)}
\Big)
\because
\Big(
\big(
\varrho \in \{
s
\ | \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\}
\big)
\land
\big(
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\iff
0
\leq
\gamma
<
2^{s}
\big)
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\varrho
=
min\Big(
\Big\{
s
\ \Big| \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Big\}
\Big)
\bigg)
}_{
\Big(
\ell_{1}
=
min(S)
=
inf(S)
\Big)
\text{ form}
}
\iff
\underbrace{
\bigg(
\Big(
\varrho
\in
\{
s
\ | \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\}
\Big)
\land
\Big(
\forall s \in 
\{
s
\ | \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\}, \quad
s \geq \varrho
\Big)
\bigg)
}_{
\ \because \
\Big(
\ell_{1}
=
min(S)
\Big)
\iff
\Big(
\big(
min(S)
\in S
\big)
\land
\big(
\forall x \in S, \quad
x \geq min(S)
\big)
\Big)
}
\\[1em]
\quad
\iff
\bigg(
\Big(
\varrho \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{\varrho}} \rfloor = 0
\Big)
\land
\underbrace{
\Big(
\forall s, \quad
\big(
s \in \{
s
\ | \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\}
\big)
\Rightarrow
\big(
s \geq \varrho
\big)
\Big)
}_{
\ \because \
(\forall x \in S, \quad R_{1}(x))
\iff
(\forall x, (x \in S \Rightarrow R_{1}(x)))
}
\bigg)
\iff
\bigg(
\Big(
\varrho \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{\varrho}} \rfloor = 0
\Big)
\land
\Big(
\forall s, \quad
\big(
\underbrace{
s \in \mathbb{N}
}_{A}
\ \
\land
\ \
\underbrace{
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
}_{B}
\big)
\Rightarrow
\underbrace{
\big(
s \geq \varrho
\big)
}_{C}
\Big)
\bigg)
\\[1em]
\quad
\iff
\bigg(
\Big(
\varrho \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{\varrho}} \rfloor = 0
\Big)
\land
\Big(
\forall s, \quad
\underbrace{
\big(
s \in \mathbb{N}
\Rightarrow
\big(
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Rightarrow
s \geq \varrho
\big)
\big)
}_{
\ \because \
\Big(
(A \land B)
\Rightarrow C
\Big)
\iff
\Big(
A
\Rightarrow
(B \Rightarrow C)
\Big)
}
\Big)
\bigg)
\iff
\bigg(
\Big(
\varrho \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{\varrho}} \rfloor = 0
\Big)
\land
\Big(
\forall s \in \mathbb{N}, \quad
\underbrace{
\big(
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Rightarrow
s \geq \varrho
\big)
}_{
\Big(
P \Rightarrow Q
\Big)
\text{ form}
}
\Big)
\bigg)
\\[1em]
\quad
\iff
\boxed{
\bigg(
\Big(
\varrho \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{\varrho}} \rfloor = 0
\Big)
\land
\Big(
\forall s \in \mathbb{N}, \quad
\underbrace{
\big(
s < \varrho
\Rightarrow
\lfloor \frac{\gamma}{2^{s}} \rfloor \neq 0
\big)
}_{
\ \because \
\Big(
P \Rightarrow Q
\Big)
\iff
\Big(
\neg Q \Rightarrow \neg P
\Big)
}
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\bigg(
\varrho
=
min\Big(
\Big\{
s
\ \Big| \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Big\}
\Big)
\bigg)
\iff
\bigg(
\Big(
\varrho \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{\varrho}} \rfloor = 0
\Big)
\land
\Big(
\forall s \in \mathbb{N}, \quad
\big(
s < \varrho
\Rightarrow
\lfloor \frac{\gamma}{2^{s}} \rfloor \neq 0
\big)
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\big(
s < \varrho
\Rightarrow
\lfloor \frac{\gamma}{2^{s}} \rfloor \neq 0
\big)
\Big)
\land
\Big(
\frac{\gamma}{2^{s}} > 0
\Big)
\land
\Big(
\lfloor \frac{\gamma}{2^{s}} \rfloor \in \mathbb{N}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\bigg(
\lfloor \frac{\gamma}{2^{(\varrho - 1)}} \rfloor \in \mathbb{N}_{\geq 1}
\bigg)
\iff
\bigg(
\lfloor \frac{\gamma}{2^{(\varrho - 1)}} \rfloor \geq 1
\bigg)
\iff
\bigg(
\frac{\gamma}{2^{(\varrho - 1)}} \geq \lceil 1 \rceil
\bigg)
\iff
\bigg(
\frac{\gamma}{2^{(\varrho - 1)}} \geq 1
\bigg)
\iff
\bigg(
\Big(
\gamma \geq 2^{(\varrho - 1)}
\Big)
\because
\Big(
2^{(\varrho - 1)} > 0
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\bigg(
\Big(
0 < 2^{(\varrho - 1)} \leq \gamma
\Big)
\land
\Big(
0
\leq
\gamma
<
2^{(\varrho)}
\Big)
\bigg)
\Rightarrow
\boxed{
\bigg(
2^{(\varrho - 1)}
\leq
\gamma
<
2^{(\varrho)}
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Part 24 :

- In this part, we show, from $2^{(\varrho - 1)} \leq \gamma < 2^{(\varrho)}$, that :

	- If $s = \varrho - 1$, then there is exactly $1$ block of size $2^{(\varrho - 1)}$ which is $B_{(1, \quad \varrho - 1)} = B_{(\lfloor \frac{\gamma}{2^{(\varrho - 1)}} \rfloor, \quad \varrho - 1)}$ (and there is not necessarily $R_{(\varrho - 1)}$ )
	
	- If $s = \varrho$, then there is exactly $0$ block of size $2^{(\varrho)}$ (and there is always $R_{(\varrho)}$ )

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! q \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\bigg(
q
=
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
\bigg)
\land
\bigg(
2^{(\varrho - 1)}
\leq
\gamma
<
2^{(\varrho)}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
2^{(\varrho - 1)}
\leq
\gamma
<
2^{\varrho}
\bigg)
\iff
\bigg(
\frac{2^{(\varrho - 1)}}{2^{(\varrho - 1)}}
\leq
\frac{\gamma}{2^{(\varrho - 1)}}
<
\frac{2^{(\varrho)}}{2^{(\varrho - 1)}}
\bigg)
\iff
\bigg(
1
\leq
\frac{\gamma}{2^{(\varrho - 1)}}
<
2^{(\varrho - (\varrho - 1))}
\bigg)
\iff
\bigg(
1
\leq
\frac{\gamma}{2^{(\varrho - 1)}}
<
2^{(1)}
\bigg)
\iff
\bigg(
1
\leq
\frac{\gamma}{2^{(\varrho - 1)}}
<
2
\bigg)
\\[1em]
\quad
\iff
\bigg(
1
\leq
\frac{\gamma}{2^{(\varrho - 1)}}
<
1 + 1
\bigg)
\iff
\bigg(
\lfloor \frac{\gamma}{2^{(\varrho - 1)}} \rfloor
=
1
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! q \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\bigg(
s
=
\varrho - 1
\bigg)
\Rightarrow
\bigg(
q
=
\lfloor \frac{\gamma}{2^{(\varrho - 1)}} \rfloor
=
1
\bigg)
\Rightarrow
\bigg(
\text{If } s = \varrho - 1 \text{ , then there is exactly 1 block of size } 2^{(\varrho - 1)} \text{ which is } 
B_{(1, \quad \varrho - 1)} = B_{(\lfloor \frac{\gamma}{2^{(\varrho - 1)}} \rfloor, \quad \varrho - 1)}
\text{ (and there is not necessarily } R_{(\varrho - 1)} \text{ )}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
1
\leq
\frac{\gamma}{2^{(\varrho - 1)}}
<
2
\Big)
\iff
\Big(
1
\cdot
\frac{1}{2}
\leq
\frac{\gamma}{2^{(\varrho - 1)}}
\cdot
\frac{1}{2}
<
2
\cdot
\frac{1}{2}
\Big)
\iff
\Big(
\frac{1}{2}
\leq
\frac{\gamma}{2^{(\varrho)}}
<
1
\Big)
\bigg)
\Rightarrow
\bigg(
\lfloor \frac{\gamma}{2^{(\varrho)}} \rfloor
=
0
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! q \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\bigg(
s
=
\varrho
\bigg)
\Rightarrow
\bigg(
q
=
\lfloor \frac{\gamma}{2^{(\varrho)}} \rfloor
=
0
\bigg)
\Rightarrow
\bigg(
B_{s}
=
\emptyset
\bigg)
\Rightarrow
\bigg(
\text{If } s = \varrho \text{ , then there is exactly 0 block of size } 2^{(\varrho)}
\text{ (and there is always } R_{(\varrho)} \text{ )}
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 25 :

- From part 25 to 40, we show by recurrence that any concerned tuple can be expressed from the starting set $S_{5}$ and all its possible subsets. We also show that these tuples 
  follow this “subdivision process”
	
	- If $\lfloor \frac{\gamma}{2^{s}} \rfloor$ is even, then the number of blocks of size $2^{s}$ is even
	
	- If $\lfloor \frac{\gamma}{2^{s}} \rfloor$ is odd, then the number of blocks of size $2^{s}$ is odd

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\Omega_{0} := 0
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\bigg(
s = 0
\bigg)
\land
\boxed{
\bigg(
\Big(
B_{s = 0}
\neq
\emptyset
\Big)
\because
\Big(
\gamma \geq 1
\Big)
\bigg)
}
\land
\bigg(
\lfloor \frac{\gamma}{2^{0}} \rfloor
=
\underbrace{
\lfloor \gamma \rfloor
}_{\in \mathbb{N}_{\geq 1}}
=
\gamma
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
S_{5}
=
\bigg(
\overset{ \lfloor \frac{\gamma}{2^{0}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
\ \
\underbrace{
\overbrace{
\bigg(
\overset{2^{0}}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot 2^{0} + \tau)}
\Big\}
}
\bigg)
}^{
\text{Singleton } B_{(\zeta, 0)}
}
}_{
\boxed{
B_{(\zeta, 0)}
}
}
\ \
}
\bigg)
\ \cup \
\underbrace{
\bigg(
\overset{\gamma - \lfloor \frac{\gamma}{2^{0}} \rfloor \cdot 2^{0}}{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{(\lfloor \frac{\gamma}{2^{0}} \rfloor \cdot 2^{0} + \phi)}
\Big\}
}
\bigg)
}_{R_{0}}
=
\bigg(
\bigg(
\overset{ \gamma }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, 0)}
}
\bigg)
\ \cup \
\underbrace{
\emptyset
}_{R_{0}}
\bigg)
=
B_{(1, 0)}
\ \cup \
B_{(2, 0)}
\ \cup \
\dots
\ \cup \
B_{(\gamma, 0)}
\ \cup \
\emptyset
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
B_{(1, 0)}
=
\{d_{(1)}\}
\bigg)
\land
\bigg(
B_{(2, 0)}
=
\{d_{(2)}\}
\bigg)
\land
\dots
\land
\bigg(
B_{(\gamma, 0)}
=
\{d_{(\gamma)}\}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\forall \mu \in \{1, \dots, \underbrace{\lfloor \frac{\gamma}{2^{0}} \rfloor}_{\boxed{\gamma}} \}, \quad
\exists d_{(\mu)} \in \mathbb{R}, \quad
\exists! \lambda_{(\mu, 0)} \in \mathbb{R}^{1}, \quad
\exists! \Lambda_{0} \in \mathbb{R}^{0}, \quad
\bigg(
\lambda_{(\mu, 0)}
:=
(d_{(\mu)})
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{0}
:=
()
\bigg)
}_{
\substack{
{
\text{Trivially sorted } 0 \text{-tuple}
}
\\
{
\text{associated to } R_{0}
}
}
}
\Bigg)
}
\\[1em]
\Rightarrow
\boxed{
\left(
E_{0}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad 0)}
, 
\lambda_{(2, \quad 0)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{0}} \rfloor}, \quad 0)}
}
}_{
\text{Sorted } (2^{0}) \text{-tuples}
}
,
\underbrace{
\Lambda_{0}
}_{
\text{Trivially sorted}
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\end{cases}
\end{array}
$$

Diagram 1 of part 25 :

- We have $\boxed{0 \leq Card(R_{0}) < 2^{0}}$ 

- The diagram illustrate the "subdivision process" for the blocks at iteration $s = 0$ 

- In this diagram, whether $\gamma$ is even or odd, the result (at $s = 0$ ) is the same. So there is a unique case for $s = 0$ 

- Case with $Card(R_{0}) = 0$ :
	
$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\gamma
\\[1em]
\hline
\begin{array}{l}
S_{5} \quad \quad
\quad \quad \quad
d_{(1)}
\quad
d_{(2)}
\quad
\dots
\quad
d_{(\gamma)}
\\[1em]
\hline
s = 0
\quad \quad \quad
\overbrace{
\{d_{(1)}\}
}^{
\boxed{
B_{(1, \quad 0)}
}
}
\quad
\quad
\dots
\quad
\overbrace{
\{d_{(\gamma)}\}
}^{
\boxed{
B_{(\gamma, \quad 0)}
}
}
\quad
\overbrace{
\emptyset
}^{
\boxed{
R_{0}
}
}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Part 26 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\boxed{
s = 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 1}
=
\emptyset
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
E_{1}
:=
E_{0}
\Bigg)
}
\end{cases}
\end{array}
$$

Part 27 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\boxed{
s = 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 1}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{1 - 1}} \rfloor
=
\lfloor \frac{\gamma}{2^{0}} \rfloor
=
\underbrace{
\lfloor \gamma \rfloor
}_{\in \mathbb{N}_{\geq 1}}
=
\gamma
=
\boxed{
2 \xi
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \varphi \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{1}} \rfloor} \}, \quad
\exists! \zeta \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{1}} \rfloor} \}, \quad
\boxed{\exists! \lambda_{(\zeta, 1)} \in \mathbb{R}^{\boxed{2^{1}}}}, \quad
\boxed{\exists! \Lambda_{1} \in \mathbb{R}^{0}}, \quad
\bigg(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 0)}, \lambda_{(2 \varphi, \quad 0)})
\Big)
=
B_{(\zeta, 1)}
\bigg)
\land
\underbrace{
\bigg(
\lambda_{(\zeta, 1)}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 0)}, \lambda_{(2 \varphi, \quad 0)})
\Big)
\bigg)
}_{
\text{Sorted } (2^{1}) \text{-tuple}
}
\\[1em]
\quad
\land
\bigg(
R_{1}
=
R_{0}
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{1}
:=
\Lambda_{0}
\bigg)
}_{
\text{Trivially sorted } 0 \text{-tuple}
}
\Bigg)
\\[1em]
\Rightarrow
\left(
S_{5}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{1}} \rfloor }{\underset{\varphi = 1}{\bigcup}}{
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 0)}, \lambda_{(2 \varphi, \quad 0)})
\Big)
}
\right)
}
\ \cup \
R_{0}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{1}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, 1)}
}
\right)
}
\ \cup \
R_{1}
=
B_{(1, 1)}
\ \cup \
B_{(2, 1)}
\ \cup \
\dots
\ \cup \
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, 1)}}
}
\ \cup \
R_{1}
\right)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{1}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad 1)}
, 
\lambda_{(2, \quad 1)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{1}} \rfloor}, \quad 1)}
}
}_{
\text{Sorted } (2^{1}) \text{-tuples}
}
,
\underbrace{
\Lambda_{1}
}_{
\text{Sorted } 0 \text{-tuple}
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\end{cases}
\end{array}
$$

Part 28 :

- More generally, if $\lfloor \frac{\gamma}{2^{s - 1}} \rfloor = 2 \xi + 1$ (= if the number of blocks of size $2^{s - 1}$ is odd), then :
	
	- $\lfloor \frac{\gamma}{2^{s - 1}} \rfloor$ denotes the index of the last block of size $2^{s-1}$ that has not been paired with the penultimate block of size $2^{s-1}$ (since all other blocks of size $2^{s-1}$ 
	  (with the exception of the last block of size $2^{s-1}$) have already been paired between themselves two by two)
	
	- $\lfloor \frac{\gamma}{2^{s}} \rfloor$ denotes the index of the last block of size $2^{s}$ that has been paired with the penultimate block of size $2^{s}$ (meaning that all other blocks of size $2^{s}$ 
	  are paired between themselves two by two)

    (See "Diagram 1 of part 26 to 28" and "Diagram 1 of part 29 and 31")

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\boxed{
s = 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 1}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{1 - 1}} \rfloor
=
\lfloor \frac{\gamma}{2^{0}} \rfloor
=
\underbrace{
\lfloor \gamma \rfloor
}_{\in \mathbb{N}_{\geq 1}}
=
\gamma
=
\boxed{
2 \xi + 1
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \varphi \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{1}} \rfloor} \}, \quad
\exists! \zeta \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{1}} \rfloor} \}, \quad
\boxed{\exists! \lambda_{(\zeta, 1)} \in \mathbb{R}^{\boxed{2^{1}}}}, \quad
\boxed{\exists! \Lambda_{1} \in \mathbb{R}^{1}}, \quad
\bigg(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 0)}, \lambda_{(2 \varphi, \quad 0)})
\Big)
=
\lambda_{(\zeta, 1)}
\bigg)
\land
\underbrace{
\bigg(
\lambda_{(\zeta, 1)}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 0)}, \lambda_{(2 \varphi, \quad 0)})
\Big)
\bigg)
}_{
\text{Sorted } (2^{1}) \text{-tuple}
}
\\[1em]
\quad
\land
\bigg(
R_{1}
=
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{9}} \rfloor, \quad 0)}}}, \Lambda_{0})
\Big)
=
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(\gamma, \quad 0)}, \Lambda_{0})
\Big)
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{1}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{9}} \rfloor, \quad 0)}}}, \Lambda_{0})
\Big)
=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(\gamma, \quad 0)}, \Lambda_{0})
\Big)
\bigg)
}_{
\text{Sorted } 1 \text{-tuple}
}
\Bigg)
\\[1em]
\Rightarrow
\left(
S_{5}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{1}} \rfloor }{\underset{\varphi = 1}{\bigcup}}{
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 0)}, \lambda_{(2 \varphi, \quad 0)})
\Big)
}
\right)
}
\ \cup \
\left(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge( \ \boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{0}} \rfloor, \quad 0)}}}, \Lambda_{0} \ )
\Big)
\right)
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{1}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, 1)}
}
\right)
}
\ \cup \
R_{1}
=
B_{(1, 1)}
\ \cup \
B_{(2, 1)}
\ \cup \
\dots
\ \cup \
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, 1)}}
}
\ \cup \
R_{1}
\right)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{1}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad 1)}
, 
\lambda_{(2, \quad 1)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{1}} \rfloor}, \quad 1)}
}
}_{
\text{Sorted } (2^{1}) \text{-tuples}
}
,
\underbrace{
\Lambda_{1}
}_{
\text{Sorted } 1 \text{-tuple}
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\end{cases}
\end{array}
$$

Diagram 1 of part 26 to 28 :

- We have $\boxed{0 \leq Card(R_{1}) < 2^{1}}$ 

- The diagram illustrate the "subdivision process" for the blocks at iteration $s = 0$ and $s = 1$  

- Cases with $Card(R_{1}) = 0$ and $Card(R_{1}) = 2$ :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\lfloor \frac{\gamma}{2^{1 - 1}} \rfloor
=
\lfloor \frac{\gamma}{2^{0}} \rfloor
=
\overbrace{
\lfloor \gamma \rfloor
}^{\in \mathbb{N}_{\geq 1}}
=
\gamma
=
2 \xi
\\[1em]
\hline
\begin{array}{l}
S_{5} \quad \quad
\quad \quad \quad
d_{(1)}
\quad
d_{(2)}
\quad
\dots
\quad
d_{(\gamma)}
\\[1em]
\hline
s = 0
\quad \quad \quad
\underbrace{
\overbrace{
\{d_{(1)}\}
}^{\boxed{B_{(1, \quad 0)}}}
\quad
\overbrace{
\{d_{(2)}\}
}^{B_{(2, \quad 0)}}
}_{
\boxed{
B_{(1, \quad 1)}
}
}
\quad
\dots
\quad
\underbrace{
\overbrace{
\{d_{(\gamma - 1)}\}
}^{B_{(2 \cdot \lfloor \frac{\gamma}{2^{1}} \rfloor - 1, \quad 0)}}
\quad
\overbrace{
\{d_{(\gamma)}\}
}^{\boxed{B_{\boxed{(2 \cdot \lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 0)}}}}
}_{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}
}
}
\quad
\underbrace{
\overbrace{
\emptyset
}^{\boxed{R_{0}}}
}_{
\boxed{
R_{1}
}
}
\\[1em]
\hline
s = 1
\quad \quad \quad
\overbrace{
\{d_{(1)}, d_{(2)}\}
}^{
\boxed{
B_{(1, \quad 1)}
}
}
\quad
\dots
\quad
\overbrace{
\{d_{(\gamma - 1)}, d_{(\gamma)}\}
}^{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}
}
}
\quad
\overbrace{
\emptyset
}^{
\boxed{R_{1}}
}
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\quad
\begin{array}{|c|}
\hline
\lfloor \frac{\gamma}{2^{1 - 1}} \rfloor
=
\lfloor \frac{\gamma}{2^{0}} \rfloor
=
\overbrace{
\lfloor \gamma \rfloor
}^{\in \mathbb{N}_{\geq 1}}
=
\gamma
=
2 \xi + 1
\\[1em]
\hline
\begin{array}{l}
S_{5} \quad \quad
\quad \quad \quad
d_{(1)}
\quad
d_{(2)}
\quad
\dots
\quad
d_{(\gamma)}
\\[1em]
\hline
s = 0
\quad \quad \quad
\underbrace{
\overbrace{
\{d_{(1)}\}
}^{\boxed{B_{(1, \quad 0)}}}
\quad
\overbrace{
\{d_{(2)}\}
}^{B_{(2, \quad 0)}}
}_{
\boxed{
B_{(1, \quad 1)}
}
}
\quad
\dots
\quad
\underbrace{
\overbrace{
\{d_{(\gamma - 2)}\}
}^{B_{(2 \cdot \lfloor \frac{\gamma}{2^{0}} \rfloor - 1, \quad 0)}}
\quad
\overbrace{
\{d_{(\gamma - 1)}\}
}^{\boxed{B_{\boxed{(2 \cdot \lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 0)}}}}
}_{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}
}
}
\quad
\underbrace{
\overbrace{
\{d_{(\gamma)}\}
}^{\boxed{B_{\boxed{(\lfloor \frac{\gamma}{2^{0}} \rfloor, \quad 0)}}}}
\quad
\overbrace{
\emptyset
}^{\boxed{R_{0}}}
}_{
\boxed{
R_{1}
}
}
\\[1em]
\hline
s = 1
\quad \quad \quad
\overbrace{
\{d_{(1)}, d_{(2)}\}
}^{
\boxed{
B_{(1, \quad 1)}
}
}
\quad
\dots
\quad
\overbrace{
\{d_{(\gamma - 2)}, d_{(\gamma - 1)}\}
}^{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}
}
}
\quad
\overbrace{
\{d_{(\gamma)}\}
}^{
\boxed{R_{1}}
}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Part 29 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\boxed{
s = 2
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 2}
=
\emptyset
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
E_{2}
:=
E_{1}
\Bigg)
}
\end{cases}
\end{array}
$$

Part 30 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\boxed{
s = 2
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 2}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{2 - 1}} \rfloor
=
\boxed{
2 \xi
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \varphi \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{2}} \rfloor} \}, \quad
\exists! \zeta \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{2}} \rfloor} \}, \quad
\boxed{\exists! \lambda_{(\zeta, 2)} \in \mathbb{R}^{\boxed{2^{2}}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{2} - 1\}, \quad
\boxed{\exists! \Lambda_{2} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{2}) < 2^{2}
}
, \quad
\bigg(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 1)}, \lambda_{(2 \varphi, \quad 1)})
\Big)
=
B_{(\zeta, 2)}
\bigg)
\land
\underbrace{
\bigg(
\lambda_{(\zeta, 2)}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 1)}, \lambda_{(2 \varphi, \quad 1)})
\Big)
\bigg)
}_{
\text{Sorted } (2^{2}) \text{-tuple}
}
\\[1em]
\quad
\land
\bigg(
R_{2}
=
R_{1}
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{2}
:=
\Lambda_{1}
\bigg)
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{2}-1
}
\Bigg)
\\[1em]
\Rightarrow
\left(
S_{5}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{2}} \rfloor }{\underset{\varphi = 1}{\bigcup}}{
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 1)}, \lambda_{(2 \varphi, \quad 1)})
\Big)
}
\right)
}
\ \cup \
R_{1}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{2}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, 2)}
}
\right)
}
\ \cup \
R_{2}
=
B_{(1, 2)}
\ \cup \
B_{(2, 2)}
\ \cup \
\dots
\ \cup \
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, 2)}}
}
\ \cup \
R_{2}
\right)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{2}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad 2)}
, 
\lambda_{(2, \quad 2)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{2}} \rfloor}, \quad 2)}
}
}_{
\text{Sorted } (2^{2}) \text{-tuples}
}
,
\underbrace{
\Lambda_{2}
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{2}-1
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\end{cases}
\end{array}
$$

Part 31 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Rightarrow
\Bigg(
\bigg(
\boxed{
s = 2
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 2}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{2 - 1}} \rfloor
=
\boxed{
2 \xi + 1
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \varphi \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{2}} \rfloor} \}, \quad
\exists! \zeta \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{2}} \rfloor} \}, \quad
\boxed{\exists! \lambda_{(\zeta, 2)} \in \mathbb{R}^{\boxed{2^{2}}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{2} - 1\}, \quad
\boxed{\exists! \Lambda_{2} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{2}) < 2^{2}
}
, \quad
\bigg(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 1)}, \lambda_{(2 \varphi, \quad 1)})
\Big)
=
\lambda_{(\zeta, 2)}
\bigg)
\land
\underbrace{
\bigg(
\lambda_{(\zeta, 2)}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 1)}, \lambda_{(2 \varphi, \quad 1)})
\Big)
\bigg)
}_{
\text{Sorted } (2^{2}) \text{-tuple}
}
\\[1em]
\quad
\land
\bigg(
R_{2}
=
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}}, \Lambda_{1})
\Big)
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{2}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}}, \Lambda_{1})
\Big)
\bigg)
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{2}-1
}
\Bigg)
\\[1em]
\Rightarrow
\left(
S_{5}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{2}} \rfloor }{\underset{\varphi = 1}{\bigcup}}{
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad 1)}, \lambda_{(2 \varphi, \quad 1)})
\Big)
}
\right)
}
\ \cup \
\left(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge( \ \boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}}, \Lambda_{1} \ )
\Big)
\right)
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{2}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, 2)}
}
\right)
}
\ \cup \
R_{2}
=
B_{(1, 2)}
\ \cup \
B_{(2, 2)}
\ \cup \
\dots
\ \cup \
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, 2)}}
}
\ \cup \
R_{2}
\right)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{2}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad 2)}
, 
\lambda_{(2, \quad 2)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{2}} \rfloor}, \quad 2)}
}
}_{
\text{Sorted } (2^{2}) \text{-tuples}
}
,
\underbrace{
\Lambda_{2}
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{2}-1
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\end{cases}
\end{array}
$$

Diagram 1 of part 29 and 31 :

- We have $\boxed{0 \leq Card(R_{2}) < 2^{2}}$ 

- The diagram illustrate the "subdivision process" for the blocks at iteration $s = 1$ and $s = 2$ 

- Cases with $Card(R_{2}) = 0$ and $Card(R_{2}) = 1$ :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\lfloor \frac{\gamma}{2^{2 - 1}} \rfloor
=
2 \xi
\\[1em]
\hline
\begin{array}{l}
S_{5} \quad \quad
\quad \quad \quad
d_{(1)}
\quad
d_{(2)}
\quad
\dots
\quad
d_{(\gamma)}
\\[1em]
\hline
s = 1
\quad \quad \quad
\underbrace{
\overbrace{
\{d_{(1)}, d_{(2)}\}
}^{
\boxed{
B_{(1, \quad 1)}
}
}
\quad
\overbrace{
\{d_{(2)}, d_{(3)}\}
}^{
B_{(2, \quad 1)}
}
}_{
\boxed{
B_{(1, \quad 2)}
}
}
\quad
\dots
\quad
\underbrace{
\overbrace{
\{d_{(\gamma - 3)}, d_{(\gamma - 2)}\}
}^{
B_{(2 \cdot \lfloor \frac{\gamma}{2^{2}} \rfloor - 1, \quad 1)}
}
\quad
\overbrace{
\{d_{(\gamma - 1)}, d_{(\gamma)}\}
}^{
\boxed{
B_{\boxed{(2 \cdot \lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 1)}}
}
}
}_{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 2)}}
}
}
\quad
\underbrace{
\overbrace{
\emptyset
}^{
\boxed{R_{1}}
}
}_{
\boxed{R_{2}}
}
\\[1em]
\hline
s = 2
\quad \quad \quad
\overbrace{
\{d_{(1)}, d_{(2)}, d_{(3)}, d_{(4)}\}
}^{
\boxed{
B_{(1, \quad 2)}
}
}
\quad
\dots
\quad
\overbrace{
\{d_{(\gamma - 3)}, d_{(\gamma - 2)}, d_{(\gamma - 1)}, d_{(\gamma)}\}
}^{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 2)}}
}
}
\quad
\overbrace{
\emptyset
}^{
\boxed{R_{2}}
}
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\quad
\begin{array}{|c|}
\hline
\lfloor \frac{\gamma}{2^{2 - 1}} \rfloor
=
2 \xi
\\[1em]
\hline
\begin{array}{l}
S_{5} \quad \quad
\quad \quad \quad
d_{(1)}
\quad
d_{(2)}
\quad
\dots
\quad
d_{(\gamma)}
\\[1em]
\hline
s = 1
\quad \quad \quad
\underbrace{
\overbrace{
\{d_{(1)}, d_{(2)}\}
}^{
\boxed{
B_{(1, \quad 1)}
}
}
\quad
\overbrace{
\{d_{(2)}, d_{(3)}\}
}^{
B_{(2, \quad 1)}
}
}_{
\boxed{
B_{(1, \quad 2)}
}
}
\quad
\dots
\quad
\underbrace{
\overbrace{
\{d_{(\gamma - 4)}, d_{(\gamma - 3)}\}
}^{
B_{(2 \cdot \lfloor \frac{\gamma}{2^{2}} \rfloor - 1, \quad 1)}
}
\quad
\overbrace{
\{d_{(\gamma - 2)}, d_{(\gamma - 1)}\}
}^{
\boxed{
B_{\boxed{(2 \cdot \lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 1)}}
}
}
}_{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 2)}}
}
}
\quad
\underbrace{
\overbrace{
\{d_{(\gamma)}\}
}^{
\boxed{R_{1}}
}
}_{
\boxed{R_{2}}
}
\\[1em]
\hline
s = 2
\quad \quad \quad
\overbrace{
\{d_{(1)}, d_{(2)}, d_{(3)}, d_{(4)}\}
}^{
\boxed{
B_{(1, \quad 2)}
}
}
\quad
\dots
\quad
\overbrace{
\{d_{(\gamma - 4)}, d_{(\gamma - 3)}, d_{(\gamma - 2)}, d_{(\gamma - 1)}\}
}^{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 2)}}
}
}
\quad
\overbrace{
\{d_{(\gamma)}\}
}^{
\boxed{R_{2}}
}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

- Cases with $Card(R_{2}) = 2$ and $Card(R_{2}) = 3$ :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\lfloor \frac{\gamma}{2^{2 - 1}} \rfloor
=
2 \xi + 1
\\[1em]
\hline
\begin{array}{l}
S_{5} \quad \quad
\quad \quad \quad
d_{(1)}
\quad
d_{(2)}
\quad
\dots
\quad
d_{(\gamma)}
\\[1em]
\hline
s = 1
\quad \quad \quad
\underbrace{
\overbrace{
\{d_{(1)}, d_{(2)}\}
}^{
\boxed{
B_{(1, \quad 1)}
}
}
\quad
\overbrace{
\{d_{(2)}, d_{(3)}\}
}^{
B_{(2, \quad 1)}
}
}_{
\boxed{
B_{(1, \quad 2)}
}
}
\quad
\dots
\quad
\underbrace{
\overbrace{
\{d_{(\gamma - 5)}, d_{(\gamma - 4)}\}
}^{
B_{(2 \cdot \lfloor \frac{\gamma}{2^{2}} \rfloor - 1, \quad 1)}
}
\quad
\overbrace{
\{d_{(\gamma - 3)}, d_{(\gamma - 2)}\}
}^{
\boxed{
B_{\boxed{(2 \cdot \lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 1)}}
}
}
}_{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 2)}}
}
}
\quad
\underbrace{
\overbrace{
\{d_{(\gamma - 1)}, d_{(\gamma)}\}
}^{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}
}
}
\quad
\overbrace{
\emptyset
}^{
\boxed{R_{1}}
}
}_{
\boxed{R_{2}}
}
\\[1em]
\hline
s = 2
\quad \quad \quad
\overbrace{
\{d_{(1)}, d_{(2)}, d_{(3)}, d_{(4)}\}
}^{
\boxed{
B_{(1, \quad 2)}
}
}
\quad
\dots
\quad
\overbrace{
\{d_{(\gamma - 5)}, d_{(\gamma - 4)}, d_{(\gamma - 3)}, d_{(\gamma - 2)}\}
}^{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 2)}}
}
}
\quad
\overbrace{
\{d_{(\gamma - 1)}, d_{(\gamma)}\}
}^{
\boxed{R_{2}}
}
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\quad
\begin{array}{|c|}
\hline
\lfloor \frac{\gamma}{2^{2 - 1}} \rfloor
=
2 \xi + 1
\\[1em]
\hline
\begin{array}{l}
S_{5} \quad \quad
\quad \quad \quad
d_{(1)}
\quad
d_{(2)}
\quad
\dots
\quad
d_{(\gamma)}
\\[1em]
\hline
s = 1
\quad \quad \quad
\underbrace{
\overbrace{
\{d_{(1)}, d_{(2)}\}
}^{
\boxed{
B_{(1, \quad 1)}
}
}
\quad
\overbrace{
\{d_{(2)}, d_{(3)}\}
}^{
B_{(2, \quad 1)}
}
}_{
\boxed{
B_{(1, \quad 2)}
}
}
\quad
\dots
\quad
\underbrace{
\overbrace{
\{d_{(\gamma - 6)}, d_{(\gamma - 5)}\}
}^{
B_{(2 \cdot \lfloor \frac{\gamma}{2^{2}} \rfloor - 1, \quad 1)}
}
\quad
\overbrace{
\{d_{(\gamma - 4)}, d_{(\gamma - 3)}\}
}^{
\boxed{
B_{\boxed{(2 \cdot \lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 1)}}
}
}
}_{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 2)}}
}
}
\quad
\underbrace{
\overbrace{
\{d_{(\gamma - 2)}, d_{(\gamma - 1)}\}
}^{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{1}} \rfloor, \quad 1)}}
}
}
\quad
\overbrace{
\{d_{(\gamma)}\}
}^{
\boxed{R_{1}}
}
}_{
\boxed{R_{2}}
}
\\[1em]
\hline
s = 2
\quad \quad \quad
\overbrace{
\{d_{(1)}, d_{(2)}, d_{(3)}, d_{(4)}\}
}^{
\boxed{
B_{(1, \quad 2)}
}
}
\quad
\dots
\quad
\overbrace{
\{d_{(\gamma - 6)}, d_{(\gamma - 5)}, d_{(\gamma - 4)}, d_{(\gamma - 3)}\}
}^{
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{2}} \rfloor, \quad 2)}}
}
}
\quad
\overbrace{
\{d_{(\gamma - 2)}, d_{(\gamma - 1)}, d_{(\gamma)}\}
}^{
\boxed{R_{2}}
}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Part 32 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\mathcal{P}(\Omega) :
\Bigg(
\bigg(
\Big(
\underline{0 \leq \Omega \leq \varrho}
\Big)
\Rightarrow
\Big(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega)}
, 
\lambda_{(2, \quad \Omega)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega}} \rfloor}, \quad \Omega)}
}
,
\Lambda_{\Omega}
\Big\}
\quad
\text{ contains sorted tuples}
\Big)
\bigg)
\Bigg)
\Bigg)
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\Omega' = 0
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(\Omega_{0}) :
\Bigg(
\bigg(
\Big(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega_{0})}
, 
\lambda_{(2, \quad \Omega_{0})}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega_{0}}} \rfloor}, \quad \Omega_{0})}
}
,
\Lambda_{\Omega_{0}}
\Big\}
\quad
\text{ contains sorted tuples}
\Big)
\bigg)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\bigg(
s = 0
\bigg)
\land
\boxed{
\bigg(
\Big(
B_{s = 0}
\neq
\emptyset
\Big)
\because
\Big(
\gamma \geq 1
\Big)
\bigg)
}
\land
\bigg(
\lfloor \frac{\gamma}{2^{0}} \rfloor
=
\underbrace{
\lfloor \gamma \rfloor
}_{\in \mathbb{N}_{\geq 1}}
=
\gamma
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{0}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad 0)}
, 
\lambda_{(2, \quad 0)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{0}} \rfloor}, \quad 0)}
}
}_{
\text{Sorted } (2^{0}) \text{-tuples}
}
,
\underbrace{
\Lambda_{0}
}_{
\text{Trivially sorted}
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(\Omega_{0})
\Bigg)
}
\end{cases}
\end{array}
$$

Part 33 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\Omega' = 1
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(\Omega' = 1) :
\Bigg(
\bigg(
\Big(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega')}
, 
\lambda_{(2, \quad \Omega')}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega'}} \rfloor}, \quad \Omega')}
}
,
\Lambda_{\Omega'}
\Big\}
\quad
\text{ contains sorted tuples}
\Big)
\bigg)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
s = 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 1}
=
\emptyset
\bigg)
}
\Rightarrow
\boxed{
\bigg(
E_{1}
:=
E_{0}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\Bigg(
\bigg(
\boxed{
s = 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 1}
\neq
\emptyset
\bigg)
}
\land
\boxed{
\bigg(
B_{s = 1}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{1 - 1}} \rfloor
=
\lfloor \frac{\gamma}{2^{0}} \rfloor
=
\underbrace{
\lfloor \gamma \rfloor
}_{\in \mathbb{N}_{\geq 1}}
=
\gamma
=
\boxed{
2 \xi
}
\bigg)
\Bigg)
\oplus
\Bigg(
\bigg(
\boxed{
s = 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 1}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{1 - 1}} \rfloor
=
\lfloor \frac{\gamma}{2^{0}} \rfloor
=
\underbrace{
\lfloor \gamma \rfloor
}_{\in \mathbb{N}_{\geq 1}}
=
\gamma
=
\boxed{
2 \xi + 1
}
\bigg)
\Bigg)
\ \
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{1}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad 1)}
, 
\lambda_{(2, \quad 1)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{1}} \rfloor}, \quad 1)}
}
}_{
\text{Sorted } (2^{1}) \text{-tuples}
}
,
\underbrace{
\Lambda_{1}
}_{
\text{Sorted } 0 \text{-tuple}
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(\Omega' = 1)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 34 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\Omega' = 2
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(\Omega' = 2) :
\Bigg(
\bigg(
\Big(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega')}
, 
\lambda_{(2, \quad \Omega')}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega'}} \rfloor}, \quad \Omega')}
}
,
\Lambda_{\Omega'}
\Big\}
\quad
\text{ contains sorted tuples}
\Big)
\bigg)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
s = 2
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 2}
=
\emptyset
\bigg)
}
\Rightarrow
\boxed{
\bigg(
E_{2}
:=
E_{1}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\Bigg(
\bigg(
\boxed{
s = 2
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 2}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{2 - 1}} \rfloor
=
\boxed{
2 \xi
}
\bigg)
\Bigg)
\oplus
\Bigg(
\bigg(
\boxed{
s = 2
}
\bigg)
\land
\boxed{
\bigg(
B_{s = 2}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{2 - 1}} \rfloor
=
\boxed{
2 \xi + 1
}
\bigg)
\Bigg)
\ \
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{2}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad 2)}
, 
\lambda_{(2, \quad 2)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{2}} \rfloor}, \quad 2)}
}
}_{
\text{Sorted } (2^{2}) \text{-tuples}
}
,
\underbrace{
\Lambda_{2}
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{2}-1
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(\Omega' = 2)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 35 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\Omega' \curvearrowright \Omega' + 1
\Bigg)
\\[1em]
\Rightarrow
\begin{cases}
\mathcal{P}(\Omega') :
\Bigg(
\bigg(
\Big(
\underline{0 \leq \Omega' \leq \varrho}
\Big)
\Rightarrow
\Big(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega')}
, 
\lambda_{(2, \quad \Omega')}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega'}} \rfloor}, \quad \Omega')}
}
,
\Lambda_{\Omega'}
\Big\}
\quad
\text{ contains sorted tuples}
\Big)
\bigg)
\Bigg)
\\[1em]
\mathcal{H}(\Omega') :
\Bigg(
\forall \Omega' \in \{0, \dots, \varrho\}, \quad
\Bigg(
\Omega' \geq \Omega_{0}
\land
\mathcal{P}(\Omega')
\Bigg)
\Rightarrow
\Bigg(
\mathcal{P}(\Omega' + 1) :
\Bigg(
\bigg(
\Big(
\underline{0 \leq \Omega' + 1 \leq \varrho}
\Big)
\Rightarrow
\Big(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega' + 1)}
, 
\lambda_{(2, \quad \Omega' + 1)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega' + 1}} \rfloor}, \quad \Omega' + 1)}
}
,
\Lambda_{\Omega' + 1}
\Big\}
\quad
\text{ contains sorted tuples}
\Big)
\bigg)
\Bigg)
\Bigg)
\end{cases}
\end{cases}
\end{array}
$$

Part 36 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\boxed{
s = \Omega' + 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = \Omega' + 1}
=
\emptyset
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
E_{\Omega' + 1}
:=
E_{\Omega'}
\Bigg)
}
\end{cases}
\end{array}
$$

Part 37 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\boxed{
s = \Omega' + 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = \Omega' + 1}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{(\Omega' + 1) - 1}} \rfloor
=
\boxed{
2 \xi
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \varphi \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor} \}, \quad
\exists! \zeta \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor} \}, \quad
\boxed{\exists! \lambda_{(\zeta, \quad \Omega' + 1)} \in \mathbb{R}^{\boxed{2^{(\Omega' + 1)}}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{(\Omega' + 1)} - 1\}, \quad
\boxed{\exists! \Lambda_{(\Omega' + 1)} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{(\Omega' + 1)}) < 2^{(\Omega' + 1)}
}
, \quad
\bigg(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega')}, \lambda_{(2 \varphi, \quad \Omega')})
\Big)
=
B_{(\zeta, \quad \Omega' + 1)}
\bigg)
\land
\underbrace{
\bigg(
\lambda_{(\zeta, \quad \Omega' + 1)}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega')}, \lambda_{(2 \varphi, \quad \Omega')})
\Big)
\bigg)
}_{
\text{Sorted } (2^{(\Omega' + 1)}) \text{-tuple}
}
\\[1em]
\quad
\land
\bigg(
R_{(\Omega' + 1)}
=
R_{(\Omega')}
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{(\Omega' + 1)}
:=
\Lambda_{(\Omega')}
\bigg)
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{(\Omega' + 1)} - 1
}
\Bigg)
\\[1em]
\Rightarrow
\left(
S_{5}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor }{\underset{\varphi = 1}{\bigcup}}{
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega')}, \lambda_{(2 \varphi, \quad \Omega')})
\Big)
}
\right)
}
\ \cup \
R_{(\Omega')}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, \quad \Omega' + 1)}
}
\right)
}
\ \cup \
R_{(\Omega' + 1)}
=
B_{(1, \quad \Omega' + 1)}
\ \cup \
B_{(2, \quad \Omega' + 1)}
\ \cup \
\dots
\ \cup \
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor, \quad \Omega' + 1)}}
}
\ \cup \
R_{(\Omega' + 1)}
\right)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{(\Omega' + 1)}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad \Omega' + 1)}
, 
\lambda_{(2, \quad \Omega' + 1)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor}, \quad \Omega' + 1)}
}
}_{
\text{Sorted } (2^{(\Omega' + 1)}) \text{-tuples}
}
,
\underbrace{
\Lambda_{(\Omega' + 1)}
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{(\Omega' + 1)} - 1
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\end{cases}
\end{array}
$$

Part 38 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Rightarrow
\Bigg(
\bigg(
\boxed{
s = \Omega' + 1
}
\bigg)
\land
\boxed{
\bigg(
B_{s = \Omega' + 1}
\neq
\emptyset
\bigg)
}
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{(\Omega' + 1) - 1}} \rfloor
=
\boxed{
2 \xi + 1
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \varphi \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor} \}, \quad
\exists! \zeta \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor} \}, \quad
\boxed{\exists! \lambda_{(\zeta, \quad \Omega' + 1)} \in \mathbb{R}^{\boxed{2^{(\Omega' + 1)}}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{(\Omega' + 1)} - 1\}, \quad
\boxed{\exists! \Lambda_{(\Omega' + 1)} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{(\Omega' + 1)}) < 2^{(\Omega' + 1)}
}
, \quad
\bigg(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega')}, \lambda_{(2 \varphi, \quad \Omega')})
\Big)
=
B_{(\zeta, \quad \Omega' + 1)}
\bigg)
\land
\underbrace{
\bigg(
\lambda_{(\zeta, \quad \Omega' + 1)}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega')}, \lambda_{(2 \varphi, \quad \Omega')})
\Big)
\bigg)
}_{
\text{Sorted } (2^{(\Omega' + 1)}) \text{-tuple}
}
\\[1em]
\quad
\land
\bigg(
R_{(\Omega' + 1)}
=
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{(\Omega')}} \rfloor, \quad \Omega')}}}, \Lambda_{(\Omega')})
\Big)
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{(\Omega' + 1)}
:=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{(\Omega')}} \rfloor, \quad \Omega')}}}, \Lambda_{(\Omega')})
\Big)
\bigg)
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{(\Omega' + 1)} - 1
}
\Bigg)
\\[1em]
\Rightarrow
\left(
S_{5}
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor }{\underset{\varphi = 1}{\bigcup}}{
\pi^{[L]}_{1, \dots, 1}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega')}, \lambda_{(2 \varphi, \quad \Omega')})
\Big)
}
\right)
}
\ \cup \
\left(
\pi^{[L]}_{1, \dots, 1}\Big(
Merge( \ \boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{(\Omega')}} \rfloor, \quad \Omega')}}}, \Lambda_{(\Omega')} \ )
\Big)
\right)
=
\boxed{
\left(
\overset{ \lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, \quad \Omega' + 1)}
}
\right)
}
\ \cup \
R_{(\Omega' + 1)}
=
B_{(1, \quad \Omega' + 1)}
\ \cup \
B_{(2, \quad \Omega' + 1)}
\ \cup \
\dots
\ \cup \
\boxed{
B_{\boxed{(\lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor, \quad \Omega' + 1)}}
}
\ \cup \
R_{(\Omega' + 1)}
\right)
\\[1em]
\Rightarrow
\boxed{
\left(
E_{(\Omega' + 1)}
:=
\overbrace{
\Big\{
\underbrace{
\lambda_{(1, \quad \Omega' + 1)}
, 
\lambda_{(2, \quad \Omega' + 1)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{(\Omega' + 1)}} \rfloor}, \quad \Omega' + 1)}
}
}_{
\text{Sorted } (2^{(\Omega' + 1)}) \text{-tuples}
}
,
\underbrace{
\Lambda_{(\Omega' + 1)}
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{(\Omega' + 1)} - 1
}
\Big\}
}^{
\text{Set of sorted tuples}
}
\right)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(\Omega' + 1)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 39 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \Omega \in \{0, \dots, \varrho\}, \quad
\mathcal{P}(\Omega) :
\Bigg(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega)}
, 
\lambda_{(2, \quad \Omega)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega}} \rfloor}, \quad \Omega)}
}
,
\Lambda_{\Omega}
\Big\}
\quad
\text{ contains sorted tuples}
\Bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 40 :

- The objective 3 is filled, and all the objectives are filled

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\mathcal{P}(\Omega) \curvearrowright P_{i}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
B_{s}
=
\emptyset
\bigg)
\Rightarrow
\bigg(
s = \varrho
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
E_{\varrho}
=
E_{\varrho - 1}
\bigg)
\land
\boxed{
\bigg(
\Big(
E_{\varrho - 1}
=
\Big\{
\lambda_{(1, \quad \varrho - 1)}
,
\underbrace{
\Lambda_{(\varrho - 1)}
}_{
\Lambda_{(\varrho - 1)}
\text{ can potentially be a 0-tuple } ()
}
\Big\}
\Big)
\because
\Big(
\text{For the value } \varrho - 1 \text{ , there is exactly 1 block of size } 2^{(\varrho - 1)} \text{ which is } 
B_{(1, \quad \varrho - 1)} = B_{(\lfloor \frac{\gamma}{2^{(\varrho - 1)}} \rfloor, \quad \varrho - 1)}
\text{ (and thus exactly 1 tuple } \lambda_{(1, \quad \varrho - 1)} \text{ of size } 2^{(\varrho - 1)} \text{ ) }
\text{ and there is not necessarily } R_{(\varrho - 1)} \text{ (thus, there is always } \Lambda_{(\varrho - 1)} 
\text{ which is a tuple whose size is between } 0
\text{ and } 2^{(\varrho - 1)} - 1
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\exists! \Gamma \in \mathbb{R}^{Card(S_{5})}, \quad
\exists! \Gamma_{1}, \dots, \Gamma_{(\gamma)} \in S_{5}, \quad
\Bigg(
S_{5}
=
\pi^{[L]}_{1, \dots, 1}\bigg(
Merge\Big(
\lambda_{(1, \quad \varrho - 1)}, \Lambda_{(\varrho - 1)}
\Big)
\bigg)
\Bigg)
\land
\Bigg(
\Gamma
:=
\pi^{[R]}_{2, \dots, 2}\bigg(
Merge\Big(
\lambda_{(1, \quad \varrho - 1)}, \Lambda_{(\varrho - 1)}
\Big)
\bigg)
=
(
\Gamma_{1}, \dots, \Gamma_{(\gamma)}
)
\Bigg)
\ \
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Gamma_{(1)} < \dots < \Gamma_{(\gamma)}
\bigg)
\land
\bigg(
\Gamma_{(1)} \in S_{5}
\land
\dots
\land
\Gamma_{(\gamma)} \in S_{5}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\Gamma
\text{ is the tuple representing the sorted version of the set } S_{5}
\Bigg)
}
\end{cases}
\end{array}
$$

Part 41 :

- In this part, we conclude

$$
\begin{array}{l}
\boxed{
\therefore
\begin{cases}
(P1) \quad
\left(
\begin{cases}
\ \
\forall n, m \in \mathbb{N}_{\geq 1}, \quad
\exists! {\iota}_{max_{(1)}} \in \mathbb{N}, \quad
\forall {\iota}_{(1)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\alpha : \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\} \to S_{3}(n, m), \quad
{\iota}_{(1)} \mapsto \alpha({\iota}_{(1)}), \quad
{\alpha}^{-1} : S_{3}(n, m) \to \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\alpha \mapsto {\iota}_{(1)}(\alpha), \quad
\\[1em]
\quad
\exists! {\iota}_{max_{(2)}} \in \mathbb{N}, \quad
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\beta : \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\} \to S_{3}(n, m), \quad
{\iota}_{(2)} \mapsto \beta({\iota}_{(2)}), \quad
{\beta}^{-1} : S_{3}(n, m) \to \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\beta \mapsto {\iota}_{(2)}(\beta), \quad
\\[1em]
\quad
V : S_{3}(n, m) \to S_{3}(n, m), \quad
(\alpha, \beta) \mapsto V(\alpha, \beta), \quad
G : S_{3}(n, m) \to S_{3}(n, m), \quad
(\alpha, \beta) \mapsto G(\alpha, \beta), \quad
\boxed{
\Bigg(
\ \
V(\alpha, \beta)
=
max\Big(
0, 
min\Big(
\lfloor n + 1 - \alpha \rfloor, \ 
\lfloor m + 1 - \beta \rfloor
\Big)
\Big)
\ \
\Bigg)
}
\land
\Bigg(
\ \
\Bigg(
\bigg(
G(\alpha, \beta)
=
min\Big(
-\alpha, -\beta
\Big)
\bigg)
\iff
\bigg(
\Big(
G(\alpha, \beta) \leq -\alpha
\land
G(\alpha, \beta) \leq -\beta
\Big)
\land
\Big(
G(\alpha, \beta) = -\alpha
\lor
G(\alpha, \beta) = -\beta
\Big)
\bigg)
\Bigg)
\Rightarrow
\boxed{
\Bigg(
G \text{ is linear}
\Bigg)
}
\ \
\Bigg)
\land
\Bigg(
\ \
V(\alpha, \beta)
\in
\underbrace{
\Big\{
V(\alpha, \beta)
\ \Big| \
\Big(
\exists \gamma \in \mathbb{R}_{>0}, \quad
\exists \alpha_{(0)}, \beta_{(0)} \in \mathbb{N}_{>0}, \quad
\forall \alpha \geq \alpha_{(0)}, \quad
\forall \beta \geq \beta_{(0)}, \quad
|V(\alpha, \beta)|
\leq
\gamma
\times
|G(\alpha, \beta)|
\Big)
\Big\}
}_{\boxed{\mathcal{O}(|G(\alpha, \beta)|) \ = \ \mathcal{O}(|min(-\alpha, -\beta)|)}}
\bigg)
\ \
\Bigg)
\end{cases}
\right)
\end{cases}
}
\end{array}
$$

$$
\begin{array}{l}
\boxed{
\therefore
\begin{cases}
(P2) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists d_{(1)}, d_{(2)}, \dots, d_{(\gamma - 1)}, d_{(\gamma)} \in \mathbb{R}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists B_{s}, R_{s} \subseteq S_{5}, \quad
\forall \zeta \in \{1, \dots, \lfloor \frac{\gamma}{2^{s}} \rfloor\}, \quad
\exists B_{(\zeta, s)} \subset S_{5}, \quad
\bigg(
0 \leq \gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s} < 2^{s}
\bigg)
\land
\left(
S_{5}
=
\Big\{
d_{(1)}, 
\dots,  
d_{(\gamma)}
\Big\}
=
\underbrace{
\Big\{
d_{(1)}, \dots, d_{\boxed{(\lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s})}}
\Big\}
}_{\boxed{B_{s}}}
\ \cup \
\underbrace{
\Big\{
d_{\boxed{(\lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s} + 1)}}, \dots, d_{(\gamma)}
\Big\}
}_{\boxed{R_{s}}}
=
\left(
\overset{ \boxed{\lfloor \frac{\gamma}{2^{s}} \rfloor} }{\underset{\zeta = 1}{\bigcup}}{
\underbrace{
\left(
\overset{2^{s}}{\underset{\tau = 1}{\bigcup}}{
\Big\{
d_{((\zeta - 1) \cdot 2^{s} + \tau)}
\Big\}
}
\right)
}_{
\boxed{
B_{(\zeta, s)}
}
}
}
\right)
\ \cup \
\left(
\overset{ \boxed{\gamma - \lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s}} }{\underset{\phi = 1}{\bigcup}}{
\Big\{
d_{\boxed{(\lfloor \frac{\gamma}{2^{s}} \rfloor \cdot 2^{s} + \phi)}}
\Big\}
}
\right)
=
\underbrace{
\left(
\overset{ \boxed{\lfloor \frac{\gamma}{2^{s}} \rfloor} }{\underset{\zeta = 1}{\bigcup}}{
B_{(\zeta, s)}
}
\right)
}_{
\boxed{B_{s}}
}
\ \cup \
R_{s}
\right)
\right)
\end{cases}
}
\end{array}
$$

$$
\begin{array}{l}
\boxed{
\therefore
\begin{cases}
(P3) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! (q, r) \in \mathbb{N}^{2}, \quad
\bigg(
q
=
\lfloor
\frac{\gamma}{2^{s}}
\rfloor
\bigg)
\land
\bigg(
L
=
\boxed{
2^{s}
}
\bigg)
\land
\overbrace{
\bigg(
\gamma
=
\underbrace{
L + L + \dots + L
}_{q \text{ times}}
+
r
=
q \cdot L + r
\bigg)
\land
\bigg(
0 \leq r < |L|
\bigg)
}^{
\forall x \in \mathbb{Z}, \quad
\forall n \in \mathbb{Z}_{>0}, \quad
\exists! (q,r) \in \mathbb{Z}^{2}, \quad
\big(
x = q \times n + r
\big)
\land
\big(
0 \leq r < |n|
\big)
\text{ form}
}
\land
\bigg(
r
=
\gamma
-
q \cdot 2^{s}
\bigg)
\right)
\\[1em]
(P4) \quad
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists! L \in \mathbb{N}_{\geq 1}, \quad
\exists! (q, r) \in \mathbb{N}^{2}, \quad
\exists B_{s}, R_{s} \subseteq S_{5}, \quad
\forall \zeta \in \{1, \dots, q\}, \quad
\exists B_{(\zeta, s)} \subset S_{5}, \quad
\bigg(
Card(B_{s}) = q \cdot L
\bigg)
\land
\bigg(
Card(B_{(\zeta, s)}) = L
\bigg)
\land
\bigg(
0 \leq Card(R_{s}) < L
\bigg)
\land
\bigg(
Card(R_{s}) = r
\bigg)
\Bigg)
\end{cases}
}
\end{array}
$$

$$
\begin{array}{l}
\boxed{
\therefore
\begin{cases}
(P5) \quad
\Bigg(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall \mu \in \{1, \dots, \underbrace{\lfloor \frac{\gamma}{2^{0}} \rfloor}_{\boxed{\gamma}} \}, \quad
\exists d_{(\mu)} \in \mathbb{R}, \quad
\exists! \lambda_{(\mu, 0)} \in \mathbb{R}^{1}, \quad
\exists! \Lambda_{0} \in \mathbb{R}^{0}, \quad
\bigg(
\lambda_{(\mu, 0)}
=
(d_{(\mu)})
\bigg)
\land
\underbrace{
\bigg(
\Lambda_{0}
:=
()
\bigg)
}_{
\substack{
{
\text{Trivially sorted } 0 \text{-tuple}
}
\\
{
\text{associated to } R_{0}
}
}
}
\Bigg)
\\[1em]
(P6) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\forall \Omega \in \{1, \dots, \varrho\}, \quad
\forall \varphi \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{(\Omega)}} \rfloor} \}, \quad
\exists! \zeta \in \{1, \dots, \boxed{\lfloor \frac{\gamma}{2^{(\Omega)}} \rfloor} \}, \quad
\boxed{\exists! \lambda_{(\zeta, \quad \Omega)} \in \mathbb{R}^{\boxed{2^{(\Omega)}}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{(\Omega)} - 1\}, \quad
\boxed{\exists! \Lambda_{(\Omega)} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{(\Omega)}) < 2^{(\Omega)}
}
, \quad
\exists B_{\Omega} \subseteq S_{5}, \quad
\begin{cases}
\Bigg(
\bigg(
B_{\Omega}
\neq
\emptyset
\bigg)
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{(\Omega) - 1}} \rfloor
=
\boxed{
2 \xi
}
\bigg)
\Bigg)
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\lambda_{(\zeta, \quad \Omega)}
=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega - 1)}, \lambda_{(2 \varphi, \quad \Omega - 1)})
\Big)
\bigg)
}_{
\text{Sorted } (2^{(\Omega)}) \text{-tuple}
}
\land
\underbrace{
\bigg(
\Lambda_{(\Omega)}
=
\Lambda_{(\Omega - 1)}
\bigg)
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{(\Omega)} - 1
}
\Bigg)
\\[1em]
\Bigg(
\bigg(
B_{\Omega}
\neq
\emptyset
\bigg)
\land
\bigg(
\exists \xi \in \mathbb{N}, \quad
\lfloor \frac{\gamma}{2^{(\Omega) - 1}} \rfloor
=
\boxed{
2 \xi + 1
}
\bigg)
\Bigg)
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\lambda_{(\zeta, \quad \Omega)}
=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\lambda_{(2 \varphi - 1, \quad \Omega - 1)}, \lambda_{(2 \varphi, \quad \Omega - 1)})
\Big)
\bigg)
}_{
\text{Sorted } (2^{(\Omega)}) \text{-tuple}
}
\land
\underbrace{
\bigg(
\Lambda_{(\Omega)}
=
\pi^{[R]}_{2, \dots, 2}\Big(
Merge(\boxed{\lambda_{\boxed{(\lfloor \frac{\gamma}{2^{(\Omega - 1)}} \rfloor, \quad \Omega - 1)}}}, \Lambda_{(\Omega - 1)})
\Big)
\bigg)
}_{
\text{Sorted tuple whose size is between } 0 \text{ and } 2^{(\Omega)} - 1
}
\Bigg)
\end{cases}
\right)
\end{cases}
}
\end{array}
$$

$$
\begin{array}{l}
\boxed{
\therefore
\begin{cases}
(P7) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\forall s \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\forall \Omega \in \{1, \dots, \varrho\}, \quad
\exists! \lambda_{(1, \quad \Omega)}, \lambda_{(2, \quad \Omega)}, \dots, \lambda_{(\lfloor \frac{\gamma}{2^{\Omega}} \rfloor, \quad \Omega)} \in \mathbb{R}^{\boxed{2^{(\Omega)}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{(\Omega)} - 1\}, \quad
\boxed{\exists! \Lambda_{(\Omega)} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{(\Omega)}) < 2^{(\Omega)}
}
, \quad
\Bigg(
\text{The set }
\quad
\Big\{
\lambda_{(1, \quad \Omega)}
, 
\lambda_{(2, \quad \Omega)}
, 
\dots
, 
\boxed{
\lambda_{(\boxed{\lfloor \frac{\gamma}{2^{\Omega}} \rfloor}, \quad \Omega)}
}
,
\Lambda_{\Omega}
\Big\}
\quad
\text{ contains sorted tuples}
\Bigg)
\land
\Bigg(
\varrho
=
min\Big(
\Big\{
s
\ \Big| \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Big\}
\Big)
\Bigg)
\right)
\end{cases}
}
\end{array}
$$

$$
\begin{array}{l}
\boxed{
\therefore
\begin{cases}
(P8) \quad
\left(
\forall \gamma \in \mathbb{N}_{\geq 1}, \quad
\exists! S_{5} \in \mathcal{P}(\mathbb{R}) \backslash \{\emptyset\}, \quad
\forall s \in \mathbb{N}, \quad
\exists! \varrho \in \mathbb{N}, \quad
\exists! \lambda_{(\zeta, \quad \varrho - 1)} \in \mathbb{R}^{\boxed{2^{(\varrho - 1)}}}, \quad
\underbrace{
\exists \omega \in \{0, \dots, 2^{(\varrho - 1)} - 1\}, \quad
\boxed{\exists! \Lambda_{(\varrho - 1)} \in \mathbb{R}^{\omega}}
}_{
\ \because \
0 \leq Card(R_{(\varrho - 1)}) < 2^{(\varrho - 1)}
}
, \quad
\exists! \Gamma \in \mathbb{R}^{Card(S_{5})}, \quad
\exists! \Gamma_{1}, \dots, \Gamma_{(\gamma)} \in S_{5}, \quad
\boxed{
\Bigg(
\Gamma
=
\pi^{[R]}_{2, \dots, 2}\bigg(
Merge\Big(
\lambda_{(1, \quad \varrho - 1)}, \Lambda_{(\varrho - 1)}
\Big)
\bigg)
=
(
\Gamma_{1}, \dots, \Gamma_{(\gamma)}
)
\Bigg)
}
\land
\boxed{
\Bigg(
\Gamma
\text{ is the tuple representing the sorted version of the set } S_{5}
\Bigg)
}
\land
\Bigg(
\varrho
=
min\Big(
\Big\{
s
\ \Big| \
s \in \mathbb{N}
\land
\lfloor \frac{\gamma}{2^{s}} \rfloor = 0
\Big\}
\Big)
\Bigg)
\right)
\end{cases}
}
\end{array}
$$



