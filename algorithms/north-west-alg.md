
Definition of the properties of the North-West Corner Method Algorithm :

Part 1 :

- In this part, we implement the algorithm in Python

```
def northwest_corner_method(emissions, receptions):
    
    emitters = list(emissions)
    receivers = list(receptions)
    
    i = len(emitters) # emitters_number
    j = len(receivers) # receivers_number
    
    # We create the `allocating_matrix` array, initially filled with zeros
    # This is where we will record the quantities transported
    allocating_matrix = np.zeros((i, j))
    
    a = 0  # a = a' = Emitter index (row)
    b = 0  # b = b' = Receiver index (column)
    
    # We continue until we have gone through all the emitters or receivers
    while a < i and b < j :
        
        
        # We check how much we can send (the maximum amount possible)
        # This is the minimum amount between what's left in stock and what's requested
        quantity = min(emitters[a], receivers[b])
        
        # Fill in the cell in the allocating_matrix table
        allocating_matrix[a][b] = quantity
        
        # We update the inventory and demand counters
        emitters[a] -= quantity
        receivers[b] -= quantity
        
        # If the emitter is 0, move down to the next line (South)
        if emitters[a] == 0: # a = a' = Emitter index (row)
            a += 1
        # Otherwise (if the receiver is full), move to the next column (East)
        elif receivers[b] == 0: # b = b' = Receiver index (column)
            b += 1
            
            
    return allocating_matrix
```

Part 2 :

- From part 2 to part 5, we choose to compute the formula for the loop variant $V$ of the algorithm

- In this part, we build a sequence $(\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}})_{\big({\iota}\big)_{(5)} \in \{0, \dots, {\iota}_{max_{(5)}}\}}$ at rank ${\iota}_{(5)}$ by taking the formula of the global loop variant and removing $max$ and $floor$ 
  Then, from this sequence at rank ${\iota}_{(5)}$, we will express the sequence at the next rank.
  The objective is to see if the difference between the sequence at next rank and at rank ${\iota}_{(5)}$ is negative. If so, then this sequence is strictly decreasing, and this sequence corresponds 
  to the loop variant $V$ of the algorithm

	- $\boxed{{\iota}_{(5)}}$ represents the ${\iota}_{(5)}$-th time the variable $a'$ ($a' = a$ in the algorithm) and $b'$ ($b' = b$ in the algorithm) change their values from their previous values in the algorithm 
	  (similar to a recurrent sequence of order 1)

	- $a'_{{(\iota)}_{(5)}}$ is the variable $a'$ ($a' = a$ in the algorithm) at its ${\iota}_{(5)}$-th update

	- $b'_{{(\iota)}_{(5)}}$ is the variable $b'$ ($b' = b$ in the algorithm) at its ${\iota}_{(5)}$-th update

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\exists! i, j \in \mathbb{N}_{\geq 1}, \quad
\exists! {\iota}_{max_{(3)}} \in \mathbb{N}, \quad
\forall {\iota}_{(3)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(3)}, \dots, {\iota}_{max_{(3)}}\}, \quad
a' : \{0, \dots, {\iota}_{max_{(3)}}\} \to \mathbb{N}, \quad
{\iota}_{(3)} \mapsto a'({\iota}_{(3)}), \quad
(a')^{-1} : \mathbb{N} \to \{0, \dots, {\iota}_{max_{(3)}}\}, \quad
a' \mapsto {\iota}_{(3)}(a'), \quad
\\[1em]
\quad \quad
\exists! {\iota}_{max_{(4)}} \in \mathbb{N}, \quad
\forall {\iota}_{(4)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(4)}, \dots, {\iota}_{max_{(4)}}\}, \quad
b' : \{0, \dots, {\iota}_{max_{(4)}}\} \to \mathbb{N}, \quad
{\iota}_{(4)} \mapsto b'({\iota}_{(4)}), \quad
(b')^{-1} : \mathbb{N} \to \{0, \dots, {\iota}_{max_{(4)}}\}, \quad
b' \mapsto {\iota}_{(4)}(b'), \quad
\\[1em]
\quad \quad
\exists! {\iota}_{max_{(5)}} \in \mathbb{N}, \quad
\forall {\iota}_{(5)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(5)}, \dots, {\iota}_{max_{(5)}}\}, \quad
a' : \{0, \dots, {\iota}_{max_{(5)}}\} \to \mathbb{N}, \quad
{\iota}_{(5)} \mapsto {a'}_{{(\iota)}_{(5)}}, \quad
b' : \{0, \dots, {\iota}_{max_{(5)}}\} \to \mathbb{N}, \quad
{\iota}_{(5)} \mapsto {b'}_{{(\iota)}_{(5)}}, \quad
\\[1em]
\quad \quad
\mathcal{V}_{{}_{[1]}{g}} : \{0, \dots, {\iota}_{max_{(5)}}\} \to \mathbb{N}, \quad
{\iota}_{(5)} \mapsto \mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}, \quad
\boxed{
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
:=
(i + 1)
\cdot
(
j - b'_{{(\iota)}_{(5)}}
)
+
(1)
\cdot
(
i - a'_{{(\iota)}_{(5)}}
)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
=
(i + 1)
\cdot
(
j - b'_{{(\iota)}_{(5)}}
)
+
(1)
\cdot
(
i - a'_{{(\iota)}_{(5)}}
)
\bigg)
\iff
\boxed{
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
=
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}}
+
i - a'_{{(\iota)}_{(5)}}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
(i + 1)
\cdot
(
j - b'_{{(\iota + 1)}_{(5)}}
)
+
(1)
\cdot
(
i - a'_{{(\iota + 1)}_{(5)}}
)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
(i + 1)
\cdot
(
j - b'_{{(\iota + 1)}_{(5)}}
)
+
(1)
\cdot
(
i - a'_{{(\iota + 1)}_{(5)}}
)
\bigg)
\iff
\boxed{
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
i \cdot j - i \cdot b'_{{(\iota + 1)}_{(5)}} + j - b'_{{(\iota + 1)}_{(5)}}
+
i - a'_{{(\iota + 1)}_{(5)}}
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Part 3 :

- In this part, we examine the first case where the variables $a'_{{(\iota)}_{(5)}}$ and $b'_{{(\iota)}_{(5)}}$ of the sequence $(\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}})_{\big({\iota}\big)_{(5)} \in \{0, \dots, {\iota}_{max_{(5)}}\}}$ are modified in the algorithm (here, in the "if") in order to express 
  $a'_{{(\iota + 1)}_{(5)}}$ and $b'_{{(\iota + 1)}_{(5)}}$ respectively in terms of $a'_{{(\iota)}_{(5)}}$ and $b'_{{(\iota)}_{(5)}}$. From there, we will compute the difference $\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}} - \mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}$ and see if this difference is negative. 
  If so, then this sequence is strictly decreasing for this case. For this sequence to be a loop variant, it needs to decrease strictly in all possible cases. We therefore need to examine 
  all cases in the algorithm where the variables in the sequence are modified

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\left(
\ \
\left(
\left\{\left\{
\begin{array}{l}
\\
\text{if emitters[a] == 0:} \\
\quad \text{a += 1}
\\
\phantom{}
\end{array}
\right\}\right\}_{T}
\right)
\Rightarrow
\Big(
a'_{{(\iota + 1)}_{(5)}}
=
a'_{{(\iota)}_{(5)}} + 1
\land
b'_{{(\iota + 1)}_{(5)}}
=
b'_{{(\iota)}_{(5)}}
\Big)
\ \
\right)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
i \cdot j - i \cdot b'_{{(\iota + 1)}_{(5)}} + j - b'_{{(\iota + 1)}_{(5)}}
+
i - a'_{{(\iota + 1)}_{(5)}}
\bigg)
\iff
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
i \cdot j - i \cdot \Big( b'_{{(\iota)}_{(5)}} \Big) + j - \Big( b'_{{(\iota)}_{(5)}} \Big)
+
i - \Big( a'_{{(\iota)}_{(5)}} + 1 \Big)
\bigg)
\\[1em]
\quad
\iff
\boxed{
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}}
+
i - a'_{{(\iota)}_{(5)}} - 1
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
=
\Big(
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}}
+
i - a'_{{(\iota)}_{(5)}} - 1
\Big)
-
\Big(
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}}
+
i - a'_{{(\iota)}_{(5)}}
\Big)
\bigg)
\iff
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
=
\Big(
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}}
+
i - a'_{{(\iota)}_{(5)}} - 1
\Big)
-
i \cdot j + i \cdot b'_{{(\iota)}_{(5)}} - j + b'_{{(\iota)}_{(5)}}
-
i + a'_{{(\iota)}_{(5)}}
\bigg)
\\[1em]
\quad
\iff
\boxed{
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
=
-1
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
\leq
-1
\bigg)
\Rightarrow
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
<
0
\bigg)
\Rightarrow
\bigg(
(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
)_{
\big({\iota}\big)_{(5)} \in \{0, \dots, {\iota}_{max_{(5)}}\}
}
\searrow
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 4 :

- In this part, we examine the last case where the variables $a'_{{(\iota)}_{(5)}}$ and $b'_{{(\iota)}_{(5)}}$ of the sequence $(\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}})_{\big({\iota}\big)_{(5)} \in \{0, \dots, {\iota}_{max_{(5)}}\}}$ are modified in the algorithm (here, in the "elif") in order to express 
  $a'_{{(\iota + 1)}_{(5)}}$ and $b'_{{(\iota + 1)}_{(5)}}$ respectively in terms of $a'_{{(\iota)}_{(5)}}$ and $b'_{{(\iota)}_{(5)}}$. From there, we will compute the difference $\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}} - \mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}$ and see if this difference is negative. 

	- The sequence $(\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}})_{\big({\iota}\big)_{(5)} \in \{0, \dots, {\iota}_{max_{(5)}}\}}$ decrease strictly in all possible cases. Therefore this sequence corresponds to the loop variant $V$ of the algorithm

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\left(
\ \
\left(
\left\{\left\{
\begin{array}{l}
\\
\text{elif receivers[b] == 0:} \\
\quad \text{b += 1}
\\
\phantom{}
\end{array}
\right\}\right\}_{T}
\right)
\Rightarrow
\Big(
a'_{{(\iota + 1)}_{(5)}}
=
a'_{{(\iota)}_{(5)}}
\land
b'_{{(\iota + 1)}_{(5)}}
=
b'_{{(\iota)}_{(5)}} + 1
\Big)
\ \
\right)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
i \cdot j - i \cdot b'_{{(\iota + 1)}_{(5)}} + j - b'_{{(\iota + 1)}_{(5)}}
+
i - a'_{{(\iota + 1)}_{(5)}}
\bigg)
\iff
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
i \cdot j - i \cdot \Big( b'_{{(\iota)}_{(5)}} + 1 \Big) + j - \Big( b'_{{(\iota)}_{(5)}} + 1 \Big)
+
i - \Big( a'_{{(\iota)}_{(5)}} \Big)
\bigg)
\\[1em]
\quad
\iff
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} - i + j - b'_{{(\iota)}_{(5)}} - 1
+
i - a'_{{(\iota)}_{(5)}}
\bigg)
\iff
\boxed{
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
=
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}} - 1
-
a'_{{(\iota)}_{(5)}}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
=
\Big(
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}} - 1
-
a'_{{(\iota)}_{(5)}}
\Big)
-
\Big(
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}}
+
i - a'_{{(\iota)}_{(5)}}
\Big)
\bigg)
\iff
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
=
\Big(
i \cdot j - i \cdot b'_{{(\iota)}_{(5)}} + j - b'_{{(\iota)}_{(5)}} - 1
-
a'_{{(\iota)}_{(5)}}
\Big)
-
i \cdot j + i \cdot b'_{{(\iota)}_{(5)}} - j + b'_{{(\iota)}_{(5)}}
-
i + a'_{{(\iota)}_{(5)}}
\bigg)
\\[1em]
\quad
\iff
\boxed{
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
=
-i - 1
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
i \geq 1
\bigg)
\Rightarrow
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
\leq
-2
\bigg)
\Rightarrow
\bigg(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota + 1}\big)_{(5)}}}}
-
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
<
0
\bigg)
\Rightarrow
\bigg(
(
\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}}
)_{
\big({\iota}\big)_{(5)} \in \{0, \dots, {\iota}_{max_{(5)}}\}
}
\searrow
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 5 :

- In this part, we build the formula of the loop variant $V$ of the algorithm using the formula of the sequence $(\mathcal{V}_{{}_{[1]}{g}_{{\big({\iota}\big)_{(5)}}}})_{\big({\iota}\big)_{(5)} \in \{0, \dots, {\iota}_{max_{(5)}}\}}$. We then examine some of its properties in the 
  following parts

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\exists! i, j \in \mathbb{N}_{\geq 1}, \quad
\exists! {\iota}_{max_{(3)}} \in \mathbb{N}, \quad
\forall {\iota}_{(3)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(3)}, \dots, {\iota}_{max_{(3)}}\}, \quad
a' : \{0, \dots, {\iota}_{max_{(3)}}\} \to \mathbb{N}, \quad
{\iota}_{(3)} \mapsto a'({\iota}_{(3)}), \quad
(a')^{-1} : \mathbb{N} \to \{0, \dots, {\iota}_{max_{(3)}}\}, \quad
a' \mapsto {\iota}_{(3)}(a'), \quad
\\[1em]
\quad \quad
\exists! {\iota}_{max_{(4)}} \in \mathbb{N}, \quad
\forall {\iota}_{(4)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(4)}, \dots, {\iota}_{max_{(4)}}\}, \quad
b' : \{0, \dots, {\iota}_{max_{(4)}}\} \to \mathbb{N}, \quad
{\iota}_{(4)} \mapsto b'({\iota}_{(4)}), \quad
(b')^{-1} : \mathbb{N} \to \{0, \dots, {\iota}_{max_{(4)}}\}, \quad
b' \mapsto {\iota}_{(4)}(b'), \quad
\\[1em]
\quad \quad
\forall a', b' \in \mathbb{N}, \quad
V_{{}_{[1]}{g}} : \mathbb{N}^{2} \to \mathbb{N}, \quad
(a', b') \mapsto V_{{}_{[1]}{g}}(a', b'), \quad
\boxed{
V_{{}_{[1]}{g}}(a', b')
:=
(i + 1)
\cdot
(
j - b'
)
+
(1)
\cdot
(
i - a'
)
}
\Bigg)
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
max\Big(
V_{{}_{[1]}{g}}(a', b')
\Big)
=
V_{{}_{[1]}{g}}(0, 0)
=
(i + 1)
\cdot
(
j - 0
)
+
(1)
\cdot
(
i - 0
)
=
i \cdot j + j + i
\bigg)
\land
\bigg(
min\Big(
V_{{}_{[1]}{g}}(a', b')
\Big)
=
V_{{}_{[1]}{g}}(i - 1, j - 1)
=
(i + 1)
\cdot
(
j - (j - 1)
)
+
(1)
\cdot
(
i - (i - 1)
)
=
(i + 1)
\cdot
(
1
)
+
(1)
\cdot
(
1
)
=
i + 2
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
max\Big(
V_{{}_{[1]}{g}}(a', b')
\Big)
-
min\Big(
V_{{}_{[1]}{g}}(a', b')
\Big)
=
\Big(
i \cdot j + j + i
\Big)
-
\Big(
i + 2
\Big)
=
\Big(
i \cdot j + j + i
\Big)
-
i - 2
=
i \cdot j + j - 2
\Bigg)
\end{cases}
\end{array}
$$

Part 6 : Loop exit condition :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\bigg(
a' \geq i
\land
b' < j
\bigg)
\oplus
\bigg(
a' < i
\land
b' \geq j
\bigg)
\oplus
\bigg(
\Big(
a' \geq i
\Big)
\land
\Big(
b' \geq j
\Big)
\bigg)
\Bigg)
}
\end{cases}
\\
\hspace{750pt}
\end{array}
$$

Part 7 :

- In this part, we define the stride $\Delta a'_{{(\iota)}_{(5)}}$ between ${a'}_{({\iota}_{(5)})}$ and ${a'}_{({\iota}_{(5)} + 1)}$ and the stride $\Delta b'_{{(\iota)}_{(5)}}$ between ${b'}_{({\iota}_{(5)})}$ and ${b'}_{({\iota}_{(5)} + 1)}$, in order to define 
  the simultaneous stride $\sigma_{{(\iota)}_{(5)}}$ (see diagram 1 of part 7)
  Stride = pas

	- With the strides defined and the diagram of this part, we can observe that $\Delta a'_{{(\iota)}_{(5)}} + \Delta b'_{{(\iota)}_{(5)}} - \sigma_{{(\iota)}_{(5)}}=1$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\exists! {\iota}_{max_{(5)}} \in \mathbb{N}, \quad
\forall {\iota}_{(5)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(5)}, \dots, {\iota}_{max_{(5)}}\}, \quad
\boxed{
\Big(
a'
:=
0
=
{a'}_{(0)}
\Big)
}
\Rightarrow
\dots
\Rightarrow
\boxed{
\Big(
a'
:=
i
=
{a'}_{({\iota}_{max_{(5)}})}
\Big)
}
\bigg)
\land
\boxed{
\bigg(
\underbrace{
{a'}_{({\iota}_{(5)} + 1)}
-
{a'}_{({\iota}_{(5)})}
}_{
\boxed{
\Delta a'_{{(\iota)}_{(5)}}
}
}
\in \{0, 1\}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\exists! {\iota}_{max_{(5)}} \in \mathbb{N}, \quad
\forall {\iota}_{(5)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(5)}, \dots, {\iota}_{max_{(5)}}\}, \quad
\boxed{
\Big(
b'
:=
0
=
{b'}_{(0)}
\Big)
}
\Rightarrow
\dots
\Rightarrow
\boxed{
\Big(
b'
:=
j
=
{b'}_{({\iota}_{max_{(5)}})}
\Big)
}
\bigg)
\land
\boxed{
\bigg(
\underbrace{
{b'}_{({\iota}_{(5)} + 1)}
-
{b'}_{({\iota}_{(5)})}
}_{
\boxed{
\Delta b'_{{(\iota)}_{(5)}}
}
}
\in \{0, 1\}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\left(
\forall \Delta a'_{{(\iota)}_{(5)}}, \Delta b'_{{(\iota)}_{(5)}} \in \{0, 1\}, \quad
\sigma : \{0, \dots, {\iota}_{max_{(5)}}\} \to \{0, 1\}, \quad
{(\iota)}_{(5)} \mapsto \sigma_{{(\iota)}_{(5)}}, \quad
\boxed{
\sigma_{{(\iota)}_{(5)}}
:=
\begin{cases}
\bigg(
\Delta a'_{{(\iota)}_{(5)}} + \Delta b'_{{(\iota)}_{(5)}} = 1
\bigg)
\Rightarrow
\bigg(
\sigma_{{(\iota)}_{(5)}}
=
0
\bigg)
\\[1em]
\bigg(
\Delta a'_{{(\iota)}_{(5)}} + \Delta b'_{{(\iota)}_{(5)}} = 2
\bigg)
\Rightarrow
\bigg(
\sigma_{{(\iota)}_{(5)}}
=
1
\bigg)
\end{cases}
}
\right)
\end{cases}
\end{array}
$$

Diagram 1 of part 7 :

$$
\begin{array}{l}
\begin{array}{|c|c|c|c|}
\hline
\Delta a'_{{(\iota)}_{(5)}} & \Delta b'_{{(\iota)}_{(5)}} & \Delta a'_{{(\iota)}_{(5)}} + \Delta b'_{{(\iota)}_{(5)}} & \sigma_{{(\iota)}_{(5)}}
\\
\hline
1 & 0 & 1 & 0
\\
\hline
0 & 1 & 1 & 0
\\
\hline
1 & 1 & 2 & 1
\\
\hline
\end{array}
\end{array}
$$

Part 8 :

- In this part, we define $\Omega$ as the number of iterations in the algorithm and by expressing $\Omega$ as a sum of several $1$, we use the relation $\Delta a'_{{(\iota)}_{(5)}} + \Delta b'_{{(\iota)}_{(5)}} - \sigma_{{(\iota)}_{(5)}}=1$ found in part 38 
  to examine if we can express $\Omega$ in terms of ${a'}_{({\iota}_{(5)})}$, or ${b'}_{({\iota}_{(5)})}$, or $\sigma_{{(\iota)}_{(5)}}$, or $i$, or $j$ 
	
	- $\Omega$ is the number of iterations in the algorithm
	
	- $\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{\sigma_{{(\iota)}_{(5)}}}$ is the number of simultaneous strides ("nombre de pas simultanés")
	
	- $\phi$ is the number of zeros in the matrix $\text{allocating\_matrix}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\bigg(
\exists! \Omega \in \mathbb{N}, \quad
\Omega
:=
{\iota}_{max_{(5)}} + 1
=
\overset{{\iota}_{max_{(5)}} + 1}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
1
}
=
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
1
}
\bigg)
\land
\bigg(
\Delta a'_{{(\iota)}_{(5)}} + \Delta b'_{{(\iota)}_{(5)}} - \sigma_{{(\iota)}_{(5)}}
=
1
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Delta a'_{{(\iota)}_{(5)}} + \Delta b'_{{(\iota)}_{(5)}} - \sigma_{{(\iota)}_{(5)}}
=
1
\bigg)
\iff
\bigg(
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\Big(
\Delta a'_{{(\iota)}_{(5)}} + \Delta b'_{{(\iota)}_{(5)}} - \sigma_{{(\iota)}_{(5)}}
\Big)
}
=
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
1
}
\bigg)
\iff
\bigg(
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\Delta a'_{{(\iota)}_{(5)}}
}
+
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\Delta b'_{{(\iota)}_{(5)}}
}
-
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\sigma_{{(\iota)}_{(5)}}
}
=
\Omega
\bigg)
\\[1em]
\quad
\iff
\bigg(
\Big(
{a'}_{({\iota}_{max_{(5)}})} - {a'}_{(0)}
\Big)
+
\Big(
{b'}_{({\iota}_{max_{(5)}})} - {b'}_{(0)}
\Big)
-
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\sigma_{{(\iota)}_{(5)}}
}
=
\Omega
\bigg)
\iff
\bigg(
{a'}_{({\iota}_{max_{(5)}})}
+
{b'}_{({\iota}_{max_{(5)}})}
-
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\sigma_{{(\iota)}_{(5)}}
}
=
\Omega
\bigg)
\iff
\bigg(
i + j
-
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\sigma_{{(\iota)}_{(5)}}
}
=
\Omega
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\Omega
=
i + j
-
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\sigma_{{(\iota)}_{(5)}}
}
\Bigg)
}
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\exists! \phi \in \mathbb{R}, \quad
\phi
:=
i \cdot j
-
\underbrace{
\Big(
i + j
-
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\sigma_{{(\iota)}_{(5)}}
}
\Big)
}_{\Omega}
\Bigg)
}
\end{cases}
\end{array}
$$


Example :

$$
\begin{array}{l}
\underbrace{
E
=
\begin{pmatrix}
50 \\
60 \\
50
\end{pmatrix}
\in \mathcal{M}_{3, 1}(\mathbb{R}_{\geq 0})
}_{\text{Emitters}}
\land
\underbrace{
R
=
\Big(
30, 
70, 
60
\Big)
\in \mathcal{M}_{1, 3}(\mathbb{R}_{\geq 0})
}_{\text{Receivers}}
\land
A
=
\begin{pmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 0
\end{pmatrix}
\in \mathcal{M}_{3, 3}(\mathbb{R}_{\geq 0})
\end{array}
$$

$$
\begin{array}{l}
\begin{array}{|c|c|c|c|c|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
& \quad \quad \quad \text{Receivers}
& \quad \quad \quad \text{Receivers}
& \quad \quad \quad \text{Receivers}
& \quad \quad \quad \text{Receivers}
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{cccc}
& \boxed{30} & 70 & 60
\\
50 & \underline{0} & 0 & 0
\\
60 & 0 & 0 & 0
\\
50 & 0 & 0 & 0
\end{array}
\quad & \quad
\begin{array}{cccc}
& 0 & 70 & 60
\\
\boxed{20} & 30 & \underline{0} & 0
\\
60 & 0 & 0 & 0
\\
50 & 0 & 0 & 0
\end{array}
\quad & \quad
\begin{array}{cccc}
& 0 & \boxed{50} & 60
\\
0 & 30 & 20 & 0
\\
60 & 0 & \underline{0} & 0
\\
50 & 0 & 0 & 0
\end{array}
\quad & \quad
\begin{array}{cccc}
& 0 & 0 & 60
\\
0 & 30 & 20 & 0
\\
\boxed{10} & 0 & 50 & \underline{0}
\\
50 & 0 & 0 & 0
\end{array}
\quad & \quad
\begin{array}{cccc}
& 0 & 0 & \boxed{50}
\\
0 & 30 & 20 & 0
\\
0 & 0 & 50 & 10
\\
\boxed{50} & 0 & 0 & \underline{0}
\end{array}
\quad & \quad
\begin{array}{cccc}
& 0 & 0 & 0
\\
0 & 30 & 20 & 0
\\
0 & 0 & 50 & 10
\\
0 & 0 & 0 & 50
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$



