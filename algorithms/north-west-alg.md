
Definition of the properties of the North-West Corner Method Algorithm :




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




Algorithm main properties :


- Each notation of the type $(P1)$, $(P2)$, etc., refers to one property of the algorithm

$$
\begin{array}{l}
\begin{cases}
(P1) \quad
\left(
\ \
\exists! i, j \in \mathbb{N}_{\geq 1}, \quad
\left(
\underbrace{
\exists! {\iota}_{max_{(1)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(1)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\exists! E_{({\iota}_{(1)})} \in \mathcal{M}_{i, 1}(\mathbb{R}_{\geq 0}), \quad
\left(
\boxed{
E_{({\iota}_{(1)})}
:=
\begin{pmatrix}
E_{{(1,1)}_{({\iota}_{(1)})}} \\
\vdots \\
E_{{(i,1)}_{({\iota}_{(1)})}}
\end{pmatrix}
}
\right)
\land
\left(
\exists! e_{(1)}, \dots, e_{(i)} \in \mathbb{R}_{\geq 0}, \quad
\boxed{
E_{({\iota}_{(1)} = 0)}
=
\begin{pmatrix}
e_{(1)} \\
\vdots \\
e_{(i)}
\end{pmatrix}
=
\begin{pmatrix}
E_{{(1,1)}_{({\iota}_{(1)} = 0)}} \\
\vdots \\
E_{{(i,1)}_{({\iota}_{(1)} = 0)}}
\end{pmatrix}
}
\right)
\right)
\ \
\right)
\\[1em]
(P2) \quad
\left(
\ \
\exists! i, j \in \mathbb{N}_{\geq 1}, \quad
\left(
\underbrace{
\exists! {\iota}_{max_{(2)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\exists! R_{({\iota}_{(2)})} \in \mathcal{M}_{1, j}(\mathbb{R}_{\geq 0}), \quad
\bigg(
\boxed{
R_{({\iota}_{(2)})}
:=
\Big(
R_{{(1,1)}_{({\iota}_{(2)})}}, 
\dots, 
R_{{(1,j)}_{({\iota}_{(2)})}}
\Big)
}
\bigg)
\land
\bigg(
\exists! r_{(1)}, \dots, r_{(j)} \in \mathbb{R}_{\geq 0}, \quad
\boxed{
R_{({\iota}_{(2)} = 0)}
=
\Big(
r_{(1)},
\dots,
r_{(j)}
\Big)
=
\Big(
R_{{(1,1)}_{({\iota}_{(2)} = 0)}}, 
\dots, 
R_{{(1,j)}_{({\iota}_{(2)} = 0)}}
\Big)
}
\bigg)
\right)
\land
\left(
\exists A \in \mathcal{M}_{i, j}(\mathbb{R}_{\geq 0}), \quad
\boxed{
A
:=
\begin{pmatrix}
0 & 0 & \dots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \dots & 0
\end{pmatrix}
}
\right)
\ \
\right)
\\[1em]
(P3) \quad
\Bigg(
\forall \Upsilon \in \{1, \dots, i\}, \quad
\forall \Upsilon' \in \{1, \dots, j\}, \quad
\bigg(
E_{(\Upsilon, 1)} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
R_{(1, \Upsilon')} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
A_{(\Upsilon, \Upsilon')} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
\overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\Upsilon, \varphi)}} = E_{(\Upsilon, 1)}
\bigg)
\land
\bigg(
\overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Upsilon')}} = R_{(1, \Upsilon')}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P4) \quad
\Bigg(
\forall \eta' \in \{0, \dots, max(S'_{1}(i, j))\}, \quad
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\Bigg)
\\[1em]
(P5) \quad
\Bigg(
\forall \Upsilon \in \{1, \dots, i\}, \quad
\forall \Upsilon' \in \{1, \dots, j\}, \quad
\exists \Phi \in \{1, \dots, i\}, \quad
\exists \Phi' \in \{1, \dots, j\}, \quad
\underbrace{
\bigg(
\Big(
A_{(\Phi, \Phi')} \leq E_{(\Upsilon, 1)}
\Big)
\land
\Big(
A_{(\Phi, \Phi')} \leq R_{(1, \Upsilon')}
\Big)
\bigg)
}_{
x
\leq
min(\alpha, \beta)
\iff
\bigg(
\Big(
x \leq \alpha
\Big)
\land
\Big(
x \leq \beta
\Big)
\bigg)
\text{ form}
}
\iff
\bigg(
A_{(\Phi, \Phi')}
\leq
min\Big(
E_{(\Upsilon, 1)}, R_{(1, \Upsilon')}
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P6) \quad
\Bigg(
\forall \eta \in \{1, \dots, max(S_{1}(i, j))\}, \quad
\exists \alpha_{(\eta)} \in \{1, \dots, min(\eta,i)\}, \quad
\exists \beta_{(\eta)} \in \{1, \dots, min(\eta,j)\}, \quad
\bigg(
A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
A_{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
min\Big(
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta - 1)}}, 
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta - 1)}}
\Big)
=
min\Big(
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta - 1)}}, 
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta - 1)}}
\Big)
\bigg)
\land
\bigg(
\forall \gamma \in \{1, \dots, min(\eta,i)\}, \quad
\Big(
i_{(\gamma)} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma' \in \{1, \dots, min(\eta,j)\}, \quad
\Big(
j_{(\gamma')} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = \eta)}}
=
0
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta)}}
=
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta)}}
=
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta)}}
=
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
0
\Big)
\bigg)
\Bigg)
\\[1em]
(P7) \quad
\left(
\left(
E_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}
=
\begin{pmatrix}
0 \\
\vdots \\
0
\end{pmatrix}
\right)
\lor
\bigg(
R_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}
=
\Big(
0, 
\dots, 
0
\Big)
\bigg)
\right)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P8) \quad
\left(
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
\right)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P9) \quad
\left(
\exists! {\iota}_{max_{(5)}} \in \mathbb{N}, \quad
\forall {\iota}_{(5)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(5)}, \dots, {\iota}_{max_{(5)}}\}, \quad
a' : \{0, \dots, {\iota}_{max_{(5)}}\} \to \mathbb{N}, \quad
{\iota}_{(5)} \mapsto {a'}_{{(\iota)}_{(5)}}, \quad
b' : \{0, \dots, {\iota}_{max_{(5)}}\} \to \mathbb{N}, \quad
{\iota}_{(5)} \mapsto {b'}_{{(\iota)}_{(5)}}, \quad
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
\land
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
\land
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
\right)
\\[1em]
(P10) \quad
\Bigg(
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
=
i + j
-
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\sigma_{{(\iota)}_{(5)}}
}
\Bigg)
\\[1em]
(P11) \quad
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
\end{cases}
\end{array}
$$




Proof of the algorithm properties :

Part 1 :


- (English) If we start from the principle that :

	- 1 physical resource denotes 1 physical object present
	
	- 0 means that the physical resource is not present
	
	- a non-zero positive number denotes the presence of one or more physical resources
	
	- subtraction is the extraction of one or more physical resources present
	
	- the objective is to manipulate physical resources

  Therefore, -1 and any number greater than -1 are not relevant because we do not extract a physical resource that is not present. 
  Here, we therefore choose to manipulate positive or zero quantities of physical resources present. 
  These quantities can also be decimal because they represent physical quantities




- (English) I. We arbitrarily choose a type of physical resource (which we will call “common resource”)


- (English) II. The following information then applies :


	- $E$ is a column matrix with $i$ rows, where each row contains a value $e_{(1 \leq \lambda \leq i)}$. Each value $e_{(1 \leq \lambda \leq i)}$ (which we will call emitter $e_{(1 \leq \lambda \leq i)}$) represents a quantity of units of
	  “common resource” (which we will call the “usable quantity”) that is emitted

	- $R$ is a row matrix with $j$ columns, where each column contains a value $r_{(1 \leq \Lambda \leq j)}$. Each value $r_{(1 \leq \Lambda \leq j)}$ (which we will call receiver $r_{(1 \leq \Lambda \leq j)}$) represents a quantity of units of
     ″common resource″ requested by the receiver $r_{(1 \leq \Lambda \leq j)}$ (which we will call a “need”) so that the receiver can do something with it. This amount can be received : 
		 either by an emitter $e_{(1 \leq \lambda_{1} \leq i)}$ (and this emitter comes from $E$)
		 either by several other different emitters $e_{(\lambda_{2} \neq \lambda_{1})}$, $e_{(\lambda_{3} \neq \lambda_{1})}$, etc. (and all these emitters come from $E$)


	- Thus, each value $e_{(1 \leq \lambda \leq i)}$ is emitted, and each value $e_{(1 \leq \lambda \leq i)}$ is either received by a single receiver $r_{(1 \leq \Lambda_{\lambda} \leq j)}$, either split among several receivers $r_{(\Lambda'_{\lambda} \neq \Lambda_{\lambda})}$, $r_{(\Lambda''_{\lambda} \neq \Lambda_{\lambda})}$, ...


	- $A$ is a matrix (which we will call the “flow matrix”) that represents the "optimal distribution" of quantities of units of “common resource” between all the emitters and 
	  all the receivers.
	  “optimal distribution” means that we do not have a situation where some receivers receive more than they need while others receive no quantity at all
	
	- Each value in matrix $A$ represents the "optimal quantity" (optimal in relation to the “optimal distribution”) of units of “common resource” that is transferred (= the quantity) from 
	  the emitter $e_{(1 \leq \lambda \leq i)}$ to its receiver $r_{(1 \leq \Lambda \leq j)}$ (= receiver of $e_{(1 \leq \lambda \leq i)}$).
	  This “optimal quantity” corresponds to a portion of the “usable quantity” from $e_{(1 \leq \lambda \leq i)}$. 
	  If a value in matrix $A$ is different from zero, then such a transfer has taken place. In this case, a portion of the “usable quantity” from $e_{(1 \leq \lambda \leq i)}$ is transferred 
	  (so this portion is subtracted from $e_{(1 \leq \lambda \leq i)}$) to $r_{(1 \leq \Lambda \leq j)}$ (which no longer requires as much since it has received this portion, so we subtract this same portion from $r_{(1 \leq \Lambda \leq j)}$).
	  The value of this portion depends on steps 1 to 7 of the part 1


    - In other words, considering the matrix $A$ as a grid of “cells”, each cell located at the intersection of a row $\lambda$ and a column $\Lambda$ contains a value denoted $A_{(\lambda, \Lambda)}$ 
	  representing the optimal quantity of units of “common resource” that is transferred (= the quantity) from the emitter $e_{(1 \leq \lambda \leq i)}$ to its receiver $r_{(1 \leq \Lambda \leq j)}$ (i.e the receiver of $e_{(1 \leq \lambda \leq i)}$)

	- Since a portion of the “usable quantity” from $e_{(1 \leq \lambda \leq i)}$ is transferred (and thus this portion is subtracted from $e_{(1 \leq \lambda \leq i)}$ ) to $r_{(1 \leq \Lambda \leq j)}$ (which no longer requires as much because it 
	  has received that portion, so we subtract that same portion from $r_{(1 \leq \Lambda \leq j)}$), then no additional quantity is added during this transfer, and no quantity goes somewhere else during 
	  this transfer.
      Therefore, in the matrix $A$, in one same row, each column represents either 0 or a portion of the value of the emitter (since each transfer does not produce extra-quantities)
	  In the same column, each row represents a portion of the value of one emitter for the same receiver (= a portion of each $e_{(1 \leq \lambda' \leq i)}$ is transferred to the same $r_{(1 \leq \Lambda \leq j)}$)




	- Therefore $\boxed{e_{(1 \leq \lambda \leq i)} \in \mathbb{R}_{\geq 0} \land r_{(1 \leq \Lambda \leq j)} \in \mathbb{R}_{\geq 0} \land A_{(\lambda, \Lambda)} \in \mathbb{R}_{\geq 0} \land \overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\lambda, \varphi)}} = e_{(1 \leq \lambda \leq i)} \land \overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Lambda)}} = r_{(1 \leq \Lambda \leq j)}}$ and :

		- $\overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\lambda, \varphi)}} = e_{(1 \leq \lambda \leq i)}$ : in the same row, for each $r_{(1 \leq \Lambda' \leq j)}$, a portion (which can be zero) of the "usable quantity" comes from the same $e_{(1 \leq \lambda \leq i)}$ 
		- $\overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Lambda)}} = r_{(1 \leq \Lambda \leq j)}$ : in the same column, for each $e_{(1 \leq \lambda' \leq i)}$, a portion (which can be zero) of the "usable quantity" of each $e_{(1 \leq \lambda' \leq i)}$ is transferred to the same $r_{(1 \leq \Lambda \leq j)}$ 




	- Starting with $\lambda = 1$ and $\Lambda = 1$, and starting from the cell (= the “northwest” cell = the top-left cell of $A$) located at the intersection of the row $\lambda = 1$ (of $A$) and 
      the column $\Lambda = 1$ (of $A$) :
		
		- 1. We examine the value $e_{(\lambda = 1)}$ (= value of the $\lambda = 1$ row of matrix $E$) and the value $r_{(\Lambda = 1)}$ (= value of the $\Lambda = 1$ column of matrix $R$)
		
		- 2. We take the minimum value between $e_{(\lambda = 1)}$ and $r_{(\Lambda = 1)}$. This minimum value is called the “current minimum”
		
		- 3. We subtract the “current minimum” from the value $e_{(\lambda = 1)}$ and we subtract the “current minimum” from the value $r_{(\Lambda = 1)}$ 
		
		- 4. If $e_{(\lambda = 1)} = 0$, then the value of $\lambda$ is increased by 1. We then proceed directly to step 7

		- 5. If $r_{(\Lambda = 1)} = 0$, then the value of $\Lambda$ is increased by 1. We then proceed directly to step 7
		
		- 6. If $e_{(\lambda = 1)} = 0$ and $r_{(\Lambda = 1)} = 0$ (at the same time), then either the value of $\lambda$ is increased by 1, either the value of $\Lambda$ is increased by 1 (whichever is chosen). We then proceed 
		  directly to step 7
		
		- 7. We repeat the process starting from step 1 until either the sum of the emitters is 0, or the sum of the receivers is 0, or the sum of the emitters and the sum of the 
          receivers (= simultaneously) is 0




- (French) I. On choisit arbitrairement un type de ressource physique / matérielle (qu'on appellera "ressource commune")


- (French) II. Les informations ci-après sont ensuite applicables :

	
	- $E$ est une matrice colonne de $i$ lignes où chaque ligne contient une valeur $e_{(1 \leq \lambda \leq i)}$. Chaque valeur $e_{(1 \leq \lambda \leq i)}$ (qu'on appellera émetteur $e_{(1 \leq \lambda \leq i)}$) représente une quantité d'unités de
	  "ressource commune" (qu'on appellera "quantité utilisable") qui est émise
	
	- $R$ est une matrice ligne de $j$ colonnes où chaque colonne contient une valeur $r_{(1 \leq \Lambda \leq j)}$. Chaque valeur $r_{(1 \leq \Lambda \leq j)}$ (qu'on appellera récepteur $r_{(1 \leq \Lambda \leq j)}$) représente une quantité d'unités de
	  "ressource commune" demandée par le récepteur $r_{(1 \leq \Lambda \leq j)}$ (qu'on appellera un "besoin") pour que le récepteur puisse en faire quelque chose. Cette quantité peut être reçue :
		- soit par un émetteur $e_{(1 \leq \lambda_{1} \leq i)}$ (et cet émetteur vient de $E$)
		- soit par plusieurs autres émetteurs différents $e_{(\lambda_{2} \neq \lambda_{1})}$, $e_{(\lambda_{3} \neq \lambda_{1})}$, etc. (et tous ces émetteurs viennent de $E$)
	
	
	- Ainsi, chaque valeur $e_{(1 \leq \lambda \leq i)}$ est émise, et chaque valeur $e_{(1 \leq \lambda \leq i)}$ est soit reçue par un seul récepteur $r_{(1 \leq \Lambda_{\lambda} \leq j)}$, soit fractionnée entre plusieurs récepteurs $r_{(\Lambda'_{\lambda} \neq \Lambda_{\lambda})}$, $r_{(\Lambda''_{\lambda} \neq \Lambda_{\lambda})}$, ...
	
	
	- $A$ est une matrice (qu'on appellera "matrice de flux") qui représente la "répartition optimale" des quantités d'unités de "ressource commune" entre l'ensemble des émetteurs et 
	  l'ensemble des récepteurs.
	  "répartition optimale" signifie qu'on n'a pas la situation où certains récepteurs reçoivent des quantités supérieures à leurs besoins et où d'autres récepteurs ne reçoivent aucune quantité
	
	- 0. Chaque valeur de la matrice $A$ représente la "quantité optimale" (optimale par rapport à la "répartition optimale") d'unités de "ressource commune" qui est transférée 
	  (= la quantité) de l'émetteur $e_{(1 \leq \lambda \leq i)}$ vers son récepteur $r_{(1 \leq \Lambda \leq j)}$ (= récepteur de $e_{(1 \leq \lambda \leq i)}$). 
	  Cette "quantité optimale" représente une partie de la "quantité utilisable" provenant de $e_{(1 \leq \lambda \leq i)}$. 
	  Si une valeur de la matrice $A$ est différente de zéro, alors un tel transfert a eu lieu.  Dans ce cas, une partie de la "quantité utilisable" provenant de $e_{(1 \leq \lambda \leq i)}$ est transférée 
	  (donc cette partie est soustraite de $e_{(1 \leq \lambda \leq i)}$) vers $r_{(1 \leq \Lambda \leq j)}$ (qui ne demande plus autant car il a reçu cette partie, donc on vient soustraire cette même partie de $r_{(1 \leq \Lambda \leq j)}$). 
	  La valeur de cette partie dépend des étapes 1 à 7 de la partie 1

	
	- Autrement dit, en considérant la matrice $A$ comme un tableau de "cases", chaque case située à l'intersection d'une ligne $\lambda$ et d'une colonne $\Lambda$ contient une valeur notée $A_{(\lambda, \Lambda)}$ 
	  représentant la quantité optimale d'unités de "ressource commune" qui est transférée (= la quantité) de l'émetteur $e_{(1 \leq \lambda \leq i)}$ vers son récepteur $r_{(1 \leq \Lambda \leq j)}$ (= récepteur de $e_{(1 \leq \lambda \leq i)}$)


	- Comme une partie de la "quantité utilisable" de $e_{(1 \leq \lambda \leq i)}$ est transférée (et que cette partie est donc soustraite de $e_{(1 \leq \lambda \leq i)}$) vers $r_{(1 \leq \Lambda \leq j)}$ (qui n'en a plus autant besoin car elle 
	  a reçu cette partie, donc on soustrait cette même partie de $r_{(1 \leq \Lambda \leq j)}$), alors aucune quantité supplémentaire n’est ajoutée pendant ce transfert, et aucune quantité ne part ailleurs 
	  pendant ce transfert.
	  Ainsi, dans la matrice $A$, sur une même ligne, chaque colonne représente soit 0, soit une partie de la valeur de l'émetteur (comme chaque transfert ne produit pas de "quantités extra")
	  Sur une même colonne, chaque ligne représente une partie de la valeur d'un émetteur pour un même récepteur (= une partie de chaque $e_{(1 \leq \lambda' \leq i)}$ est transférée vers un même $r_{(1 \leq \Lambda \leq j)}$)




	- Donc $\boxed{e_{(1 \leq \lambda \leq i)} \in \mathbb{R}_{\geq 0} \land r_{(1 \leq \Lambda \leq j)} \in \mathbb{R}_{\geq 0} \land A_{(\lambda, \Lambda)} \in \mathbb{R}_{\geq 0} \land \overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\lambda, \varphi)}} = e_{(1 \leq \lambda \leq i)} \land \overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Lambda)}} = r_{(1 \leq \Lambda \leq j)}}$ et :

		- $\overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\lambda, \varphi)}} = e_{(1 \leq \lambda \leq i)}$ : sur la même ligne, pour chaque $r_{(1 \leq \Lambda' \leq j)}$, une partie (qui peut valoir zéro) de la "quantité utilisable" provient du même $e_{(1 \leq \lambda \leq i)}$ 
		- $\overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Lambda)}} = r_{(1 \leq \Lambda \leq j)}$ : sur la même colonne, pour chaque $e_{(1 \leq \lambda' \leq i)}$, une partie (qui peut valoir zéro) de la "quantité utilisable" de chaque $e_{(1 \leq \lambda' \leq i)}$ est transférée vers le 
		  même $r_{(1 \leq \Lambda \leq j)}$ 




	- En partant de $\lambda = 1$ et de $\Lambda = 1$, et en partant de la case (= case "Nord-Ouest" = case la plus en haut et la plus à gauche de $A$) située à l'intersection de la ligne $\lambda = 1$ (de $A$) et 
	  de la colonne $\Lambda = 1$ (de $A$) :
		
		- 1. On regarde la valeur $e_{(\lambda = 1)}$ (= valeur de la ligne $\lambda = 1$ de la matrice $E$) et la valeur $r_{(\Lambda = 1)}$ (= valeur de la colonne $\Lambda = 1$ de la matrice $R$)
		
		- 2. On prend la valeur minimale entre $e_{(\lambda = 1)}$ et $r_{(\Lambda = 1)}$. Cette valeur minimale est appelée "minimum actuel"
		
		- 3. On soustrait le "minimum actuel" à la valeur $e_{(\lambda = 1)}$ et on soustrait le "minimum actuel" à la valeur $r_{(\Lambda = 1)}$ 
		
		- 4. Si $e_{(\lambda = 1)} = 0$, alors la valeur de $\lambda$ augmente de 1. On passe ensuite directement à l'étape 7
		
		- 5. Si $r_{(\Lambda = 1)} = 0$, alors la valeur de $\Lambda$ augmente de 1. On passe ensuite directement à l'étape 7
		
		- 6. Si $e_{(\lambda = 1)} = 0$ et $r_{(\Lambda = 1)} = 0$ (en même temps), alors soit la valeur de $\lambda$ augmente de 1, soit la valeur de $\Lambda$ augmente de 1 (au choix). On passe ensuite directement à l'étape 7
		
		- 7. On recommence à partir de l'étape 1 jusqu'à ce que soit la somme des émetteurs vaut 0, soit la somme des récepteurs vaut 0, soit la somme des émetteurs et la somme des 
		  récepteurs (= en même temps) vaut 0




- In this part, we initialize the elements needed for the algorithm

	- The northwest corner method starts from the cell (= the “northwest” cell = the top-left cell of $A$) located at the intersection of the row $\lambda = 1$ (of $A$) and 
      the column $\Lambda = 1$ (of $A$) because it corresponds to the sense of scanning commonly used in computer science to scan two-dimensional data structures such as matrices


	- $E$ can be viewed as a column matrix and $R$ as a row matrix, since visually the flow matrix $A$ can be in the center, with $E$ to its left and $R$ at the top of $A$ 


	- $\boxed{{\iota}_{(1)}}$ represents the ${\iota}_{(1)}$-th time the matrix $E$ change its value from its previous value in the algorithm (similar to a recurrent sequence of order 1). Each time a value in matrix $E$ is 
	  modified, ${\iota}_{(1)}$ increases by 1, and matrix $E$ is considered updated. Moreover, each time ${\iota}_{(1)}$ is increased by 1, then matrix $E$ is also considered updated, even if its values remain the same
	
	- $\boxed{{\iota}_{(2)}}$ represents the ${\iota}_{(2)}$-th time the matrix $R$ change its value from its previous value in the algorithm (similar to a recurrent sequence of order 1). Each time a value in matrix $R$ is 
	  modified, ${\iota}_{(2)}$ increases by 1, and matrix $R$ is considered updated. Moreover, each time ${\iota}_{(2)}$ is increased by 1, then matrix $R$ is also considered updated, even if its values remain the same
	
	
	- $E_{({\iota}_{(1)})}$ corresponds to matrix $E$ at the ${\iota}_{(1)}$-th update. Thus, $E_{({\iota}_{(1)} = 0)}$ refers to the first version of matrix $E$ (= the initialization of $E$)
	
	- $R_{({\iota}_{(2)})}$ corresponds to matrix $R$ at the ${\iota}_{(2)}$-th update. Thus, $R_{({\iota}_{(2)} = 0)}$ refers to the first version of matrix $R$ (= the initialization of $R$)

$$
\begin{array}{l}
\exists! i, j \in \mathbb{N}_{\geq 1}, \quad
\left(
\ \
\left(
\underbrace{
\exists! {\iota}_{max_{(1)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(1)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\exists! E_{({\iota}_{(1)})} \in \mathcal{M}_{i, 1}(\mathbb{R}_{\geq 0}), \quad
\boxed{
E_{({\iota}_{(1)})}
:=
\begin{pmatrix}
E_{{(1,1)}_{({\iota}_{(1)})}} \\
\vdots \\
E_{{(i,1)}_{({\iota}_{(1)})}}
\end{pmatrix}
}
\right)
\land
\bigg(
\underbrace{
\exists! {\iota}_{max_{(2)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\exists! R_{({\iota}_{(2)})} \in \mathcal{M}_{1, j}(\mathbb{R}_{\geq 0}), \quad
\boxed{
R_{({\iota}_{(2)})}
:=
\Big(
R_{{(1,1)}_{({\iota}_{(2)})}}, 
\dots, 
R_{{(1,j)}_{({\iota}_{(2)})}}
\Big)
}
\bigg)
\ \
\right)
\\[1em]
\Rightarrow
\begin{cases}
\left(
\ \
\left(
\exists! e_{(1)}, \dots, e_{(i)} \in \mathbb{R}_{\geq 0}, \quad
\boxed{
E_{({\iota}_{(1)} = 0)}
=
\begin{pmatrix}
e_{(1)} \\
\vdots \\
e_{(i)}
\end{pmatrix}
=
\begin{pmatrix}
E_{{(1,1)}_{({\iota}_{(1)} = 0)}} \\
\vdots \\
E_{{(i,1)}_{({\iota}_{(1)} = 0)}}
\end{pmatrix}
}
\right)
\land
\bigg(
\exists! r_{(1)}, \dots, r_{(j)} \in \mathbb{R}_{\geq 0}, \quad
\boxed{
R_{({\iota}_{(2)} = 0)}
=
\Big(
r_{(1)},
\dots,
r_{(j)}
\Big)
=
\Big(
R_{{(1,1)}_{({\iota}_{(2)} = 0)}}, 
\dots, 
R_{{(1,j)}_{({\iota}_{(2)} = 0)}}
\Big)
}
\bigg)
\ \
\right)
\\[1em]
\Rightarrow
\left(
\exists A \in \mathcal{M}_{i, j}(\mathbb{R}_{\geq 0}), \quad
\boxed{
A
:=
\begin{pmatrix}
0 & 0 & \dots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \dots & 0
\end{pmatrix}
}
\right)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\forall \Upsilon \in \{1, \dots, i\}, \quad
\forall \Upsilon' \in \{1, \dots, j\}, \quad
\bigg(
E_{(\Upsilon, 1)} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
R_{(1, \Upsilon')} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
A_{(\Upsilon, \Upsilon')} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
\overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\Upsilon, \varphi)}} = E_{(\Upsilon, 1)}
\bigg)
\land
\bigg(
\overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Upsilon')}} = R_{(1, \Upsilon')}
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 2 :

- Since a portion of the “usable quantity” from $e_{(1 \leq \lambda \leq i)}$ is transferred (and thus this portion is subtracted from $e_{(1 \leq \lambda \leq i)}$ ) to $r_{(1 \leq \Lambda \leq j)}$ (which no longer requires as much because it has received 
  that portion, so we subtract that same portion from $r_{(1 \leq \Lambda \leq j)}$), then no additional quantity is added during this transfer, and no quantity goes somewhere else during this transfer.
  Since we subtract the same value (= portion) from both sides (= $e_{(1 \leq \lambda \leq i)}$ and $r_{(1 \leq \Lambda \leq j)}$), the gap (= the difference) between $e_{(1 \leq \lambda \leq i)}$ and $r_{(1 \leq \Lambda \leq j)}$ remains the same

- Thus, if before the transfer we had $e_{(1 \leq \lambda \leq i)} < r_{(1 \leq \Lambda \leq j)}$, then after the transfer we will still have $e_{(1 \leq \lambda \leq i)} < r_{(1 \leq \Lambda \leq j)}$ because the gap (= the difference) between $e_{(1 \leq \lambda \leq i)}$ and $r_{(1 \leq \Lambda \leq j)}$ remains 
  the same (during all the execution of the algorithm)

- It means that, at the scale of all the emitters and all the receivers, the gap (= the difference) between the sum of all the emitters ($\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}}$) and the sum of all the receivers ($\overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}$) 
  remains the same (during all the execution of the algorithm).
  It also means that the order relation between the sum of all the emitters and the sum of all the receivers is preserved (during all the execution of the algorithm)

- Concretely, if before the transfer of a part of a “usable quantity” from a $e_{(1 \leq \lambda \leq i)}$, we have $\Big(\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}} = \overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}\Big) \oplus \Big(\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}} < \overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}\Big) \oplus \Big(\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}} > \overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}\Big)$, then after 
  such a transfer we will still have $\Big(\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}} = \overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}\Big) \oplus \Big(\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}} < \overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}\Big) \oplus \Big(\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}} > \overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}\Big)$ 


- From part 2 to part 12, we show by reccurence that the order relation between the sum of all the emitters ($\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}}$) and the sum of all the receivers ($\overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}$) is preserved during all 
  the execution of the algorithm

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\eta'_{0}
:=
0
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\exists \Psi_{(1)} \in \{1, \dots, i\}, \quad
\exists \Psi'_{(1)} \in \{1, \dots, j\}, \quad
\bigg(
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
=
min\Big(
E_{{(\Psi_{(1)}, 1)}_{({\iota}_{(1)} = 0)}}, 
R_{{(1, \Psi'_{(1)} )}_{({\iota}_{(2)} = 0)}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
E_{{(\Psi_{(1)}, 1)}_{({\iota}_{(1)} = 1)}}
=
E_{{(\Psi_{(1)}, 1)}_{({\iota}_{(1)} = 0)}}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
\bigg)
\land
\bigg(
R_{{(1, \Psi'_{(1)} )}_{({\iota}_{(2)} = 1)}}
=
R_{{(1, \Psi'_{(1)} )}_{({\iota}_{(2)} = 0)}}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
=
\overset{i}{\underset{\substack{{ \psi = 1 } \\ { \psi \neq \Psi_{(1)} }}}{\sum}}{
\big(
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
\big)
}
+
(
E_{{(\Psi_{(1)}, 1)}_{({\iota}_{(1)} = 0)}}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
)
=
\overset{i}{\underset{\psi = 1}{\sum}}{
\big(
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
\big)
}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
\bigg)
\land
\bigg(
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
=
\overset{j}{\underset{\substack{{ \psi = 1 } \\ { \psi \neq \Psi'_{(1)} }}}{\sum}}{
\big(
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
\big)
}
+
(
R_{{(1, \Psi'_{(1)} )}_{({\iota}_{(2)} = 0)}}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
)
=
\overset{j}{\underset{\psi = 1}{\sum}}{
\big(
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
\big)
}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
-
A_{(\Psi_{(1)}, \Psi'_{(1)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 3 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\exists \Psi_{(2)} \in \{1, \dots, i\}, \quad
\exists \Psi'_{(2)} \in \{1, \dots, j\}, \quad
\bigg(
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
=
min\Big(
E_{{(\Psi_{(2)}, 1)}_{({\iota}_{(1)} = 1)}}, 
R_{{(1, \Psi'_{(2)} )}_{({\iota}_{(2)} = 1)}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
E_{{(\Psi_{(2)}, 1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(\Psi_{(2)}, 1)}_{({\iota}_{(1)} = 1)}}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
\bigg)
\land
\bigg(
R_{{(1, \Psi'_{(2)} )}_{({\iota}_{(2)} = 2)}}
=
R_{{(1, \Psi'_{(2)} )}_{({\iota}_{(2)} = 1)}}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
=
\overset{i}{\underset{\substack{{ \psi = 1 } \\ { \psi \neq \Psi_{(2)} }}}{\sum}}{
\big(
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
\big)
}
+
(
E_{{(\Psi_{(2)}, 1)}_{({\iota}_{(1)} = 1)}}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
)
=
\overset{i}{\underset{\psi = 1}{\sum}}{
\big(
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
\big)
}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
\bigg)
\land
\bigg(
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
=
\overset{j}{\underset{\substack{{ \psi = 1 } \\ { \psi \neq \Psi'_{(2)} }}}{\sum}}{
\big(
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
\big)
}
+
(
R_{{(1, \Psi'_{(2)} )}_{({\iota}_{(2)} = 1)}}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
)
=
\overset{j}{\underset{\psi = 1}{\sum}}{
\big(
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
\big)
}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 4 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
-
A_{(\Psi_{(2)}, \Psi'_{(2)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 5 :

- Since we need to specify bounds in the recurrence to specify the recurrence hypothesis, then we can suppose that the comparison between $e_{(1 \leq \lambda \leq i)}$ and $r_{(1 \leq \Lambda \leq j)}$ (to get a minimal value for 
  the matrix $A$) can be performed on all the "length" of $E$ (the "length" is $i$), or on all the "length" of $R$ (the "length" is $j$). Thus then :
  
	- it means that $e_{(1 \leq \lambda \leq i)}$ and $r_{(1 \leq \Lambda \leq j)}$ can change simultaneously their values (from their previous values in the algorithm) a maximum of either $i$ times (because it is on all the "length" of $E$), 
	  either (= here, not both) $j$ times (because it is on all the "length" of $R$). 
	  Indeed, for each comparison performed between $e_{(1 \leq \lambda \leq i)}$ and $r_{(1 \leq \Lambda \leq j)}$, we subtract simultaneously a "portion" from $e_{(1 \leq \lambda \leq i)}$ and $r_{(1 \leq \Lambda \leq j)}$ in order to get new versions of $e_{(1 \leq \lambda \leq i)}$ 
	  and $r_{(1 \leq \Lambda \leq j)}$ (thus their values change simultaneously, ${\iota}_{(1)}$ and ${\iota}_{(2)}$ increase by 1, and $E$ and $R$ are considered updated). 
	  The simultaneous value changes of ${\iota}_{(1)}$ and ${\iota}_{(2)}$ can be viewed as an increase of 1 of one same index (which we will call $\boxed{\eta'}$). 
	  This index can vary either between 0 (no update of ${\iota}_{(1)}$ and ${\iota}_{(2)}$) and $j$ (maximum number of times possible), either (= here, not both) between 0 (no update of ${\iota}_{(1)}$ and ${\iota}_{(2)}$) and $i$ 
	  (maximum number of times possible) (these variations can be defined in the set $\boxed{S'_{1}(i, j)}$)

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\left(
\ \
S'_{1}(i, j)
:=
\begin{cases}
i < j
\Rightarrow
S'_{1}(i, j)
=
\{0, \dots, j\}
\\[1em]
i \geq j
\Rightarrow
S'_{1}(i, j)
=
\{0, \dots, i\}
\end{cases}
\ \
\right)
}
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\mathcal{P}(\eta') :
\Bigg(
\bigg(
\Big(
\underline{0 \leq \eta' \leq max(S'_{1}(i, j))}
\Big)
\Rightarrow
\Big(
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\Big)
\Big)
\bigg)
\Bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 6 :

$$
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
k' = 0
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(\eta'_{0}) :
\Bigg(
\bigg(
\Big(
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{0})}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{0})}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{0})}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{0})}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{0})}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{0})}}
}
\Big)
\Big)
\bigg)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg[
\ \
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\Bigg)
\iff
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\bigg)
\Bigg)
}
\ \
\Bigg]
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(\eta'_{0})
\Bigg)
}
\end{cases}
$$

Part 7 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
k' = 1
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(k' = 1) :
\Bigg(
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{1})}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{1})}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{1})}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{1})}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{1})}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{1})}}
}
\Big)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(k' = 1)
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
\Bigg(
k' = 2
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\mathcal{P}(k' = 2) :
\Bigg(
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{2})}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{2})}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{2})}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{2})}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \boxed{2})}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \boxed{2})}}
}
\Big)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 1)}}
}
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 2)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 2)}}
}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(k' = 2)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 9 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
k' \curvearrowright k' + 1
\Bigg)
\\[1em]
\Rightarrow
\begin{cases}
\mathcal{P}(k') :
\Bigg(
\bigg(
\Big(
\underline{0 \leq k' \leq max(S'_{1}(i, j))}
\Big)
\Rightarrow
\Big(
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\Big)
\Big)
\bigg)
\Bigg)
\\[1em]
\mathcal{H}(k') :
\Bigg(
\forall k' \in \mathbb{N}, \quad
\Bigg(
k' \geq \eta'_{0}
\land
\mathcal{P}(k')
\Bigg)
\Rightarrow
\Bigg(
\mathcal{P}(k' + 1) :
\Bigg(
\bigg(
\Big(
\underline{0 \leq k' + 1 \leq max(S'_{1}(i, j))}
\Big)
\Rightarrow
\Big(
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\Big)
\oplus
\Big(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\Big)
\Big)
\bigg)
\Bigg)
\Bigg)
\end{cases}
\end{cases}
\end{array}
$$

Part 10 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\exists \Psi_{(k' + 1)} \in \{1, \dots, i\}, \quad
\exists \Psi'_{(k' + 1)} \in \{1, \dots, j\}, \quad
\bigg(
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
=
min\Big(
E_{{(\Psi_{(k' + 1)}, 1)}_{({\iota}_{(1)} = k')}}, 
R_{{(1, \Psi'_{(k' + 1)} )}_{({\iota}_{(2)} = k')}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
E_{{(\Psi_{(k' + 1)}, 1)}_{({\iota}_{(1)} = k' + 1)}}
=
E_{{(\Psi_{(k' + 1)}, 1)}_{({\iota}_{(1)} = k')}}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
\bigg)
\land
\bigg(
R_{{(1, \Psi'_{(k' + 1)} )}_{({\iota}_{(2)} = k' + 1)}}
=
R_{{(1, \Psi'_{(k' + 1)} )}_{({\iota}_{(2)} = k')}}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
=
\overset{i}{\underset{\substack{{ \psi = 1 } \\ { \psi \neq \Psi_{(k' + 1)} }}}{\sum}}{
\big(
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
\big)
}
+
(
E_{{(\Psi_{(2)}, 1)}_{({\iota}_{(1)} = k')}}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
)
=
\overset{i}{\underset{\psi = 1}{\sum}}{
\big(
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
\big)
}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
\bigg)
\land
\bigg(
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
=
\overset{j}{\underset{\substack{{ \psi = 1 } \\ { \psi \neq \Psi'_{(k' + 1)} }}}{\sum}}{
\big(
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
\big)
}
+
(
R_{{(1, \Psi'_{(k' + 1)} )}_{({\iota}_{(2)} = k')}}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
)
=
\overset{j}{\underset{\psi = 1}{\sum}}{
\big(
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
\big)
}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 11 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k')}}
}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k')}}
}
-
A_{(\Psi_{(k' + 1)}, \Psi'_{(k' + 1)} )}
\iff
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = k' + 1)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = k' + 1)}}
}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(k'+1)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 12 :

- We have shown by reccurence that the order relation between the sum of all the emitters ($\overset{i}{\underset{\psi = 1}{\sum}}{E_{(\psi, 1)}}$) and the sum of all the receivers ($\overset{j}{\underset{\psi = 1}{\sum}}{R_{(1, \psi)}}$) is preserved during all 
  the execution of the algorithm

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\forall \eta' \in \{0, \dots, max(S'_{1}(i, j))\}, \quad
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 13 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall \Upsilon \in \{1, \dots, i\}, \quad
\forall \Upsilon' \in \{1, \dots, j\}, \quad
\boxed{
\bigg(
E_{(\Upsilon, 1)} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
R_{(1, \Upsilon')} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
A_{(\Upsilon, \Upsilon')} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
\overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\Upsilon, \varphi)}} = E_{(\Upsilon, 1)}
\bigg)
\land
\bigg(
\overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Upsilon')}} = R_{(1, \Upsilon')}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underline{
\exists \Phi \in \{1, \dots, i\}, \quad
\exists \Phi' \in \{1, \dots, j\}
}
, \quad
\bigg(
\Big(
\overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\Upsilon, \varphi)}} = E_{(\Upsilon, 1)}
\Big)
\iff
\Big(
A_{(\Upsilon, 1)} + A_{(\Upsilon, 2)} + \dots + \boxed{A_{(\Phi, \Phi')}} + \dots + A_{(\Upsilon, j)}
=
\boxed{
E_{(\Upsilon, 1)}
}
\Big)
\bigg)
\land
\bigg(
\Big(
\overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Upsilon')}} = R_{(1, \Upsilon')}
\Big)
\iff
\Big(
A_{(1, \Upsilon')} + A_{(2, \Upsilon')} + \dots + \boxed{A_{(\Phi, \Phi')}} + \dots + A_{(i, \Upsilon')}
=
\boxed{
R_{(1, \Upsilon')}
}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underline{
\forall \varphi \in \{1, \dots, j\}, \quad
\forall \Upsilon \in \{1, \dots, i\}, \quad
\forall \varphi' \in \{1, \dots, i\}, \quad
\forall \Upsilon' \in \{1, \dots, j\}, \quad
\exists \Phi \in \{1, \dots, i\}, \quad
\exists \Phi' \in \{1, \dots, j\}
}
, \quad
\bigg(
\Big(
\underbrace{A_{(\Upsilon, 1)}}_{\geq 0} + \underbrace{A_{(\Upsilon, 2)}}_{\geq 0} + \dots + \boxed{\underbrace{A_{(\Phi, \Phi')}}_{\geq 0}} + \dots + \underbrace{A_{(\Upsilon, j)}}_{\geq 0}
=
E_{(\Upsilon, 1)}
\Big)
\Rightarrow
\Big(
A_{(\Upsilon, \varphi)} \leq E_{(\Upsilon, 1)}
\Big)
\Rightarrow
\boxed{
\Big(
A_{(\Phi, \Phi')} \leq E_{(\Upsilon, 1)}
\Big)
}
\bigg)
\land
\bigg(
\Big(
\underbrace{A_{(1, \Upsilon')}}_{\geq 0} + \underbrace{A_{(2, \Upsilon')}}_{\geq 0} + \dots + \boxed{\underbrace{A_{(\Phi, \Phi')}}_{\geq 0}} + \dots + \underbrace{A_{(i, \Upsilon')}}_{\geq 0}
=
R_{(1, \Upsilon')}
\Big)
\Rightarrow
\Big(
A_{(\varphi', \Upsilon')} \leq R_{(1, \Upsilon')}
\Big)
\Rightarrow
\boxed{
\Big(
A_{(\Phi, \Phi')} \leq R_{(1, \Upsilon')}
\Big)
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\forall \Upsilon \in \{1, \dots, i\}, \quad
\forall \Upsilon' \in \{1, \dots, j\}, \quad
\exists \Phi \in \{1, \dots, i\}, \quad
\exists \Phi' \in \{1, \dots, j\}, \quad
\underbrace{
\bigg(
\Big(
A_{(\Phi, \Phi')} \leq E_{(\Upsilon, 1)}
\Big)
\land
\Big(
A_{(\Phi, \Phi')} \leq R_{(1, \Upsilon')}
\Big)
\bigg)
}_{
x
\leq
min(\alpha, \beta)
\iff
\bigg(
\Big(
x \leq \alpha
\Big)
\land
\Big(
x \leq \beta
\Big)
\bigg)
\text{ form}
}
\iff
\bigg(
A_{(\Phi, \Phi')}
\leq
min\Big(
E_{(\Upsilon, 1)}, R_{(1, \Upsilon')}
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 14 :

- From part 14 to part 30, we show by reccurence several properties (see afterwards $\mathcal{P}(\eta)$ in part 21 for all the properties concerned)


- In this part, considering the matrix $A$ as a grid of “cells”, we start from the cell (= the “northwest” cell = the top-left cell of $A$) located at the intersection of the row $\lambda = 1$ (of $A$) and the 
  column $\Lambda = 1$ (of $A$), and we use the property found in part 13. Then, we examine what happens here and in the following parts

	- $E$ can be viewed as a column matrix and $R$ as a row matrix, since visually the flow matrix $A$ can be in the center, with $E$ to its left and $R$ at the top of $A$ (see the diagrams)

	- For $A_{(1, 1)}$, since there is an unique combination of arguments for the $min$ function, we can generalize it into a general pair $(\alpha_{(1)}, \beta_{(1)})$ 




- (French) Explications pour $i_{(\eta \ \in \ \mathbb{N}_{\geq 1})}$ et $j_{(\eta \ \in \ \mathbb{N}_{\geq 1})}$ :

	
	- Dans le texte qui suit, les termes "ligne(s)" et "colonne(s)" font référence à "ligne(s) de la matrice de flux $A$" et à "colonne(s) de la matrice de flux $A$" :
	
		
		- Si la "quantité utilisable" de "l'émetteur après la ${\iota}_{(1)}$-ième mise à jour" (= émetteur actuel) vaut 0, alors cela signifie qu'on ne peut plus émettre de "quantité utilisable" depuis cet 
		  émetteur vers les colonnes suivantes (colonnes suivantes étant à droite, comme le parcours a commencé à 1,1) correspondant aux "récepteurs après la $({\iota}_{(2)} + 1)$-ième mise à jour" 
		  (= récepteurs suivants) (cf. voir récurrence).
		  On passe donc à la ligne suivante (lignes suivantes étant en bas, comme le parcours a commencé à 1,1) pour utiliser la "quantité utilisable" de 
		  "l'émetteur après la $({\iota}_{(1)} + 1)$-ième mise à jour" (= émetteur suivant) correspondant à cette ligne suivante. 
		  Ce passage à la ligne suivante est représenté par $i_{(\eta \ \in \ \mathbb{N}_{\geq 1})} = 1$. Qu'il y ait un passage à la ligne suivante ou non, pour des raisons de généralisation, $i_{(\eta \ \in \ \mathbb{N}_{\geq 1})}$ sera quoi qu'il advienne 
		  ajouté (même s'il vaut 0) à la valeur actuelle de l'indice ligne (pour $A$ et l'émetteur suivant)
		
		
		- Si le "besoin" du "récepteur après la ${\iota}_{(2)}$-ième mise à jour" (= récepteur actuel) vaut 0, alors cela signifie que ce récepteur a reçu tout ce qu'il demandait. 
		  Ce n'est donc plus pertinent de rester sur la même colonne correspondant à ce récepteur, car le récepteur ne recevra plus de "quantité utilisable". 
		  On se déplace donc vers la colonne suivante (colonnes suivantes étant à droite, comme le parcours a commencé à 1,1) pour émettre vers le récepteur (= récepteur suivant) 
		  correspondant à cette colonne suivante (qui en a besoin)
		  Ce passage à la colonne suivante est représenté par $j_{(\eta \ \in \ \mathbb{N}_{\geq 1})} = 1$. Qu'il y ait un passage à la colonne suivante ou non, pour des raisons de généralisation, $j_{(\eta \ \in \ \mathbb{N}_{\geq 1})}$ sera quoi qu'il 
		  advienne ajouté (même s'il vaut 0) à la valeur actuelle de l'indice colonne (pour $A$ et le récepteur suivant)




- (French) Explications pour $min(1, i)$ et $min(1, j)$ :

	- Pour des raisons de généralisation dans la récurrence, on peut supposer que la comparaison entre $e_{(1 \leq \lambda \leq i)}$ and $r_{(1 \leq \Lambda \leq j)}$ (pour obtenir la valeur minimale pour la matrice $A$) peut être 
	  effectuée sur toute la "longueur" de $E$ (la "longueur" est $i$), ou sur toute la "longueur" de $R$ (la "longueur" est $j$). Alors :
	  
		- Cela signifie que $e_{(1 \leq \lambda \leq i)}$ et $r_{(1 \leq \Lambda \leq j)}$ peuvent changer de valeur simultanément (par rapport à leurs valeurs précédentes dans l’algorithme) au maximum soit $i$ fois (car c'est  
		  sur toute la "longueur" de $E$), soit (= ici, pas les deux) $j$ fois (car c'est sur toute la "longueur" de $R$). 
          En effet, pour chaque comparaison effectuée entre $e_{(1 \leq \lambda \leq i)}$ et $r_{(1 \leq \Lambda \leq j)}$, on soustrait simultanément une "portion" de $e_{(1 \leq \lambda \leq i)}$ et de $r_{(1 \leq \Lambda \leq j)}$ pour obtenir de nouvelles versions 
          de $e_{(1 \leq \lambda \leq i)}$ et $r_{(1 \leq \Lambda \leq j)}$ (leurs valeurs changent donc simultanément, ${\iota}_{(1)}$ et ${\iota}_{(2)}$ augmentent de 1, et $E$ et $R$ sont considérés comme mis à jour). 
		  Les changement de valeur simultanés de ${\iota}_{(1)}$ et ${\iota}_{(2)}$ peuvent être considérés comme une augmentation de 1 d’un même indice (qu'on appellera $\boxed{\eta}$). 
          Cet indice peut varier soit entre 0 (aucune mise à jour de ${\iota}_{(1)}$ et ${\iota}_{(2)}$) et $j$ (nombre maximal de fois possible), soit (= ici, pas les deux) entre 0 (aucune mise à jour de ${\iota}_{(1)}$ et ${\iota}_{(2)}$) et $i$ 
		  (nombre maximal de fois possible) (ces variations peuvent être définies dans l'ensemble $\boxed{S_{1}(i, j)}$)
    
        - Dans $S_{1}(i, j)$, pour cette récurrence spécifique, on choisit, toujours pour des raisons de généralisation dans la récurrence, de commencer à 1 et donc de décaler $\eta$ de -1 pour 
          commencer à 0


	- De plus, en partant de la définition de $S_{1}(i, j)$ :
	
		- 1. Si des variables s'appliquent sur un indice ligne (indice ligne de $A$ et de tout émetteur de $E$) et si le domaine de définition de ces variables a pour valeur maximale $\eta$ 
		  (pour des raisons de généralisation dans la récurrence), alors on peut avoir les cas suivants :
	
			- Le changement de valeur de $\eta$ se fait un nombre maximal de $i$ fois. Dans ce cas spécifique, le domaine de définition de ces variables est 
			  $\{\text{domain\_minimum}, \dots, \eta\} = \{\text{domain\_minimum}, \dots, i\}$ 
			
			- Le changement de valeur de $\eta$ se fait un nombre maximal de $j$ fois, et $j$ est plus grand que $i$, et $\eta$ peut être supérieur à $i$. 
			  Dans ce cas spécifique, le domaine de définition de ces variables a besoin de ne pas dépasser $i$ (car on est sur l'indice ligne de $A$ et de tout émetteur de $E$ et cet indice 
			  vaut au maximum $i$). 
			  Le domaine de définition de ces variables est $\{\text{domain\_minimum}, \dots, i\}$. De plus, ici $\{\text{domain\_minimum}, \dots, \eta\} \neq \{\text{domain\_minimum}, \dots, i\} \because \eta > i$ 
	
			Pour couvrir tous ces cas simultanément, on peut utiliser la fonction $min$ et définir un unique domaine de définition de ces variables pour tous ces cas. 
			Ce domaine de définition est $\{\text{domain\_minimum}, \dots, min(\eta, i)\}$ 
	
	
		- 2. Si des variables s'appliquent sur un indice colonne (indice colonne de $A$ et de tout récepteur de $R$) et si le domaine de définition de ces variables a pour valeur maximale $\eta$ 
		  (pour des raisons de généralisation dans la récurrence), alors on peut avoir les cas suivants :
			
			- Le changement de valeur de $\eta$ se fait un nombre maximal de $j$ fois. Dans ce cas spécifique, le domaine de définition de ces variables est 
			  $\{\text{domain\_minimum}, \dots, \eta\} = \{\text{domain\_minimum}, \dots, j\}$ 
			
			- Le changement de valeur de $\eta$ se fait un nombre maximal de $i$ fois, et $i$ est plus grand que $j$, et $\eta$ peut être supérieur à $j$. 
			  Dans ce cas spécifique, le domaine de définition de ces variables a besoin de ne pas dépasser $j$ (car on est sur l'indice colonne de $A$ et de tout récepteur de $R$ et cet indice 
			  vaut au maximum $j$). 
			  Le domaine de définition de ces variables est $\{\text{domain\_minimum}, \dots, j\}$. De plus, ici $\{\text{domain\_minimum}, \dots, \eta\} \neq \{\text{domain\_minimum}, \dots, j\} \because \eta > j$ 
	
			Pour couvrir tous ces cas simultanément, on peut utiliser la fonction $min$ et définir un unique domaine de définition de ces variables pour tous ces cas. 
			Ce domaine de définition est $\{\text{domain\_minimum}, \dots, min(\eta, j)\}$ 




- $\Big(i_{(\gamma_{(k)})} = 1\Big)\Rightarrow\Big(E_{{(\overset{\gamma_{(k)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}}=0\Big)$ : if several jumps to the next row are made directly and consecutively in matrix $A$ (i.e. if we have $i_{(1)} = 1, \ i_{(2)} = 1, \dots, \ i_{(\gamma_{(k)})} = 1$), then 
  we have $E_{(1,1)} = 0, E_{(2,1)} = 0, \dots, E_{(\alpha_{(k)}, 1)} = 0$ directly and consecutively

- $\Big(j_{(\gamma'_{(k)})} = 1\Big)\Rightarrow\Big(R_{{(1,\overset{\gamma'_{(k)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = k)}}=0\Big)$ : if several jumps to the next column are made directly and consecutively in matrix $A$ (i.e. if we have $j_{(1)} = 1, \ j_{(2)} = 1, \dots, \ j_{(\gamma_{(k)})} = 1$), then 
  we have $R_{(1,1)} = 0, R_{(1,2)} = 0, \dots, R_{(1, \beta_{(k)})} = 0$ directly and consecutively

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\eta_{0} := 1
\Bigg)
\\[1em]
\Rightarrow
\left(
\left(
A_{(1,1)}
:=
\begin{cases}
\bigg(
E_{{(1,1)}_{({\iota}_{(1)} = 0)}} \leq R_{{(1,1)}_{({\iota}_{(2)} = 0)}}
\bigg)
\Rightarrow
\bigg(
A_{(1,1)}
=
E_{{(1,1)}_{({\iota}_{(1)} = 0)}}
\bigg)
\\[1em]
\bigg(
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 0)}} > R_{{(1,1)}_{({\iota}_{(2)} = 0)}}
\Big)
\iff
\Big(
R_{{(1,1)}_{({\iota}_{(2)} = 0)}} < E_{{(1,1)}_{({\iota}_{(1)} = 0)}}
\Big)
\bigg)
\Rightarrow
\bigg(
A_{(1,1)}
=
R_{{(1,1)}_{({\iota}_{(2)} = 0)}}
\bigg)
\end{cases}
\right)
\Rightarrow
\boxed{
\left(
A_{(1,1)}
=
min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}})
=
\begin{cases}
\bigg(
E_{{(1,1)}_{({\iota}_{(1)} = 0)}} \leq R_{{(1,1)}_{({\iota}_{(2)} = 0)}}
\bigg)
\Rightarrow
\bigg(
A_{(1,1)}
=
min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}}) = E_{{(1,1)}_{({\iota}_{(1)} = 0)}}
\bigg)
\\[1em]
\bigg(
R_{{(1,1)}_{({\iota}_{(2)} = 0)}} < E_{{(1,1)}_{({\iota}_{(1)} = 0)}}
\bigg)
\Rightarrow
\bigg(
A_{(1,1)}
=
min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}}) = R_{{(1,1)}_{({\iota}_{(2)} = 0)}}
\bigg)
\end{cases}
\right)
}
\right)
\\[1em]
\Rightarrow
\left(
\left(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
:=
\begin{cases}
\bigg(
\boxed{
A_{(1,1)}
=
E_{{(1,1)}_{({\iota}_{(1)} = 0)}}
=
e_{(1)}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
E_{{(1,1)}_{({\iota}_{(1)} = 0)}} - A_{(1,1)}
}
=
e_{(1)} - A_{(1,1)}
=
e_{(1)} - e_{(1)}
=
\boxed{
0
}
\bigg)
\\[1em]
\bigg(
\boxed{
A_{(1,1)}
=
R_{{(1,1)}_{({\iota}_{(2)} = 0)}}
=
r_{(1)}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
}
=
E_{{(1,1)}_{({\iota}_{(1)} = 0)}} - A_{(1,1)}
=
e_{(1)} - A_{(1,1)}
=
\boxed{
e_{(1)} - r_{(1)}
}
\bigg)
\end{cases}
\right)
\land
\left(
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
:=
\begin{cases}
\bigg(
\boxed{
A_{(1,1)}
=
E_{{(1,1)}_{({\iota}_{(1)} = 0)}}
=
e_{(1)}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
}
=
R_{{(1,1)}_{({\iota}_{(2)} = 0)}} - A_{(1,1)}
=
r_{(1)} - A_{(1,1)}
=
\boxed{
r_{(1)} - e_{(1)}
}
\bigg)
\\[1em]
\bigg(
\boxed{
A_{(1,1)}
=
R_{{(1,1)}_{({\iota}_{(2)} = 0)}}
=
r_{(1)}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
R_{{(1,1)}_{({\iota}_{(2)} = 0)}} - A_{(1,1)}
}
=
r_{(1)} - A_{(1,1)}
=
r_{(1)} - r_{(1)}
=
\boxed{
0
}
\bigg)
\end{cases}
\right)
\right)
\\[1em]
\Rightarrow
\left(
\left(
\boxed{
i_{(1)}
}
:=
\begin{cases}
\bigg(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(1)}
=
1
\bigg)
\\[1em]
\bigg(
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(1)}
=
0
\bigg)
\end{cases}
\right)
\ \land \
\left(
\boxed{
j_{(1)}
}
:=
\begin{cases}
\bigg(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(1)}
=
0
\bigg)
\\[1em]
\bigg(
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(1)}
=
1
\bigg)
\end{cases}
\right)
\right)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\forall \gamma_{(1)} \in \{1, \dots, min(1,i)\}, \quad
\Big(
i_{(\gamma_{(1)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(1)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 1)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma'_{(1)} \in \{1, \dots, min(1,j)\}, \quad
\Big(
j_{(\gamma'_{(1)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(1)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\exists \alpha_{(1)} \in \{1, \dots, min(1,i)\}, \quad
\exists \beta_{(1)} \in \{1, \dots, min(1,j)\}, \quad
\bigg(
A_{(\alpha_{(1)}, \beta_{(1)})}
=
min\Big(
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 0)}}, 
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 0)}}
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 1)}}
=
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 0)}} - A_{(\alpha_{(1)}, \beta_{(1)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 1)}}
=
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 0)}} - A_{(\alpha_{(1)}, \beta_{(1)})}
=
0
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Diagram 1 of part 14 :

- Case 1 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\Big(
A_{(1,1)} = min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}}) = E_{{(1,1)}_{({\iota}_{(1)} = 0)}} = e_{(1)}
\Big)
\\
\hline
\begin{array}{l}
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{e_{(1)}} & \boxed{0} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} - A_{(1,1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{e_{(1)} - A_{(1,1)}} & \boxed{e_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} - e_{(1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{0} & \boxed{e_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

- Case 2 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\Big(
A_{(1,1)} = min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}}) = R_{{(1,1)}_{({\iota}_{(2)} = 0)}} = r_{(1)}
\Big)
\\
\hline
\begin{array}{l}
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{r_{(1)}} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} & \boxed{0} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{r_{(1)} - A_{(1,1)}} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} - A_{(1,1)} & \boxed{r_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{0} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} - r_{(1)} & \boxed{r_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Part 15 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\boxed{
A_{(1 + i_{(1)},1 + j_{(1)})}
}
:=
\begin{cases}
\left(
\boxed{
\bigg(
\Big(
A_{(1,1)}
=
e_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
0
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
r_{(1)} - \underbrace{e_{(1)}}_{\boxed{A_{(1,1)}}}
\Big)
\land
\Big(
i_{(1)}
=
1
\land
j_{(1)}
=
0
\Big)
\bigg)
}
\Rightarrow
\left(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
A_{(2,1)}
}
=
\begin{cases}
\bigg(
\Big(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}} \leq R_{{(1,1 + j_{(1)}}_{({\iota}_{(2)} = 1)})}
\Big)
\iff
\boxed{
\Big(
E_{{(2,1)}_{({\iota}_{(1)} = 1)}} \leq R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
\Big)
}
\bigg)
\Rightarrow
\bigg(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
A_{(2,1)}
=
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}
=
E_{{(2,1)}_{({\iota}_{(1)} = 1)}}
}
\bigg)
\\[1em]
\bigg(
\Big(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}} > R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}
\Big)
\iff
\Big(
E_{{(2,1)}_{({\iota}_{(1)} = 1)}} > R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
\Big)
\iff
\boxed{
\Big(
R_{{(1,1)}_{({\iota}_{(2)} = 1)}} < E_{{(2,1)}_{({\iota}_{(1)} = 1)}}
\Big)
}
\bigg)
\Rightarrow
\bigg(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
A_{(2,1)}
=
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}
=
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\end{cases}
\right)
\right)
\\[1em]
\left(
\boxed{
\bigg(
\Big(
A_{(1,1)}
=
r_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
e_{(1)} - \underbrace{r_{(1)}}_{\boxed{A_{(1,1)}}}
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\land
\Big(
i_{(1)}
=
0
\land
j_{(1)}
=
1
\Big)
\bigg)
}
\Rightarrow
\left(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
A_{(1, 2)}
}
=
\begin{cases}
\bigg(
\Big(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}} \leq R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}
\Big)
\iff
\boxed{
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}} \leq R_{{(1,2)}_{({\iota}_{(2)} = 1)}}
\Big)
}
\bigg)
\Rightarrow
\bigg(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
A_{(1,2)}
=
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}
=
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
}
\bigg)
\\[1em]
\bigg(
\Big(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}} > R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}
\Big)
\iff
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}} > R_{{(1,2)}_{({\iota}_{(2)} = 1)}}
\Big)
\iff
\boxed{
\Big(
R_{{(1,2)}_{({\iota}_{(2)} = 1)}} < E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
\Big)
}
\bigg)
\Rightarrow
\bigg(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
A_{(1,2)}
=
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}
=
R_{{(1,2)}_{({\iota}_{(2)} = 1)}}
}
\bigg)
\end{cases}
\right)
\right)
\end{cases}
\right)
\end{cases}
\end{array}
$$

Part 16 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\begin{cases}
\left(
\bigg(
\Big(
A_{(1,1)}
=
e_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
0
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
r_{(1)} - \underbrace{e_{(1)}}_{A_{(1,1)}}
\Big)
\land
\Big(
i_{(1)}
=
1
\land
j_{(1)}
=
0
\Big)
\bigg)
\Rightarrow
\left(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
A_{(2,1)}
}
=
min\Big(E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}\Big)
=
\boxed{
min\Big(E_{{(2,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1)}_{({\iota}_{(2)} = 1)}}\Big)
=
\begin{cases}
\bigg(
E_{{(2,1)}_{({\iota}_{(1)} = 1)}} \leq R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
\bigg)
\Rightarrow
\bigg(
A_{(2,1)}
=
min\Big(E_{{(2,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1)}_{({\iota}_{(2)} = 1)}}\Big)
=
E_{{(2,1)}_{({\iota}_{(1)} = 1)}}
\bigg)
\\[1em]
\bigg(
R_{{(1,1)}_{({\iota}_{(2)} = 1)}} < E_{{(2,1)}_{({\iota}_{(1)} = 1)}}
\bigg)
\Rightarrow
\bigg(
A_{(2,1)}
=
min\Big(E_{{(2,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1)}_{({\iota}_{(2)} = 1)}}\Big)
=
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
\bigg)
\end{cases}
}
\right)
\right)
\\[1em]
\left(
\bigg(
\Big(
A_{(1,1)}
=
r_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
e_{(1)} - \underbrace{r_{(1)}}_{A_{(1,1)}}
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\land
\Big(
i_{(1)}
=
0
\land
j_{(1)}
=
1
\Big)
\bigg)
\Rightarrow
\left(
A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
A_{(1, 2)}
}
=
min\Big(E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}\Big)
=
\boxed{
min\Big(E_{{(1,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,2)}_{({\iota}_{(2)} = 1)}}\Big)
=
\begin{cases}
\bigg(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}} \leq R_{{(1,2)}_{({\iota}_{(2)} = 1)}}
\bigg)
\Rightarrow
\bigg(
A_{(1,2)}
=
min\Big(E_{{(1,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,2)}_{({\iota}_{(2)} = 1)}}\Big)
=
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
\bigg)
\\[1em]
\bigg(
R_{{(1,2)}_{({\iota}_{(2)} = 1)}} < E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
\bigg)
\Rightarrow
\bigg(
A_{(1,2)}
=
min\Big(E_{{(1,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,2)}_{({\iota}_{(2)} = 1)}}\Big)
=
R_{{(1,2)}_{({\iota}_{(2)} = 1)}}
\bigg)
\end{cases}
}
\right)
\right)
\end{cases}
\right)
\\[1em]
\Rightarrow
\left(
\boxed{
A_{(1 + i_{(1)}, 1 + j_{(1)})}
}
=
\begin{cases}
\boxed{
\bigg(
A_{(1, 1)}
=
e_{(1)}
\bigg)
}
\Rightarrow
\bigg(
A_{(1 + i_{(1)}, 1 + j_{(1)})}
=
\boxed{
A_{(2, 1)}
}
=
min\Big(E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}\Big)
=
\boxed{
min\Big(E_{{(2,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1)}_{({\iota}_{(2)} = 1)}}\Big)
}
\bigg)
\\[1em]
\boxed{
\bigg(
A_{(1, 1)}
=
r_{(1)}
\bigg)
}
\Rightarrow
\bigg(
A_{(1 + i_{(1)}, 1 + j_{(1)})}
=
\boxed{
A_{(1, 2)}
}
=
min\Big(E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}\Big)
=
\boxed{
min\Big(E_{{(1,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,2)}_{({\iota}_{(2)} = 1)}}\Big)
}
\bigg)
\end{cases}
\right)
\end{cases}
\end{array}
$$

Part 17 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\boxed{
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 2)}}
}
:=
\begin{cases}
\bigg(
\Big(
A_{(1,1)}
=
e_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
0
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
r_{(1)} - e_{(1)}
\Big)
\land
\Big(
\underline{
i_{(1)}
=
1
}
\land
j_{(1)}
=
0
\Big)
\land
\Big(
\boxed{
A_{(2,1)}
=
E_{{(2,1)}_{({\iota}_{(1)} = 1)}}
=
e_{(2)}
}
\Big)
\bigg)
\Rightarrow
\bigg(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 2)}}
=
\boxed{
E_{{(2,1)}_{({\iota}_{(1)} = 2)}}
}
=
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}} - A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
E_{{(2,1)}_{({\iota}_{(1)} = 1)}} - A_{(2,1)}
}
=
e_{(2)} - A_{(2,1)}
=
e_{(2)} - e_{(2)}
=
\boxed{
0
}
\bigg)
\\[1em]
\bigg(
\Big(
A_{(1,1)}
=
e_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
0
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
r_{(1)} - e_{(1)}
\Big)
\land
\Big(
\underline{
i_{(1)}
=
1
}
\land
j_{(1)}
=
0
\Big)
\land
\Big(
\boxed{
A_{(2,1)}
=
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
}
=
r_{(1)} - e_{(1)}
\Big)
\bigg)
\Rightarrow
\bigg(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 2)}}
=
\boxed{
E_{{(2,1)}_{({\iota}_{(1)} = 2)}}
}
=
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}} - A_{(1 + i_{(1)},1 + j_{(1)})}
=
E_{{(2,1)}_{({\iota}_{(1)} = 1)}} - A_{(2,1)}
=
e_{(2)} - A_{(2,1)}
=
e_{(2)} - (r_{(1)} - e_{(1)})
=
e_{(1)} + e_{(2)} - r_{(1)}
\bigg)
\\[1em]
\bigg(
\boxed{
\Big(
A_{(1,1)}
=
r_{(1)}
\Big)
}
\land
\Big(
\boxed{
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
e_{(1)} - r_{(1)}
}
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\land
\Big(
\underline{
i_{(1)}
=
0
}
\land
j_{(1)}
=
1
\Big)
\land
\Big(
\boxed{
A_{(1,2)}
=
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
}
=
e_{(1)} - r_{(1)}
\Big)
\bigg)
\Rightarrow
\bigg(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 2)}}
=
\boxed{
E_{{(1, 1)}_{({\iota}_{(1)} = 2)}}
}
=
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}} - A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
E_{{(1, 1)}_{({\iota}_{(1)} = 1)}} - A_{(1,2)}
}
=
e_{(1)} - r_{(1)} - (e_{(1)} - r_{(1)})
=
\boxed{
0
}
\bigg)
\\[1em]
\bigg(
\Big(
A_{(1,1)}
=
r_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
e_{(1)} - r_{(1)}
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\land
\Big(
\underline{
i_{(1)}
=
0
}
\land
j_{(1)}
=
1
\Big)
\land
\Big(
\boxed{
A_{(1,2)}
=
R_{{(1,2)}_{({\iota}_{(2)} = 1)}}
}
=
r_{(2)}
\Big)
\bigg)
\Rightarrow
\bigg(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 2)}}
=
\boxed{
E_{{(1,1)}_{({\iota}_{(1)} = 2)}}
}
=
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}} - A_{(1 + i_{(1)},1 + j_{(1)})}
=
E_{{(1,1)}_{({\iota}_{(1)} = 1)}} - A_{(1,2)}
=
e_{(1)} - r_{(1)} - r_{(2)}
\bigg)
\end{cases}
\right)
\end{cases}
\end{array}
$$

Part 18 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\boxed{
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 2)}}
}
:=
\begin{cases}
\bigg(
\Big(
A_{(1,1)}
=
e_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
0
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
r_{(1)} - e_{(1)}
\Big)
\land
\Big(
i_{(1)}
=
1
\land
\underline{
j_{(1)}
=
0
}
\Big)
\land
\Big(
\boxed{
A_{(2,1)}
=
E_{{(2,1)}_{({\iota}_{(1)} = 1)}}
}
=
e_{(2)}
\Big)
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 2)}}
=
\boxed{
R_{{(1,1)}_{({\iota}_{(2)} = 2)}}
}
=
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}} - A_{(1 + i_{(1)},1 + j_{(1)})}
=
R_{{(1,1)}_{({\iota}_{(2)} = 1)}} - A_{(2,1)}
=
r_{(1)} - e_{(1)} - A_{(2,1)}
=
r_{(1)} - e_{(1)} - e_{(2)}
\bigg)
\\[1em]
\bigg(
\boxed{
\Big(
A_{(1,1)}
=
e_{(1)}
\Big)
}
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
0
\land
\boxed{
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
r_{(1)} - e_{(1)}
}
\Big)
\land
\Big(
i_{(1)}
=
1
\land
\underline{
j_{(1)}
=
0
}
\Big)
\land
\Big(
\boxed{
A_{(2,1)}
=
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
}
=
r_{(1)} - e_{(1)}
\Big)
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 2)}}
=
\boxed{
R_{{(1,1)}_{({\iota}_{(2)} = 2)}}
}
=
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}} - A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
R_{{(1,1)}_{({\iota}_{(2)} = 1)}} - A_{(2,1)}
}
=
r_{(1)} - e_{(1)} - A_{(2,1)}
=
r_{(1)} - e_{(1)} - (r_{(1)} - e_{(1)})
=
\boxed{
0
}
\bigg)
\\[1em]
\bigg(
\Big(
A_{(1,1)}
=
r_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
e_{(1)} - r_{(1)}
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\land
\Big(
i_{(1)}
=
0
\land
\underline{
j_{(1)}
=
1
}
\Big)
\land
\Big(
\boxed{
A_{(1,2)}
=
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
}
=
e_{(1)} - r_{(1)}
\Big)
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 2)}}
=
\boxed{
R_{{(1, 2)}_{({\iota}_{(2)} = 2)}}
}
=
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}} - A_{(1 + i_{(1)},1 + j_{(1)})}
=
R_{{(1, 2)}_{({\iota}_{(2)} = 1)}} - A_{(1,2)}
=
r_{(2)} - (e_{(1)} - r_{(1)})
=
r_{(1)} + r_{(2)} - e_{(1)}
\bigg)
\\[1em]
\bigg(
\Big(
A_{(1,1)}
=
r_{(1)}
\Big)
\land
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = 1)}}
=
e_{(1)} - r_{(1)}
\land
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\land
\Big(
i_{(1)}
=
0
\land
\underline{
j_{(1)}
=
1
}
\Big)
\land
\Big(
\boxed{
A_{(1,2)}
=
R_{{(1,2)}_{({\iota}_{(2)} = 1)}}
=
r_{(2)}
}
\Big)
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 2)}}
=
\boxed{
R_{{(1,2)}_{({\iota}_{(2)} = 2)}}
}
=
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}} - A_{(1 + i_{(1)},1 + j_{(1)})}
=
\boxed{
R_{{(1,2)}_{({\iota}_{(2)} = 1)}} - A_{(1,2)}
}
=
r_{(2)} - r_{(2)}
=
\boxed{
0
}
\bigg)
\end{cases}
\right)
\end{cases}
\end{array}
$$

Part 19 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\left(
i_{(2)}
:=
\begin{cases}
\boxed{
\bigg(
E_{{(2, 1)}_{({\iota}_{(1)} = 2)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(2)}
=
1
\bigg)
}
\\[1em]
\bigg(
R_{{(1, 1)}_{({\iota}_{(2)} = 2)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(2)}
=
0
\bigg)
\\[1em]
\bigg(
E_{{(1, 1)}_{({\iota}_{(1)} = 2)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(2)}
=
1
\bigg)
\\[1em]
\bigg(
R_{{(1, 2)}_{({\iota}_{(2)} = 2)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(2)}
=
0
\bigg)
\end{cases}
\right)
\ \land \
\left(
j_{(2)}
:=
\begin{cases}
\bigg(
E_{{(2, 1)}_{({\iota}_{(1)} = 2)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(2)}
=
0
\bigg)
\\[1em]
\bigg(
R_{{(1, 1)}_{({\iota}_{(2)} = 2)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(2)}
=
1
\bigg)
\\[1em]
\bigg(
E_{{(1, 1)}_{({\iota}_{(1)} = 2)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(2)}
=
0
\bigg)
\\[1em]
\bigg(
R_{{(1, 2)}_{({\iota}_{(2)} = 2)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(2)}
=
1
\bigg)
\end{cases}
\right)
\right)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\forall \gamma_{(2)} \in \{1, \dots, min(2,i)\}, \quad
\Big(
i_{(\gamma_{(2)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(2)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 2)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma'_{(2)} \in \{1, \dots, min(2,j)\}, \quad
\Big(
j_{(\gamma'_{(2)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(2)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = 2)}}
=
0
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 20 :

- Since there are several possible combinations of arguments for the $min$ function, we generalize all these combinations (we "group them together") into a general pair $(\alpha_{(2)}, \beta_{(2)})$ 
  for $A_{(\alpha_{(2)}, \beta_{(2)})}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg[
\ \
\Bigg(
\bigg(
A_{(1, 1)}
=
e_{(1)}
\bigg)
\Rightarrow
\bigg(
A_{(2, 1)}
=
min\Big(E_{{(2,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1)}_{({\iota}_{(2)} = 1)}}\Big)
=
min\Big(E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}\Big)
=
E_{{(2,1)}_{({\iota}_{(1)} = 1)}}
=
e_{(2)}
\bigg)
\Rightarrow
\bigg(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 2)}}
=
\boxed{
E_{{(2,1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(2,1)}_{({\iota}_{(1)} = 1)}} - A_{(2, 1)}
}
=
e_{(2)} - A_{(2, 1)}
=
\boxed{
0
}
\bigg)
\Bigg)
\\[1em]
\quad \quad
\oplus
\Bigg(
\bigg(
A_{(1, 1)}
=
e_{(1)}
\bigg)
\Rightarrow
\bigg(
A_{(2, 1)}
=
min\Big(E_{{(2,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1)}_{({\iota}_{(2)} = 1)}}\Big)
=
min\Big(E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}\Big)
=
R_{{(1,1)}_{({\iota}_{(2)} = 1)}}
=
r_{(1)} - e_{(1)}
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 2)}}
=
R_{{(1,1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = 2)}}
=
\boxed{
R_{{(1,1)}_{({\iota}_{(2)} = 2)}}
=
R_{{(1,1)}_{({\iota}_{(2)} = 1)}} - A_{(2, 1)}
}
=
r_{(1)} - e_{(1)} - A_{(2, 1)}
=
r_{(1)} - A_{(1, 1)} - A_{(2, 1)}
=
\boxed{
0
}
\bigg)
\Bigg)
\\[1em]
\quad \quad
\oplus
\Bigg(
\bigg(
A_{(1, 1)}
=
r_{(1)}
\bigg)
\Rightarrow
\bigg(
A_{(1, 2)}
=
min\Big(E_{{(1,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,2)}_{({\iota}_{(2)} = 1)}}\Big)
=
min\Big(E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}\Big)
=
E_{{(1, 1)}_{({\iota}_{(1)} = 1)}}
=
e_{(1)} - r_{(1)}
\bigg)
\Rightarrow
\bigg(
E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 2)}}
=
\boxed{
E_{{(1, 1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(1, 1)}_{({\iota}_{(1)} = 1)}} - A_{(1, 2)}
}
=
e_{(1)} - r_{(1)} - A_{(1, 2)}
=
e_{(1)} - A_{(1, 1)} - A_{(1, 2)}
=
\boxed{
0
}
\bigg)
\Bigg)
\\[1em]
\quad \quad
\oplus
\Bigg(
\bigg(
A_{(1, 1)}
=
r_{(1)}
\bigg)
\Rightarrow
\bigg(
A_{(1, 2)}
=
min\Big(E_{{(1,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,2)}_{({\iota}_{(2)} = 1)}}\Big)
=
min\Big(E_{{(1 + i_{(1)},1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 1)}}\Big)
=
R_{{(1, 2)}_{({\iota}_{(2)} = 1)}}
=
r_{(2)}
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + j_{(1)})}_{({\iota}_{(2)} = 2)}}
=
R_{{(1,1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = 2)}}
=
\boxed{
R_{{(1, 2)}_{({\iota}_{(2)} = 2)}}
=
R_{{(1, 2)}_{({\iota}_{(2)} = 1)}} - A_{(1, 2)}
}
=
r_{(2)} - A_{(1, 2)}
=
\boxed{
0
}
\bigg)
\Bigg)
\ \
\Bigg]
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\exists \alpha_{(2)} \in \{1, \dots, min(2,i)\}, \quad
\exists \beta_{(2)} \in \{1, \dots, min(2,j)\}, \quad
\bigg(
A_{(\alpha_{(2)}, \beta_{(2)})}
=
A_{(1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
min\Big(
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 1)}}, 
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 1)}}
\Big)
=
min\Big(
E_{{(1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 1)}}, 
R_{{(1,1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = 1)}}
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 1)}} - A_{(\alpha_{(2)}, \beta_{(2)})}
=
E_{{(1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 1)}} - A_{(\alpha_{(2)}, \beta_{(2)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 2)}}
=
R_{{(1,1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = 2)}}
=
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 1)}} - A_{(\alpha_{(2)}, \beta_{(2)})}
=
R_{{(1,1 + \overset{2 - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = 1)}} - A_{(\alpha_{(2)}, \beta_{(2)})}
=
0
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Diagram 1 of part 20 :

- Case 1 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\Big(
A_{(1,1)} = min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}}) = E_{{(1,1)}_{({\iota}_{(1)} = 0)}} = e_{(1)}
\Big)
\land
\Big(
A_{(2,1)} = min(E_{{(2,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1)}_{({\iota}_{(2)} = 1)}}) = E_{{(2,1)}_{({\iota}_{(1)} = 1)}} = e_{(2)}
\Big)
\\
\hline
\begin{array}{l}
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{e_{(1)}} & \boxed{0} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} - A_{(1,1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{e_{(1)} - A_{(1,1)}} & \boxed{e_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} - e_{(1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{0} & \boxed{e_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\\[1em]
\begin{array}{l}
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} - e_{(1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
0 & e_{(1)} & 0 & \dots & 0
\\
\boxed{e_{(2)}} & \boxed{0} & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& (r_{(1)} - e_{(1)}) - A_{(2,1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
0 & e_{(1)} & 0 & \dots & 0
\\
\boxed{e_{(2)} - A_{(2,1)}} & \boxed{e_{(2)}} & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& (r_{(1)} - e_{(1)}) - e_{(2)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
0 & e_{(1)} & 0 & \dots & 0
\\
\boxed{0} & \boxed{e_{(2)}} & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

- Case 2 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\Big(
A_{(1,1)} = min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}}) = E_{{(1,1)}_{({\iota}_{(1)} = 0)}} = e_{(1)}
\Big)
\land
\Big(
A_{(2,1)} = min(E_{{(2,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,1)}_{({\iota}_{(2)} = 1)}}) = R_{{(1,1)}_{({\iota}_{(2)} = 1)}} = r_{(1)} - e_{(1)}
\Big)
\\
\hline
\begin{array}{l}
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{e_{(1)}} & \boxed{0} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} - A_{(1,1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{e_{(1)} - A_{(1,1)}} & \boxed{e_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& r_{(1)} - e_{(1)} & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{0} & \boxed{e_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\\[1em]
\begin{array}{l}
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{r_{(1)} - e_{(1)}} & r_{(2)} & \dots & r_{(j)}
\\
\hline
0 & e_{(1)} & 0 & \dots & 0
\\
e_{(2)} & \boxed{0} & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{(r_{(1)} - e_{(1)}) - A_{(2,1)}} & r_{(2)} & \dots & r_{(j)}
\\
\hline
0 & e_{(1)} & 0 & \dots & 0
\\
e_{(2)} - A_{(2,1)} & \boxed{e_{(2)}} & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{0} & r_{(2)} & \dots & r_{(j)}
\\
\hline
0 & e_{(1)} & 0 & \dots & 0
\\
e_{2} - (r_{(1)} - e_{(1)}) & \boxed{e_{(2)}} & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

- Case 3 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\Big(
A_{(1,1)} = min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}}) = R_{{(1,1)}_{({\iota}_{(2)} = 0)}} = r_{(1)}
\Big)
\land
\Big(
A_{(1,2)} = min(E_{{(1,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,2)}_{({\iota}_{(2)} = 1)}}) = E_{{(1,1)}_{({\iota}_{(1)} = 1)}} = e_{(1)} - r_{(1)}
\Big)
\\
\hline
\begin{array}{l}
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{r_{(1)}} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} & \boxed{0} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{r_{(1)} - A_{(1,1)}} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} - A_{(1,1)} & \boxed{r_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{0} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} - r_{(1)} & \boxed{r_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\\[1em]
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& 0 & r_{(2)} & \dots & r_{(j)}
\\
\hline
\boxed{e_{(1)} - r_{(1)}} & r_{(1)} & \boxed{0} & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& 0 & r_{(2)} - A_{(1,2)} & \dots & r_{(j)}
\\
\hline
\boxed{e_{(1)} - r_{(1)} - A_{(1,2)}} & r_{(1)} & \boxed{r_{(2)}} & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& 0 & r_{(2)} - (e_{(1)} - r_{(1)}) & \dots & r_{(j)}
\\
\hline
\boxed{0} & r_{(1)} & \boxed{r_{(2)}} & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

- Case 4 :

$$
\begin{array}{l}
\begin{array}{|c|}
\hline
\Big(
A_{(1,1)} = min(E_{{(1,1)}_{({\iota}_{(1)} = 0)}}, R_{{(1,1)}_{({\iota}_{(2)} = 0)}}) = R_{{(1,1)}_{({\iota}_{(2)} = 0)}} = r_{(1)}
\Big)
\land
\Big(
A_{(1,2)} = min(E_{{(1,1)}_{({\iota}_{(1)} = 1)}}, R_{{(1,2)}_{({\iota}_{(2)} = 1)}}) = R_{{(1,2)}_{({\iota}_{(2)} = 1)}} = r_{(2)}
\Big)
\\
\hline
\begin{array}{l}
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{r_{(1)}} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} & \boxed{0} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{r_{(1)} - A_{(1,1)}} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} - A_{(1,1)} & \boxed{r_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& \boxed{0} & r_{(2)} & \dots & r_{(j)}
\\
\hline
e_{(1)} - r_{(1)} & \boxed{r_{(1)}} & 0 & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\\[1em]
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& 0 & \boxed{r_{(2)}} & \dots & r_{(j)}
\\
\hline
e_{(1)} - r_{(1)} & r_{(1)} & \boxed{0} & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& 0 & \boxed{r_{(2)} - A_{(1,2)}} & \dots & r_{(j)}
\\
\hline
e_{(1)} - r_{(1)} - A_{(1,2)} & r_{(1)} & \boxed{r_{(2)}} & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\quad
\quad
\begin{array}{|c|c|}
\hline
& \quad \quad \quad \text{Receivers}
\\
\text{Emitters}
&
\begin{array}{c|cccc}
& 0 & \boxed{0} & \dots & r_{(j)}
\\
\hline
e_{(1)} - r_{(1)} - r_{(2)} & r_{(1)} & \boxed{r_{(2)}} & \dots & 0
\\
e_{(2)} & 0 & 0 & \dots & 0
\\
\vdots & \vdots & \vdots & \ddots & \vdots
\\
e_{(i)} & 0 & 0 & \dots & 0
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
\\[1em]
\hline
\end{array}
\end{array}
$$

Part 21 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\left(
\ \
S_{1}(i, j)
:=
\begin{cases}
i < j
\Rightarrow
S_{1}(i, j)
=
\{1, \dots, j\}
\\[1em]
i \geq j
\Rightarrow
S_{1}(i, j)
=
\{1, \dots, i\}
\end{cases}
\ \
\right)
}
\end{cases}
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\mathcal{P}(\eta) :
\Bigg(
\bigg(
\Big(
\underline{1 \leq \eta \leq max(S_{1}(i, j))}
\Big)
\Rightarrow
\Big(
\exists \alpha_{(\eta)} \in \{1, \dots, min(\eta,i)\}, \quad
\exists \beta_{(\eta)} \in \{1, \dots, min(\eta,j)\}, \quad
\Big(
A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
A_{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
min\Big(
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta - 1)}}, 
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta - 1)}}
\Big)
=
min\Big(
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta - 1)}}, 
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta - 1)}}
\Big)
\Big)
\land
\Big(
\forall \gamma_{(\eta)} \in \{1, \dots, min(\eta,i)\}, \quad
\Big(
i_{(\gamma_{(\eta)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(\eta)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
0
\Big)
\Big)
\land
\Big(
\forall \gamma'_{(\eta)} \in \{1, \dots, min(\eta,j)\}, \quad
\Big(
j_{(\gamma'_{(\eta)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(\eta)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = \eta)}}
=
0
\Big)
\Big)
\land
\Big(
\Big(
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta)}}
=
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta)}}
=
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta)}}
=
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
0
\Big)
\Big)
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
\mathcal{P}(\eta_{0}) :
\Bigg(
\bigg(
\Big(
\exists \alpha_{(1)} \in \{1, \dots, min(1,i)\}, \quad
\exists \beta_{(1)} \in \{1, \dots, min(1,j)\}, \quad
\Big(
A_{(\alpha_{(1)}, \beta_{(1)})}
=
min\Big(
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 0)}}, 
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 0)}}
\Big)
\Big)
\land
\Big(
\forall \gamma_{(1)} \in \{1, \dots, min(1,i)\}, \quad
\Big(
i_{(\gamma_{(1)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(1)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 1)}}
=
0
\Big)
\Big)
\land
\Big(
\forall \gamma'_{(1)} \in \{1, \dots, min(1,j)\}, \quad
\Big(
j_{(\gamma'_{(1)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(1)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\Big)
\land
\Big(
\big(
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 1)}}
=
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 0)}} - A_{(\alpha_{(1)}, \beta_{(1)})}
=
0
\big)
\oplus
\big(
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 1)}}
=
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 0)}} - A_{(\alpha_{(1)}, \beta_{(1)})}
=
0
\big)
\Big)
\Big)
\bigg)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(1)} \in \{1, \dots, min(1,i)\}, \quad
\exists \beta_{(1)} \in \{1, \dots, min(1,j)\}, \quad
\boxed{
\bigg(
A_{(\alpha_{(1)}, \beta_{(1)})}
=
min\Big(
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 0)}}, 
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 0)}}
\Big)
\bigg)
\land
\bigg(
\forall \gamma_{(1)} \in \{1, \dots, min(1,i)\}, \quad
\Big(
i_{(\gamma_{(1)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(1)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 1)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma'_{(1)} \in \{1, \dots, min(1,j)\}, \quad
\Big(
j_{(\gamma'_{(1)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(1)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = 1)}}
=
0
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 1)}}
=
E_{{(\alpha_{(1)},1)}_{({\iota}_{(1)} = 0)}} - A_{(\alpha_{(1)}, \beta_{(1)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 1)}}
=
R_{{(1,\beta_{(1)})}_{({\iota}_{(2)} = 0)}} - A_{(\alpha_{(1)}, \beta_{(1)})}
=
0
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{P}(\eta_{0})
\Bigg)
}
\end{cases}
\end{array}
$$

Part 22 :

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
\exists \alpha_{(2)} \in \{1, \dots, min(2,i)\}, \quad
\exists \beta_{(2)} \in \{1, \dots, min(2,j)\}, \quad
\Big(
A_{(\alpha_{(2)}, \beta_{(2)})}
=
min\Big(
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 1)}}, 
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 1)}}
\Big)
\Big)
\land
\Big(
\forall \gamma_{(2)} \in \{1, \dots, min(2,i)\}, \quad
\Big(
i_{(\gamma_{(2)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(2)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 2)}}
=
0
\Big)
\Big)
\land
\Big(
\forall \gamma'_{(2)} \in \{1, \dots, min(2,j)\}, \quad
\Big(
j_{(\gamma'_{(2)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(2)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = 2)}}
=
0
\Big)
\Big)
\land
\Big(
\big(
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 1)}} - A_{(\alpha_{(2)}, \beta_{(2)})}
=
0
\big)
\oplus
\big(
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 2)}}
=
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 1)}} - A_{(\alpha_{(2)}, \beta_{(2)})}
=
0
\big)
\Big)
\Bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(2)} \in \{1, \dots, min(2,i)\}, \quad
\exists \beta_{(2)} \in \{1, \dots, min(2,j)\}, \quad
\boxed{
\bigg(
A_{(\alpha_{(2)}, \beta_{(2)})}
=
min\Big(
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 1)}}, 
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 1)}}
\Big)
\bigg)
\land
\bigg(
\forall \gamma_{(2)} \in \{1, \dots, min(2,i)\}, \quad
\Big(
i_{(\gamma_{(2)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(2)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = 2)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma'_{(2)} \in \{1, \dots, min(2,j)\}, \quad
\Big(
j_{(\gamma'_{(2)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(2)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = 2)}}
=
0
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 2)}}
=
E_{{(\alpha_{(2)},1)}_{({\iota}_{(1)} = 1)}} - A_{(\alpha_{(2)}, \beta_{(2)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 2)}}
=
R_{{(1,\beta_{(2)})}_{({\iota}_{(2)} = 1)}} - A_{(\alpha_{(2)}, \beta_{(2)})}
=
0
\Big)
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
\end{array}
$$

Part 23 :

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
\underline{1 \leq k \leq max(S_{1}(i, j))}
\Big)
\Rightarrow
\Big(
\exists \alpha_{(k)} \in \{1, \dots, min(k,i)\}, \quad
\exists \beta_{(k)} \in \{1, \dots, min(k,j)\}, \quad
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
A_{(1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
min\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}, 
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\Big)
=
min\Big(
E_{{(1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k - 1)}}, 
R_{{(1,1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k - 1)}}
\Big)
\Big)
\land
\Big(
\forall \gamma_{(k)} \in \{1, \dots, min(k,i)\}, \quad
\Big(
i_{(\gamma_{(k)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(k)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}}
=
0
\Big)
\Big)
\land
\Big(
\forall \gamma'_{(k)} \in \{1, \dots, min(k,j)\}, \quad
\Big(
j_{(\gamma'_{(k)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(k)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = k)}}
=
0
\Big)
\Big)
\land
\Big(
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
E_{{(1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
R_{{(1,1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k)}}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
0
\Big)
\Big)
\Big)
\bigg)
\Bigg)
\\[1em]
\mathcal{H}(k) :
\Bigg(
\forall k \in \mathbb{N}, \quad
\Bigg(
k \geq \eta_{0}
\land
\mathcal{P}(k)
\Bigg)
\Rightarrow
\Bigg(
\mathcal{P}(k + 1) :
\Bigg(
\bigg(
\Big(
\underline{1 \leq k + 1 \leq max(S_{1}(i, j))}
\Big)
\Rightarrow
\Big(
\exists \alpha_{(k + 1)} \in \{1, \dots, min(k+1,i)\}, \quad
\exists \beta_{(k + 1)} \in \{1, \dots, min(k+1,j)\}, \quad
\Big(
A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
A_{(1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
min\Big(
E_{{(\alpha_{(k + 1)},1)}_{({\iota}_{(1)} = k)}}, 
R_{{(1,\beta_{(k + 1)})}_{({\iota}_{(2)} = k)}}
\Big)
=
min\Big(
E_{{(1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}}, 
R_{{(1,1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k)}}
\Big)
\Big)
\land
\Big(
\forall \gamma_{(k + 1)} \in \{1, \dots, min(k + 1,i)\}, \quad
\Big(
i_{(\gamma_{(k + 1)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(k + 1)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
0
\Big)
\Big)
\land
\Big(
\forall \gamma'_{(k + 1)} \in \{1, \dots, min(k + 1,j)\}, \quad
\Big(
j_{(\gamma'_{(k + 1)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(k + 1)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = k + 1)}}
=
0
\Big)
\Big)
\land
\Big(
\Big(
E_{{(\alpha_{(k + 1)},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\alpha_{(k + 1)},1)}_{({\iota}_{(1)} = k)}} - A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
E_{{(1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}} - A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(k + 1)})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\beta_{(k + 1)})}_{({\iota}_{(2)} = k)}} - A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
R_{{(1,1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k)}} - A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
0
\Big)
\Big)
\Big)
\bigg)
\Bigg)
\Bigg)
\end{cases}
\end{cases}
\end{array}
$$

Part 24 :

- Since there are several possible combinations of arguments for the $min$ function, we generalize all these combinations (we "group them together") into a general pair $(\alpha_{(k)}, \beta_{(k)})$ 
  for $A_{(\alpha_{(k)}, \beta_{(k)})}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\left(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
\begin{cases}
\bigg(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}} \leq R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\bigg)
\Rightarrow
\bigg(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\bigg)
\\[1em]
\bigg(
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}} > R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\Big)
\iff
\Big(
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}} < E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\Big)
\bigg)
\Rightarrow
\bigg(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\bigg)
\end{cases}
\right)
\Rightarrow
\boxed{
\left(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
min(E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}, R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}})
=
\begin{cases}
\bigg(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}} \leq R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\bigg)
\Rightarrow
\bigg(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
min(E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}, R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}) = E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\bigg)
\\[1em]
\bigg(
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}} < E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\bigg)
\Rightarrow
\bigg(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
min(E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}, R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}) = R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\bigg)
\end{cases}
\right)
}
\right)
\\[1em]
\Rightarrow
\left(
\left(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
\begin{cases}
\bigg(
\boxed{
A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
0
}
\bigg)
\\[1em]
\bigg(
\boxed{
A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
\boxed{
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}} - R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
}
\bigg)
\end{cases}
\right)
\land
\left(
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
:=
\begin{cases}
\bigg(
\boxed{
A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
\boxed{
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}} - E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
}
\bigg)
\\[1em]
\bigg(
\boxed{
A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}} - R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
=
\boxed{
0
}
\bigg)
\end{cases}
\right)
\right)
\\[1em]
\Rightarrow
\left(
\left(
i_{(k)}
=
\begin{cases}
\bigg(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(k)}
=
1
\bigg)
\\[1em]
\bigg(
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(k)}
=
0
\bigg)
\end{cases}
\right)
\ \land \
\left(
j_{(k)}
=
\begin{cases}
\bigg(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(k)}
=
0
\bigg)
\\[1em]
\bigg(
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(k)}
=
1
\bigg)
\end{cases}
\right)
\right)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\forall \gamma_{(k)} \in \{1, \dots, min(k,i)\}, \quad
\Big(
i_{(\gamma_{(k)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(k)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma'_{(k)} \in \{1, \dots, min(k,j)\}, \quad
\Big(
j_{(\gamma'_{(k)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(k)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = k)}}
=
0
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists \alpha_{(k)} \in \{1, \dots, min(k,i)\}, \quad
\exists \beta_{(k)} \in \{1, \dots, min(k,j)\}, \quad
\bigg(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
min\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}, 
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}} - A_{(\alpha_{(k)}, \beta_{(k)})}
=
0
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 25 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\exists \theta_{(1)}, \theta_{(2)}, \theta_{(3)}, \theta_{(4)} \in \mathbb{N}_{\geq 1}, \quad
A_{(1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}} + i_{(k)},1 + \overset{k - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}} + j_{(k)})}
=
A_{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
\begin{cases}
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
\neq
0
\Big)
\bigg)
\Rightarrow
\bigg(
A_{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
A_{(\theta_{(1)},\theta_{(2)})}
=
min\Big(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}},
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k)}}
\Big)
=
min\Big(
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k)}},
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}}
\Big)
\bigg)
\\[1em]
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
\neq
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
0
\Big)
\bigg)
\Rightarrow
\bigg(
A_{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
A_{(\theta_{(3)},\theta_{(4)})}
=
min\Big(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}},
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k)}}
\Big)
=
min\Big(
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k)}},
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}}
\Big)
\bigg)
\end{cases}
\right)
\end{cases}
\end{array}
$$

Part 26 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
\begin{cases}
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
\neq
0
\Big)
\land
\Big(
A_{(\theta_{(1)},\theta_{(2)})}
=
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k)}}
\Big)
\bigg)
\Rightarrow
\bigg(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k)}} - A_{(\theta_{(1)},\theta_{(2)})}
=
0
\bigg)
\\[1em]
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
\neq
0
\Big)
\land
\Big(
A_{(\theta_{(1)},\theta_{(2)})}
=
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}}
\Big)
\bigg)
\Rightarrow
\bigg(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k)}} - A_{(\theta_{(1)},\theta_{(2)})}
=
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k)}} - R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}}
\bigg)
\\[1em]
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
\neq
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
0
\Big)
\land
\Big(
A_{(\theta_{(3)},\theta_{(4)})}
=
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k)}}
\Big)
\bigg)
\Rightarrow
\bigg(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k)}} - A_{(\theta_{(3)},\theta_{(4)})}
=
0
\bigg)
\\[1em]
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
\neq
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
0
\Big)
\land
\Big(
A_{(\theta_{(3)},\theta_{(4)})}
=
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}}
\Big)
\bigg)
\Rightarrow
\bigg(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k)}} - A_{(\theta_{(3)},\theta_{(4)})}
=
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k)}} - R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}}
\bigg)
\end{cases}
\right)
\end{cases}
\end{array}
$$

Part 27 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
\begin{cases}
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
\neq
0
\Big)
\land
\Big(
A_{(\theta_{(1)},\theta_{(2)})}
=
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k)}}
\Big)
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}} - A_{(\theta_{(1)},\theta_{(2)})}
=
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}} - E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k)}}
\bigg)
\\[1em]
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
=
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
\neq
0
\Big)
\land
\Big(
A_{(\theta_{(1)},\theta_{(2)})}
=
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}}
\Big)
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}} - A_{(\theta_{(1)},\theta_{(2)})}
=
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}} - R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k)}}
=
0
\bigg)
\\[1em]
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
\neq
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
0
\Big)
\land
\Big(
A_{(\theta_{(3)},\theta_{(4)})}
=
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k)}}
\Big)
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}} - A_{(\theta_{(3)},\theta_{(4)})}
=
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}} - E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k)}}
\bigg)
\\[1em]
\bigg(
\Big(
A_{(\alpha_{(k)}, \beta_{(k)})}
=
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k - 1)}}
\Big)
\land
\Big(
E_{{(\alpha_{(k)},1)}_{({\iota}_{(1)} = k)}}
\neq
0
\land
R_{{(1,\beta_{(k)})}_{({\iota}_{(2)} = k)}}
=
0
\Big)
\land
\Big(
A_{(\theta_{(3)},\theta_{(4)})}
=
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}}
\Big)
\bigg)
\Rightarrow
\bigg(
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}} - A_{(\theta_{(3)},\theta_{(4)})}
=
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}} - R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k)}}
=
0
\bigg)
\end{cases}
\right)
\end{cases}
\end{array}
$$

Part 28 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\left(
i_{(k + 1)}
=
\begin{cases}
\bigg(
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k + 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(k + 1)}
=
1
\bigg)
\\[1em]
\bigg(
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k + 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(k + 1)}
=
0
\bigg)
\\[1em]
\bigg(
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k + 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(k + 1)}
=
1
\bigg)
\\[1em]
\bigg(
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k + 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
i_{(k + 1)}
=
0
\bigg)
\end{cases}
\right)
\ \land \
\left(
j_{(k + 1)}
=
\begin{cases}
\bigg(
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k + 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(k + 1)}
=
0
\bigg)
\\[1em]
\bigg(
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k + 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(k + 1)}
=
1
\bigg)
\\[1em]
\bigg(
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k + 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(k + 1)}
=
0
\bigg)
\\[1em]
\bigg(
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k + 1)}}
=
0
\bigg)
\Rightarrow
\bigg(
j_{(k + 1)}
=
1
\bigg)
\end{cases}
\right)
\right)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\forall \gamma_{(k)} \in \{1, \dots, min(k,i)\}, \quad
\Big(
i_{(\gamma_{(k)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(k)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma'_{(k)} \in \{1, \dots, min(k,j)\}, \quad
\Big(
j_{(\gamma'_{(k)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(k)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = k)}}
=
0
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\Bigg(
\bigg(
\Big(
E_{{(\theta_{(1)},1)}_{({\iota}_{(1)} = k + 1)}} = 0
\oplus
E_{{(\theta_{(3)},1)}_{({\iota}_{(1)} = k + 1)}} = 0
\Big)
\Rightarrow
\Big(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
0
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\overset{k + 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
\Big)
\because
\Big(
1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}}
=
i_{(k + 1)}
+
\overset{k}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}}
=
\overset{k + 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}}
\Big)
\bigg)
\Bigg)
\Rightarrow
\Bigg(
E_{{(\overset{k + 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
0
\Bigg)
\ \
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\Bigg(
\bigg(
\Big(
R_{{(1,\theta_{(2)})}_{({\iota}_{(2)} = k + 1)}}
\oplus
R_{{(1,\theta_{(4)})}_{({\iota}_{(2)} = k + 1)}}
\Big)
\Rightarrow
\Big(
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
0
\Big)
\bigg)
\land
\bigg(
\Big(
R_{{(1,1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\overset{k + 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
\Big)
\because
\Big(
1 + \overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}}
=
j_{(k + 1)}
+
\overset{k}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}}
=
\overset{k + 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}}
\Big)
\bigg)
\Bigg)
\Rightarrow
\Bigg(
R_{{(1,\overset{k + 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
0
\Bigg)
\ \
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\forall \gamma_{(k + 1)} \in \{1, \dots, min(k+1,i)\}, \quad
\Big(
i_{(\gamma_{(k + 1)})} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma_{(k + 1)}}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma'_{(k + 1)} \in \{1, \dots, min(k+1,j)\}, \quad
\Big(
j_{(\gamma'_{(k + 1)})} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'_{(k + 1)}}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(1)} = k + 1)}}
=
0
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 29 :

- Since there are several possible combinations of arguments for the $min$ function, we generalize all these combinations (we "group them together") into a general pair $(\alpha_{(k + 1)}, \beta_{(k + 1)})$ 
  for $A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\exists \alpha_{(k + 1)} \in \{1, \dots, min(k+1,i)\}, \quad
\exists \beta_{(k + 1)} \in \{1, \dots, min(k+1,j)\}, \quad
\bigg(
A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
A_{(1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
min\Big(
E_{{(\alpha_{(k + 1)},1)}_{({\iota}_{(1)} = k)}}, 
R_{{(1,\beta_{(k + 1)})}_{({\iota}_{(2)} = k)}}
\Big)
=
min\Big(
E_{{(1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}}, 
R_{{(1,1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k)}}
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(k + 1)},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k + 1)}}
=
E_{{(\alpha_{(k + 1)},1)}_{({\iota}_{(1)} = k)}} - A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
E_{{(1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = k)}} - A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(k + 1)})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k + 1)}}
=
R_{{(1,\beta_{(k + 1)})}_{({\iota}_{(2)} = k)}} - A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
R_{{(1,1 + \overset{(k + 1) - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = k)}} - A_{(\alpha_{(k + 1)}, \beta_{(k + 1)})}
=
0
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

Part 30 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\forall \eta \in \{1, \dots, max(S_{1}(i, j))\}, \quad
\exists \alpha_{(\eta)} \in \{1, \dots, min(\eta,i)\}, \quad
\exists \beta_{(\eta)} \in \{1, \dots, min(\eta,j)\}, \quad
\bigg(
A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
A_{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
min\Big(
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta - 1)}}, 
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta - 1)}}
\Big)
=
min\Big(
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta - 1)}}, 
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta - 1)}}
\Big)
\bigg)
\land
\bigg(
\forall \gamma \in \{1, \dots, min(\eta,i)\}, \quad
\Big(
i_{(\gamma)} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma' \in \{1, \dots, min(\eta,j)\}, \quad
\Big(
j_{(\gamma')} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = \eta)}}
=
0
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta)}}
=
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta)}}
=
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta)}}
=
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
0
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 31 :

- In this part, we show that if several jumps to the next row are made directly and consecutively, then the matrix $E$ at the ${\iota}_{max_{(1)}}$-th update (= last update before the algorithm stops), which is 
  the final version of matrix $E$, contains only zero values. 
  We also show that if several jumps to the next column are made directly and consecutively, then the matrix $R$ at the ${\iota}_{max_{(2)}}$-th update (= last update before the algorithm stops), which is
  the final version of matrix $R$, contains only zero values

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\mathcal{P}(\eta) \curvearrowright P_{i}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \eta \in \{1, \dots, max(S_{1}(i, j))\}, \quad
\bigg(
\forall \gamma \in \{1, \dots, min(\eta,i)\}, \quad
\Big(
i_{(\gamma)} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma' \in \{1, \dots, min(\eta,j)\}, \quad
\Big(
j_{(\gamma')} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = \eta)}}
=
0
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \eta \in \{1, \dots, max(S_{1}(i, j))\}, \quad
\forall \gamma \in \{1, \dots, min(\eta,i)\}, \quad
\bigg(
i_{(\gamma)} = 1
\bigg)
\Rightarrow
\bigg(
\Big(
E_{{(\overset{\gamma}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta )}}
=
0
\Big)
\iff
\Big(
\forall \vartheta_{(1)} \in \{1, \dots, min(\eta,i)\}, \quad
E_{{(\vartheta_{(1)},1)}_{({\iota}_{(1)} = \eta )}}
=
0
\Big)
\iff
\Big(
E_{{(1, 1)}_{({\iota}_{(1)} = \eta )}} = 0
\land
E_{{(2, 1)}_{({\iota}_{(1)} = \eta )}} = 0
\land
\dots
\land
E_{{(min(\eta,i), 1)}_{({\iota}_{(1)} = \eta )}} = 0
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall \eta \in \{1, \dots, max(S_{1}(i, j))\}, \quad
\forall \gamma' \in \{1, \dots, min(\eta,j)\}, \quad
\bigg(
j_{(\gamma')} = 1
\bigg)
\Rightarrow
\bigg(
\Big(
R_{{(1,\overset{\gamma'}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = \eta)}}
=
0
\Big)
\iff
\Big(
\forall \vartheta_{(2)} \in \{1, \dots, min(\eta,j)\}, \quad
R_{{(1,\vartheta_{(2)})}_{({\iota}_{(2)} = \eta )}}
=
0
\Big)
\iff
\Big(
R_{{(1, 1)}_{({\iota}_{(2)} = \eta )}} = 0
\land
R_{{(1, 2)}_{({\iota}_{(2)} = \eta )}} = 0
\land
\dots
\land
R_{{(1, min(\eta,j))}_{({\iota}_{(2)} = \eta )}} = 0
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg\{
\ \
\Bigg[
\eta
=
max(S_{1}(i, j))
=
{\iota}_{max_{(1)}}
=
{\iota}_{max_{(2)}}
\Bigg]
\Rightarrow
\Bigg[
\quad \quad
\Bigg(
\forall \gamma \in \{1, \dots, i\}, \quad
\bigg(
i_{(\gamma)} = 1
\bigg)
\Rightarrow
\bigg(
\Big(
E_{{(\overset{\gamma}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}}
=
0
\Big)
\iff
\Big(
E_{{(\overset{1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}}
=
0
\land
E_{{(\overset{2}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}}
=
0
\land
\dots
\land
E_{{(\overset{i}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}}
=
0
\Big)
\iff
\Big(
E_{{(1,1)}_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}}
=
0
\land
E_{{(2,1)}_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}}
=
0
\land
\dots
\land
E_{{(i,1)}_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}}
=
0
\Big)
\bigg)
\Bigg)
\quad \quad
\oplus
\quad \quad
\Bigg(
\forall \gamma' \in \{1, \dots, j\}, \quad
\bigg(
j_{(\gamma')} = 1
\bigg)
\Rightarrow
\bigg(
\Big(
R_{{(1,\overset{\gamma'}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}}
=
0
\Big)
\iff
\Big(
R_{{(1,\overset{1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}}
=
0
\land
R_{{(1,\overset{2}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}}
=
0
\land
\dots
\land
R_{{(1,\overset{j}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}}
=
0
\Big)
\iff
\Big(
R_{{(1,1)}_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}}
=
0
\land
R_{{(1,2)}_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}}
=
0
\land
\dots
\land
R_{{(1,j)}_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}}
=
0
\Big)
\bigg)
\Bigg)
\quad \quad
\Bigg]
\ \
\Bigg\}
\\[1em]
\Rightarrow
\boxed{
\left(
\left(
E_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}
=
\begin{pmatrix}
0 \\
\vdots \\
0
\end{pmatrix}
\right)
\lor
\bigg(
R_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}
=
\Big(
0, 
\dots, 
0
\Big)
\bigg)
\right)
}
\end{cases}
\end{array}
$$

Part 32 :

- In this part, we implement the algorithm which describes the recurrence (recurrence from part 14 to part 30) in Python

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

Part 33 :

- From part 33 to part 36, we choose to compute the formula for the loop variant $V$ of the algorithm

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

Part 34 :

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

Part 35 :

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

Part 36 :

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

Part 37 : Loop exit condition :

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

Part 38 :

- In this part, we define the stride $\Delta a'_{{(\iota)}_{(5)}}$ between ${a'}_{({\iota}_{(5)})}$ and ${a'}_{({\iota}_{(5)} + 1)}$ and the stride $\Delta b'_{{(\iota)}_{(5)}}$ between ${b'}_{({\iota}_{(5)})}$ and ${b'}_{({\iota}_{(5)} + 1)}$, in order to define 
  the simultaneous stride $\sigma_{{(\iota)}_{(5)}}$ (see diagram 1 of part 38)
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

Diagram 1 of part 38 :

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

Part 39 :

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

Part 40 :

- In this part, we conclude

$$
\begin{array}{l}
\boxed{
\therefore
\begin{cases}
(P1) \quad
\left(
\ \
\exists! i, j \in \mathbb{N}_{\geq 1}, \quad
\left(
\underbrace{
\exists! {\iota}_{max_{(1)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(1)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\exists! E_{({\iota}_{(1)})} \in \mathcal{M}_{i, 1}(\mathbb{R}_{\geq 0}), \quad
\left(
\boxed{
E_{({\iota}_{(1)})}
:=
\begin{pmatrix}
E_{{(1,1)}_{({\iota}_{(1)})}} \\
\vdots \\
E_{{(i,1)}_{({\iota}_{(1)})}}
\end{pmatrix}
}
\right)
\land
\left(
\exists! e_{(1)}, \dots, e_{(i)} \in \mathbb{R}_{\geq 0}, \quad
\boxed{
E_{({\iota}_{(1)} = 0)}
=
\begin{pmatrix}
e_{(1)} \\
\vdots \\
e_{(i)}
\end{pmatrix}
=
\begin{pmatrix}
E_{{(1,1)}_{({\iota}_{(1)} = 0)}} \\
\vdots \\
E_{{(i,1)}_{({\iota}_{(1)} = 0)}}
\end{pmatrix}
}
\right)
\right)
\ \
\right)
\\[1em]
(P2) \quad
\left(
\ \
\exists! i, j \in \mathbb{N}_{\geq 1}, \quad
\left(
\underbrace{
\exists! {\iota}_{max_{(2)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\exists! R_{({\iota}_{(2)})} \in \mathcal{M}_{1, j}(\mathbb{R}_{\geq 0}), \quad
\bigg(
\boxed{
R_{({\iota}_{(2)})}
:=
\Big(
R_{{(1,1)}_{({\iota}_{(2)})}}, 
\dots, 
R_{{(1,j)}_{({\iota}_{(2)})}}
\Big)
}
\bigg)
\land
\bigg(
\exists! r_{(1)}, \dots, r_{(j)} \in \mathbb{R}_{\geq 0}, \quad
\boxed{
R_{({\iota}_{(2)} = 0)}
=
\Big(
r_{(1)},
\dots,
r_{(j)}
\Big)
=
\Big(
R_{{(1,1)}_{({\iota}_{(2)} = 0)}}, 
\dots, 
R_{{(1,j)}_{({\iota}_{(2)} = 0)}}
\Big)
}
\bigg)
\right)
\land
\left(
\exists A \in \mathcal{M}_{i, j}(\mathbb{R}_{\geq 0}), \quad
\boxed{
A
:=
\begin{pmatrix}
0 & 0 & \dots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \dots & 0
\end{pmatrix}
}
\right)
\ \
\right)
\\[1em]
(P3) \quad
\Bigg(
\forall \Upsilon \in \{1, \dots, i\}, \quad
\forall \Upsilon' \in \{1, \dots, j\}, \quad
\bigg(
E_{(\Upsilon, 1)} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
R_{(1, \Upsilon')} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
A_{(\Upsilon, \Upsilon')} \in \mathbb{R}_{\geq 0}
\bigg)
\land
\bigg(
\overset{j}{\underset{\varphi = 1}{\sum}}{A_{(\Upsilon, \varphi)}} = E_{(\Upsilon, 1)}
\bigg)
\land
\bigg(
\overset{i}{\underset{\varphi' = 1}{\sum}}{A_{(\varphi', \Upsilon')}} = R_{(1, \Upsilon')}
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
(P4) \quad
\Bigg(
\forall \eta' \in \{0, \dots, max(S'_{1}(i, j))\}, \quad
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
=
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
<
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\oplus
\bigg(
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = 0)}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = 0)}}
}
\Rightarrow
\dots
\Rightarrow
\overset{i}{\underset{\psi = 1}{\sum}}{
E_{{(\psi, 1)}_{({\iota}_{(1)} = \eta')}}
}
>
\overset{j}{\underset{\psi = 1}{\sum}}{
R_{{(1, \psi)}_{({\iota}_{(2)} = \eta')}}
}
\bigg)
\Bigg)
\\[1em]
(P5) \quad
\Bigg(
\forall \Upsilon \in \{1, \dots, i\}, \quad
\forall \Upsilon' \in \{1, \dots, j\}, \quad
\exists \Phi \in \{1, \dots, i\}, \quad
\exists \Phi' \in \{1, \dots, j\}, \quad
\underbrace{
\bigg(
\Big(
A_{(\Phi, \Phi')} \leq E_{(\Upsilon, 1)}
\Big)
\land
\Big(
A_{(\Phi, \Phi')} \leq R_{(1, \Upsilon')}
\Big)
\bigg)
}_{
x
\leq
min(\alpha, \beta)
\iff
\bigg(
\Big(
x \leq \alpha
\Big)
\land
\Big(
x \leq \beta
\Big)
\bigg)
\text{ form}
}
\iff
\bigg(
A_{(\Phi, \Phi')}
\leq
min\Big(
E_{(\Upsilon, 1)}, R_{(1, \Upsilon')}
\Big)
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
(P6) \quad
\Bigg(
\forall \eta \in \{1, \dots, max(S_{1}(i, j))\}, \quad
\exists \alpha_{(\eta)} \in \{1, \dots, min(\eta,i)\}, \quad
\exists \beta_{(\eta)} \in \{1, \dots, min(\eta,j)\}, \quad
\bigg(
A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
A_{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}
=
min\Big(
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta - 1)}}, 
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta - 1)}}
\Big)
=
min\Big(
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta - 1)}}, 
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta - 1)}}
\Big)
\bigg)
\land
\bigg(
\forall \gamma \in \{1, \dots, min(\eta,i)\}, \quad
\Big(
i_{(\gamma)} = 1
\Big)
\Rightarrow
\Big(
E_{{(\overset{\gamma}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
0
\Big)
\bigg)
\land
\bigg(
\forall \gamma' \in \{1, \dots, min(\eta,j)\}, \quad
\Big(
j_{(\gamma')} = 1
\Big)
\Rightarrow
\Big(
R_{{(1,\overset{\gamma'}{\underset{\vartheta' = 1}{\sum}}{j_{(\vartheta')}})}_{({\iota}_{(2)} = \eta)}}
=
0
\Big)
\bigg)
\land
\bigg(
\Big(
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta)}}
=
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta)}}
=
E_{{(\alpha_{(\eta)},1)}_{({\iota}_{(1)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
E_{{(1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{i_{(\vartheta)}},1)}_{({\iota}_{(1)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
0
\Big)
\oplus
\Big(
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta)}}
=
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta)}}
=
R_{{(1,\beta_{(\eta)})}_{({\iota}_{(2)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
R_{{(1,1 + \overset{\eta - 1}{\underset{\vartheta = 1}{\sum}}{j_{(\vartheta)}})}_{({\iota}_{(2)} = \eta - 1)}} - A_{(\alpha_{(\eta)}, \beta_{(\eta)})}
=
0
\Big)
\bigg)
\Bigg)
\\[1em]
(P7) \quad
\left(
\left(
E_{({\iota}_{(1)} = {\iota}_{max_{(1)}} )}
=
\begin{pmatrix}
0 \\
\vdots \\
0
\end{pmatrix}
\right)
\lor
\bigg(
R_{({\iota}_{(2)} = {\iota}_{max_{(2)}} )}
=
\Big(
0, 
\dots, 
0
\Big)
\bigg)
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
(P9) \quad
\left(
\exists! {\iota}_{max_{(5)}} \in \mathbb{N}, \quad
\forall {\iota}_{(5)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(5)}, \dots, {\iota}_{max_{(5)}}\}, \quad
a' : \{0, \dots, {\iota}_{max_{(5)}}\} \to \mathbb{N}, \quad
{\iota}_{(5)} \mapsto {a'}_{{(\iota)}_{(5)}}, \quad
b' : \{0, \dots, {\iota}_{max_{(5)}}\} \to \mathbb{N}, \quad
{\iota}_{(5)} \mapsto {b'}_{{(\iota)}_{(5)}}, \quad
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
\land
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
\land
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
\right)
\\[1em]
(P10) \quad
\Bigg(
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
=
i + j
-
\overset{\Omega}{\underset{{(\iota)}_{(5)} = 1}{\sum}}{
\sigma_{{(\iota)}_{(5)}}
}
\Bigg)
\\[1em]
(P11) \quad
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
\end{cases}
}
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



