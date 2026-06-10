
Definition of the properties of the Boyer-Moore algorithm :




- (English) Starting from the current block from $j_{min}$ to $j_{min} + m - 1$ :




	- 1. We align the first character (= $t_{(j_{min} + m - 1)}$) on the far left of the pattern $P$ with the first character (= $p_{(m - 1)}$) on the far left of the current block from $j_{min}$ to $j_{min} + m - 1$ 

	- 2. We compare the last character of the pattern to the last character of the current block :

		- 2.1. If there is a correspondence between the last character of the pattern and the last character of the current block, then we move on to the step 3
	  
		- 2.2. If there is no correspondence between the two, then we align the last character of the current block with its first occurrence on the far right in the pattern 
		  (= "first occurrence of the last character of the block"), by offsetting the pattern to the right (= in order to enable alignment). If 2.2 is satisfied, then we 
		  move on to the next block from $j_{min} + m - 1 - \beta'$ to $(j_{min} + m - 1 - \beta') + m - 1$, and we start again from step 1 (see part 9) until all the characters of the pattern 
		  correspond consecutively and respectively to all the characters of the current block. If 2.2 is not satisfied, then we move on to the step 2.3
		  
		- 2.3. If the last character of the current block is not present in the pattern, then we move on to the next block from $j_{min} + m$ to $j_{min} + m + m - 1$ and 
		  we start again from step 1 until all the characters of the pattern correspond consecutively and respectively to all the characters of the current block




	- 3. If several characters of the pattern (forming a "pattern suffix") correspond consecutively and respectively to several characters of the current block (forming a "text suffix") and if 
	  the last character of the pattern (= the previous character of the pattern when moving to the left) does not correspond, then we move on to the step 4

	- 4. We look to see if the "pattern suffix" is present another time in the pattern just before itself (itself = the "pattern suffix") :

		- 4.1. If so, the new "pattern suffix" is aligned with the position of the "text suffix" by offsetting the pattern (to enable alignment). The offset of the pattern forms a new block 
		  which will be examined in the next iteration.
		  This new "pattern suffix" forms potentially a whole pattern in a new block that needs to be examined in the next iteration. 
		  Indeed, the final goal is to align the whole pattern (= $P$) with a block of the text $T$ 

		- 4.2. If not, then we go straight to step 7

	- 5. We move on to the next block from $j_{min} + m - 1 - \Lambda$ to $(j_{min} + m - 1 - \Lambda) + m - 1$ 

	- 6. We start again from step 1 until all the characters in the pattern correspond consecutively and respectively to all the characters of the current block




	- 7. If several characters of the pattern (forming a "pattern suffix") correspond consecutively and respectively to several characters of the current block (forming a "text suffix") 
	 and if the last character of the pattern (= the previous character of the pattern when moving to the left) does not correspond, then we move on to the step 8

	- 8. We look to see if the "longest prefix of the pattern" is also the longest suffix of the "pattern suffix". In other words, we look to see if the start of the pattern 
	  corresponds to the end of the "pattern suffix" :

		- 8.1. If so, the "longest prefix of the pattern" is aligned with the position of the "text suffix" by offsetting the pattern (to enable alignment). The offset of the pattern forms 
		 a new block which will be examined in the next iteration
		 This "longest prefix of the pattern" forms potentially a whole pattern in a new block that needs to be examined in the next iteration. 
		 Indeed, the final goal is to align the whole pattern (= $P$) with a block of the text $T$ 

		- 8.2. If not, then we go straight to step 11 (see part 23)

	- 9. We move on to the next block from $j_{min} + m - 1 - \Lambda$ to $(j_{min} + m - 1 - \Lambda) + m - 1$ 

	- 10. We start again from step 1 (see part 9) until all the characters of the pattern correspond consecutively and respectively to all the characters of the current block




	- 11. We skip the whole current block and we move on to the next block from $j_{min} + m - 1 + 1$ to $(j_{min} + m - 1 + 1) + m - 1$ 

	- 12. We start again from step 1 (see part 9) until all the characters of the pattern correspond consecutively and respectively to all the characters of the current block




	- The final goal is to align the whole pattern (= $P$) with a block of the text $T$ 




- (French) En partant du bloc courant allant $j_{min}$ à $j_{min} + m - 1$ :




	- 1. On aligne le premier caractère (= $t_{(j_{min} + m - 1)}$) tout à gauche du motif $P$ avec le premier caractère (= $p_{(m - 1)}$) tout à gauche du bloc courant allant de $j_{min}$ à $j_{min} + m - 1$ 
	
	- 2. On compare le dernier caractère du motif au dernier caractère du bloc courant :

		- 2.1. S'il y a une correspondance entre le dernier caractère du motif et la dernier caractère du bloc courant, alors on passe à l'étape 3

		- 2.2. S'il n'y a aucune correspondance entre les deux, alors on aligne le dernier caractère du bloc courant avec sa première occurrence la plus à droite dans le motif 
		  (= "première occurrence du dernier caractère de bloc"), en décalant le motif vers la droite (= pour permettre l'alignement). Si la 2.2 est satisfaite, alors on 
		  passe au bloc suivant allant de $j_{min} + m - 1 - \beta'$ à $(j_{min} + m - 1 - \beta') + m - 1$, et on recommence à partir de l'étape 1 (voir partie 9) jusqu'à ce que tous les caractères 
		  du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant. Si la 2.2 n'est pas satisfaite, alors on passe à l'étape 2.3

		- 2.3. Si le dernier caractère du bloc courant n'est pas présent dans le motif, alors on passe au bloc suivant allant de $j_{min} + m$ à $j_{min} + m + m - 1$ et  
		  on recommence à partir de l'étape 1 jusqu'à ce que tous les caractères du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant




	- 3. Si plusieurs caractères du motif (formant un "suffixe de motif") correspondent d'affilée et respectivement à plusieurs caractères du bloc courant (formant un "suffixe de texte") et 
	  que le dernier caractère du motif (= caractère précédent du motif en allant vers la gauche) ne correspond pas, alors on passe à l'étape 4

	- 4. On regarde si le "suffixe de motif" est présent une nouvelle fois dans le motif juste avant lui-même (lui-même = le "suffixe de motif") :

		- 4.1. Si oui, alors on aligne le nouveau "suffixe de motif" sur la position du "suffixe de texte" en décalant le motif (pour permettre l'alignement). Le décalage du motif forme un 
		  nouveau bloc qui sera examiné à l'itération suivante.
		  Ce nouveau "suffixe de motif" forme potentiellement un motif entier dans un nouveau bloc qui a besoin d'être examiné à l'itération suivante. 
		  En effet, l'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 
		  
		- 4.2. Si non, alors on passe directement à l'étape 7

	- 5. On passe au bloc suivant allant de $j_{min} + m - 1 - \Lambda$ à $(j_{min} + m - 1 - \Lambda) + m - 1$ 

	- 6. On recommence à partir de l'étape 1 jusqu'à ce que tous les caractères du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant




	- 7. Si plusieurs caractères du motif (formant un "suffixe de motif") correspondent d'affilée et respectivement à plusieurs caractères du bloc courant (formant un "suffixe de texte") 
	 et que le dernier caractère du motif (= caractère précédent du motif en allant vers la gauche) ne correspond pas, alors on passe à l'étape 8

	- 8. On regarde si le "plus grand préfixe du motif" est aussi le plus grand suffixe du "suffixe de motif". Autrement dit, on regarde si le début du motif correspond à la fin 
	  du "suffixe de motif" :

		- 8.1. Si oui, alors on aligne le "plus grand suffixe du motif" sur la position du "suffixe de texte" en décalant le motif (pour permettre l'alignement). Le décalage du motif forme 
		  un nouveau bloc qui sera examiné à l'itération suivante
		  Ce "plus grand suffixe du motif" forme potentiellement un motif entier dans un nouveau bloc qui a besoin d'être examiné à l'itération suivante. 
		  En effet, l'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 

		- 8.2. Si non, alors on passe directement à l'étape 11 (voir partie 23)

	- 9. On passe au bloc suivant allant de $j_{min} + m - 1 - \Lambda$ à $(j_{min} + m - 1 - \Lambda) + m - 1$ 

	- 10. On recommence à partir de l'étape 1 (voir partie 9) jusqu'à ce que tous les caractères du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant




	- 11. On saute le bloc courant tout entier et on passe au bloc suivant allant de $j_{min} + m - 1 + 1$ à $(j_{min} + m - 1 + 1) + m - 1$ 

	- 12. On recommence à partir de l'étape 1 (voir partie 9) jusqu'à ce que tous les caractères du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant



	
	- L'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 




- Whatever the iteration, the first character on the far left of the pattern is always aligned with the first character on the far left of the current block


- The verb $\boxed{\text{"align" has the same meaning as “superimposed”}}$

- The $\boxed{\text{final goal of the algorithm}}$ is to align the whole pattern (= $P$) with a block of the text $T$. As soon as this objective is met, then the "first occurrence of the pattern $P$ " is found 
  in the text $T$ 

- $\boxed{\text{The algorithm stops as soon as the "first occurrence of the pattern } P \text{ " is found in the text } T }$


- $\beta'$ is the index (= position) of the occurrence ( = occurrence of the last character of the current block) most to the right in the pattern $P$ 

- In other words, $\beta'$ is the index (= position) of the “first occurrence of the last character of the current block” in the pattern $P$ 

- If there is at least one occurrence of $P_{suffix_{(1)}}$ in $P$, then $\Lambda$ is the index (= position) of the last letter (= letter most to the right) of the "first occurrence of $P_{suffix_{(1)}}$" 
  (= occurrence most to the right) in the pattern $P$ 

- If no "occurrence of $P_{suffix_{(1)}}$" are found in $P$ and if there is at least one pattern prefix $P_{prefix_{(1)}}$, then $\Lambda$ is the index (= position) of the last letter of the "longest pattern prefix" 
  (= one specific $P_{prefix_{(1)}}$ ), which is the pattern prefix "most to the right" in the pattern $P$ 

- If no "occurrence of $P_{suffix_{(1)}}$" are found in $P$ and if no "longest pattern prefix" is found in $P$, then $\Lambda$ is the "block jump" that is equal to $+m$ 

- $\xi$ is an index (which we will call the "boundary position") :

	- $\xi$ is an index denoting a position (which is never the end of the current block) in the current block, located to the right of the current block. This position corresponds to the boundary 
	  where the pattern suffix ends, and the character at this position is not a character of the pattern suffix. All characters located after (to the right of) this position are characters of the 
	  pattern suffix


- $\mathcal{W}_{{}_{[2]}total}$ and $\mathcal{W}'_{{}_{[2]}total}$ are respectively the total numbers of operations performed before, during and after the scan of the text $T$ in the case linked to the variable ${\iota}_{(2)}$ without and with a 
  pre-computation phase

- $\mathcal{W}_{{}_{[3]}total}$ and $\mathcal{W}'_{{}_{[3]}total}$ are respectively the total numbers of operations performed before, during and after the scan of the text $T$ in the case linked to the variable ${\iota}_{(3)}$ without and with a 
  pre-computation phase

- $\mathcal{W}_{{}_{[4]}total}$ and $\mathcal{W}'_{{}_{[4]}total}$ are respectively the total numbers of operations performed before, during and after the scan of the text $T$ in the case linked to the variable ${\iota}_{(4)}$ without and with a 
  pre-computation phase


- $\delta_{[2]}(\alpha)$ is called the "table of the non-corresponding character". The "table of the non-corresponding character" corresponds to the step 2 to 2.3. 

- $\delta_{[3]}(\phi)$ is called the "table of corresponding suffixes and prefixes". The "table of corresponding suffixes and prefixes" corresponds to the step 3 to 12

- $\delta(\alpha, \phi)$ brings together the two tables $\delta_{[2]}(\alpha)$ and $\delta_{[3]}(\phi)$. Within $\delta(\alpha, \phi)$, properties 1 to 2 are associated to $\delta_{[2]}(\alpha)$, and properties 3 to 5 are associated to $\delta_{[3]}(\phi)$ 

- The two tables $\delta_{[2]}(\alpha)$ and $\delta_{[3]}(\phi)$ are filled in during the pre-computation phase, and $\delta_{[2]}(\alpha)$ and $\delta_{[3]}(\phi)$ are then consulted (during the scan of the text $T$) at each 
  non-correspondence between the last character inspected of the current block and the last character inspected of the pattern $P$ 


- See $\boxed{\text{part 14}}$ for more details about $\lambda$ and $\psi$. See $\boxed{\text{part 19}}$ for more details about $\lambda'$ and $\psi'$ 




Algorithm main properties :


- Each notation of the type $(P1)$, $(P2)$, etc., refers to one property of the algorithm

$$
\begin{array}{l}
\begin{cases}
(P1) \quad
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\bigg(
\forall t_{(0)}, \dots, t_{(n - 1)} \in \varsigma, \quad
\exists! T \in \varsigma^{n}, \quad
T
=
(t_{(0)}, \dots, t_{(n - 1)})
\bigg)
\Rightarrow
\bigg(
\forall m \in \{1, \dots, n\}, \quad
\forall p_{(0)}, \dots, p_{(m - 1)} \in \varsigma, \quad
\exists! P \in \varsigma^{m}, \quad
P
=
(p_{(0)}, \dots, p_{(m - 1)})
\bigg)
\Bigg)
\\[1em]
(P2) \quad
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{suffixpos_{(\xi)}}
=
\underbrace{
\bigg\{
\lambda
\ \bigg| \
\bigg(
\psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}
\bigg)
\land
\bigg(
\lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\}
\bigg)
\land
\bigg(
P_{suffix_{(2)}}
=
(p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)})
=
(p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)})
=
P_{suffix_{(1)}}
\bigg)
\land
\bigg(
\Big(
\psi - 1 \geq 0
\Big)
\Rightarrow
\Big(
p_{(\psi - 1)} \neq p_{(\xi)}
\Big)
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{suffixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{suffix_{(2)}} \text{, where } P_{suffix_{(2)}}
\text{ can be preceded by at least one character in } P \text{, or can be flushed with the left edge of } P
}
\ \
\Bigg)
\\[1em]
(P3) \quad
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{prefixpos_{(\xi)}}
=
\underbrace{
\bigg\{
\lambda'
\ \bigg| \
\bigg(
\psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}
\bigg)
\land
\bigg(
\lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\}
\bigg)
\land
\bigg(
P_{prefix_{(1)}}
=
(p_{(0)}, \dots, p_{(\lambda')})
=
(p_{(m - \lambda' - 1)}, \dots, p_{(m - 1)})
\bigg)
\land
\bigg(
Card(B_{P_{prefix_{(1)}}})
<
Card(B_{P_{suffix_{(1)}}})
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{prefixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{prefix_{(1)}} \text{, where } P_{prefix_{(1)}}
\text{ has a length exactly less than that of } P_{suffix_{(1)}}
}
\ \
\Bigg)
\\[1em]
(P4) \quad
\Bigg(
\bigg(
B_{P_{suffix_{(1)}}}
=
\Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\land
\underbrace{
\bigg(
B_{P_{suffix_{(2)}}}
=
\Big\{\Big\{ p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{suffix_{(2)}} \text{ (= one possible occurrence of } P_{suffix_{(1)}} \text{ )}
}
\\
{
\text{ in the current block and each } P_{suffix_{(2)}} \text{ can also be viewed as a multiset of characters in } P
}
}
}
\land
\bigg(
Card(B_{P_{suffix_{(1)}}})
=
Card(B_{P_{suffix_{(2)}}})
=
m - 1 - \xi
\bigg)
\land
\underbrace{
\bigg(
B_{P_{prefix_{(1)}}}
=
\Big\{\Big\{ p_{(0)}, p_{(1)}, \dots, p_{(\lambda' - 1)}, p_{(\lambda')} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{prefix_{(1)}} \text{ (= one possible pattern suffix)}
}
\\
{
\text{ in the current block and each } P_{prefix_{(1)}} \text{ can be viewed as a multiset of characters in } P
}
}
}
\land
\bigg(
Card(B_{P_{prefix_{(1)}}})
=
\lambda' + 1
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P5) \quad
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\delta_{[2]}(\alpha)
=
\begin{cases}
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\bigg(
\beta'
=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
\alpha
\land
\gamma < m - 1
\Big\}
\Big)
\bigg)
\Rightarrow
\bigg(
\delta_{[2]}(\alpha)
=
m - 1 - \beta'
\bigg)
\\[1em]
\bigg(
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta_{[2]}(\alpha)
=
m
\bigg)
\end{cases}
\right)
\\[1em]
(P6) \quad
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \phi \in \{0, \dots, m - 2\}, \quad
\delta_{[3]}(\phi)
=
\begin{cases}
\bigg(
P_{suffixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
max\Big(
P_{suffixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
max\Big(
P_{prefixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
m
\bigg)
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
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\underbrace{
\exists! {\iota}_{max} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall \iota \in \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max}\}, \quad
\mathcal{J}_{min} : \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max}\} \to \{0, \dots, n - m\}, \quad
\iota \mapsto \mathcal{J}_{{min}_{{\big({\iota}\big)}}}, \quad
\begin{cases}
\mathcal{J}_{{min}_{{\big({0}\big)}}}
=
0
\\[1em]
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
:=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)}
\land
\gamma < m - 1
\Big\}
\Big)
\\[1em]
\forall \xi \in \{0, \dots, m - 2\}, \quad
\exists! \Lambda \in \{0, \dots, m\}, \quad
\Lambda
:=
\begin{cases}
\bigg(
P_{suffixpos_{(\xi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
max\Big(
P_{suffixpos_{(\xi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
max\Big(
P_{prefixpos_{(\xi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
m
\bigg)
\end{cases}
\\[1em]
\forall \iota \in \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max} - 1\}, \quad
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
:=
\begin{cases}
\bigg(
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)} \neq p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
=
\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1 - \beta'
\bigg)
\\[1em]
\bigg(
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
=
\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1 - \Lambda
\bigg)
\end{cases}
\end{cases}
\ \
\right)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P8) \quad
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\forall \phi \in \{0, \dots, m - 2\}, \quad
\delta : \varsigma \times \{0, \dots, m - 2\} \to \{0, \dots, m\}, \quad
(\alpha, \phi) \mapsto \delta(\alpha, \phi), \quad
\delta(\alpha, \phi)
:=
\begin{cases}
\text{(Property 1)} \quad
\bigg(
\Big(
\alpha \neq p_{(m - 1)}
\Big)
\land
\Big(
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
:=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
\alpha
\land
\gamma < m - 1
\Big\}
\Big)
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m - 1 - \beta'
\bigg)
\\[1em]
\text{(Property 2)} \quad
\bigg(
\alpha \neq p_{(m - 1)}
\land
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m
\bigg)
\\[1em]
\text{(Property 3)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
max\Big(
P_{suffixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\text{(Property 4)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
max\Big(
P_{prefixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\text{(Property 5)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m
\bigg)
\end{cases}
\ \
\right)
\end{cases}
\end{array}
$$

$$
\begin{array}{l}
\begin{cases}
(P9) \quad
\Bigg(
\underbrace{
\frac{n}{m} + Card(\varsigma)
}_{\mathcal{W}'_{{}_{[2]}total}}
<
\underbrace{
n
}_{\mathcal{W}_{{}_{[2]}total}}
\Bigg)
\\[1em]
(P10) \quad
\Bigg(
\bigg(
\underbrace{
\frac{n - 1 - \beta'}{m - 1 - \beta'} + 2 \cdot Card(\varsigma)
}_{\mathcal{W}'_{{}_{[3]}total}}
<
\underbrace{
\frac{nm - m - m \beta'}{m - 1 - \beta'}
}_{\mathcal{W}_{{}_{[3]}total}}
\bigg)
\iff
\bigg(
\Big(
\beta' < m - 1
\Big)
\land
\Big(
n >
\beta' + 2 \cdot Card(\varsigma) - \frac{2 \cdot Card(\varsigma) \cdot \beta'}{(m - 1)} + 1
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\Bigg)
\\[1em]
(P11) \quad
\Bigg(
\bigg(
\underbrace{
\frac{n + 2 + 2 \Lambda + 3m^{2} - 6m - 3m \Lambda}{m - 1 - \Lambda}
}_{\mathcal{W}'_{{}_{[4]}total}}
<
\underbrace{
\frac{nm - m - m \Lambda}{m - 1 - \Lambda}
}_{\mathcal{W}_{{}_{[4]}total}}
\bigg)
\iff
\bigg(
\Big(
\Lambda < m - 1
\Big)
\land
\Big(
n
>
3m - 2 - 2 \Lambda
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda > m - 1
\Big)
\land
\Big(
n
<
3m - 2 - 2 \Lambda
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$




Proof of the algorithm properties :

Part 1 :

- In the proof, the verb $\boxed{\text{"align" has the same meaning as “superimposed”}}$

- In this part, we initialize the elements needed for the algorithm

	- $T$ is the text in which a pattern $P$ is being searched. Its length is $n$ 
	
	- $P$ is a string that we choose to find in $T$. Its length is $m$ 
	
	- A text $\boxed{\text{block}}$ is a portion of $T$ and has the same length as the pattern $P$ (length $m$), and the content of the text block is not necessarily the content of the pattern $P$ :
	
		- If the content of the text block is exactly the content of the pattern $P$, then this text block is the pattern $P$ itself in the text $T$ 
		
		- We choose to check, at each iteration of the algorithm, if the current text block is the pattern $P$ itself. 
		  $\boxed{\text{Therefore, we need to examine all possible cases where the pattern aligns with this current block}}$ 
	
	- $j_{min}$ is the index of the first letter of the current text block (which we will also call "current block"). If the current block is the pattern $P$ itself, then $j_{min}$ is also a possible position of $p_{(0)}$ 
	  in $T$ 


- The $\boxed{\text{final goal of the algorithm}}$ is to align the whole pattern (= $P$) with a block of the text $T$. As soon as this objective is met, then the "first occurrence of the pattern $P$ " is found 
  in the text $T$ 

- $\boxed{\text{The algorithm stops as soon as the "first occurrence of the pattern } P \text{ " is found in the text } T }$

$$
\begin{array}{l}
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\bigg(
\forall t_{(0)}, \dots, t_{(n - 1)} \in \varsigma, \quad
\exists! T \in \varsigma^{n}, \quad
T
:=
(t_{(0)}, \dots, t_{(n - 1)})
\bigg)
\Rightarrow
\bigg(
\forall m \in \{1, \dots, n\}, \quad
\forall p_{(0)}, \dots, p_{(m - 1)} \in \varsigma, \quad
\exists! P \in \varsigma^{m}, \quad
P
:=
(p_{(0)}, \dots, p_{(m - 1)})
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\begin{cases}
\Bigg(
\forall i \in \{0, \dots, n - 1\}, \quad
\boxed{
\bigg(
T
=
(t_{(0)}, t_{(1)}, \dots, \ \underbrace{t_{(i)}, t_{(i + 1)}, \dots, t_{(i + m - 1)}}_{\boxed{\text{Block of size } m}} \ , \dots, t_{(n - 1)})
\bigg)
\land
\bigg(
P
=
(\ \underbrace{p_{(0)}, p_{(1)} \dots, p_{(m - 1)}}_{\boxed{\text{Pattern of size } m}} \ )
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
\big(
0 \leq i \leq n - 1
\big)
\iff
\boxed{
\big(
m - 1 \leq i + m - 1 \leq n + m - 2
\big)
}
\Big)
\land
\Big(
\boxed{
\big(
n + m - 2 \geq n - 1
\big)
}
\because
\big(
\forall m \in \{1, \dots, n\}, \quad
n + m - 2 \geq n - 1
\iff
m - 2 \geq -1
\iff
m - 1 \geq 0
\big)
\Big)
\bigg)
\Rightarrow
\boxed{
\bigg(
m - 1 \leq i + m - 1 \leq n - 1
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall j \in \{i \dots, i + m - 1\}, \quad
\bigg(
\underbrace{
\overbrace{
\Big(
j_{min} = i
\Big)
}^{\in \mathbb{N}}
}_{
\boxed{
\text{Possible position of } p_{0} \text{ in } T
}
}
\land
\underbrace{
\overbrace{
\Big(
j_{max} = i + m - 1
\Big)
}^{\in \mathbb{N}}
}_{
\boxed{
\text{Possible position of } p_{m - 1} \text{ in } T
}
}
\bigg)
\Rightarrow
\bigg(
\boxed{
\Big(
m - 1 \leq \underbrace{i + m - 1}_{j_{max}} \leq n - 1
\Big)
}
\iff
\Big(
0 \leq \underbrace{i}_{\boxed{j_{min}}} \leq n - m
\Big)
\iff
\boxed{
\Big(
0 \leq j_{min} \leq n - m
\Big)
}
\bigg)
\Rightarrow
\boxed{
\bigg(
j_{min} \in \{0, \dots, n - m\}
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Part 2 :

- From part 2 to part 3, we examine (whatever the case may be) the properties of the set of all the positions of $p_{(0)}$ in $T$ 

	- $\boxed{{\iota}_{(1)}}$ represents the ${\iota}_{(1)}$-th time the variable $\mathcal{J}_{min}$ change its value from its previous value in the algorithm $\boxed{\text{all cases considered}}$ (similar to a recurrent sequence of order 1)
	  if the text $T$ does not contain any characters from the pattern $P$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\ \
\underbrace{
\bigg(
S
:=
\bigg\{
j_{min}
\ \bigg| \
\bigg(
j_{min} \in \{0, \dots, n - m\}
\bigg)
\land
\bigg(
\forall k \in \{0, \dots, m - 1\}, \quad
\boxed{
t_{(j_{min} + k)}
=
p_{(k)}
}
\bigg)
\bigg\}
\bigg)
}_{
\substack{
{
\text{Here, no } j_{min} \text{ is fixed in advance. We test all values of } j_{min} \text{ specified in } S \text{ . Some values in } \{0, \dots, n - m\} \text{ might not be in } S
}
\\
{
S \text{ is the set of all the positions of } p_{(0)} \text{ in } T
\text{ (set of all } j_{min} \text{ satisfying the condition of } S \text{ , which means that } j_{min} \text{ values can be spaced apart)}
}
}
}
\land
\underbrace{
\bigg(
j_{min} \in S
\Rightarrow
0 \leq j_{min} \leq n - m
\bigg)
}_{
\substack{
{
\text{If a value of } j_{min} \text{ is in } S \text{ , then it is in } \{0, \dots, n - m\}
}
\\
{
\text{This does not necessarily mean that all } j_{min} \text{ values are in } S
}
}
}
\ \
\Bigg)
\\[1em]
\Rightarrow
\left(
\ \
\underbrace{
\exists! {\iota}_{max_{(1)}} \in \mathbb{N}, \quad
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(1)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\forall x \in S, \quad
f : S \to S, \quad
x \mapsto f(x), \quad
\underbrace{
\mathcal{J}_{{}_{[1]}{min}} : \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\} \to S
}_{
\text{Thus, } \mathcal{J}_{{}_{[1]}{min}} \text{ denotes a sequence, whereas } j_{min} \text{ denotes a variable}
}
, \quad
\Delta_{{}_{[1]}} : \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\} \to \mathbb{N}, \quad
\begin{cases}
\ \
\boxed{
\Bigg(
\mathcal{J}_{{}_{[1]}{min}_{{\big({0}\big)_{(1)}}}}
=
min(S)
\Bigg)
}
\\[1em]
f_{1}(x)
:=
min\Big(
\Big\{
j_{S}
\ \Big| \
\Big(
j_{S} \in S
\Big)
\land
\Big(
j_{S} > x
\Big)
\Big\}
\Big)
\\[1em]
\underbrace{
\forall \iota \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota + 1}\big)_{(1)}}}}
:=
f(\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}})
}_{
\text{Each term of the sequence } \mathcal{J}_{{}_{[1]}{min}} \text{ represents a distinct possible value of } j_{min} \text{ in } S
}
\\[1em]
\underbrace{
\forall \iota \in \{0, 1, 2, 3, \dots, {\iota'}_{(1)}, \dots, {\iota}_{max_{(1)}}\}, \quad
\Delta_{{}_{[1]}{\big({\iota}\big)_{(1)}}}
:=
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota + 1}\big)_{(1)}}}}
-
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}}
}_{
\substack{
{
\text{Since the values of } j_{min} \text{ can be spaced apart in } S 
\text{ , there can be a distinct gap between two elements of } S
}
\\
{
\text{ and between two consecutive values of the sequence } \mathcal{J}_{{}_{[1]}{min}}
}
}
}
\end{cases}
\ \
\right)
\end{cases}
\end{array}
$$

Part 3 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\ \
\boxed{
\mathcal{J}_{{}_{[1]}{min}_{{\big({1}\big)_{(1)}}}}
}
=
f(\mathcal{J}_{{}_{[1]}{min}_{{\big({0}\big)_{(1)}}}})
=
min\Big(\Big\{
j_{S}
\ \Big| \
\Big(
j_{S} \in S
\Big)
\land
\Big(
j_{S} > \mathcal{J}_{{}_{[1]}{min}_{{\big({0}\big)_{(1)}}}}
\Big)
\Big\}
\Big)
=
\underline{
min\Big(\Big\{
\overbrace{
\mathcal{J}_{{}_{[1]}{min}_{{\big({1}\big)_{(1)}}}}
}^{\text{First element of } S}
, \
\mathcal{J}_{{}_{[1]}{min}_{{\big({2}\big)_{(1)}}}}, \
\dots, \
\overbrace{
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}}
}^{{\iota}_{(1)} \text{-th element of } S}
, \
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota + 1}\big)_{(1)}}}}, \
\dots, \
\overbrace{
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max}}\big)_{(1)}}}}
}^{\text{Last element of } S}
\Big\}
\Big)
}
=
min\Big(\Big\{
\ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({0}\big)_{(1)}}}} + \Delta_{{\big({0}\big)_{(1)}}}
\big)
, \ \ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({1}\big)_{(1)}}}} + \Delta_{{\big({1}\big)_{(1)}}}
\big)
, \ \ \
\dots, \ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota - 1}\big)_{(1)}}}} + \Delta_{{\big({\iota - 1}\big)_{(1)}}}
\big)
, \ \ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}} + \Delta_{{\big({\iota}\big)_{(1)}}}
\big)
, \ \ \
\dots, \ \ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max} - 1}\big)_{(1)}}}} + \Delta_{{\big({\iota_{max} - 1}\big)_{(1)}}}
\big)
\ \
\Big\}
\Big)
\ \
\bigg)
\\[1em]
\quad \quad
\land
\bigg(
\ \
\boxed{
\mathcal{J}_{{}_{[1]}{min}_{{\big({2}\big)_{(1)}}}}
}
=
f(\mathcal{J}_{{}_{[1]}{min}_{{\big({1}\big)_{(1)}}}})
=
min\Big(\Big\{
j_{S}
\ \Big| \
\Big(
j_{S} \in S
\Big)
\land
\Big(
j_{S} > \mathcal{J}_{{}_{[1]}{min}_{{\big({1}\big)_{(1)}}}}
\Big)
\Big\}
\Big)
=
\underline{
min\Big(\Big\{
\mathcal{J}_{{}_{[1]}{min}_{{\big({2}\big)_{(1)}}}}, \
\dots, \
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}}, \
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota + 1}\big)_{(1)}}}}, \
\dots, \
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max}}\big)_{(1)}}}}
\Big\}
\Big)
}
=
min\Big(\Big\{
\ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({1}\big)_{(1)}}}} + \Delta_{{\big({1}\big)_{(1)}}}
\big)
, \ \ \
\dots, \ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota - 1}\big)_{(1)}}}} + \Delta_{{\big({\iota - 1}\big)_{(1)}}}
\big)
, \ \ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}} + \Delta_{{\big({\iota}\big)_{(1)}}}
\big)
, \ \ \
\dots, \ \ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max} - 1}\big)_{(1)}}}} + \Delta_{{\big({\iota_{max} - 1}\big)_{(1)}}}
\big)
\ \
\Big\}
\Big)
\ \
\bigg)
\\[1em]
\quad \quad
\land
\dots
\land
\bigg(
\ \
\boxed{
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota + 1}\big)_{(1)}}}}
}
=
f(\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}})
=
min\Big(\Big\{
j_{S}
\ \Big| \
\Big(
j_{S} \in S
\Big)
\land
\Big(
j_{S} > \mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}}
\Big)
\Big\}
\Big)
=
\underline{
min\Big(\Big\{
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota + 1}\big)_{(1)}}}}, \
\dots, \
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max}}\big)_{(1)}}}}
\Big\}
\Big)
}
=
min\Big(\Big\{
\ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota}\big)_{(1)}}}} + \Delta_{{\big({\iota}\big)_{(1)}}}
\big)
, \ \ \
\dots, \ \ \
\big(
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max} - 1}\big)_{(1)}}}} + \Delta_{{\big({\iota_{max} - 1}\big)_{(1)}}}
\big)
\ \
\Big\}
\Big)
\ \
\bigg)
\\[1em]
\quad \quad
\land
\dots
\land
\bigg(
\ \
\boxed{
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max}}\big)_{(1)}}}}
}
=
f(\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max} - 1}\big)_{(1)}}}})
=
min\Big(\Big\{
j_{S}
\ \Big| \
\Big(
j_{S} \in S
\Big)
\land
\Big(
j_{S} > \mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max} - 1}\big)_{(1)}}}}
\Big)
\Big\}
\Big)
=
\underline{
min\Big(\Big\{
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max}}\big)_{(1)}}}}
\Big\}
\Big)
}
=
min\Big(\Big\{
\ \
\mathcal{J}_{{}_{[1]}{min}_{{\big({\iota_{max} - 1}\big)_{(1)}}}} + \Delta_{{\big({\iota_{max} - 1}\big)_{(1)}}}
\ \
\Big\}
\Big)
\ \
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 4 :

- From part 4 to part 26, we choose to cover as many cases as possible

	- From part 4 to part 26, we choose to scan the text $T$ from left to right and we choose to scan the current block from right to left
	
	- A "block jump" is by how many characters the first character of the pattern $P$ moves to the right in order to go to the next block on the next iteration of the algorithm

	- Thus, from part 4 to part 8, we begin by examining the following first case :

		- Starting from the current block from $j_{min}$ to $j_{min} + m - 1$ :

			- 1. We align the first character (= $t_{(j_{min} + m - 1)}$) on the far left of the pattern $P$ with the first character (= $p_{(m - 1)}$) on the far left of the current block from $j_{min}$ to $j_{min} + m - 1$ 
	
			- 2. We compare the last character of the pattern to the last character of the current block :
	
				- If the last character of the current block is not present in the pattern, then we move on to the next block from $j_{min} + m$ to $j_{min} + m + m - 1$ and 
				  we start again from step 1 (see part 4) until all the characters of the pattern correspond consecutively and respectively to all the characters of the current block
	
			- The final goal is to align the whole pattern (= $P$) with a block of the text $T$ 


	- $\boxed{{\iota}_{(2)}}$ represents the ${\iota}_{(2)}$-th time the variable $\mathcal{J}_{min}$ change its value from its previous value in the algorithm $\boxed{\text{in this specific case}}$ (similar to a recurrent sequence of order 1)
      Thus, it means that $\mathcal{J}_{{}_{[1]}min}$ and $\mathcal{J}_{{}_{[2]}min}$ are not the same sequences
	
	- Starting from this part, multisets are used because a multi-set views duplicate characters as independent characters, which provides a clear view of the operations performed 
	  on the pattern $P$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\bigg(
\Big(
t_{(0)} = \,''C''\,
\Big)
\land
\dots
\land
\Big(
t_{(n - 1)} = \,''R''\,
\Big)
\bigg)
\land
\bigg(
\Big(
p_{(0)} = \,''A''\,
\Big)
\land
\dots
\land
\Big(
p_{(m - 1)} = \,''R''\,
\Big)
\bigg)
\Bigg)
}_{\text{Example}}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
T = \ \ \ \ \ \ (
\,''C''\,, \,''\_''\,, \,''E''\,, \,''S''\,, \,''T''\,
\,''\_''\,, 
\,''U''\,, \,''N''\,,
\,''\_''\,, 
\,''A''\,, \,''S''\,, \,''C''\,, \,''E''\,, \,''N''\,, \,''S''\,, \,''E''\,, \,''U''\,, \,''R''\,
)
}_{
\text{Example of text of length } n
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
P = (
\,''A''\,, \,''S''\,, \,''C''\,, \,''E''\,, \,''N''\,, \,''S''\,, \,''E''\,, \,''U''\,, \,''R''\,
)
}_{
\text{Example of pattern of length } m
}
\Bigg)
\end{cases}
\end{array}
$$

Part 5 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
k = m - 1
\Bigg)
}_{
\substack{
{
\text{Index of the starting position of the scan}
}
\\
{
\text{from right to left}
}
}
}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({0}\big)_{(2)}}}}
\bigg)
}_{
\text{Index of the starting position of the current block}
}
\Rightarrow
\underbrace{
\overbrace{
\bigg(
t_{(0 + m - 1)} \neq p_{(m - 1)}
\bigg)
}^{
t_{(\mathcal{J}_{{}_{[2]}{min}_{(0)}} + k)}
=
t_{(0 + m - 1)}
}
}_{
\substack{
{
\text{The last character of the current block in } T
}
\\
{
\text{is not the last character of } P
}
}
}
\Rightarrow
\bigg(
\underbrace{
\Big(
\big(
t_{(0 + m - 1)} \neq p_{(m - 2)}
\big)
\land
\dots
\land
\big(
t_{(0 + m - 1)} \neq p_{(1)}
\big)
\land
\big(
t_{(0 + m - 1)} \neq p_{(0)}
\big)
\Big)
\Rightarrow
\Big(
t_{(0 + m - 1)} \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
}_{
\substack{
{
t_{(0 + m - 1)} \neq p_{(m - 1)} \text{ , and } t_{(0 + m - 1)} \text{ does not correspond to one or more characters of } P \text{ from }
}
\\
{
p_{(0)} \text{ to } p_{(m - 2)} \text{ (it does not form a whole pattern } P \text{ )}
}
}
}
\bigg)
\Rightarrow
\bigg(
\underbrace{
\Big(
\mathcal{J}_{min}
:=
0
+
m - 1 + 1
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({0}\big)_{(2)}}}}
+
m
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({1}\big)_{(2)}}}}
\Big)
}_{
\text{Index of the starting position of the next block}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
j_{min}
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota'}\big)_{(2)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(j_{min} + m - 1)} \neq p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\Big(
\big(
t_{(j_{min} + m - 1)} \neq p_{(m - 2)}
\big)
\land
\dots
\land
\big(
t_{(j_{min} + m - 1)} \neq p_{(1)}
\big)
\land
\big(
t_{(j_{min} + m - 1)} \neq p_{(0)}
\big)
\Big)
\Rightarrow
\Big(
t_{(j_{min} + m - 1)} \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\mathcal{J}_{min}
:=
j_{min}
+
m - 1 + 1
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota'}\big)_{(2)}}}}
+
m
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota' + 1}\big)_{(2)}}}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
n - m
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota_{max}}\big)_{(2)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(n - m + m - 1)} \neq p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\Big(
\big(
t_{(n - m + m - 1)} \neq p_{(m - 2)}
\big)
\land
\dots
\land
\big(
t_{(n - m + m - 1)} \neq p_{(1)}
\big)
\land
\big(
t_{(n - m + m - 1)} \neq p_{(0)}
\big)
\Big)
\Rightarrow
\Big(
t_{(n - m + m - 1)} \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 5 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({0}\big)_{(2)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \
\underbrace{
\phantom{\big(}
\,''C''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''\_''\,, \,''E''\,, \,''S''\,, \,''T''\,, \,''\_''\,, \,''U''\,, \,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
\neq p_{(m - 1)}
}
}
}
, 
\,''A''\,, \,''S''\,, \,''C''\,, \,''E''\,, \,''N''\,, \,''S''\,, \,''E''\,, \,''U''\,, \,''R''\,
\\[2em]
P \quad
\underbrace{
\phantom{\big(}
\,''A''\,
\phantom{\big)}
}_{
p_{(0)}
}
,\,''S''\,, \,''C''\,, \,''E''\,, \,''N''\,, \,''S''\,, \,''E''\,, \,''U''\,,
\underbrace{
\phantom{\big(}
\,''R''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
\\[2em]
\text{(Iteration 2) : Scanning from right to left in the current block from } t_{(0 + m - 1 + 1)} \text{ to } t_{(n - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0 + m - 1 + 1
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({1}\big)_{(2)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad
\underbrace{
\phantom{\big(}
\,''C''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''\_''\,, \,''E''\,, \,''S''\,, \,''T''\,, \,''\_''\,, \,''U''\,, \,''N''\,, \,''\_''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''A''\,
\phantom{\big)}
}_{
t_{(0 + m - 1 + 1)}
}
}^{
\substack{
{
\text{Ending}
}
\\
{
t_{(0 + m - 1 + 1)}
}
\\
{
= p_{(0)}
}
}
}
, \,''S''\,, \,''C''\,, \,''E''\,, \,''N''\,, \,''S''\,, \,''E''\,, \,''U''\,,
\overbrace{
\underbrace{
\phantom{\big(}
\,''R''\,
\phantom{\big)}
}_{
t_{(n - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(n - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
\\[2em]
P \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad
\underbrace{
\underbrace{
\phantom{\big(}
\,''A''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''S''\,, \,''C''\,, \,''E''\,, \,''N''\,, \,''S''\,, \,''E''\,, \,''U''\,,
\underbrace{
\phantom{\big(}
\,''R''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
\text{Pattern found in the block from } t_{(0 + m - 1 + 1)} \text{ to } t_{(n - 1)}
}
\end{array}
$$

Part 6 :

- In this part, we examine what happens if the text $T$ does not contain any characters from the pattern $P$ 

	- ${\iota}_{(2)}$ represents the ${\iota}_{(2)}$-th time the variable $\mathcal{J}_{min}$ change its value from its previous value in the algorithm (similar to a recurrent sequence of order 1)
	  if the text $T$ does not contain any characters from the pattern $P$ 
	
	- $\frac{n}{m}$ is the number of block of text examined in the case when the text $T$ does not contain any characters of the pattern $P$ 
	
	- $\frac{n}{m}$ is also the number of times $P$ can “fit” into $T$ without overlapping

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\underbrace{
\exists! {\iota}_{max_{(2)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\}, \quad
\mathcal{J}_{{}_{[2]}min} : \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}}\} \to \{0, \dots, n - m\}, \quad
{\iota}_{(2)} \mapsto \mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}}, \quad
\boxed{
\begin{cases}
\mathcal{J}_{{}_{[2]}{min}_{{\big({0}\big)_{(2)}}}}
=
0
\\[1em]
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}} - 1\}, \quad
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota + 1}\big)_{(2)}}}}
:=
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}} + m
\end{cases}
}
\ \
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists! {\iota}_{max_{(2)}} \in \mathbb{N}, \quad
\forall {\iota}_{(2)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(2)}, \dots, {\iota}_{max_{(2)}} - 1\}, \quad
\boxed{
\bigg(
\Big(
\big(
\underbrace{
t_{(\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}} + m - 1)}
}_{\in \varsigma}
\neq p_{(m - 1)}
\big)
\land
\big(
\underbrace{
t_{(\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}} + m - 1)}
}_{\in \varsigma}
\neq p_{(m - 2)}
\big)
\land
\dots
\land
\big(
\underbrace{
t_{(\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}} + m - 1)}
}_{\in \varsigma}
\neq p_{(1)}
\big)
\land
\big(
\underbrace{
t_{(\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}} + m - 1)}
}_{\in \varsigma}
\neq p_{(0)}
\big)
\Big)
\iff
\Big(
\ \
t_{(\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}} + m - 1)} \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\ \
\Big)
\bigg)
}
\Rightarrow
\bigg(
\underbrace{
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota + 1}\big)_{(2)}}}}
-
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}}
}_{
\Delta_{{}_{[2]}{\big({\iota}\big)_{(2)}}}
}
=
m
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\underline{
\Bigg(
\forall \alpha \in \varsigma, \quad
\bigg(
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\Delta_{{}_{[2]}{\big({\iota}\big)_{(2)}}}
=
m
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\left(
\boxed{
\bigg(
t_{(\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}} + m - 1)} \neq p_{(m - 1)}
\bigg)
}
\land
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\delta_{[1]} : \varsigma \to \mathbb{N}, \quad
\alpha \mapsto \delta_{[1]}(\alpha), \quad
\boxed{
\delta_{[1]}(\alpha)
:=
\begin{cases}
\bigg(
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta_{[1]}(\alpha)
=
\underbrace{
m
}_{
\Delta_{{}_{[2]}{\big({\iota}\big)_{(2)}}}
}
\bigg)
\end{cases}
}
\right)
\right)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{{}_{[2]}{min}_{{\big({0}\big)_{(2)}}}}
=
0
\bigg)
\land
\bigg(
\mathcal{J}_{{}_{[2]}{min}_{{\big({1}\big)_{(2)}}}}
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({0}\big)_{(2)}}}} + m
=
0 + m
=
m
\bigg)
\land
\bigg(
\mathcal{J}_{{}_{[2]}{min}_{{\big({2}\big)_{(2)}}}}
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({1}\big)_{(2)}}}} + m
=
m + m
=
2m
\bigg)
\land
\dots
\land
\bigg(
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota}\big)_{(2)}}}}
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota - 1}\big)_{(2)}}}} + m
=
{\iota}_{(2)} \cdot m
\bigg)
\land
\dots
\land
\bigg(
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota_{max}}\big)_{(2)}}}}
=
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota_{max} - 1}\big)_{(2)}}}} + m
=
{\iota}_{max_{(2)}} \cdot m
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\Big(
\mathcal{J}_{{}_{[2]}{min}_{{\big({\iota_{max}}\big)_{(2)}}}}
=
{\iota}_{max_{(2)}} \cdot m
=
n - m
\Big)
}
\iff
\Big(
{\iota}_{max_{(2)}} \cdot m
=
n - m
\Big)
\iff
\Big(
{\iota}_{max_{(2)}}
=
\frac{n - m}{m}
\Big)
\iff
\boxed{
\Big(
{\iota}_{max_{(2)}}
=
\frac{n}{m} - 1
\Big)
}
\bigg)
\Rightarrow
\boxed{
\bigg(
\Big(
{\iota}_{(2)} \in \{0, \dots, \underbrace{\frac{n}{m} - 1}_{{\iota}_{max_{(2)}}}\}
\Big)
\land
\Big(
Card(\{0, \dots, \underbrace{\frac{n}{m} - 1}_{{\iota}_{max_{(2)}}}\})
=
{\iota}_{max_{(2)}} + 1
=
\frac{n}{m}
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\Big(
\text{The maximum number of times } j_{min} \text{ can be repeated is } \frac{n}{m}
\Big)
\iff
\Big(
\text{The maximum number of times } P \text{ can be repeated in } T \text{ without overlapping is } \frac{n}{m}
\Big)
\bigg)
\because
\bigg(
\text{Each distinct position of } p_{(0)} \text{ corresponds to a possible whole pattern in } T
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 7 :

- In this part, we compute the total number of operations $\mathcal{W}_{{}_{[2]}total}$ performed before, during and after the scan of the text $T$, by comparing for each block of text the last character of 
  the block of text with each letter of the pattern

	- In this context, all the operations are performed during the scan of the text $T$ 
	
	- Here, $m$ operations are performed per block of text, because we compare (by calling the function $Cmp()$ ) for each block of text the last character of the block of text with each letter 
	  of the pattern
	
	- $\mathcal{W}_{{}_{[2]}pre}$ is the number of operations performed before the scan of the text $T$ 
	
	- $\mathcal{W}_{{}_{[2]}inter}$ is the number of operations performed during the scan of the text $T$ 
	
	- $\mathcal{W}_{{}_{[2]}pos}$ is the number of operations performed after the scan of the text $T$ 

	- $\mathcal{W}_{{}_{[2]}total}$ is the new total number of operations performed before, during and after the scan of the text $T$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\mathcal{W}_{{}_{[2]}inter}
:=
\overset{\frac{n}{m} - 1}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
\mathbb{1}\Big[
Cmp(t_{(\mathcal{J}_{{}_{[2]}{min}_{(\Psi)}} + k)}, p_{(k)})
\Big]
}
\Big)
}
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{W}_{{}_{[2]}inter}
=
\overset{\frac{n}{m} - 1}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
\mathbb{1}\Big[
Cmp(t_{(\mathcal{J}_{{}_{[2]}{min}_{(\Psi)}} + k)}, p_{(k)})
\Big]
}
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[2]}inter}
=
\overset{\frac{n}{m} - 1}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
1
}
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[2]}inter}
=
\overset{\frac{n}{m} - 1}{\underset{\Psi = 0}{\sum}}{
\Big(
\big( (m - 1) - (0) + 1 \big) \cdot 1
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[2]}inter}
=
\overset{\frac{n}{m} - 1}{\underset{\Psi = 0}{\sum}}{
\Big(
m
\Big)
}
\bigg)
\\[1em]
\iff
\bigg(
\mathcal{W}_{{}_{[2]}inter}
=
\Big(
\big( (\frac{n}{m} - 1) - 0 \big) + 1
\Big)
\cdot
\Big(
m
\Big)
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[2]}inter}
=
\Big(
\frac{n - m}{m} + \frac{m}{m}
\Big)
\cdot
\Big(
m
\Big)
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[2]}inter}
=
\frac{n}{m} \cdot m
\bigg)
\iff
\boxed{
\bigg(
\mathcal{W}_{{}_{[2]}inter}
=
n
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}_{{}_{[2]}total}
:=
\mathcal{W}_{{}_{[2]}post}
+
\mathcal{W}_{{}_{[2]}inter}
+
\mathcal{W}_{{}_{[2]}pre}
=
0 + n + 0
=
n
\Bigg)
}
\end{cases}
\end{array}
$$

Part 8 :

- In this part, we compute the new total number of operations $\mathcal{W}'_{{}_{[2]}total}$ performed before, during and after the scan of the text $T$, by performing a pre-computation phase in which we 
  compute the "block jump" before the scan of the text $T$ 
  
    - In this context, this pre-computation phase provides information in advance that the pattern $P$ will be offset to the right by $+m$ characters 
      in the text $T$ if the last letter of the current block is not in the pattern $P$ 
	
	- Here, only a single operation (which is the call to function $\delta_{[1]}(\alpha)$ ) is performed per block of text, because the tests for each block of text have already been performed during 
	  the pre-computation phase
	
	- By performing such a pre-computation phase, the total number of operations $\mathcal{W}'_{{}_{[2]}total}$ performed before, during and after the scan of the text $T$ is less than $\mathcal{W}_{{}_{[2]}total}$. 
	  It means that the algorithm does not need to perform as many operations as in the case with $\mathcal{W}_{{}_{[2]}total}$, which makes the algorithm more efficient

	- $\mathcal{W}'_{{}_{[2]}pre}$ is the new number of operations performed before the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[2]}inter}$ is the new number of operations performed during the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[2]}pos}$ is the new number of operations performed after the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[2]}total}$ is the new total number of operations performed before, during and after the scan of the text $T$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\overbrace{
\Bigg(
\underbrace{
\bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\delta_{[1]}(\alpha)
=
\begin{cases}
\bigg(
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta_{[1]}(\alpha)
=
m
\bigg)
\end{cases}
\bigg)
}_{
\text{Here, since the number of operations is equal to the number of calls to } \delta_{[1]}(\alpha)
\text{ , and since } \delta_{[1]}(\alpha) \text{ is called for every } \alpha \text{ in } \varsigma \text{ , }
\delta_{[1]}(\alpha) \text{ is called } Card(\varsigma) \text{ times}
}
\Rightarrow
\boxed{
\bigg(
\mathcal{W}'_{{}_{[2]}pre}
:=
Card(\varsigma)
\bigg)
}
\Bigg)
}^{
\text{Performed before the algorithm}
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}'_{{}_{[2]}inter}
:=
\overset{\frac{n}{m} - 1}{\underset{\Psi = 0}{\sum}}{
\Big(
\mathbb{1}\Big[
\delta_{[1]}(t_{(\mathcal{J}_{{}_{[2]}{min}_{(\Psi)}} + m - 1)})
\Big]
\Big)
}
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{W}'_{{}_{[2]}inter}
=
\overset{\frac{n}{m} - 1}{\underset{\Psi = 0}{\sum}}{
\Big(
\mathbb{1}\Big[
\delta_{[1]}(t_{(\mathcal{J}_{{}_{[2]}{min}_{(\Psi)}} + m - 1)})
\Big]
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}'_{{}_{[2]}inter}
=
\overset{\frac{n}{m} - 1}{\underset{\Psi = 0}{\sum}}{
\Big(
1
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}'_{{}_{[2]}inter}
=
\Big(
\big( (\frac{n}{m} - 1) - 0 \big) + 1
\Big)
\cdot
\Big(
1
\Big)
\bigg)
\iff
\boxed{
\bigg(
\mathcal{W}'_{{}_{[2]}inter}
=
\frac{n}{m}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}'_{{}_{[2]}total}
:=
\mathcal{W}'_{{}_{[2]}post}
+
\mathcal{W}'_{{}_{[2]}inter}
+
\mathcal{W}'_{{}_{[2]}pre}
=
0 + \frac{n}{m} + Card(\varsigma)
=
\frac{n}{m} + Card(\varsigma)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 9 :

- From part 9 to part 11, since we choose to cover as many cases as possible, we examine the following case :

	- (English) Starting from the current block from $j_{min}$ to $j_{min} + m - 1$ :

		- 1. We align the first character (= $t_{(j_{min} + m - 1)}$) on the far left of the pattern $P$ with the first character (= $p_{(m - 1)}$) on the far left of the current block from $j_{min}$ to $j_{min} + m - 1$ 

		- 2. We compare the last character of the pattern to the last character of the current block :

			- 2.1. If there is a correspondence between the last character of the pattern and the last character of the current block, then we move on to the step 3 (see part 12)
		  
			- 2.2. If there is no correspondence between the two, then we align the last character of the current block with its first occurrence on the far right in the pattern 
			  (= "first occurrence of the last character of the block"), by offsetting the pattern to the right (= in order to enable alignment). If 2.2 is satisfied, then we 
			  move on to the next block from $j_{min} + m - 1 - \beta'$ to $(j_{min} + m - 1 - \beta') + m - 1$, and we start again from step 1 (see part 9) until all the characters of the pattern 
			  correspond consecutively and respectively to all the characters of the current block. If 2.2 is not satisfied, then we move on to the step 2.3
			  
			- 2.3. If the last character of the current block is not present in the pattern, then we move on to the next block from $j_{min} + m$ to $j_{min} + m + m - 1$ and 
			  we start again from step 1 (see part 9) until all the characters of the pattern correspond consecutively and respectively to all the characters of the current block


		- The final goal is to align the whole pattern (= $P$) with a block of the text $T$ 


	- (French) En partant du bloc courant allant $j_{min}$ à $j_{min} + m - 1$ :

		- 1. On aligne le premier caractère (= $t_{(j_{min} + m - 1)}$) tout à gauche du motif $P$ avec le premier caractère (= $p_{(m - 1)}$) tout à gauche du bloc courant allant de $j_{min}$ à $j_{min} + m - 1$ 
		
		- 2. On compare le dernier caractère du motif au dernier caractère du bloc courant :

			- 2.1. S'il y a une correspondance entre le dernier caractère du motif et la dernier caractère du bloc courant, alors on passe à l'étape 3 (voir partie 12)

			- 2.2. S'il n'y a aucune correspondance entre les deux, alors on aligne le dernier caractère du bloc courant avec sa première occurrence la plus à droite dans le motif 
			  (= "première occurrence du dernier caractère de bloc"), en décalant le motif vers la droite (= pour permettre l'alignement). Si la 2.2 est satisfaite, alors on 
			  passe au bloc suivant allant de $j_{min} + m - 1 - \beta'$ à $(j_{min} + m - 1 - \beta') + m - 1$, et on recommence à partir de l'étape 1 (voir partie 9) jusqu'à ce que tous les caractères 
			  du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant. Si la 2.2 n'est pas satisfaite, alors on passe à l'étape 2.3

			- 2.3. Si le dernier caractère du bloc courant n'est pas présent dans le motif, alors on passe au bloc suivant allant de $j_{min} + m$ à $j_{min} + m + m - 1$ et  
			  on recommence à partir de l'étape 1 (voir partie 9) jusqu'à ce que tous les caractères du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant

		
		- L'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 

	
	- Whatever the iteration, the first character on the far left of the pattern is always aligned with the first character on the far left of the current block


	- $\boxed{{\iota}_{(3)}}$ represents the ${\iota}_{(3)}$-th time the variable $\mathcal{J}_{min}$ change its value from its previous value in the algorithm $\boxed{\text{in this specific case}}$ (similar to a recurrent sequence of order 1)
      Thus, it means that $\mathcal{J}_{{}_{[1]}min}$, $\mathcal{J}_{{}_{[2]}min}$ and $\mathcal{J}_{{}_{[3]}min}$ are not the same sequences

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\bigg(
\Big(
t_{(0)} = \,''L''\,
\Big)
\land
\dots
\land
\Big(
t_{(n - 1)} = \,''E''\,
\Big)
\bigg)
\land
\bigg(
\Big(
p_{(0)} = \,''P''\,
\Big)
\land
\dots
\land
\Big(
p_{(m - 1)} = \,''E''\,
\Big)
\bigg)
\Bigg)
}_{\text{Example}}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
T = \ \ (
\,''L''\,, \,''A''\,, 
\,''\_''\,, 
\,''P''\,, \,''O''\,, \,''I''\,, \,''R''\,, \,''E''\,
)
}_{
\text{Example of text of length } n
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
P = (
\,''P''\,, \,''O''\,, \,''I''\,, \,''R''\,, \,''E''\,
)
}_{
\text{Example of pattern of length } m
}
\Bigg)
\end{cases}
\end{array}
$$

Part 10 :

- $\beta'$ is the index (= position) of the occurrence ( = occurrence of the last character of the current block) most to the right in the pattern $P$ 

- In other words, $\beta'$ is the index (= position) of the “first occurrence of the last character of the current block” in the pattern $P$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
k = m - 1
\Bigg)
}_{
\substack{
{
\text{Index of the starting position of the scan}
}
\\
{
\text{from right to left}
}
}
}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({0}\big)_{(3)}}}}
\bigg)
}_{
\text{Index of the starting position of the current block}
}
\Rightarrow
\underbrace{
\overbrace{
\bigg(
t_{(0 + m - 1)} \neq p_{(m - 1)}
\bigg)
}^{
t_{(\mathcal{J}_{{}_{[3]}{min}_{(0)}} + k)}
=
t_{(0 + m - 1)}
}
}_{
\substack{
{
\text{The last character of the current block in } T
}
\\
{
\text{is not the last character of } P
}
}
}
\Rightarrow
\bigg(
\underbrace{
\exists \beta \in \{1, \dots, m - 1\}
}_{
\substack{
{
\text{For this case to be defined, }
}
\\
{
\text{we assume that there is at least one } \beta
}
}
}
, \quad
\underbrace{
\Big(
t_{(0 + m - 1)} = p_{(m - 1 - \beta)}
\Big)
\Rightarrow
\Big(
t_{(0 + m - 1)} \in \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
}_{
\substack{
{
\text{Since } t_{(0 + m - 1)} \neq p_{(m - 1)} \text{ , } t_{(0 + m - 1)} \text{ can potentially correspond to one or more characters of } P \text{ from }
}
\\
{
p_{(0)} \text{ to } p_{(m - 2)} \text{ (it can form potentially a whole pattern } P \text{ which have one or more characters from }
}
\\
{
p_{(0)} \text{ to } p_{(m - 2)} \text{ superimposed on the character } t_{(0 + m - 1)} \text{ )}
}
}
}
\bigg)
\Rightarrow
\bigg(
\underbrace{
\Big(
\big(
(
\beta = 1
\Rightarrow
m - 1 - \beta
=
m - 2
)
\land
(
\beta = m - 1
\Rightarrow
m - 1 - \beta
=
0
)
\big)
\Rightarrow
\big(
\overbrace{
m - 1 - \beta
}^{:= \gamma}
\in \{0, \dots, m - 2\}
\big)
\Big)
}_{
\text{Since } t_{(0 + m - 1)} \neq p_{(m - 1)} \text{ , } m - 1 - \beta \text{ can be the index of a character from } p_{(0)} \text{ to } p_{(m - 2)}
}
\Rightarrow
\underbrace{
\Big(
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
t_{(0 + m - 1)}
\land
\gamma < m - 1
\Big\}
\Big)
}_{
\text{Because the scan goes from right to left, we take the "first occurrence of the last character"}
}
\Rightarrow
\underbrace{
\Big(
\mathcal{J}_{min}
:=
0
+
m - 1 - \beta'
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({0}\big)_{(3)}}}}
+
m - 1 - \beta'
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({1}\big)_{(3)}}}}
\Big)
}_{
\text{Index of the starting position of the next block}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
j_{min}
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota'}\big)_{(3)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(j_{min} + m - 1)} \neq p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \beta \in \{1, \dots, m - 1\}
, \quad
\Big(
t_{(j_{min} + m - 1)} = p_{(m - 1 - \beta)}
\Big)
\Rightarrow
\Big(
t_{(j_{min} + m - 1)} \in \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\big(
(
\beta = 1
\Rightarrow
m - 1 - \beta
=
m - 2
)
\land
(
\beta = m - 1
\Rightarrow
m - 1 - \beta
=
0
)
\big)
\Rightarrow
\big(
m - 1 - \beta
\in \{0, \dots, m - 2\}
\big)
\Big)
\Rightarrow
\Big(
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
t_{(j_{min} + m - 1)}
\land
\gamma < m - 1
\Big\}
\Big)
\Rightarrow
\Big(
\mathcal{J}_{min}
:=
j_{min}
+
m - 1 - \beta'
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota'}\big)_{(3)}}}}
+
m - 1 - \beta'
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota' + 1}\big)_{(3)}}}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
n - m
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota_{max}}\big)_{(3)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(n - m + m - 1)} \neq p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \beta \in \{1, \dots, m - 1\}
, \quad
\Big(
t_{(n - m + m - 1)} = p_{(m - 1 - \beta)}
\Big)
\Rightarrow
\Big(
t_{(n - m + m - 1)} \in \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 10 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({0}\big)_{(3)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \
\underbrace{
\phantom{\big(}
\,''L''\,
\phantom{\big)}
}_{
t_{(0)}
}
, 
\phantom{\big(}
\,''A''\,
\phantom{\big)}
, \,''\_''\,, \,''P''\,,
\overbrace{
\underbrace{
\phantom{\big(}
\,''O''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
\neq p_{(m - 1)}
}
}
}
, 
\,''I''\,, \,''R''\,, \,''E''\,
\\[2em]
P \quad
\underbrace{
\phantom{\big(}
\,''P''\,
\phantom{\big)}
}_{
p_{(0)}
}
,
\overbrace{
\underbrace{
\phantom{\big(}
\,''O''\,
\phantom{\big)}
}_{
p_{(0 + m - 1 - \beta)}
}
}^{
\substack{
{
t_{(0 + m - 1)}
}
\\
{
= p_{(m - 1 - \beta)}
}
}
}
, 
\,''I''\,, \,''R''\,, 
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
\\[2em]
\text{(Iteration 2) : Scanning from right to left in the current block from } t_{(0 + m - 1 - \beta')} \text{ to } t_{(n - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0 + m - 1 - \beta'
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({1}\big)_{(3)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad
\underbrace{
\phantom{\big(}
\,''L''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''A''\,, \,''\_''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''P''\,
\phantom{\big)}
}_{
t_{(0 + m - 1 - \beta')}
}
}^{
\substack{
{
\text{Ending}
}
\\
{
t_{(0 + m - 1 - \beta')}
}
\\
{
= p_{(0)}
}
}
}
\,''O''\,, \,''I''\,, \,''R''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(n - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(n - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
\\[2em]
P \quad \quad \quad \quad \quad \quad \quad \quad
\underbrace{
\underbrace{
\phantom{\big(}
\,''P''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''O''\,, \,''I''\,, \,''R''\,, 
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
\text{Pattern found in the block from } t_{(0 + m - 1 - \beta')} \text{ to } t_{(n - 1)}
}
\end{array}
$$

Part 11 :

- $\delta_{[2]}(\alpha)$ is called the "table of the non-corresponding character"

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\underbrace{
\exists! {\iota}_{max_{(3)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(3)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(3)}, \dots, {\iota}_{max_{(3)}}\}, \quad
\mathcal{J}_{{}_{[3]}min} : \{0, 1, 2, 3, \dots, {\iota'}_{(3)}, \dots, {\iota}_{max_{(3)}}\} \to \{0, \dots, n - m\}, \quad
{\iota}_{(3)} \mapsto \mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}}, \quad
\begin{cases}
\mathcal{J}_{{}_{[3]}{min}_{{\big({0}\big)_{(3)}}}}
=
0
\\[1em]
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
:=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
t_{(\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}} + m - 1)}
\land
\gamma < m - 1
\Big\}
\Big)
\\[1em]
\forall {\iota}_{(3)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(3)}, \dots, {\iota}_{max_{(3)}} - 1\}, \quad
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota + 1}\big)_{(3)}}}}
:=
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}} + m - 1 - \beta'
\end{cases}
\ \
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists! {\iota}_{max_{(3)}} \in \mathbb{N}, \quad
\forall {\iota}_{(3)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(3)}, \dots, {\iota}_{max_{(3)}} - 1\}, \quad
\boxed{
\bigg(
\quad
\Big(
\big(
\underbrace{
t_{(\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}} + m - 1)}
}_{\in \varsigma}
\neq p_{(m - 1)}
\big)
\land
\big(
\exists \beta \in \{1, \dots, m - 1\}, \quad
\underbrace{
t_{(\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}} + m - 1)}
}_{\in \varsigma}
= p_{(m - 1 - \beta)}
\big)
\Big)
\Rightarrow
\Big(
t_{(\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}} + m - 1)} \in \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
\quad
\bigg)
}
\Rightarrow
\bigg(
\underbrace{
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota + 1}\big)_{(3)}}}}
-
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}}
}_{
\Delta_{{}_{[3]}{\big({\iota}\big)_{(3)}}}
}
=
m - 1 - \beta'
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\left(
\boxed{
\bigg(
t_{(\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}} + m - 1)} \neq p_{(m - 1)}
\bigg)
}
\land
\left(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\delta_{[2]} : \varsigma \to \mathbb{N}, \quad
\alpha \mapsto \delta_{[2]}(\alpha), \quad
\boxed{
\delta_{[2]}(\alpha)
:=
\begin{cases}
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\bigg(
\beta'
:=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
\alpha
\land
\gamma < m - 1
\Big\}
\Big)
\bigg)
\Rightarrow
\bigg(
\delta_{[2]}(\alpha)
=
\underbrace{
m - 1 - \beta'
}_{
\Delta_{{}_{[3]}{\big({\iota}\big)_{(3)}}}
}
\bigg)
\\[1em]
\bigg(
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta_{[2]}(\alpha)
=
\underbrace{
m
}_{
\Delta_{{}_{[2]}{\big({\iota}\big)_{(2)}}}
}
\bigg)
\end{cases}
}
\ \
\right)
\right)
\end{cases}
\end{array}
$$

Part 12 :

- From part 12 to part 17, since we choose to cover as many cases as possible, we examine the following case :

	- (English) Starting from the current block from $j_{min}$ to $j_{min} + m - 1$ :

		- 3. If several characters of the pattern (forming a "pattern suffix") correspond consecutively and respectively to several characters of the current block (forming a "text suffix") and if 
		  the last character of the pattern (= the previous character of the pattern when moving to the left) does not correspond, then we move on to the step 4

		- 4. We look to see if the "pattern suffix" is present another time in the pattern just before itself (itself = the "pattern suffix") :

			- 4.1. If so, the new "pattern suffix" is aligned with the position of the "text suffix" by offsetting the pattern (to enable alignment). The offset of the pattern forms a new block 
			  which will be examined in the next iteration.
			  This new "pattern suffix" forms potentially a whole pattern in a new block that needs to be examined in the next iteration. 
	          Indeed, the final goal is to align the whole pattern (= $P$) with a block of the text $T$ 
	
			- 4.2. If not, then we go straight to step 7 (see part 18)

		- 5. We move on to the next block from $j_{min} + m - 1 - \Lambda$ to $(j_{min} + m - 1 - \Lambda) + m - 1$ 

		- 6. We start again from step 1 (see part 9) until all the characters in the pattern correspond consecutively and respectively to all the characters of the current block

		  The final goal is to align the whole pattern (= $P$) with a block of the text $T$ 


	- (French) En partant du bloc courant allant $j_{min}$ à $j_{min} + m - 1$ :
	
		- 3. Si plusieurs caractères du motif (formant un "suffixe de motif") correspondent d'affilée et respectivement à plusieurs caractères du bloc courant (formant un "suffixe de texte") et 
		  que le dernier caractère du motif (= caractère précédent du motif en allant vers la gauche) ne correspond pas, alors on passe à l'étape 4

		- 4. On regarde si le "suffixe de motif" est présent une nouvelle fois dans le motif juste avant lui-même (lui-même = le "suffixe de motif") :

			- 4.1. Si oui, alors on aligne le nouveau "suffixe de motif" sur la position du "suffixe de texte" en décalant le motif (pour permettre l'alignement). Le décalage du motif forme un 
			  nouveau bloc qui sera examiné à l'itération suivante.
			  Ce nouveau "suffixe de motif" forme potentiellement un motif entier dans un nouveau bloc qui a besoin d'être examiné à l'itération suivante. 
			  En effet, l'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 
			  
			- 4.2. Si non, alors on passe directement à l'étape 7 (voir partie 17)

		- 5. On passe au bloc suivant allant de $j_{min} + m - 1 - \Lambda$ à $(j_{min} + m - 1 - \Lambda) + m - 1$ 

		- 6. On recommence à partir de l'étape 1 (voir partie 9) jusqu'à ce que tous les caractères du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant

		  L'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 


	- $\xi$ is an index (which we will call the "boundary position") :
	
		- $\xi$ is an index denoting a position (which is never the end of the current block) in the current block, located to the right of the current block. This position corresponds to the boundary 
		  where the pattern suffix ends, and the character at this position is not a character of the pattern suffix. All characters located after (to the right of) this position are characters of the 
		  pattern suffix

	- $\boxed{{\iota}_{(4)}}$ represents the ${\iota}_{(4)}$-th time the variable $\mathcal{J}_{min}$ change its value from its previous value in the algorithm $\boxed{\text{in this specific case}}$ (similar to a recurrent sequence of order 1)
      Thus, it means that $\mathcal{J}_{{}_{[1]}min}$, $\mathcal{J}_{{}_{[2]}min}$, $\mathcal{J}_{{}_{[3]}min}$ and $\mathcal{J}_{{}_{[4]}min}$ are not the same sequences

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
\bigg(
\Big(
t_{(0)} = \,''I''\,
\Big)
\land
\dots
\land
\Big(
t_{(n - 1)} = \,''T''\,
\Big)
\bigg)
\land
\bigg(
\Big(
p_{(0)} = \,''\_''\,
\Big)
\land
\dots
\land
\Big(
p_{(m - 1)} = \,''T''\,
\Big)
\bigg)
\Bigg)
}_{\text{Example}}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
T = \ \ \ (\,''I''\,, \,''L''\,, \,''S''\,, \,''\_''\,, \,''P''\,, \,''R''\,, \,''E''\,, \,''S''\,, \,''E''\,, \,''N''\,, \,''T''\,, \,''E''\,, \,''N''\,, \,''T''\,)
}_{
\text{Example of text of length } n
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
P = (\,''\_''\,, \,''P''\,, \,''R''\,, \,''E''\,, \,''S''\,, \,''E''\,, \,''N''\,, \,''T''\,, \,''E''\,, \,''N''\,, \,''T''\,)
}_{
\text{Example of pattern of length } m
}
\Bigg)
\\[1em]
\Rightarrow
\underbrace{
\Bigg(
k = m - 1
\Bigg)
}_{
\substack{
{
\text{Index of the starting position of the scan}
}
\\
{
\text{from right to left}
}
}
}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\bigg)
}_{
\text{Index of the starting position of the current block}
}
\Rightarrow
\underbrace{
\bigg(
t_{(0 + m - 1)} = p_{(m - 1)}
\bigg)
}_{
\substack{
{
\text{The last character of the current block in } T
}
\\
{
\text{is the last character of } P
}
}
}
\Rightarrow
\bigg(
\underbrace{
\exists \xi \in \{0, \dots, m - 2\}
}_{
\substack{
{
\text{For this case to be defined, }
}
\\
{
\text{we assume that there is at least one } \xi
}
}
}
, \quad
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\Big)
}_{
\substack{
{
\text{The character } t_{(0 + \xi)} \text{ of the current block in } T
}
\\
{
\text{is not the character } p_{(\xi)} \text{ of } P
}
}
}
\Rightarrow
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\land
t_{(0 + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(0 + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(0 + m - 2)} = p_{(m - 2)}
\land
t_{(0 + m - 1)} = p_{(m - 1)}
\Big)
}_{
\substack{
{
\text{The characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)} \text{ of the pattern } P
\text{ (forming a “pattern suffix”) correspond consecutively and respectively }
}
\\
{
\text{ to the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the text } T 
\text{ (characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ forming a “text suffix”)}
}
\\
{
\text{The character } p_{(\xi)} \text{ of the pattern } P \text{ does not correspond to the character } t_{(0 + \xi)} \text{ of the text } T
}
\\
{
\text{The characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the current block in } T \text{ are respectively the characters } p_{(m - 1)} \text{ to } 
p_{(\xi + 1)} \text{ of } P \text{ (it forms potentially a whole pattern } P
}
\\
{
\text{ which have its characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)}
\text{ superimposed on the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ )}
}
}
}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 12 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \ 
\underbrace{
\phantom{\big(}
\,''I''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''L''\,, \,''S''\,, \,''\_''\,, \,''P''\,, \,''R''\,, \,''E''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''S''\,
\phantom{\big)}
}_{
t_{(0 + \xi)}
}
}^{
\substack{
{
t_{(0 + \xi)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(0 + \xi + 1)}
}
}^{
\substack{
{
t_{(0 + \xi + 1)}
}
\\
{
= p_{(\xi)}
}
}
}
, \,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
, \,''E''\,, \,''N''\,, \,''T''\,
\\[2em]
P \quad 
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''P''\,, \,''R''\,, \,''E''\,, \,''S''\,, \,''E''\,, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(\xi)}
}
, 
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\xi + 1)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
\end{array}
$$

Diagram 2 of part 12 :

$$
\begin{array}{l}
\begin{array}{c|}
T
\\
\\
P
\\
\\
\end{array}
\ \ \
\overbrace{
\begin{array}{cccccccccccccccccccc}
t_{(0)} & \dots & t_{(\psi - 1)} & t_{(\psi)} & t_{(\psi + 1)} & \dots & t_{(\lambda - 1)} & t_{(\lambda)} & \dots & t_{(0 + \xi - 1)} & t_{(0 + \xi)} & t_{(0 + \xi + 1)} & t_{(0 + \xi + 2)} & \dots & t_{(0 + m - 2)} & t_{(0 + m - 1)}
\\
/ & \dots & / & / & / & \dots & / & / & \dots & / & \neq & = & = & \dots & = & =
\\
p_{(0)} & \dots & p_{(\psi - 1)} & p_{(\psi)} & p_{(\psi + 1)} & \dots & p_{(\lambda - 1)} & p_{(\lambda)} & \dots & p_{(\xi - 1)} & p_{(\xi)} & p_{(\xi + 1)} & p_{(\xi + 2)} & \dots & p_{(m - 2)} & p_{(m - 1)}
\\
\\
\end{array}
}^{
\text{Current block (first iteration) = block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ ( with } \mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}} = 0 \text{ ) in } T
}
\ \ \
\begin{array}{cccc}
t_{(m = 0 + (m - 1) + 1)} & t_{(m + 1)} & \dots & t_{(n - 1)}
\\
/ & / & \dots & /
\\
/ & / & \dots & /
\\
\\
\end{array}
\end{array}
$$

Part 13 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\underbrace{
\exists! t_{(0 + \xi + 1)}, t_{(0 + \xi + 2)}, \dots, t_{(0 + m - 2)}, t_{(0 + m - 1)} \in \varsigma
}_{
\text{There is a unique combination of characters in the current block}
}
, \quad
\underbrace{
\Big(
t_{(0 + \xi + 1)} \in \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
\land
\Big(
t_{(0 + \xi + 2)} \in \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
\land
\dots
\land
\Big(
t_{(0 + m - 2)} \in \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
\land
\Big(
t_{(0 + m - 1)} \in \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)} \Big\}\Big\}_{M}
\Big)
}_{
\text{Each character } t_{(0 + \xi + 1)} \text{ to } t_{(0 + m - 1)} \text{ is present in the pattern } P
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists! t_{(0 + \xi + 1)}, t_{(0 + \xi + 2)}, \dots, t_{(0 + m - 2)}, t_{(0 + m - 1)} \in \varsigma, \quad
\underbrace{
\Big(
t_{(0 + \xi + 1)} \in \Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\Big)
\land
\Big(
t_{(0 + \xi + 2)} \in \Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\Big)
\land
\dots
\land
\Big(
t_{(0 + m - 2)} \in \Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\Big)
\land
\Big(
t_{(0 + m - 1)} \in \Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\Big)
}_{
\text{Each character } t_{(0 + \xi + 1)} \text{ to } t_{(0 + m - 1)} \text{ is present in the pattern } P \text{ and is present in the pattern suffix}
\text{ formed by the characters } p_{(\xi + 1)} \text{ to } p_{(m - 1)}
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\boxed{
B_{P_{suffix_{(1)}}}
}
:=
\Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
}_{
\text{The pattern suffix can be viewed as a multiset of characters of } P
}
\land
\underbrace{
\bigg(
\boxed{
B_{T_{suffix_{(1)}}}
}
:=
\Big\{\Big\{ t_{(0 + \xi + 1)}, t_{(0 + \xi + 2)}, \dots, t_{(0 + m - 2)}, t_{(0 + m - 1)} \Big\}\Big\}_{M}
\bigg)
}_{
\text{The text suffix can be viewed as a multiset of characters of } T
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\boxed{
Card\Big(
B_{P_{suffix_{(1)}}}
\Big)
}
=
(m - 1) - (\xi + 1) + 1
=
m - 1 - \xi - 1 + 1
=
\boxed{
m - 1 - \xi
}
\bigg)
}_{
\substack{
{
\ \because \
\Big(
Card\big(
\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}
\big)
=
(\text{endingIndex} - \text{startingIndex}) + 1
\Big)
}
\\
{
\iff
\Big(
\text{startingIndex}
=
\text{endingIndex}
-
Card\big(
\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}
\big)
+
1
\Big)
}
}
}
\land
\underbrace{
\bigg(
\boxed{
Card\Big(
B_{T_{suffix_{(1)}}}
\Big)
}
=
(m - 1) - (\xi + 1) + 1
=
m - 1 - \xi - 1 + 1
=
\boxed{
m - 1 - \xi
}
\bigg)
}_{
\substack{
{
\ \because \
\Big(
Card\big(
\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}
\big)
=
(\text{endingIndex} - \text{startingIndex}) + 1
\Big)
}
\\
{
\iff
\Big(
\text{startingIndex}
=
\text{endingIndex}
-
Card\big(
\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}
\big)
+
1
\Big)
}
}
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\boxed{
\Bigg(
Card\Big(
B_{P_{suffix_{(1)}}}
\Big)
\in \{1, \dots, m - 1\}
\Bigg)
}
\because
\Bigg(
\bigg(
\xi \in \{0, \dots, m - 2\}
\bigg)
\land
\bigg(
\Big(
\boxed{
\xi = m - 2
}
\Rightarrow
\boxed{
Card\big(
B_{P_{suffix_{(1)}}}
\big)
}
=
m - 1 - (\xi + 1) + 1
=
m - 1 - (m - 1) + 1
=
\boxed{
1
}
\Big)
\land
\Big(
\boxed{
\xi = 0
}
\Rightarrow
\boxed{
Card\big(
B_{P_{suffix_{(1)}}}
\big)
}
=
m - 1 - (\xi + 1) + 1
=
m - 1 - (1) + 1
=
\boxed{
m - 1
}
\Big)
\bigg)
\Bigg)
\ \
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\underbrace{
\bigg(
\exists! P_{suffix_{(1)}} \in \varsigma^{m - 1 - \xi}, \quad
P_{suffix_{(1)}}
:=
(p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)})
\bigg)
}_{
P_{suffix_{(1)}} \text{ is the unique pattern suffix of the current block and can be viewed as a } (m - 1 - \xi) \text{-tuple of characters}
}
\land
\underbrace{
\bigg(
\exists! T_{suffix_{(1)}} \in \varsigma^{m - 1 - \xi}, \quad
T_{suffix_{(1)}}
:=
(t_{(0 + \xi + 1)}, t_{(0 + \xi + 2)}, \dots, t_{(0 + m - 2)}, t_{(0 + m - 1)})
\bigg)
}_{
T_{suffix_{(1)}} \text{ is the unique text suffix of the current block and can be viewed as a } (m - 1 - \xi) \text{-tuple of characters}
}
\Bigg)
}
\end{cases}
\end{array}
$$

Diagram 1 of part 13 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\begin{array}{c|}
T
\\
\\
P
\\
\\
P_{suffix_{(1)}}
\\
\\
T_{suffix_{(1)}}
\\
\\
\end{array}
\ \ \
\overbrace{
\begin{array}{cccccccccccccccccccc}
t_{(0)} & \dots & t_{(\psi - 1)} & t_{(\psi)} & t_{(\psi + 1)} & \dots & t_{(\lambda - 1)} & t_{(\lambda)} & \dots & t_{(0 + \xi - 1)} & t_{(0 + \xi)} & t_{(0 + \xi + 1)} & t_{(0 + \xi + 2)} & \dots & t_{(0 + m - 2)} & t_{(0 + m - 1)}
\\
/ & \dots & / & / & / & \dots & / & / & \dots & / & \neq & = & = & \dots & = & =
\\
p_{(0)} & \dots & p_{(\psi - 1)} & p_{(\psi)} & p_{(\psi + 1)} & \dots & p_{(\lambda - 1)} & p_{(\lambda)} & \dots & p_{(\xi - 1)} & p_{(\xi)} & p_{(\xi + 1)} & p_{(\xi + 2)} & \dots & p_{(m - 2)} & p_{(m - 1)}
\\
\\
 &  &  &  &  &  &  &  &  &  &  & p_{(\xi + 1)} & p_{(\xi + 2)} & \dots & p_{(m - 2)} & p_{(m - 1)}
\\
\\
 &  &  &  &  &  &  &  &  &  &  & t_{(0 + \xi + 1)} & t_{(0 + \xi + 2)} & \dots & t_{(0 + m - 2)} & t_{(0 + m - 1)}
\\
\\
\end{array}
}^{
\text{Current block (first iteration) = block from position } 0 \text{ to position } 0 + m - 1
\text{ ( with } \mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}} = 0 \text{ ) in } T
}
\ \ \
\begin{array}{cccc}
t_{(m = 0 + (m - 1) + 1)} & t_{(m + 1)} & \dots & t_{(n - 1)}
\\
/ & / & \dots & /
\\
/ & / & \dots & /
\\
\\
\\
\\
\\
\\
\end{array}
\right)
\end{cases}
\end{array}
$$

Part 14 :

- (French) Explications pour $\lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\} \land \psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}$ :
	
	- Pour un balayage de droite à gauche en partant de la fin du bloc courant :
		
		- Si plusieurs lettres du motif (formant un "suffixe de motif") correspondent d'affilée et respectivement à plusieurs lettres du bloc courant (lettres du bloc formant un 
		  "suffixe de texte") et que la dernière lettre inspectée (= balayée) du motif ne correspond pas à la dernière lettre inspectée du bloc courant, alors :
	
			- L'objectif est de regarder si le "suffixe de motif" est présent une nouvelle fois dans le motif juste avant lui-même (lui-même = le "suffixe de motif"). 
			  Si le "suffixe de motif" est présent une ou plusieurs autres fois, alors on dit qu'on a trouvé (à chaque présence) une "occurrence du suffixe de motif"

			- Comme on a choisi de faire un balayage de droite à gauche, on a besoin de trouver la "première occurrence du suffixe de motif" dans le motif pour pouvoir la tester directement. 
			  En effet, la "première occurrence du suffixe de motif" peut potentiellement former un motif entier dans un nouveau bloc qui a besoin d'être examiné à l'itération suivante


			- Comme les première et dernière lettres du "suffixe de motif" sont repérées respectivement par un indice distinct dans le motif, alors les première et dernière lettres de la 
			  "première occurrence du suffixe de motif" peuvent également être repérées respectivement par un indice distinct


			- Si on pose $\psi$ comme étant l'indice de la première lettre de la "première occurrence du suffixe de motif" et si on pose $\lambda$ comme étant l'indice de la dernière lettre de 
			  la "première occurrence du suffixe de motif", alors :
	
				- Dans un cas optimal, la "première occurrence du suffixe de motif" est collée (collée ne signifie pas superposée) au "suffixe de motif" à gauche :
	
					- Cela signifie que $p_{(\xi)}$ est la dernière lettre (repérée par l'indice $\xi$) de la "première occurrence du suffixe de motif". De plus, toute "occurrence du suffixe de motif" 
					 a la même longueur que le "suffixe de motif"
					 
					 On peut ensuite calculer l'indice $\psi$ de la première lettre de la "première occurrence du suffixe de motif" en utilisant la formule :
	                 $Card\big(\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}\big) = (\text{endingIndex} - \text{startingIndex}) + 1$ 
	                 Ainsi $\psi = \xi - Card(B_{P_{suffix_{(1)}}}) + 1$ 

					- Cela signifie que la dernière lettre de la "première occurrence du suffixe de motif" est à la position $\xi$ dans le motif. Comme la dernière lettre de 
					  la "première occurrence du suffixe de motif" est repérée par l'indice $\xi$, alors $\lambda = \xi$ 


				- Dans un cas non-optimal, la "première occurrence du suffixe de motif" est au tout début du motif :
	
					- Cela signifie que la première lettre de la "première occurrence du suffixe de motif" est à la position 0 dans le motif. Comme la première lettre de 
					  la "première occurrence du suffixe de motif" est repérée par l'indice $\psi$, alors $\psi = 0$ 

					- En partant de l'indice 0, on peut ensuite calculer l'indice $\lambda$ de la dernière lettre de la "première occurrence du suffixe de motif" en utilisant la formule :
	                  $Card\big(\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}\big) = (\text{endingIndex} - \text{startingIndex}) + 1$ 
	                  Ainsi $\lambda = 0 + Card(B_{P_{suffix_{(1)}}}) - 1$ 

- (French) Explications pour $p_{(\psi - 1)} \neq p_{(\xi)}$ :

	- Comme la dernière lettre inspectée du motif ne correspond pas à la dernière lettre inspectée du bloc, on a besoin d'une lettre différente de $p_{(\xi)}$ pour augmenter la probabilité 
	  (en ne conservant pas $p_{(\xi)}$) de trouver une correspondance entre la lettre $p_{(\psi - 1)}$ du motif $P$ et la lettre $t_{(0 + \xi)}$ du texte $T$ 
	
	- En effet, l'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 
	
	- A l'itération suivante, $p_{(\psi - 1)}$ est aligné avec $t_{(0 + \xi)}$ car le motif est décalé

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\ \
\underbrace{
\forall n \in \mathbb{N}_{\geq 1}
}_{
\substack{
{
\text{For any text } T \text{ containing}
}
\\
{
\text{at least one character}
}
}
}
, \quad
\underbrace{
\forall m \in \{1, \dots, n\}
}_{
\substack{
{
\text{For any pattern } P \text{ containing}
}
\\
{
\text{at least one character}
}
}
}
, \quad
\underbrace{
\forall \xi \in \{0, \dots, m - 2\}
}_{
\text{For any boundary position } \xi
}
, \quad
\underbrace{
\exists \lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\}
}_{
\substack{
{
\text{There is at least one "index of the last character of the occurrence of } P_{suffix_{(1)}} \text{",}
}
\\
{
\text{since there is at least one "occurrence of } P_{suffix_{(1)}} \text{".}
}
\\
{
\text{Since } P_{suffix_{(1)}} \text{ is formed by at least 1 character (which is } p_{(m - 1)} \text{), each "occurrence of}
}
\\
{
P_{suffix_{(1)}} \text{ " has a minimum of 1 character and the first occurrence can be present just}
}
\\
{
\text{before } P_{suffix_{(1)}} \text{ (we can have } p_{(\lambda)} = p_{(m - 2)} \text{ and } \lambda = m - 2 \text{). If each occurrence has at most}
}
\\
{
\text{1 character, then the last character of each is also the first character of each. We can also }
}
\\
{
\text{have a unique occurrence that has at most 1 letter and that is present only at position 0 in } P
}
\\
{
\text{ (we can have } p_{(\lambda)} = p_{(0)} \text{ and } \lambda = 0 \text{)}
}
}
}
, \quad
\underbrace{
\exists \psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}
}_{
\substack{
{
\text{There is at least one "index of the first character of the occurrence of } P_{suffix_{(1)}} \text{",}
}
\\
{
\text{since there is at least one "occurrence of } P_{suffix_{(1)}} \text{".}
}
\\
{
\text{If each occurrence of } P_{suffix_{(1)}} \text{ has at most 1 character, then the last character}
}
\\
{
\text{of each is also the first character of each (we can have } p_{(\lambda)} = p_{(\psi)} \text{ and } \lambda = \psi \text{)}
}
\\
{
\text{We can also have a unique occurrence that has at most 1 letter and that is}
}
\\
{
\text{present only at position 0 in } P \text{ (we can have } p_{(\lambda)} = p_{(\psi)} = p_{(0)} \text{ and } \lambda = \psi = 0 \text{)}
}
}
}
, \quad
\underbrace{
\bigg(
p_{(\lambda)}
\in \Big\{\Big\{ p_{(0 + Card(B_{P_{suffix_{(1)}}}) - 1)}, \dots, p_{(\xi)} \Big\}\Big\}_{M}
\subset
\Big\{\Big\{ p_{(0)}, \dots, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{The last character of each "occurrence of } P_{suffix_{(1)}} \text{" is present in the part of } P \text{ formed by}
}
\\
{
\text{the characters } p_{(0 + Card(B_{P_{suffix_{(1)}}}) - 1)} \text{ to } p_{(\xi)}
}
}
}
\land
\underbrace{
\bigg(
p_{(\psi)}
\in \Big\{\Big\{ p_{(0)}, \dots, p_{(\xi - Card(B_{P_{suffix_{(1)}}}) + 1)} \Big\}\Big\}_{M}
\subset
\Big\{\Big\{ p_{(0)}, \dots, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{The first character of each "occurrence of } P_{suffix_{(1)}} \text{" is present in the part of } P \text{ formed by}
}
\\
{
\text{the characters } p_{(0)} \text{ to } p_{(\xi - Card(B_{P_{suffix_{(1)}}}) + 1)}
}
}
}
\\[1em]
\quad
\land
\underbrace{
\bigg(
Card\Big(
\Big\{\Big\{ p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)} \Big\}\Big\}_{M}
\Big)
=
\overbrace{
Card\Big(
\Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\Big)
}^{
Card(B_{P_{suffix_{(1)}}})
}
\bigg)
}_{
\text{Each "occurrence of } P_{suffix_{(1)}} \text{" has the same length as } P_{suffix_{(1)}}
}
\land
\underbrace{
\bigg(
\Big(
p_{(\psi)}
=
p_{(\xi + 1)}
\Big)
\land
\Big(
p_{(\psi + 1)}
=
p_{(\xi + 2)}
\Big)
\land
\dots
\land
\Big(
p_{(\lambda - 1)}
=
p_{(m - 2)}
\Big)
\land
\Big(
p_{(\lambda)}
=
p_{(m - 1)}
\Big)
\bigg)
}_{
\text{Each "occurrence of } P_{suffix_{(1)}} \text{" has exactly the same characters as } P_{suffix_{(1)}}
}
\\[1em]
\quad
\land
\bigg(
\Big(
0 \leq \psi \leq \lambda
\Big)
\because
\Big(
Card\big(
B_{P_{suffix_{(1)}}}
\big)
\in \{1, \dots, m - 1\}
\Big)
\bigg)
\land
\underbrace{
\bigg(
\boxed{
\Big(
p_{(\psi - 1)} \neq p_{(\xi)}
\Big)
}
\because
\Big(
p_{(\psi - 1)} = p_{(\xi)}
\Rightarrow
t_{(0 + \xi)} \neq p_{(\psi - 1)}
\Big)
\bigg)
}_{
\substack{
{
\text{Since the final goal is to have } P \text{ fully superimposed on a block of the text, and since }
}
\\
{
t_{(0 + \xi)} \neq p_{(\xi)} \text{ , we need a character other than } p_{(\xi)} \text{ to increase the probability}
}
\\
{
\text{(by not keeping } p_{(\xi)} \text{ ) of finding a correspondence between the character } p_{(\psi - 1)} \text{ and } t_{(0 + \xi)}
}
\\
{
\text{in the next iteration}
}
}
}
\ \
\Bigg)
\end{cases}
\end{array}
$$

Part 15 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\bigg(
\psi
=
\lambda - Card(B_{P_{suffix_{(1)}}}) + 1
\bigg)
}
\because
\bigg(
\Big(
Card\big(
\Big\{\Big\{ p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)} \Big\}\Big\}_{M}
\big)
=
Card\big(
B_{P_{suffix_{(1)}}}
\big)
\Big)
\land
\underbrace{
\Big(
Card\big(
\Big\{\Big\{ p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)} \Big\}\Big\}_{M}
\big)
=
(\lambda - \psi) + 1
\Big)
}_{
Card\big(
\big\{ \text{startingIndex}, \dots, \text{endingIndex} \big\}
\big)
=
(\text{endingIndex} - \text{startingIndex}) + 1
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\Big(
\psi \geq 0
\Big)
}
\iff
\Big(
\lambda - Card(B_{P_{suffix_{(1)}}}) + 1 \geq 0
\Big)
\iff
\Big(
\lambda
\geq
Card(B_{P_{suffix_{(1)}}}) - 1
\Big)
\bigg)
\land
\bigg(
\Big(
\psi \geq 0
\Big)
\iff
\Big(
\underbrace{\psi - 1}_{\in \mathbb{Z}} \geq - 1
\Big)
\iff
\boxed{
\Big(
\underbrace{
\overbrace{
\big(
\psi - 1 > - 1
\big)
}^{
\iff \psi - 1 \geq 0
}
}_{
\substack{
{
\text{There is at least one character }
}
\\
{
\text{(which is at least } p_{(\psi - 1)} \text{ )}
}
\\
{
\text{ that precedes the character } p_{(\psi)}
}
}
}
\lor
\underbrace{
\big(
\psi - 1 = - 1
\big)
}_{
\substack{
{
\text{No character precedes } p_{(\psi)}
}
\\
{
\text{Thus } p_{(\psi)} \text{ is the first character}
}
\\
{
\text{ of } P \text{ and } p_{(\psi)} = p_{(0)}
}
}
}
\Big)
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
\boxed{\exists} \lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\}, \quad
\boxed{\exists} \psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}, \quad
\boxed{
\underbrace{
\bigg(
\exists P_{suffix_{(2)}} \in \varsigma^{m - 1 - \xi}, \quad
P_{suffix_{(2)}}
:=
(p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)})
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{suffix_{(2)}} \text{ (= one possible occurrence of } P_{suffix_{(1)}} \text{ )}
}
\\
{
\text{ in the current block and each } P_{suffix_{(2)}} \text{ can be viewed as a } (m - 1 - \xi) \text{-tuple of characters in } P
}
}
}
\land
\underbrace{
\bigg(
B_{P_{suffix_{(2)}}}
:=
\Big\{\Big\{ p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{suffix_{(2)}} \text{ (= one possible occurrence of } P_{suffix_{(1)}} \text{ )}
}
\\
{
\text{ in the current block and each } P_{suffix_{(2)}} \text{ can also be viewed as a multiset of characters in } P
}
}
}
\land
\underbrace{
\bigg(
Card(B_{P_{suffix_{(2)}}})
=
Card(B_{P_{suffix_{(1)}}})
\bigg)
}_{
\text{Each } P_{suffix_{(2)}} \text{ has the same length as } P_{suffix_{(1)}}
}
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\underbrace{
\bigg(
P_{suffix_{(2)}}
=
(p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)})
=
(p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)})
=
P_{suffix_{(1)}}
\bigg)
}_{
\text{Each } P_{suffix_{(2)}} \text{ has exactly the same characters as } P_{suffix_{(1)}}
}
}
\because
\bigg(
\Big(
p_{(\psi)}
=
p_{(\xi + 1)}
\Big)
\land
\Big(
p_{(\psi + 1)}
=
p_{(\xi + 2)}
\Big)
\land
\dots
\land
\Big(
p_{(\lambda - 1)}
=
p_{(m - 2)}
\Big)
\land
\Big(
p_{(\lambda)}
=
p_{(m - 1)}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
\exists \lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\}, \quad
\exists \psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}, \quad
\exists P_{suffix_{(2)}} \in \varsigma^{m - 1 - \xi}, \quad
\boxed{
\bigg(
P_{suffix_{(2)}}
=
(p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)})
=
(p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)})
=
P_{suffix_{(1)}}
\bigg)
\land
\underbrace{
\bigg(
\Big(
\psi - 1 \geq 0
\Big)
\Rightarrow
\Big(
p_{(\psi - 1)} \neq p_{(\xi)}
\Big)
\bigg)
}_{
\substack{
{
\text{If } P_{suffix_{(2)}} \text{is preceded by at least one character in } P \text{, then }
}
\\
{
\text{there is } p_{(\psi - 1)} \text{ and } p_{(\psi - 1)} \neq p_{(\xi)}
}
\\
{
\text{If } \psi - 1 = -1 \text{, then } P_{suffix_{(2)}} \text{ is flush with the left edge of } P
}
}
}
}
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 15 :

$$
\begin{array}{l}
\begin{array}{c|}
T
\\
\\
P
\\
\\
P_{suffix_{(1)}}
\\
\\
P_{suffix_{(2)}}
\\
\\
T_{suffix_{(1)}}
\\
\\
\end{array}
\ \ \
\overbrace{
\begin{array}{cccccccccccccccccccc}
t_{(0)} & \dots & t_{(\psi - 1)} & t_{(\psi)} & t_{(\psi + 1)} & \dots & t_{(\lambda - 1)} & t_{(\lambda)} & \dots & t_{(0 + \xi - 1)} & t_{(0 + \xi)} & t_{(0 + \xi + 1)} & t_{(0 + \xi + 2)} & \dots & t_{(0 + m - 2)} & t_{(0 + m - 1)}
\\
/ & \dots & / & / & / & \dots & / & / & \dots & / & \neq & = & = & \dots & = & =
\\
p_{(0)} & \dots & p_{(\psi - 1)} & p_{(\psi)} & p_{(\psi + 1)} & \dots & p_{(\lambda - 1)} & p_{(\lambda)} & \dots & p_{(\xi - 1)} & p_{(\xi)} & p_{(\xi + 1)} & p_{(\xi + 2)} & \dots & p_{(m - 2)} & p_{(m - 1)}
\\
\\
 &  &  &  &  &  &  &  &  &  &  & p_{(\xi + 1)} & p_{(\xi + 2)} & \dots & p_{(m - 2)} & p_{(m - 1)}
\\
\\
 &  &  & p_{(\psi)} & p_{(\psi + 1)} & \dots & p_{(\lambda - 1)} & p_{(\lambda)}
\\
\\
 &  &  &  &  &  &  &  &  &  &  & t_{(0 + \xi + 1)} & t_{(0 + \xi + 2)} & \dots & t_{(0 + m - 2)} & t_{(0 + m - 1)}
\\
\\
\end{array}
}^{
\text{Current block (first iteration) = block from position } 0 \text{ to position } 0 + m - 1
\text{ ( with } \mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}} = 0 \text{ ) in } T
}
\ \ \
\begin{array}{cccc}
t_{(m = 0 + (m - 1) + 1)} & t_{(m + 1)} & \dots & t_{(n - 1)}
\\
/ & / & \dots & /
\\
/ & / & \dots & /
\\
\\
\\
\\
\\
\\
\\
\\
\end{array}
\end{array}
$$

Diagram 2 of part 15 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \ 
\underbrace{
\phantom{\big(}
\,''I''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''L''\,, \,''S''\,, \,''\_''\,, 
\phantom{\big(}
\,''P''\,
\phantom{\big)}
, 
\phantom{\big(}
\,''R''\,
\phantom{\big)}
, \,''E''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''S''\,
\phantom{\big)}
}_{
t_{(0 + \xi)}
}
}^{
\substack{
{
t_{(0 + \xi)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\underbrace{
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(0 + \xi + 1)}
}
}^{
\substack{
{
t_{(0 + \xi + 1)}
}
\\
{
= p_{(\xi)}
}
}
}
, \,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
}_{
T_{suffix_{(1)}}
}
, \,''E''\,, \,''N''\,, \,''T''\,
\\[2em]
P \quad 
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''P''\,, \,''R''\,, \,''E''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''S''\,
\phantom{\big)}
}_{
p_{(\psi - 1)}
}
}^{
\substack{
{
p_{(\psi - 1)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\psi)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(\lambda)}
=
p_{(\xi)}
}
}_{
P_{suffix_{(2)}}
}
, 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\xi + 1)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
P_{suffix_{(1)}}
}
\end{array}
$$

Part 16 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{suffixpos_{(\xi)}}
:=
\underbrace{
\bigg\{
\lambda
\ \bigg| \
\bigg(
\psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}
\bigg)
\land
\bigg(
\lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\}
\bigg)
\land
\bigg(
P_{suffix_{(2)}}
=
(p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)})
=
(p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)})
=
P_{suffix_{(1)}}
\bigg)
\land
\bigg(
\Big(
\psi - 1 \geq 0
\Big)
\Rightarrow
\Big(
p_{(\psi - 1)} \neq p_{(\xi)}
\Big)
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{suffixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{suffix_{(2)}} \text{, where } P_{suffix_{(2)}}
\text{ can be preceded by at least one character in } P \text{, or can be flushed with the left edge of } P
}
\ \
\Bigg)
\\[1em]
\Rightarrow
\underbrace{
\Bigg(
\bigg(
\Big(
t_{(0)} = \,''I''\,
\Big)
\land
\dots
\land
\Big(
t_{(n - 1)} = \,''T''\,
\Big)
\bigg)
\land
\bigg(
\Big(
p_{(0)} = \,''\_''\,
\Big)
\land
\dots
\land
\Big(
p_{(m - 1)} = \,''T''\,
\Big)
\bigg)
\Bigg)
}_{\text{Example}}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
T = \ \ \ (\,''I''\,, \,''L''\,, \,''S''\,, \,''\_''\,, \,''P''\,, \,''R''\,, \,''E''\,, \,''S''\,, \,''E''\,, \,''N''\,, \,''T''\,, \,''E''\,, \,''N''\,, \,''T''\,)
}_{
\text{Example of text of length } n
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
P = (\,''\_''\,, \,''P''\,, \,''R''\,, \,''E''\,, \,''S''\,, \,''E''\,, \,''N''\,, \,''T''\,, \,''E''\,, \,''N''\,, \,''T''\,)
}_{
\text{Example of pattern of length } m
}
\Bigg)
\end{cases}
\end{array}
$$

Part 17 :

- If there is at least one occurrence of $P_{suffix_{(1)}}$ in $P$, then $\Lambda$ is the index (= position) of the last letter (= letter most to the right) of the "first occurrence of $P_{suffix_{(1)}}$" 
  (= occurrence most to the right) in the pattern $P$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
k = m - 1
\Bigg)
}_{
\substack{
{
\text{Index of the starting position of the scan}
}
\\
{
\text{from right to left}
}
}
}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\bigg)
}_{
\text{Index of the starting position of the current block}
}
\Rightarrow
\underbrace{
\bigg(
t_{(0 + m - 1)} = p_{(m - 1)}
\bigg)
}_{
\substack{
{
\text{The last character of the current block in } T
}
\\
{
\text{is the last character of } P
}
}
}
\Rightarrow
\bigg(
\underbrace{
\exists \xi \in \{0, \dots, m - 2\}
}_{
\substack{
{
\text{For this case to be defined, }
}
\\
{
\text{we assume that there is at least one } \xi
}
}
}
, \quad
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\Big)
}_{
\substack{
{
\text{The character } t_{(0 + \xi)} \text{ of the current block in } T
}
\\
{
\text{is not the character } p_{(\xi)} \text{ of } P
}
}
}
\Rightarrow
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\land
t_{(0 + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(0 + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(0 + m - 2)} = p_{(m - 2)}
\land
t_{(0 + m - 1)} = p_{(m - 1)}
\Big)
}_{
\substack{
{
\text{The characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)} \text{ of the pattern } P
\text{ (forming a “pattern suffix”) correspond consecutively and respectively }
}
\\
{
\text{ to the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the text } T 
\text{ (characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ forming a “text suffix”)}
}
\\
{
\text{The character } p_{(\xi)} \text{ of the pattern } P \text{ does not correspond to the character } t_{(0 + \xi)} \text{ of the text } T
}
\\
{
\text{The characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the current block in } T \text{ are respectively the characters } p_{(m - 1)} \text{ to } 
p_{(\xi + 1)} \text{ of } P \text{ (it forms potentially a whole pattern } P
}
\\
{
\text{ which have its characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)}
\text{ superimposed on the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ )}
}
}
}
\bigg)
\Rightarrow
\bigg(
\underbrace{
\Big(
P_{suffixpos_{(\xi)}} \neq \emptyset
\Big)
\Rightarrow
\Big(
\exists! \Lambda \in \{0, \dots, m - 2\}, \quad
\Lambda
:=
max\big(
P_{suffixpos_{(\xi)}}
\big)
\Big)
}_{
\substack{
{
\text{If there is at least one occurrence of } P_{suffix_{(1)}} \text{ in } P \text{ , then we take the index of the last letter }
}
\\
{
\text{of the first occurrence of } P_{suffix_{(1)}} \text{ (the occurrence most to the right, so we use } max \text{ function ),}
}
\\
{
\text{ as the scan goes from right to left}
}
}
}
\Rightarrow
\underbrace{
\Big(
\mathcal{J}_{min}
:=
0
+
m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
+
m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({1}\big)_{(4)}}}}
\Big)
}_{
\text{Index of the start position of the next block}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
j_{min}
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota'}\big)_{(4)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(j_{min} + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \xi \in \{0, \dots, m - 2\}, \quad
\Big(
t_{(j_{min} + \xi)} \neq p_{(\xi)}
\Big)
\Rightarrow
\Big(
t_{(j_{min} + \xi)} \neq p_{(\xi)}
\land
t_{(j_{min} + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(j_{min} + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(j_{min} + m - 2)} = p_{(m - 2)}
\land
t_{(j_{min} + m - 1)} = p_{(m - 1)}
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
P_{suffixpos_{(\xi)}} \neq \emptyset
\Big)
\Rightarrow
\Big(
\exists! \Lambda \in \{0, \dots, m - 2\}, \quad
\Lambda
:=
max\big(
P_{suffixpos_{(\xi)}}
\big)
\Big)
\Rightarrow
\Big(
\mathcal{J}_{min}
:=
j_{min}
+
m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota'}\big)_{(4)}}}}
+
m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota' + 1}\big)_{(4)}}}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
n - m
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota_{max}}\big)_{(4)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(n - m + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \xi \in \{0, \dots, m - 2\}, \quad
\Big(
t_{(n - m + \xi)} \neq p_{(\xi)}
\Big)
\Rightarrow
\Big(
t_{(n - m + \xi)} \neq p_{(\xi)}
\land
t_{(n - m + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(n - m + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(n - m + m - 2)} = p_{(m - 2)}
\land
t_{(n - m + m - 1)} = p_{(m - 1)}
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 17 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \ 
\underbrace{
\phantom{\big(}
\,''I''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''L''\,, \,''S''\,, \,''\_''\,, 
\phantom{\big(}
\,''P''\,
\phantom{\big)}
, 
\phantom{\big(}
\,''R''\,
\phantom{\big)}
, \,''E''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''S''\,
\phantom{\big)}
}_{
t_{(0 + \xi)}
}
}^{
\substack{
{
t_{(0 + \xi)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\underbrace{
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(0 + \xi + 1)}
}
}^{
\substack{
{
t_{(0 + \xi + 1)}
}
\\
{
= p_{(\xi)}
}
}
}
, \,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
}_{
T_{suffix_{(1)}}
}
, \,''E''\,, \,''N''\,, \,''T''\,
\\[2em]
P \quad 
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''P''\,, \,''R''\,, \,''E''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''S''\,
\phantom{\big)}
}_{
p_{(\psi - 1)}
}
}^{
\substack{
{
p_{(\psi - 1)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\psi)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(\lambda)}
=
p_{(\xi)}
}
}_{
P_{suffix_{(2)}}
}
, 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\xi + 1)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
P_{suffix_{(1)}}
}
\\[2em]
\text{(Iteration 2) : Scanning from right to left in the current block from } t_{(0 + m - 1 - \Lambda)} \text{ to } t_{(n - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0 + m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({1}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \ \ \ \ \ 
\underbrace{
\phantom{\big(}
\,''I''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''L''\,, \,''S''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
t_{(0 + m - 1 - \Lambda)}
}
}^{
\substack{
{
\text{Ending}
}
\\
{
t_{(0 + m - 1 - \Lambda)}
}
\\
{
= p_{(0)}
}
}
}
, \,''P''\,, \,''R''\,, \,''E''\,, 
\,''S''\,
, 
\,''E''\,
, \,''N''\,, 
\,''T''\,
, \,''E''\,, \,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(n - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(n - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
\\[2em]
P \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad 
\underbrace{
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''P''\,, \,''R''\,, \,''E''\,, \,''S''\,, \,''E''\,, \,''N''\,, 
\,''T''\,
, 
\,''E''\,
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
\text{Pattern found in the block from } t_{(0 + m - 1 - \Lambda)} \text{ to } t_{(n - 1)}
}
\end{array}
$$

Part 18 :

- From part 18 to part 22, since we choose to cover as many cases as possible, we examine the following case :

	- (English) If no "occurrence of $P_{suffix_{(1)}}$" are found in $P$ :

		- Starting from the current block from $j_{min}$ to $j_{min} + m - 1$ :
	
			- 7. If several characters of the pattern (forming a "pattern suffix") correspond consecutively and respectively to several characters of the current block (forming a "text suffix") 
			 and if the last character of the pattern (= the previous character of the pattern when moving to the left) does not correspond, then we move on to the step 8

			- 8. We look to see if the "longest prefix of the pattern" is also the longest suffix of the "pattern suffix". In other words, we look to see if the start of the pattern 
			  corresponds to the end of the "pattern suffix" :
		
				- 8.1. If so, the "longest prefix of the pattern" is aligned with the position of the "text suffix" by offsetting the pattern (to enable alignment). The offset of the pattern forms 
				 a new block which will be examined in the next iteration
				 This "longest prefix of the pattern" forms potentially a whole pattern in a new block that needs to be examined in the next iteration. 
		         Indeed, the final goal is to align the whole pattern (= $P$) with a block of the text $T$ 
	
				- 8.2. If not, then we go straight to step 11 (see part 23)

			- 9. We move on to the next block from $j_{min} + m - 1 - \Lambda$ to $(j_{min} + m - 1 - \Lambda) + m - 1$ 

			- 10. We start again from step 1 (see part 9) until all the characters of the pattern correspond consecutively and respectively to all the characters of the current block
	
			  The final goal is to align the whole pattern (= $P$) with a block of the text $T$ 
	

	- (French) Si aucune "occurrence de $P_{suffix_{(1)}}$" n'est trouvée dans $P$ :

		- En partant du bloc courant allant $j_{min}$ à $j_{min} + m - 1$ :
		
			- 7. Si plusieurs caractères du motif (formant un "suffixe de motif") correspondent d'affilée et respectivement à plusieurs caractères du bloc courant (formant un "suffixe de texte") 
			 et que le dernier caractère du motif (= caractère précédent du motif en allant vers la gauche) ne correspond pas, alors on passe à l'étape 8

			- 8. On regarde si le "plus grand préfixe du motif" est aussi le plus grand suffixe du "suffixe de motif". Autrement dit, on regarde si le début du motif correspond à la fin 
			  du "suffixe de motif" :

				- 8.1. Si oui, alors on aligne le "plus grand suffixe du motif" sur la position du "suffixe de texte" en décalant le motif (pour permettre l'alignement). Le décalage du motif forme 
				  un nouveau bloc qui sera examiné à l'itération suivante
				  Ce "plus grand suffixe du motif" forme potentiellement un motif entier dans un nouveau bloc qui a besoin d'être examiné à l'itération suivante. 
				  En effet, l'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 
	
				- 8.2. Si non, alors on passe directement à l'étape 11 (voir partie 23)

			- 9. On passe au bloc suivant allant de $j_{min} + m - 1 - \Lambda$ à $(j_{min} + m - 1 - \Lambda) + m - 1$ 

			- 10. On recommence à partir de l'étape 1 (voir partie 9) jusqu'à ce que tous les caractères du motif correspondent d'affilée et respectivement à tous les caractères du bloc courant
	
			  L'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 


	- $\xi$ is an index (which we will call the "boundary position") :
	
		- $\xi$ is an index denoting a position (which is never the end of the current block) in the current block, located to the right of the current block. This position corresponds to the boundary 
		  where the pattern suffix ends, and the character at this position is not a character of the pattern suffix. All characters located after (to the right of) this position are characters of the 
		  pattern suffix

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
\bigg(
\Big(
t_{(0)} = \,''D''\,
\Big)
\land
\dots
\land
\Big(
t_{(n - 1)} = \,''T''\,
\Big)
\bigg)
\land
\bigg(
\Big(
p_{(0)} = \,''E''\,
\Big)
\land
\dots
\land
\Big(
p_{(m - 1)} = \,''T''\,
\Big)
\bigg)
\Bigg)
}_{\text{Example}}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
T = \ \ \ \ \ \ \ (
\,''D''\,, \,''E''\,, \,''S''\,, \,''\_''\,,
\,''V''\,, \,''O''\,, \,''I''\,, \,''E''\,, \,''S''\,,
\,''\_''\,, \,''D''\,, \,''\_''\,,
\,''E''\,, \,''N''\,, \,''T''\,, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,
)
}_{
\text{Example of text of length } n
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
P = (
\,''E''\,, \,''N''\,, \,''T''\,, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,
)
}_{
\text{Example of pattern of length } m
}
\Bigg)
\\[1em]
\Rightarrow
\underbrace{
\Bigg(
k = m - 1
\Bigg)
}_{
\substack{
{
\text{Index of the starting position of the scan}
}
\\
{
\text{from right to left}
}
}
}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\bigg)
}_{
\text{Index of the starting position of the current block}
}
\Rightarrow
\underbrace{
\bigg(
t_{(0 + m - 1)} = p_{(m - 1)}
\bigg)
}_{
\substack{
{
\text{The last character of the current block in } T
}
\\
{
\text{is the last character of } P
}
}
}
\Rightarrow
\bigg(
\underbrace{
\exists \xi \in \{0, \dots, m - 2\}
}_{
\substack{
{
\text{For this case to be defined, }
}
\\
{
\text{we assume that there is at least one } \xi
}
}
}
, \quad
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\Big)
}_{
\substack{
{
\text{The character } t_{(0 + \xi)} \text{ of the current block in } T
}
\\
{
\text{is not the character } p_{(\xi)} \text{ of } P
}
}
}
\Rightarrow
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\land
t_{(0 + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(0 + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(0 + m - 2)} = p_{(m - 2)}
\land
t_{(0 + m - 1)} = p_{(m - 1)}
\Big)
}_{
\substack{
{
\text{The characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)} \text{ of the pattern } P
\text{ (forming a “pattern suffix”) correspond consecutively and respectively }
}
\\
{
\text{ to the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the text } T 
\text{ (characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ forming a “text suffix”)}
}
\\
{
\text{The character } p_{(\xi)} \text{ of the pattern } P \text{ does not correspond to the character } t_{(0 + \xi)} \text{ of the text } T
}
\\
{
\text{The characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the current block in } T \text{ are respectively the characters } p_{(m - 1)} \text{ to } 
p_{(\xi + 1)} \text{ of } P \text{ (it forms potentially a whole pattern } P
}
\\
{
\text{ which have its characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)}
\text{ superimposed on the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ )}
}
}
}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 18 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \ \ \ \
\underbrace{
\phantom{\big(}
\,''D''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''E''\,, \,''S''\,, \,''\_''\,,
\,''V''\,, \,''O''\,, \,''I''\,, \,''E''\,, \,''S''\,,
\,''\_''\,, \,''D''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
t_{(0 + \xi)}
}
}^{
\substack{
{
t_{(0 + \xi)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(0 + \xi + 1)}
}
}^{
\substack{
{
t_{(0 + \xi + 1)}
}
\\
{
= p_{(\xi)}
}
}
}
\,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,
\\[2em]
P \quad 
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''N''\,, \,''T''\,, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, 
\underbrace{
\phantom{\big(}
\,''M''\,
\phantom{\big)}
}_{
p_{(\xi)}
}
, 
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\xi + 1)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
\end{array}
$$

Diagram 2 of part 18 :

$$
\begin{array}{l}
\begin{array}{c|}
T
\\
\\
P
\\
\\
\end{array}
\ \ \
\overbrace{
\begin{array}{ccccccccccccc}
t_{(0)} & t_{(1)} & \dots & t_{(\lambda' - 1)} & t_{(\lambda')} & \dots & t_{(0 + \xi - 1)} & t_{(0 + \xi)} & t_{(0 + \xi + 1)} & t_{(0 + \xi + 2)} & \dots & t_{(0 + m - 2)} & t_{(0 + m - 1)}
\\
/ & / & \dots & / & / & \dots & / & \neq & = & = & \dots & = & =
\\
p_{(0)} & p_{(1)} & \dots & p_{(\lambda' - 1)} & p_{(\lambda')} & \dots & p_{(\xi - 1)} & p_{(\xi)} & p_{(\xi + 1)} & p_{(\xi + 2)} & \dots & p_{(m - 2)} & p_{(m - 1)}
\\
\\
\end{array}
}^{
\text{Current block (first iteration) = block from position } 0 \text{ to position } 0 + m - 1
\text{ ( with } \mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}} = 0 \text{ ) in } T
}
\ \ \
\begin{array}{cccc}
t_{(m = 0 + (m - 1) + 1)} & t_{(m + 1)} & \dots & t_{(n - 1)}
\\
/ & / & \dots & /
\\
/ & / & \dots & /
\\
\\
\end{array}
\end{array}
$$

Part 19 :

- (French) Explications pour $\lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\} \land \psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}$ :

	- Pour un balayage de droite à gauche en partant de la fin du bloc courant :
		
		- Si plusieurs lettres du motif (formant un "suffixe de motif") correspondent d'affilée et respectivement à plusieurs lettres du bloc courant (lettres du bloc courant formant un 
		  "suffixe de texte") et que la dernière lettre inspectée (= balayée) du motif ne correspond pas à la dernière lettre inspectée du bloc courant, alors :


			- L'objectif est de regarder si le "plus grand préfixe du motif" est aussi le plus grand suffixe du "suffixe de motif" :

				- Autrement dit, on regarde si le début du motif correspond à la fin du "suffixe de motif".
				  Le "plus grand préfixe du motif" est lui-même constitué de "plus petits préfixes du motif". Si le "plus grand préfixe du motif" est aussi le plus grand suffixe du "suffixe de motif", 
				  alors les "plus petits préfixes du motif" sont aussi des plus petits suffixes du "suffixe de motif"
				  
				- Pour généraliser, on choisit d'appeler ces types de préfixe des "préfixes de motif".
				  Si plusieurs "préfixe de motif" sont présents, alors on dit qu'on a trouvé (à chaque présence) une "occurrence du préfixe de motif" (distincte donc unique)


				- Si on coulisse le "suffixe de motif" de sorte à ce que la dernière lettre du "suffixe de motif" coulisse jusqu'à l'une des premières lettres du motif (premières lettres du motif 
				  = lettres les plus à gauche dans le motif qui ne sont pas des lettres du "suffixe de motif"), alors la partie située avant la première lettre du motif 
				  (première lettre du motif = lettre la plus à gauche dans le motif) déborde du motif. 
				  Chaque coulissage du "suffixe de motif" peut ainsi être vu comme une "occurrence débordante du suffixe de motif"

				- Chaque "occurrence du préfixe de motif" peut être vue comme une "occurrence débordante du suffixe de motif" dont la partie située avant la première lettre du motif 
				  (première lettre du motif = lettre la plus à gauche dans le motif) a été supprimée


			- Le "plus grand préfixe du motif" est appelé la "première occurrence du préfixe de motif"




			- Comme on a choisi de faire un balayage de droite à gauche, on a besoin de trouver la "première occurrence du préfixe de motif" dans le motif pour pouvoir la tester directement. 
			  En effet, la "première occurrence du préfixe de motif" peut potentiellement former un motif entier dans un nouveau bloc qui a besoin d'être examiné à l'itération suivante


			- Comme les première et dernière lettres du "suffixe de motif" sont repérées respectivement par un indice distinct dans le motif, alors les première et dernière lettres d'une 
			  "occurrence débordante du suffixe de motif" peuvent également être repérées respectivement par un indice distinct


			- Si on pose $\psi'$ comme étant l'indice de la première lettre d'une "occurrence débordante du suffixe de motif" et si on pose $\lambda'$ comme étant l'indice de la dernière lettre d'une 
			  "occurrence débordante du suffixe de motif", alors :

				- Dans un cas optimal, une "occurrence débordante du suffixe de motif" a uniquement sa première lettre (située avant la première lettre du motif) qui déborde du motif :

					- Cela signifie que la première lettre d'une telle "occurrence débordante du suffixe de motif" est à la position -1 dans le motif. En effet, la première lettre du motif est 
					  en position 0. Comme la première lettre d'une telle "occurrence débordante du suffixe de motif" est repérée par l'indice $\psi'$, alors $\psi' = -1$ 


					- En partant de l'indice 0 (= sans prendre en compte l'indice -1 = en le retirant), cela signifie qu'on a littéralement le "plus grand préfixe du motif", car il est de longueur 
					  égale à $Card(B_{P_{suffix_{(1)}}}) - 1$ 
					  Toujours en partant de l'indice 0 (= sans prendre en compte l'indice -1), on peut ensuite calculer l'indice $\lambda'$ de la dernière lettre d'une telle 
					  "occurrence débordante du suffixe de motif" en utilisant la formule :
	                  $Card\big(\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}\big) = (\text{endingIndex} - \text{startingIndex}) + 1$ 
	                  Ainsi $\lambda' = (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1$, et $\lambda'$ est aussi l'indice de la dernière lettre du "plus grand préfixe du motif"


				- Dans un cas non-optimal, une "occurrence débordante du suffixe de motif" a toutes ses lettres sauf sa lettre la plus à droite 
				  (les lettres étant situées avant la première lettre du motif) qui débordent du motif :

					- Pour obtenir la position de la première lettre d'une telle "occurrence débordante du suffixe de motif", on fait coulisser le "suffixe de motif" de sorte que la 
					  dernière lettre du "suffixe de motif" coulisse jusqu'à la première lettre du motif (première lettre du motif = lettre la plus à gauche dans le motif)
					  
					  Le coulissage de la dernière lettre du "suffixe de motif" est équivalent à effectuer un déplacement de l'indice $m - 1$ à la position 0. 
					  Le coulissage de la première lettre du "suffixe de motif" est équivalent à venir soustraire "le déplacement de l'indice $m - 1$ à la position $\xi + 1$ " au 
					  "résultat du déplacement de l'indice $m - 1$ à la position 0" :
					  $X = \underbrace{m - 1 - Card(P) + 1}_{\text{sliding last letter}}$ 
					  $Y = \underbrace{X - Card(B_{P_{suffix_{(1)}}}) + 1}_{\text{sliding first letter}}$ 
					  Cela signifie que la première lettre d'une telle "occurrence débordante du suffixe de motif" est à la position $Y$. Comme la première lettre d'une telle 
					  "occurrence débordante du suffixe de motif" est repérée par l'indice $\psi'$, alors $\psi' = Y$ 


					- Cela signifie que la dernière lettre d'une telle "occurrence débordante du suffixe de motif" est à la position 0 dans le motif. En effet, la première lettre du motif est 
					  en position 0. Comme la dernière lettre d'une telle "occurrence débordante du suffixe de motif" est repérée par l'indice $\lambda'$, alors $\lambda' = 0$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\ \
\underbrace{
\forall n \in \mathbb{N}_{\geq 1}
}_{
\substack{
{
\text{For any text } T \text{ containing}
}
\\
{
\text{at least one character}
}
}
}
, \quad
\underbrace{
\forall m \in \{1, \dots, n\}
}_{
\substack{
{
\text{For any pattern } P \text{ containing}
}
\\
{
\text{at least one character}
}
}
}
, \quad
\underbrace{
\forall \xi \in \{0, \dots, m - 2\}
}_{
\text{For any boundary position } \xi
}
, \quad
\underbrace{
\exists \lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\}
}_{
\substack{
{
\text{There is at least 1 "index of the last character of the overflowing occurrence of } P_{suffix_{(1)}} \text{",}
}
\\
{
\text{since there is at least 1 "pattern prefix" forming a suffix in } P_{suffix_{(1)}} \text{. If } P_{suffix_{(1)}} \text{ is formed}
}
\\
{
\text{by at least 2 characters (which are } p_{(m - 1)} \text{ and } p_{(m - 2)} \text{), then a "pattern prefix" can have}
}
\\
{
\text{a minimum of 1 character. If } P_{suffix_{(1)}} \text{ is formed by } 2 \text{ characters, then the "longest pattern prefix"}
}
\\
{
\text{is formed by 1 character : the last character is also the first character, and is located}
}
\\
{
\text{at position 0 in } P \text{ (we can have } p_{(\lambda')} = p_{(0)} \text{ and } \lambda' = 0 \text{)}
}
}
}
, \quad
\underbrace{
\exists \psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}
}_{
\substack{
{
\text{There is at least 1 "index of the first character of the overflowing occurrence of } P_{suffix_{(1)}} \text{",}
}
\\
{
\text{since there is at least 1 "pattern prefix" forming a suffix in } P_{suffix_{(1)}} \text{.}
}
\\
{
\text{If } P_{suffix_{(1)}} \text{ is formed by } 2 \text{ characters, then the "longest pattern prefix" is formed by}
}
\\
{
\text{1 character : the last character is also the first character, and is located at position 0 in } P
}
\\
{
\text{(we can have } p_{(\lambda')} = p_{(\psi')} = p_{(0)} \text{ and } \lambda' = \psi' = 0 \text{)}
}
}
}
, \quad
\underbrace{
\bigg(
\lambda'
\in \Big\{\Big\{ p_{(0)}, \dots, p_{((0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1)} \Big\}\Big\}_{M}
\subset
\Big\{\Big\{ p_{(0)}, \dots, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{The last character of each "pattern prefix" is present in the part of } P \text{ formed by}
}
\\
{
\text{the characters } p_{(0)} \text{ to } p_{((0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1)}
}
}
}
\land
\underbrace{
\bigg(
\psi'
\in \Big\{\Big\{ p_{(m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1)}, \dots, p_{((0) - 1)} \Big\}\Big\}_{M}
\not\subset
\Big\{\Big\{ p_{(0)}, \dots, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
}_{
\text{The first character of each "overflowing occurrence of } P_{suffix_{(1)}} \text{" is not present in } P
}
\\[1em]
\quad
\land
\underbrace{
\bigg(
Card\Big(
\Big\{\Big\{ p_{(0)}, \dots, p_{(\lambda' - 1)}, p_{(\lambda')} \Big\}\Big\}_{M}
\Big)
\leq
\overbrace{
Card\Big(
\Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\Big)
}^{
Card(B_{P_{suffix_{(1)}}})
}
-
1
\bigg)
}_{
\text{Each "pattern prefix" has a length exactly less than that of } P_{suffix_{(1)}}
}
\land
\underbrace{
\bigg(
\Big(
p_{(\lambda')}
=
p_{(m - 1)}
\Big)
\land
\Big(
p_{(\lambda' - 1)}
=
p_{(m - 2)}
\Big)
\land
\dots
\land
\Big(
p_{(0)}
=
p_{(\xi + 1 + |\psi'|)}
\Big)
\bigg)
}_{
\text{Each "pattern prefix" shares the same characters as } P_{suffix_{(1)}}
}
\\[1em]
\quad
\land
\underbrace{
\bigg(
m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1
\leq
\psi'
<
\lambda'
\bigg)
}_{
\substack{
{
\text{Since } P_{suffix_{(1)}} \text{ is formed by at least } 2 \text{ characters, then each "overflowing occurrence of } P_{suffix_{(1)}} \text{"}
}
\\
{
\text{is formed by at least } 2 \text{ characters. Thus we always have }
\psi'
<
\lambda'
}
}
}
\ \
\Bigg)
\end{cases}
\end{array}
$$

Part 20 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\bigg(
\psi'
=
\lambda' - Card(B_{P_{suffix_{(1)}}}) + 1
\bigg)
}
\because
\bigg(
\Big(
Card\big(
\Big\{\Big\{ p_{(\psi')}, p_{(\psi' + 1)}, \dots, p_{(\lambda' - 1)}, p_{(\lambda')} \Big\}\Big\}_{M}
\big)
=
Card\big(
B_{P_{suffix_{(1)}}}
\big)
\Big)
\land
\underbrace{
\Big(
Card\big(
\Big\{\Big\{ p_{(\psi')}, p_{(\psi' + 1)}, \dots, p_{(\lambda' - 1)}, p_{(\lambda')} \Big\}\Big\}_{M}
\big)
=
(\lambda' - \psi') + 1
\Big)
}_{
Card\big(
\big\{ \text{startingIndex}, \dots, \text{endingIndex} \big\}
\big)
=
(\text{endingIndex} - \text{startingIndex}) + 1
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
\psi' < 0
\bigg)
}
\iff
\bigg(
\lambda' - Card(B_{P_{suffix_{(1)}}}) + 1 < 0
\bigg)
\iff
\bigg(
\lambda'
<
Card(B_{P_{suffix_{(1)}}}) - 1
\bigg)
\iff
\boxed{
\underbrace{
\bigg(
\lambda'
\leq
(Card(B_{P_{suffix_{(1)}}}) - 1) - 1
\bigg)
}_{
\ \because \
\lambda' \in \mathbb{N}
}
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
\boxed{\exists} \lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\}, \quad
\boxed{\exists} \psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}, \quad
\boxed{
\underbrace{
\bigg(
\exists P_{prefix_{(1)}} \in \varsigma^{\lambda' + 1}, \quad
P_{prefix_{(1)}}
:=
(p_{(0)}, p_{(1)}, \dots, p_{(\lambda' - 1)}, p_{(\lambda')})
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{prefix_{(1)}} \text{ (= one possible pattern suffix)}
}
\\
{
\text{ in the current block and each } P_{prefix_{(1)}} \text{ can be viewed as a } (\lambda' + 1) \text{-tuple of characters in } P
}
}
}
\land
\underbrace{
\bigg(
B_{P_{prefix_{(1)}}}
:=
\Big\{\Big\{ p_{(0)}, p_{(1)}, \dots, p_{(\lambda' - 1)}, p_{(\lambda')} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{prefix_{(1)}} \text{ (= one possible pattern suffix)}
}
\\
{
\text{ in the current block and each } P_{prefix_{(1)}} \text{ can be viewed as a multiset of characters in } P
}
}
}
\land
\bigg(
Card\Big(
B_{P_{prefix_{(1)}}}
\Big)
=
\lambda' - 0 + 1
=
\lambda' + 1
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\Big(
0
\leq
\lambda'
\leq
(0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1
\Big)
}
\iff
\Big(
0
\leq
\lambda'
\leq
Card(B_{P_{suffix_{(1)}}}) - 2
\Big)
\iff
\Big(
1
\leq
\lambda' + 1
\leq
Card(B_{P_{suffix_{(1)}}}) - 1
\Big)
\iff
\Big(
1
\leq
Card(B_{P_{prefix_{(1)}}})
\leq
Card(B_{P_{suffix_{(1)}}}) - 1
\Big)
\bigg)
\Rightarrow
\bigg(
1
\leq
Card(B_{P_{prefix_{(1)}}})
\leq
Card(B_{P_{suffix_{(1)}}}) - 1
<
Card(B_{P_{suffix_{(1)}}})
\bigg)
\Rightarrow
\boxed{
\underbrace{
\bigg(
Card(B_{P_{prefix_{(1)}}})
<
Card(B_{P_{suffix_{(1)}}})
\bigg)
}_{
\text{Each } P_{prefix_{(1)}} \text{ has a length exactly less than that of } P_{suffix_{(1)}}
}
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\quad
P
=
\underbrace{
\overbrace{
\Big(
p_{(0)}, \dots, p_{(\lambda')}
}^{
P_{prefix_{(1)}}
}
}_{
\text{Prefix of length } \lambda' + 1
}, \quad
\dots, \quad 
\underbrace{
p_{(\xi + 1)} \ , 
\dots \ , 
\overbrace{
p_{(m - \lambda' - 1)} \ , 
\dots \ , 
p_{(m - 2)} \ , 
p_{(m - 1)}
\Big)
}^{
\text{End of suffix } P_{suffix_{(1)}}
\text{ = }
\text{end of pattern } P
\text{ = }
\text{prefix } P_{prefix_{(1)}}
}
}_{
P_{suffix_{(1)}}
\text{ (= Suffix of length } m - \lambda' - 1 \text{ )}
}
\quad
\bigg)
\land
\underbrace{
\bigg(
(m - 1)
-
Card\big(
B_{P_{prefix_{(1)}}}
\big)
+
1
=
m
-
Card\big(
B_{P_{prefix_{(1)}}}
\big)
=
m - (\lambda' + 1)
=
m - \lambda' - 1
\bigg)
}_{
\ \because \
\text{startingIndex}
=
\text{endingIndex}
-
Card\big(
\big\{ \text{startingIndex}, \text{startingIndex} + 1, \dots, \text{endingIndex} \big\}
\big)
+
1
}
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
\exists \lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\}, \quad
\exists \psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}, \quad
\exists P_{prefix_{(1)}} \in \varsigma^{\lambda' + 1}, \quad
\boxed{
P_{prefix_{(1)}}
=
(p_{(0)}, \dots, p_{(\lambda')})
=
(p_{(m - \lambda' - 1)}, \dots, p_{(m - 1)})
}
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 20 :

$$
\begin{array}{l}
\begin{array}{c|}
T
\\
\\
P
\\
\\
P_{suffix_{(1)}}
\\
\\
P_{prefix_{(1)}}
\\
\\
T_{suffix_{(1)}}
\\
\\
\end{array}
\ \ \
\overbrace{
\begin{array}{ccccccccccccc}
t_{(0)} & t_{(1)} & \dots & t_{(\lambda' - 1)} & t_{(\lambda')} & \dots & t_{(0 + \xi - 1)} & t_{(0 + \xi)} & t_{(0 + \xi + 1)} & t_{(0 + \xi + 2)} & \dots & t_{(0 + m - 2)} & t_{(0 + m - 1)}
\\
/ & / & \dots & / & / & \dots & / & \neq & = & = & \dots & = & =
\\
p_{(0)} & p_{(1)} & \dots & p_{(\lambda' - 1)} & p_{(\lambda')} & \dots & p_{(\xi - 1)} & p_{(\xi)} & p_{(\xi + 1)} & p_{(\xi + 2)} & \dots & p_{(m - 2)} & p_{(m - 1)}
\\
\\
 &  &  &  &  &  &  &  & p_{(\xi + 1)} & p_{(\xi + 2)} & \dots & p_{(m - 2)} & p_{(m - 1)}
\\
\\
p_{(0)} & p_{(1)} & \dots & p_{(\lambda' - 1)} & p_{(\lambda')}
\\
\\
 &  &  &  &  &  &  &  & t_{(0 + \xi + 1)} & t_{(0 + \xi + 2)} & \dots & t_{(0 + m - 2)} & t_{(0 + m - 1)}
\\
\\
\end{array}
}^{
\text{Current block (first iteration) = block from position } 0 \text{ to position } 0 + m - 1
\text{ ( with } \mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}} = 0 \text{ ) in } T
}
\ \ \
\begin{array}{cccc}
t_{(m = 0 + (m - 1) + 1)} & t_{(m + 1)} & \dots & t_{(n - 1)}
\\
/ & / & \dots & /
\\
/ & / & \dots & /
\\
\\
\\
\\
\\
\\
\\
\\
\end{array}
\end{array}
$$

Diagram 2 of part 20 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \ \ \ \
\underbrace{
\phantom{\big(}
\,''D''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''E''\,, 
\phantom{\big(}
\,''S''\,
\phantom{\big)}
, \,''\_''\,,
\,''V''\,, \,''O''\,, \,''I''\,, \,''E''\,, \,''S''\,,
\,''\_''\,, \,''D''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
t_{(0 + \xi)}
}
}^{
\substack{
{
t_{(0 + \xi)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\underbrace{
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(0 + \xi + 1)}
}
}^{
\substack{
{
t_{(0 + \xi + 1)}
}
\\
{
= p_{(\xi)}
}
}
}
\,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
}_{
T_{suffix_{(1)}}
}
, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,
\\[2em]
P \quad 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(\lambda')}
}
}_{
\substack{
{
\text{"longest pattern prefix"}
}
\\
{
\text{(= one specific } P_{prefix_{(1)}} \text{ )}
}
}
}
, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, 
\underbrace{
\phantom{\big(}
\,''M''\,
\phantom{\big)}
}_{
p_{(\xi)}
}
, 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\xi + 1)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
P_{suffix_{(1)}}
}
\end{array}
$$

Part 21 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{prefixpos_{(\xi)}}
:=
\underbrace{
\bigg\{
\lambda'
\ \bigg| \
\bigg(
\psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}
\bigg)
\land
\bigg(
\lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\}
\bigg)
\land
\bigg(
P_{prefix_{(1)}}
=
(p_{(0)}, \dots, p_{(\lambda')})
=
(p_{(m - \lambda' - 1)}, \dots, p_{(m - 1)})
\bigg)
\land
\bigg(
Card(B_{P_{prefix_{(1)}}})
<
Card(B_{P_{suffix_{(1)}}})
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{prefixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{prefix_{(1)}} \text{, where } P_{prefix_{(1)}}
\text{ has a length exactly less than that of } P_{suffix_{(1)}}
}
\ \
\Bigg)
\\[1em]
\Rightarrow
\underbrace{
\Bigg(
\bigg(
\Big(
t_{(0)} = \,''D''\,
\Big)
\land
\dots
\land
\Big(
t_{(n - 1)} = \,''T''\,
\Big)
\bigg)
\land
\bigg(
\Big(
p_{(0)} = \,''E''\,
\Big)
\land
\dots
\land
\Big(
p_{(m - 1)} = \,''T''\,
\Big)
\bigg)
\Bigg)
}_{\text{Example}}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
T = \ \ \ \ \ \ \ (
\,''D''\,, \,''E''\,, \,''S''\,, \,''\_''\,,
\,''V''\,, \,''O''\,, \,''I''\,, \,''E''\,, \,''S''\,,
\,''\_''\,, \,''D''\,, \,''\_''\,,
\,''E''\,, \,''N''\,, \,''T''\,, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,
)
}_{
\text{Example of text of length } n
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
P = (
\,''E''\,, \,''N''\,, \,''T''\,, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,
)
}_{
\text{Example of pattern of length } m
}
\Bigg)
\end{cases}
\end{array}
$$

Part 22 :

- If no "occurrence of $P_{suffix_{(1)}}$" are found in $P$ and if there is at least one pattern prefix $P_{prefix_{(1)}}$, then $\Lambda$ is the index (= position) of the last letter of the "longest pattern prefix" 
  (= one specific $P_{prefix_{(1)}}$ ), which is the pattern prefix "most to the right" in the pattern $P$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
k = m - 1
\Bigg)
}_{
\substack{
{
\text{Index of the starting position of the scan}
}
\\
{
\text{from right to left}
}
}
}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\bigg)
}_{
\text{Index of the starting position of the current block}
}
\Rightarrow
\underbrace{
\bigg(
t_{(0 + m - 1)} = p_{(m - 1)}
\bigg)
}_{
\substack{
{
\text{The last character of the current block in } T
}
\\
{
\text{is the last character of } P
}
}
}
\Rightarrow
\bigg(
\underbrace{
\exists \xi \in \{0, \dots, m - 2\}
}_{
\substack{
{
\text{For this case to be defined, }
}
\\
{
\text{we assume that there is at least one } \xi
}
}
}
, \quad
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\Big)
}_{
\substack{
{
\text{The character } t_{(0 + \xi)} \text{ of the current block in } T
}
\\
{
\text{is not the character } p_{(\xi)} \text{ of } P
}
}
}
\Rightarrow
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\land
t_{(0 + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(0 + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(0 + m - 2)} = p_{(m - 2)}
\land
t_{(0 + m - 1)} = p_{(m - 1)}
\Big)
}_{
\substack{
{
\text{The characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)} \text{ of the pattern } P
\text{ (forming a “pattern suffix”) correspond consecutively and respectively }
}
\\
{
\text{ to the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the text } T 
\text{ (characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ forming a “text suffix”)}
}
\\
{
\text{The character } p_{(\xi)} \text{ of the pattern } P \text{ does not correspond to the character } t_{(0 + \xi)} \text{ of the text } T
}
\\
{
\text{The characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the current block in } T \text{ are respectively the characters } p_{(m - 1)} \text{ to } 
p_{(\xi + 1)} \text{ of } P \text{ (it forms potentially a whole pattern } P
}
\\
{
\text{ which have its characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)}
\text{ superimposed on the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ )}
}
}
}
\bigg)
\Rightarrow
\bigg(
\underbrace{
\Big(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} \neq \emptyset
\Big)
\Rightarrow
\Big(
\exists! \Lambda \in \{0, \dots, m - 2\}, \quad
\Lambda
:=
max\big(
P_{prefixpos_{(\xi)}}
\big)
\Big)
}_{
\substack{
{
\text{If no "occurrence of } P_{suffix_{(1)}} \text{" are found in } P \text{ and if there is at least one pattern prefix } P_{prefix_{(1)}} \text{ , then we take}
}
\\
{
\text{the index of the last letter of the "longest pattern prefix" (= one specific } P_{prefix_{(1)}} \text{ ), which is the pattern prefix} 
}
\\
{
\text{"most to the right" in } P \text{ (so we use } max \text{ function, as the scan goes from right to left)}
}
}
}
\Rightarrow
\underbrace{
\Big(
\mathcal{J}_{min}
:=
0
+
m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
+
m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({1}\big)_{(4)}}}}
\Big)
}_{
\text{Index of the start position of the next block}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
j_{min}
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota'}\big)_{(4)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(j_{min} + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \xi \in \{0, \dots, m - 2\}, \quad
\Big(
t_{(j_{min} + \xi)} \neq p_{(\xi)}
\Big)
\Rightarrow
\Big(
t_{(j_{min} + \xi)} \neq p_{(\xi)}
\land
t_{(j_{min} + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(j_{min} + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(j_{min} + m - 2)} = p_{(m - 2)}
\land
t_{(j_{min} + m - 1)} = p_{(m - 1)}
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} \neq \emptyset
\Big)
\Rightarrow
\Big(
\exists! \Lambda \in \{0, \dots, m - 2\}, \quad
\Lambda
:=
max\big(
P_{prefixpos_{(\xi)}}
\big)
\Big)
\Rightarrow
\Big(
\mathcal{J}_{min}
:=
j_{min}
+
m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota'}\big)_{(4)}}}}
+
m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota' + 1}\big)_{(4)}}}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
n - m
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota_{max}}\big)_{(4)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(n - m + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \xi \in \{0, \dots, m - 2\}, \quad
\Big(
t_{(n - m + \xi)} \neq p_{(\xi)}
\Big)
\Rightarrow
\Big(
t_{(n - m + \xi)} \neq p_{(\xi)}
\land
t_{(n - m + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(n - m + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(n - m + m - 2)} = p_{(m - 2)}
\land
t_{(n - m + m - 1)} = p_{(m - 1)}
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 22 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \ \ \ \
\underbrace{
\phantom{\big(}
\,''D''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''E''\,, 
\phantom{\big(}
\,''S''\,
\phantom{\big)}
, \,''\_''\,,
\,''V''\,, \,''O''\,, \,''I''\,, \,''E''\,, \,''S''\,,
\,''\_''\,, \,''D''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
t_{(0 + \xi)}
}
}^{
\substack{
{
t_{(0 + \xi)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\underbrace{
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(0 + \xi + 1)}
}
}^{
\substack{
{
t_{(0 + \xi + 1)}
}
\\
{
= p_{(\xi)}
}
}
}
\,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
}_{
T_{suffix_{(1)}}
}
, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,
\\[2em]
P \quad 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(\lambda')}
}
}_{
\substack{
{
\text{"longest pattern prefix"}
}
\\
{
\text{(= one specific } P_{prefix_{(1)}} \text{ )}
}
}
}
, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, 
\underbrace{
\phantom{\big(}
\,''M''\,
\phantom{\big)}
}_{
p_{(\xi)}
}
, 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\xi + 1)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
P_{suffix_{(1)}}
}
\\[2em]
\text{(Iteration 2) : Scanning from right to left in the current block from } t_{(0 + m - 1 - \Lambda)} \text{ to } t_{(n - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0 + m - 1 - \Lambda
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({1}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad \ \ \ \ \ \ \ \ \ \
\underbrace{
\phantom{\big(}
\,''D''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''E''\,, \,''S''\,, \,''\_''\,,
\,''V''\,, \,''O''\,, \,''I''\,, \,''E''\,, \,''S''\,,
\,''\_''\,, \,''D''\,, \,''\_''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(0 + m - 1 - \Lambda)}
}
}^{
\substack{
{
\text{Ending}
}
\\
{
t_{(0 + m - 1 - \Lambda)}
}
\\
{
= p_{(0)}
}
}
}
\,''N''\,, \,''T''\,, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(n - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(n - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
\\[2em]
P \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad 
\quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''N''\,, \,''T''\,, \,''R''\,, \,''E''\,, \,''C''\,, \,''R''\,, \,''O''\,, \,''I''\,, \,''S''\,, \,''E''\,, \,''M''\,, \,''E''\,, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
\text{Pattern found in the block from } t_{(0 + m - 1 - \Lambda)} \text{ to } t_{(n - 1)}
}
\end{array}
$$

Part 23 :

- From part 23 to part 26, since we choose to cover as many cases as possible, we examine the following case :

	- (English) If no "occurrence of $P_{suffix_{(1)}}$" are found in $P$ and if no "longest pattern prefix" (= one specific $P_{prefix_{(1)}}$) is found in $P$ :

		- Starting from the current block from $j_{min}$ to $j_{min} + m - 1$ :

			- 11. We skip the whole current block and we move on to the next block from $j_{min} + m - 1 + 1$ to $(j_{min} + m - 1 + 1) + m - 1$ 

			- 12. We start again from step 1 (see part 9) until all the characters of the pattern correspond consecutively and respectively to all the characters of the current block
	
			  The final goal is to align the whole pattern (= $P$) with a block of the text $T$ 	


	- (French) Si aucune "occurence de $P_{suffix_{(1)}}$" n'est trouvée dans $P$ et si aucun "plus grand préfixe du motif" (= un spécifique $P_{prefix_{(1)}}$) n'est trouvé dans $P$ :

		- En partant du bloc courant allant $j_{min}$ à $j_{min} + m - 1$ :

			- 11. On saute le bloc courant tout entier et on passe au bloc suivant allant de $j_{min} + m - 1 + 1$ à $(j_{min} + m - 1 + 1) + m - 1$ 

			- 12. On recommence à partir de l'étape 1 (voir partie 9) jusqu'à ce que tous les caractères du motif correspondent d'affilée et respectivement à tous les caractères 
			  du bloc courant
	
			  L'objectif final est d'aligner le motif entier (= $P$) sur un bloc du texte $T$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\bigg(
\Big(
t_{(0)} = \,''R''\,
\Big)
\land
\dots
\land
\Big(
t_{(n - 1)} = \,''T''\,
\Big)
\bigg)
\land
\bigg(
\Big(
p_{(0)} = \,''\_''\,
\Big)
\land
\dots
\land
\Big(
p_{(m - 1)} = \,''T''\,
\Big)
\bigg)
\Bigg)
}_{\text{Example}}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
T = \ (
\,''R''\,, \,''E''\,, \,''C''\,, \,''E''\,, \,''M''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,, 
\,''\_''\,, 
\,''F''\,, \,''R''\,, \,''E''\,, \,''Q''\,, \,''U''\,, \,''E''\,, \,''N''\,, \,''T''\,
)
}_{
\text{Example of text of length } n
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
P = \ \ \ \ (
\,''\_''\,, \,''F''\,, \,''R''\,, \,''E''\,, \,''Q''\,, \,''U''\,, \,''E''\,, \,''N''\,, \,''T''\,
)
}_{
\text{Example of pattern of length } m
}
\Bigg)
\end{cases}
\end{array}
$$

Part 24 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\underbrace{
\Bigg(
k = m - 1
\Bigg)
}_{
\substack{
{
\text{Index of the starting position of the scan}
}
\\
{
\text{from right to left}
}
}
}
\\[1em]
\Rightarrow
\Bigg(
\underbrace{
\bigg(
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\bigg)
}_{
\text{Index of the starting position of the current block}
}
\Rightarrow
\underbrace{
\bigg(
t_{(0 + m - 1)} = p_{(m - 1)}
\bigg)
}_{
\substack{
{
\text{The last character of the current block in } T
}
\\
{
\text{is the last character of } P
}
}
}
\Rightarrow
\bigg(
\underbrace{
\exists \xi \in \{0, \dots, m - 2\}
}_{
\substack{
{
\text{For this case to be defined, }
}
\\
{
\text{we assume that there is at least one } \xi
}
}
}
, \quad
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\Big)
}_{
\substack{
{
\text{The character } t_{(0 + \xi)} \text{ of the current block in } T
}
\\
{
\text{is not the character } p_{(\xi)} \text{ of } P
}
}
}
\Rightarrow
\underbrace{
\Big(
t_{(0 + \xi)} \neq p_{(\xi)}
\land
t_{(0 + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(0 + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(0 + m - 2)} = p_{(m - 2)}
\land
t_{(0 + m - 1)} = p_{(m - 1)}
\Big)
}_{
\substack{
{
\text{The characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)} \text{ of the pattern } P
\text{ (forming a “pattern suffix”) correspond consecutively and respectively }
}
\\
{
\text{ to the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the text } T 
\text{ (characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ forming a “text suffix”)}
}
\\
{
\text{The character } p_{(\xi)} \text{ of the pattern } P \text{ does not correspond to the character } t_{(0 + \xi)} \text{ of the text } T
}
\\
{
\text{The characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ of the current block in } T \text{ are respectively the characters } p_{(m - 1)} \text{ to } 
p_{(\xi + 1)} \text{ of } P \text{ (it forms potentially a whole pattern } P
}
\\
{
\text{ which have its characters } p_{(m - 1)} \text{ to } p_{(\xi + 1)}
\text{ superimposed on the characters } t_{(0 + m - 1)} \text{ to } t_{(0 + \xi + 1)} \text{ )}
}
}
}
\bigg)
\Rightarrow
\bigg(
\underbrace{
\Big(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} = \emptyset
\Big)
}_{
\substack{
{
\text{If no "occurrence of } P_{suffix_{(1)}} \text{" are found in } P \text{ and if no}
}
\\
{
\text{"longest pattern prefix" (= one specific } P_{prefix_{(1)}} \text{) is found in } P \text{,}
}
\\
{
\text{then we skip the whole current block}
}
}
}
\Rightarrow
\underbrace{
\Big(
\mathcal{J}_{min}
:=
0
+
m - 1 + 1
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
+
m
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({1}\big)_{(4)}}}}
\Big)
}_{
\text{Index of the start position of the next block}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
j_{min}
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota'}\big)_{(4)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(j_{min} + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \xi \in \{0, \dots, m - 2\}, \quad
\Big(
t_{(j_{min} + \xi)} \neq p_{(\xi)}
\Big)
\Rightarrow
\Big(
t_{(j_{min} + \xi)} \neq p_{(\xi)}
\land
t_{(j_{min} + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(j_{min} + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(j_{min} + m - 2)} = p_{(m - 2)}
\land
t_{(j_{min} + m - 1)} = p_{(m - 1)}
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} = \emptyset
\Big)
\Rightarrow
\Big(
\mathcal{J}_{min}
:=
j_{min}
+
m - 1 + 1
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota'}\big)_{(4)}}}}
+
m
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota' + 1}\big)_{(4)}}}}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\dots
\Rightarrow
\Bigg(
\bigg(
\mathcal{J}_{min}
:=
n - m
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota_{max}}\big)_{(4)}}}}
\bigg)
\Rightarrow
\bigg(
t_{(n - m + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \xi \in \{0, \dots, m - 2\}, \quad
\Big(
t_{(n - m + \xi)} \neq p_{(\xi)}
\Big)
\Rightarrow
\Big(
t_{(n - m + \xi)} \neq p_{(\xi)}
\land
t_{(n - m + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(n - m + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(n - m + m - 2)} = p_{(m - 2)}
\land
t_{(n - m + m - 1)} = p_{(m - 1)}
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Diagram 1 of part 24 :

$$
\begin{array}{l}
\text{(Iteration 1) : Scanning from right to left in the current block from } t_{(0)} \text{ to } t_{(0 + m - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad
\underbrace{
\phantom{\big(}
\,''R''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''E''\,, , \,''C''\,, , \,''E''\,,
\phantom{\big(}
\,''M''\,
\phantom{\big)}
,
\overbrace{
\underbrace{
\phantom{\big(}
\,''M''\,
\phantom{\big)}
}_{
t_{(0 + \xi)}
}
}^{
\substack{
{
t_{(0 + \xi)}
}
\\
{
\neq p_{(\xi)}
}
}
}
, 
\underbrace{
\overbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
t_{(0 + \xi + 1)}
}
}^{
\substack{
{
t_{(0 + \xi + 1)}
}
\\
{
= p_{(\xi)}
}
}
}
\,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(0 + m - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(0 + m - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
}_{
T_{suffix_{(1)}}
}
, \,''\_''\,, \,''F''\,, \,''R''\,, \,''E''\,, \,''Q''\,, \,''U''\,, \,''E''\,, \,''N''\,, \,''T''\, 
\\[2em]
P \quad \ \ \ \ \ \ \ \ \
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''F''\,, \,''R''\,, \,''E''\,, \,''Q''\,, 
\underbrace{
\phantom{\big(}
\,''U''\,
\phantom{\big)}
}_{
p_{(\xi)}
}
, 
\underbrace{
\underbrace{
\phantom{\big(}
\,''E''\,
\phantom{\big)}
}_{
p_{(\xi + 1)}
}
, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
P_{suffix_{(1)}}
}
\\[2em]
\text{(Iteration 2) : Scanning from right to left in the current block from } t_{(0 + m - 1 + 1)} \text{ to } t_{(n - 1)}
\text{ (with }
\mathcal{J}_{min}
:=
0 + m - 1 + 1
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({1}\big)_{(4)}}}}
\text{ )}
\\[1em]
\xleftarrow{}
\\[1em]
T \quad
\underbrace{
\phantom{\big(}
\,''R''\,
\phantom{\big)}
}_{
t_{(0)}
}
, \,''E''\,, \,''C''\,, \,''E''\,, \,''M''\,, \,''M''\,, \,''E''\,, \,''N''\,, \,''T''\,,
\overbrace{
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
t_{(0 + m - 1 + 1)}
}
}^{
\substack{
{
\text{Ending}
}
\\
{
t_{(0 + m - 1 + 1)}
}
\\
{
= p_{(0)}
}
}
}
\,''F''\,, \,''R''\,, \,''E''\,, \,''Q''\,, \,''U''\,, \,''E''\,, \,''N''\,, 
\overbrace{
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
t_{(n - 1)}
}
}^{
\substack{
{
\text{Starting}
}
\\
{
t_{(n - 1)}
}
\\
{
= p_{(m - 1)}
}
}
}
\\[2em]
P \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad 
\quad \quad \quad
\underbrace{
\underbrace{
\phantom{\big(}
\,''\_''\,
\phantom{\big)}
}_{
p_{(0)}
}
, \,''F''\,, \,''R''\,, \,''E''\,, \,''Q''\,, \,''U''\,, \,''E''\,, \,''N''\,, 
\underbrace{
\phantom{\big(}
\,''T''\,
\phantom{\big)}
}_{
p_{(m - 1)}
}
}_{
\text{Pattern found in the block from } t_{(0 + m - 1 + 1)} \text{ to } t_{(n - 1)}
}
\end{array}
$$

Part 25 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{suffixpos_{(\xi)}}
=
\underbrace{
\bigg\{
\lambda
\ \bigg| \
\bigg(
\psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}
\bigg)
\land
\bigg(
\lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\}
\bigg)
\land
\bigg(
P_{suffix_{(2)}}
=
(p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)})
=
(p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)})
=
P_{suffix_{(1)}}
\bigg)
\land
\bigg(
\Big(
\psi - 1 \geq 0
\Big)
\Rightarrow
\Big(
p_{(\psi - 1)} \neq p_{(\xi)}
\Big)
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{suffixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{suffix_{(2)}} \text{, where } P_{suffix_{(2)}}
\text{ can be preceded by at least one character in } P \text{, or can be flushed with the left edge of } P
}
\ \
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{prefixpos_{(\xi)}}
=
\underbrace{
\bigg\{
\lambda'
\ \bigg| \
\bigg(
\psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}
\bigg)
\land
\bigg(
\lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\}
\bigg)
\land
\bigg(
P_{prefix_{(1)}}
=
(p_{(0)}, \dots, p_{(\lambda')})
=
(p_{(m - \lambda' - 1)}, \dots, p_{(m - 1)})
\bigg)
\land
\bigg(
Card(B_{P_{prefix_{(1)}}})
<
Card(B_{P_{suffix_{(1)}}})
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{prefixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{prefix_{(1)}} \text{, where } P_{prefix_{(1)}}
\text{ has a length exactly less than that of } P_{suffix_{(1)}}
}
\ \
\Bigg)
\end{cases}
\end{array}
$$

Part 26 :

- $\delta_{[3]}(\phi)$ is called the "table of corresponding suffixes and prefixes"

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\underbrace{
\exists! {\iota}_{max_{(4)}} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall {\iota}_{(4)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(4)}, \dots, {\iota}_{max_{(4)}}\}, \quad
\mathcal{J}_{{}_{[4]}min} : \{0, 1, 2, 3, \dots, {\iota'}_{(4)}, \dots, {\iota}_{max_{(4)}}\} \to \{0, \dots, n - m\}, \quad
{\iota}_{(4)} \mapsto \mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}}, \quad
\begin{cases}
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
=
0
\\[1em]
\forall \xi \in \{0, \dots, m - 2\}, \quad
\exists! \Lambda \in \{0, \dots, m\}, \quad
\Lambda
:=
\begin{cases}
\bigg(
P_{suffixpos_{(\xi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
max\Big(
P_{suffixpos_{(\xi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
max\Big(
P_{prefixpos_{(\xi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
m
\bigg)
\end{cases}
\\[1em]
\forall {\iota}_{(4)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(4)}, \dots, {\iota}_{max_{(4)}} - 1\}, \quad
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota + 1}\big)_{(4)}}}}
:=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + m - 1 - \Lambda
\end{cases}
\ \
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists! {\iota}_{max_{(4)}} \in \mathbb{N}, \quad
\forall {\iota}_{(4)} \in \{0, 1, 2, 3, \dots, {\iota'}_{(4)}, \dots, {\iota}_{max_{(4)}} - 1\}, \quad
\boxed{
\bigg(
t_{(\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\exists \xi \in \{0, \dots, m - 2\}, \quad
\Big(
t_{(\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + \xi)} \neq p_{(\xi)}
\Big)
\Rightarrow
\Big(
t_{(\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + \xi)} \neq p_{(\xi)}
\land
t_{(\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + \xi + 1)} = p_{(\xi + 1)}
\land
t_{(\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + \xi + 2)} = p_{(\xi + 2)}
\land
\dots
\land
t_{(\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + m - 2)} = p_{(m - 2)}
\land
t_{(\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + m - 1)} = p_{(m - 1)}
\Big)
\bigg)
}
\Rightarrow
\bigg(
\underbrace{
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota + 1}\big)_{(4)}}}}
-
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}}
}_{
\Delta_{{}_{[4]}{\big({\iota}\big)_{(4)}}}
}
=
m - 1 - \Lambda
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\left(
\boxed{
\bigg(
t_{(\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}} + m - 1)} = p_{(m - 1)}
\bigg)
}
\land
\left(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \phi \in \{0, \dots, m - 2\}, \quad
\delta_{[3]} : \{0, \dots, m - 2\} \to \{0, \dots, m\}, \quad
\phi \mapsto \delta_{[3]}(\phi), \quad
\boxed{
\delta_{[3]}(\phi)
:=
\begin{cases}
\bigg(
P_{suffixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
max\Big(
P_{suffixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
max\Big(
P_{prefixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
m
\bigg)
\end{cases}
}
\ \
\right)
\right)
\end{cases}
\end{array}
$$

Part 27 :

- From part 27 to part 29, we generalize by combining all the cases examined from part 4 to part 26

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\bigg(
\forall t_{(0)}, \dots, t_{(n - 1)} \in \varsigma, \quad
\exists! T \in \varsigma^{n}, \quad
T
=
(t_{(0)}, \dots, t_{(n - 1)})
\bigg)
\Rightarrow
\bigg(
\forall m \in \{1, \dots, n\}, \quad
\forall p_{(0)}, \dots, p_{(m - 1)} \in \varsigma, \quad
\exists! P \in \varsigma^{m}, \quad
P
=
(p_{(0)}, \dots, p_{(m - 1)})
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{suffixpos_{(\xi)}}
=
\underbrace{
\bigg\{
\lambda
\ \bigg| \
\bigg(
\psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}
\bigg)
\land
\bigg(
\lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\}
\bigg)
\land
\bigg(
P_{suffix_{(2)}}
=
(p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)})
=
(p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)})
=
P_{suffix_{(1)}}
\bigg)
\land
\bigg(
\Big(
\psi - 1 \geq 0
\Big)
\Rightarrow
\Big(
p_{(\psi - 1)} \neq p_{(\xi)}
\Big)
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{suffixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{suffix_{(2)}} \text{, where } P_{suffix_{(2)}}
\text{ can be preceded by at least one character in } P \text{, or can be flushed with the left edge of } P
}
\ \
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{prefixpos_{(\xi)}}
=
\underbrace{
\bigg\{
\lambda'
\ \bigg| \
\bigg(
\psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}
\bigg)
\land
\bigg(
\lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\}
\bigg)
\land
\bigg(
P_{prefix_{(1)}}
=
(p_{(0)}, \dots, p_{(\lambda')})
=
(p_{(m - \lambda' - 1)}, \dots, p_{(m - 1)})
\bigg)
\land
\bigg(
Card(B_{P_{prefix_{(1)}}})
<
Card(B_{P_{suffix_{(1)}}})
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{prefixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{prefix_{(1)}} \text{, where } P_{prefix_{(1)}}
\text{ has a length exactly less than that of } P_{suffix_{(1)}}
}
\ \
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
B_{P_{suffix_{(1)}}}
=
\Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\land
\underbrace{
\bigg(
B_{P_{suffix_{(2)}}}
=
\Big\{\Big\{ p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{suffix_{(2)}} \text{ (= one possible occurrence of } P_{suffix_{(1)}} \text{ )}
}
\\
{
\text{ in the current block and each } P_{suffix_{(2)}} \text{ can also be viewed as a multiset of characters in } P
}
}
}
\land
\bigg(
Card(B_{P_{suffix_{(1)}}})
=
Card(B_{P_{suffix_{(2)}}})
=
m - 1 - \xi
\bigg)
\land
\underbrace{
\bigg(
B_{P_{prefix_{(1)}}}
=
\Big\{\Big\{ p_{(0)}, p_{(1)}, \dots, p_{(\lambda' - 1)}, p_{(\lambda')} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{prefix_{(1)}} \text{ (= one possible pattern suffix)}
}
\\
{
\text{ in the current block and each } P_{prefix_{(1)}} \text{ can be viewed as a multiset of characters in } P
}
}
}
\land
\bigg(
Card(B_{P_{prefix_{(1)}}})
=
\lambda' + 1
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 28 :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\underbrace{
\exists! {\iota}_{max} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall \iota \in \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max}\}, \quad
\mathcal{J}_{min} : \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max}\} \to \{0, \dots, n - m\}, \quad
\iota \mapsto \mathcal{J}_{{min}_{{\big({\iota}\big)}}}, \quad
\begin{cases}
\mathcal{J}_{{min}_{{\big({0}\big)}}}
=
0
\\[1em]
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
:=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)}
\land
\gamma < m - 1
\Big\}
\Big)
\\[1em]
\forall \xi \in \{0, \dots, m - 2\}, \quad
\exists! \Lambda \in \{0, \dots, m\}, \quad
\Lambda
:=
\begin{cases}
\bigg(
P_{suffixpos_{(\xi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
max\Big(
P_{suffixpos_{(\xi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
max\Big(
P_{prefixpos_{(\xi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
m
\bigg)
\end{cases}
\\[1em]
\forall \iota \in \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max} - 1\}, \quad
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
:=
\begin{cases}
\bigg(
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)} \neq p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
=
\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1 - \beta'
\bigg)
\\[1em]
\bigg(
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
=
\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1 - \Lambda
\bigg)
\end{cases}
\end{cases}
\ \
\right)
\end{cases}
\end{array}
$$

Part 29 :

- $\delta(\alpha, \phi)$ brings together the two tables $\delta_{[2]}(\alpha)$ and $\delta_{[3]}(\phi)$. Within $\delta(\alpha, \phi)$, properties 1 to 2 are associated to $\delta_{[2]}(\alpha)$, and properties 3 to 5 are associated to $\delta_{[3]}(\phi)$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\forall \phi \in \{0, \dots, m - 2\}, \quad
\delta : \varsigma \times \{0, \dots, m - 2\} \to \{0, \dots, m\}, \quad
(\alpha, \phi) \mapsto \delta(\alpha, \phi), \quad
\delta(\alpha, \phi)
:=
\begin{cases}
\text{(Property 1)} \quad
\bigg(
\Big(
\alpha \neq p_{(m - 1)}
\Big)
\land
\Big(
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
:=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
\alpha
\land
\gamma < m - 1
\Big\}
\Big)
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m - 1 - \beta'
\bigg)
\\[1em]
\text{(Property 2)} \quad
\bigg(
\alpha \neq p_{(m - 1)}
\land
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m
\bigg)
\\[1em]
\text{(Property 3)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
max\Big(
P_{suffixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\text{(Property 4)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
max\Big(
P_{prefixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\text{(Property 5)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m
\bigg)
\end{cases}
\ \
\right)
\end{cases}
\end{array}
$$

Part 30 :

- From parts 30 to 35, we choose to compute the total number of operations performed before, during and after the scan of the text $T$ $\boxed{\text{in the case linked to the variable } {\iota}_{(3)}}$ and
   $\boxed{\text{in the case linked to the variable } {\iota}_{(4)}}$ without a pre-computation phase and with a pre-computation phase
	
	- In this part, we examine a property $\boxed{\text{in the case linked to the variable } {\iota}_{(3)}}$ 
	
		- $\frac{n - m}{m - 1 - \beta'} + 1$ is the number of block of text examined $\boxed{\text{in the case linked to the variable } {\iota}_{(3)}}$ 
		
		- $\frac{n - m}{m - 1 - \beta'} + 1$ is also the number of times $P$ can “fit” into $T$ without overlapping $\boxed{\text{in the case linked to the variable } {\iota}_{(3)}}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\mathcal{J}_{{}_{[3]}{min}_{{\big({0}\big)_{(3)}}}}
=
0
\bigg)
\land
\bigg(
\mathcal{J}_{{}_{[3]}{min}_{{\big({1}\big)_{(3)}}}}
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({0}\big)_{(3)}}}} + m - 1 - \beta'
=
0 + m - 1 - \beta'
=
m - 1 - \beta'
\bigg)
\land
\bigg(
\mathcal{J}_{{}_{[3]}{min}_{{\big({2}\big)_{(3)}}}}
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({1}\big)_{(3)}}}} + m - 1 - \beta'
=
(m - 1 - \beta') + m - 1 - \beta'
=
2 \cdot (m - 1 - \beta')
\bigg)
\land
\dots
\land
\bigg(
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota}\big)_{(3)}}}}
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota - 1}\big)_{(3)}}}} + m - 1 - \beta'
=
{\iota}_{(3)} \cdot (m - 1 - \beta')
\bigg)
\land
\dots
\land
\bigg(
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota_{max}}\big)_{(3)}}}}
=
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota_{max} - 1}\big)_{(3)}}}} + m - 1 - \beta'
=
{\iota}_{max_{(3)}} \cdot (m - 1 - \beta')
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\Big(
\mathcal{J}_{{}_{[3]}{min}_{{\big({\iota_{max}}\big)_{(3)}}}}
=
{\iota}_{max_{(3)}} \cdot (m - 1 - \beta')
=
n - m
\Big)
}
\iff
\Big(
{\iota}_{max_{(3)}} \cdot (m - 1 - \beta')
=
n - m
\Big)
\iff
\boxed{
\Big(
{\iota}_{max_{(3)}}
=
\frac{n - m}{m - 1 - \beta'}
\Big)
}
\bigg)
\Rightarrow
\boxed{
\bigg(
\Big(
{\iota}_{(3)} \in \{0, \dots, \underbrace{\frac{n - m}{m - 1 - \beta'}}_{{\iota}_{max_{(3)}}}\}
\Big)
\land
\Big(
Card(\{0, \dots, \underbrace{\frac{n - m}{m - 1 - \beta'}}_{{\iota}_{max_{(3)}}}\})
=
{\iota}_{max_{(3)}} + 1
=
\frac{n - m}{m - 1 - \beta'} + 1
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\Big(
\text{The maximum number of times } j_{min} \text{ can be repeated is } \frac{n - m}{m - 1 - \beta'} + 1
\Big)
\iff
\Big(
\text{The maximum number of times } P \text{ can be repeated in } T \text{ without overlapping is } \frac{n - m}{m - 1 - \beta'} + 1
\Big)
\bigg)
\because
\bigg(
\text{Each distinct position of } p_{(0)} \text{ corresponds to a possible whole pattern in } T
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 31 :

- In this part, we compute the total number of operations $\mathcal{W}_{{}_{[3]}total}$ performed before, during and after the scan of the text $T$, by comparing for each block of text the last character of 
  the block of text with each letter of the pattern

	- In this context, all the operations are performed during the scan of the text $T$ 
	
	- Here, $m$ operations are performed per block of text, because we compare (by calling the function $Cmp()$ ) for each block of text the last character of the block of text with each letter 
	  of the pattern
	
	- $\mathcal{W}_{{}_{[3]}pre}$ is the number of operations performed before the scan of the text $T$ 
	
	- $\mathcal{W}_{{}_{[3]}inter}$ is the number of operations performed during the scan of the text $T$ 
	
	- $\mathcal{W}_{{}_{[3]}pos}$ is the number of operations performed after the scan of the text $T$ 

	- $\mathcal{W}_{{}_{[3]}total}$ is the new total number of operations performed before, during and after the scan of the text $T$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\mathcal{W}_{{}_{[3]}inter}
:=
\overset{\frac{n - m}{m - 1 - \beta'}}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
\mathbb{1}\Big[
Cmp(t_{(\mathcal{J}_{{}_{[3]}{min}_{(\Psi)}} + k)}, p_{(k)})
\Big]
}
\Big)
}
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{W}_{{}_{[3]}inter}
=
\overset{\frac{n - m}{m - 1 - \beta'}}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
\mathbb{1}\Big[
Cmp(t_{(\mathcal{J}_{{}_{[3]}{min}_{(\Psi)}} + k)}, p_{(k)})
\Big]
}
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[3]}inter}
=
\overset{\frac{n - m}{m - 1 - \beta'}}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
1
}
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[3]}inter}
=
\overset{\frac{n - m}{m - 1 - \beta'}}{\underset{\Psi = 0}{\sum}}{
\Big(
\big( (m - 1) - (0) + 1 \big) \cdot 1
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[3]}inter}
=
\overset{\frac{n - m}{m - 1 - \beta'}}{\underset{\Psi = 0}{\sum}}{
\Big(
m
\Big)
}
\bigg)
\\[1em]
\iff
\bigg(
\mathcal{W}_{{}_{[3]}inter}
=
\Big(
\big( (\frac{n - m}{m - 1 - \beta'}) - 0 \big) + 1
\Big)
\cdot
\Big(
m
\Big)
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[3]}inter}
=
\Big(
\frac{n - 1 - \beta'}{m - 1 - \beta'}
\Big)
\cdot
\Big(
m
\Big)
\bigg)
\iff
\boxed{
\bigg(
\mathcal{W}_{{}_{[3]}inter}
=
\frac{nm - m - m \beta'}{m - 1 - \beta'}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}_{{}_{[3]}total}
:=
\mathcal{W}_{{}_{[3]}post}
+
\mathcal{W}_{{}_{[3]}inter}
+
\mathcal{W}_{{}_{[3]}pre}
=
0 + \frac{nm - m - m \beta'}{m - 1 - \beta'} + 0
=
\frac{nm - m - m \beta'}{m - 1 - \beta'}
\Bigg)
}
\end{cases}
\end{array}
$$

Part 32 :

- In this part, we compute the new total number of operations $\mathcal{W}'_{{}_{[3]}total}$ performed before, during and after the scan of the text $T$, by performing a pre-computation phase in which we 
  compute the "block jump" before the scan of the text $T$ 
	
	- Here, only a single operation (which is the call to function $\delta_{[2]}(\alpha)$ ) is performed per block of text, because the tests for each block of text have already been performed during 
	  the pre-computation phase
	
	- By performing such a pre-computation phase, the total number of operations $\mathcal{W}'_{{}_{[3]}total}$ performed before, during and after the scan of the text $T$ is less than $\mathcal{W}_{{}_{[3]}total}$. 
	  It means that the algorithm does not need to perform as many operations as in the case with $\mathcal{W}_{{}_{[3]}total}$, which makes the algorithm more efficient

	- $\mathcal{W}'_{{}_{[3]}pre}$ is the new number of operations performed before the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[3]}inter}$ is the new number of operations performed during the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[3]}pos}$ is the new number of operations performed after the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[3]}total}$ is the new total number of operations performed before, during and after the scan of the text $T$ 
	
	- The table $\delta_{[2]}(\alpha)$ is filled in during the pre-computation phase, and $\delta_{[2]}(\alpha)$ is then consulted (during the scan of the text $T$) at each 
	  non-correspondence between the last character inspected of the current block and the last character inspected of the pattern $P$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\overbrace{
\left(
\underbrace{
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\delta_{[2]}(\alpha)
=
\begin{cases}
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\bigg(
\beta'
=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
\alpha
\land
\gamma < m - 1
\Big\}
\Big)
\bigg)
\Rightarrow
\bigg(
\delta_{[2]}(\alpha)
=
m - 1 - \beta'
\bigg)
\\[1em]
\bigg(
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta_{[2]}(\alpha)
=
m
\bigg)
\end{cases}
\right)
}_{
\text{Here, since the number of operations is equal to the number of calls to } \delta_{[2]}(\alpha)
\text{ , and since } \delta_{[2]}(\alpha) \text{ is called for every } \alpha \text{ in } \varsigma \text{ and for each case, }
\delta_{[2]}(\alpha) \text{ is called } Card(\varsigma) + Card(\varsigma) \text{ times (case 1 + case 2)}
}
\Rightarrow
\boxed{
\bigg(
\mathcal{W}'_{{}_{[3]}pre}
:=
Card(\varsigma)
+
Card(\varsigma)
\bigg)
}
\right)
}^{
\text{Performed before the algorithm}
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}'_{{}_{[3]}inter}
:=
\overset{\frac{n - m}{m - 1 - \beta'}}{\underset{\Psi = 0}{\sum}}{
\Big(
\mathbb{1}\Big[
\delta_{[2]}(t_{(\mathcal{J}_{{}_{[3]}{min}_{(\Psi)}} + m - 1)})
\Big]
\Big)
}
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{W}'_{{}_{[3]}inter}
=
\overset{\frac{n - m}{m - 1 - \beta'}}{\underset{\Psi = 0}{\sum}}{
\Big(
\mathbb{1}\Big[
\delta_{[2]}(t_{(\mathcal{J}_{{}_{[3]}{min}_{(\Psi)}} + m - 1)})
\Big]
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}'_{{}_{[3]}inter}
=
\overset{\frac{n - m}{m - 1 - \beta'}}{\underset{\Psi = 0}{\sum}}{
\Big(
1
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}'_{{}_{[3]}inter}
=
\Big(
\big( (\frac{n - m}{m - 1 - \beta'}) - 0 \big) + 1
\Big)
\cdot
\Big(
1
\Big)
\bigg)
\iff
\boxed{
\bigg(
\mathcal{W}'_{{}_{[3]}inter}
=
\frac{n - 1 - \beta'}{m - 1 - \beta'}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}'_{{}_{[3]}total}
:=
\mathcal{W}'_{{}_{[3]}post}
+
\mathcal{W}'_{{}_{[3]}inter}
+
\mathcal{W}'_{{}_{[3]}pre}
=
0 + \frac{n - 1 - \beta'}{m - 1 - \beta'} + Card(\varsigma) + Card(\varsigma)
=
\frac{n - 1 - \beta'}{m - 1 - \beta'} + 2 \cdot Card(\varsigma)
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
\bigg(
\frac{n - 1 - \beta'}{m - 1 - \beta'} + 2 \cdot Card(\varsigma)
<
\frac{nm - m - m \beta'}{m - 1 - \beta'}
\bigg)
\iff
\bigg(
\frac{n - 1 - \beta'}{m - 1 - \beta'}
+
\frac{2 \cdot Card(\varsigma) \cdot (m - 1 - \beta')}{m - 1 - \beta'}
<
\frac{nm - m - m \beta'}{m - 1 - \beta'}
\bigg)
\iff
\bigg(
\frac{n - 1 - \beta' + 2 \cdot Card(\varsigma) \cdot (m - 1 - \beta')}{m - 1 - \beta'}
<
\frac{nm - m - m \beta'}{m - 1 - \beta'}
\bigg)
\iff
\bigg(
\frac{nm - m - m \beta'}{m - 1 - \beta'}
>
\frac{n - 1 - \beta' + 2 \cdot Card(\varsigma) \cdot (m - 1 - \beta')}{m - 1 - \beta'}
\bigg)
\\[1em]
\quad
\iff
\bigg(
\frac{nm - m - m \beta'}{m - 1 - \beta'}
-
\frac{n - 1 - \beta' + 2 \cdot Card(\varsigma) \cdot (m - 1 - \beta')}{m - 1 - \beta'}
>
0
\bigg)
\iff
\bigg(
\frac{nm - m - m \beta' + \Big( - n + 1 + \beta' - 2 \cdot Card(\varsigma) \cdot (m - 1 - \beta') \Big)}{m - 1 - \beta'}
>
0
\bigg)
\iff
\bigg(
\frac{nm - n - m \beta' + \beta' - 2 \cdot Card(\varsigma) \cdot (m - 1 - \beta') + 1 - m}{m - 1 - \beta'}
>
0
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
m - 1 - \beta' \neq 0
\Big)
\iff
\Big(
- \beta' \neq 1 - m
\Big)
\iff
\Big(
\beta'
\neq
m - 1
\Big)
\bigg)
\land
\bigg(
\Big(
m - 1 - \beta' \centernot{<} 0
\Big)
\because
\Big(
\big(
\beta' \in \{0, \dots, m - 2\}
\big)
\land
\big(
- \beta' < 1 - m
\Rightarrow
\beta' \centernot{>} m - 1
\big)
\Big)
\bigg)
\land
\bigg(
\Big(
m - 1 - \beta' > 0
\Big)
\iff
\Big(
- \beta' > 1 - m
\Big)
\iff
\Big(
\beta' < m - 1
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\frac{nm - n - m \beta' + \beta' - 2 \cdot Card(\varsigma) \cdot (m - 1 - \beta') + 1 - m}{m - 1 - \beta'}
>
0
\bigg)
\iff
\bigg(
\Big(
\beta' < m - 1
\Big)
\land
\Big(
n \cdot (m - 1) - \beta' \cdot (m - 1) - 2 \cdot Card(\varsigma) \cdot (m - 1) + 2 \cdot Card(\varsigma) \cdot \beta' - (m - 1) > 0
\Big)
\bigg)
\iff
\bigg(
\Big(
\beta' < m - 1
\Big)
\land
\Big(
n \cdot (m - 1) > \beta' \cdot (m - 1) + 2 \cdot Card(\varsigma) \cdot (m - 1) - 2 \cdot Card(\varsigma) \cdot \beta' + (m - 1)
\Big)
\bigg)
\\[1em]
\quad
\iff
\bigg(
\Big(
\beta' < m - 1
\Big)
\land
\Big(
n >
\frac{
\beta' \cdot (m - 1) + 2 \cdot Card(\varsigma) \cdot (m - 1) - 2 \cdot Card(\varsigma) \cdot \beta' + (m - 1)
}
{
(m - 1)
}
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\iff
\bigg(
\Big(
\beta' < m - 1
\Big)
\land
\Big(
n >
\beta' + 2 \cdot Card(\varsigma) - \frac{2 \cdot Card(\varsigma) \cdot \beta'}{(m - 1)} + 1
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\underbrace{
\frac{n - 1 - \beta'}{m - 1 - \beta'} + 2 \cdot Card(\varsigma)
}_{\mathcal{W}'_{{}_{[3]}total}}
<
\underbrace{
\frac{nm - m - m \beta'}{m - 1 - \beta'}
}_{\mathcal{W}_{{}_{[3]}total}}
\bigg)
\iff
\bigg(
\Big(
\beta' < m - 1
\Big)
\land
\Big(
n >
\beta' + 2 \cdot Card(\varsigma) - \frac{2 \cdot Card(\varsigma) \cdot \beta'}{(m - 1)} + 1
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 34 :

- In this part, we examine a property $\boxed{\text{in the case linked to the variable } {\iota}_{(4)}}$ 
	
	- $\frac{n - m}{m - 1 - \Lambda} + 1$ is the number of block of text examined $\boxed{\text{in the case linked to the variable } {\iota}_{(4)}}$ 
	
	- $\frac{n - m}{m - 1 - \Lambda} + 1$ is also the number of times $P$ can “fit” into $T$ without overlapping $\boxed{\text{in the case linked to the variable } {\iota}_{(4)}}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}}
=
0
\bigg)
\land
\bigg(
\mathcal{J}_{{}_{[4]}{min}_{{\big({1}\big)_{(4)}}}}
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({0}\big)_{(4)}}}} + m - 1 - \Lambda
=
0 + m - 1 - \Lambda
=
m - 1 - \Lambda
\bigg)
\land
\bigg(
\mathcal{J}_{{}_{[4]}{min}_{{\big({2}\big)_{(4)}}}}
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({1}\big)_{(4)}}}} + m - 1 - \Lambda
=
(m - 1 - \Lambda) + m - 1 - \Lambda
=
2 \cdot (m - 1 - \Lambda)
\bigg)
\land
\dots
\land
\bigg(
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota}\big)_{(4)}}}}
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota - 1}\big)_{(4)}}}} + m - 1 - \Lambda
=
{\iota}_{(4)} \cdot (m - 1 - \Lambda)
\bigg)
\land
\dots
\land
\bigg(
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota_{max}}\big)_{(4)}}}}
=
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota_{max} - 1}\big)_{(4)}}}} + m - 1 - \Lambda
=
{\iota}_{max_{(4)}} \cdot (m - 1 - \Lambda)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\Big(
\mathcal{J}_{{}_{[4]}{min}_{{\big({\iota_{max}}\big)_{(4)}}}}
=
{\iota}_{max_{(4)}} \cdot (m - 1 - \Lambda)
=
n - m
\Big)
}
\iff
\Big(
{\iota}_{max_{(4)}} \cdot (m - 1 - \Lambda)
=
n - m
\Big)
\iff
\boxed{
\Big(
{\iota}_{max_{(4)}}
=
\frac{n - m}{m - 1 - \Lambda}
\Big)
}
\bigg)
\Rightarrow
\boxed{
\bigg(
\Big(
{\iota}_{(4)} \in \{0, \dots, \underbrace{\frac{n - m}{m - 1 - \Lambda}}_{{\iota}_{max_{(4)}}}\}
\Big)
\land
\Big(
Card(\{0, \dots, \underbrace{\frac{n - m}{m - 1 - \Lambda}}_{{\iota}_{max_{(4)}}}\})
=
{\iota}_{max_{(4)}} + 1
=
\frac{n - m}{m - 1 - \Lambda} + 1
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\Big(
\text{The maximum number of times } j_{min} \text{ can be repeated is } \frac{n - m}{m - 1 - \Lambda} + 1
\Big)
\iff
\Big(
\text{The maximum number of times } P \text{ can be repeated in } T \text{ without overlapping is } \frac{n - m}{m - 1 - \Lambda} + 1
\Big)
\bigg)
\because
\bigg(
\text{Each distinct position of } p_{(0)} \text{ corresponds to a possible whole pattern in } T
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 35 :

- In this part, we compute the total number of operations $\mathcal{W}_{{}_{[4]}total}$ performed before, during and after the scan of the text $T$, by comparing for each block of text the last character of 
  the block of text with each letter of the pattern

	- In this context, all the operations are performed during the scan of the text $T$ 
	
	- Here, $m$ operations are performed per block of text, because we compare (by calling the function $Cmp()$ ) for each block of text the last character of the block of text with each letter 
	  of the pattern
	
	- $\mathcal{W}_{{}_{[4]}pre}$ is the number of operations performed before the scan of the text $T$ 
	
	- $\mathcal{W}_{{}_{[4]}inter}$ is the number of operations performed during the scan of the text $T$ 
	
	- $\mathcal{W}_{{}_{[4]}pos}$ is the number of operations performed after the scan of the text $T$ 

	- $\mathcal{W}_{{}_{[4]}total}$ is the new total number of operations performed before, during and after the scan of the text $T$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\boxed{
\Bigg(
\mathcal{W}_{{}_{[4]}inter}
:=
\overset{\frac{n - m}{m - 1 - \Lambda}}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
\mathbb{1}\Big[
Cmp(t_{(\mathcal{J}_{{}_{[4]}{min}_{(\Psi)}} + k)}, p_{(k)})
\Big]
}
\Big)
}
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{W}_{{}_{[4]}inter}
=
\overset{\frac{n - m}{m - 1 - \Lambda}}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
\mathbb{1}\Big[
Cmp(t_{(\mathcal{J}_{{}_{[4]}{min}_{(\Psi)}} + k)}, p_{(k)})
\Big]
}
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[4]}inter}
=
\overset{\frac{n - m}{m - 1 - \Lambda}}{\underset{\Psi = 0}{\sum}}{
\Big(
\overset{m - 1}{\underset{k = 0}{\sum}}{
1
}
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[4]}inter}
=
\overset{\frac{n - m}{m - 1 - \Lambda}}{\underset{\Psi = 0}{\sum}}{
\Big(
\big( (m - 1) - (0) + 1 \big) \cdot 1
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[4]}inter}
=
\overset{\frac{n - m}{m - 1 - \Lambda}}{\underset{\Psi = 0}{\sum}}{
\Big(
m
\Big)
}
\bigg)
\\[1em]
\iff
\bigg(
\mathcal{W}_{{}_{[4]}inter}
=
\Big(
\big( (\frac{n - m}{m - 1 - \Lambda}) - 0 \big) + 1
\Big)
\cdot
\Big(
m
\Big)
\bigg)
\iff
\bigg(
\mathcal{W}_{{}_{[4]}inter}
=
\Big(
\frac{n - 1 - \Lambda}{m - 1 - \Lambda}
\Big)
\cdot
\Big(
m
\Big)
\bigg)
\iff
\boxed{
\bigg(
\mathcal{W}_{{}_{[4]}inter}
=
\frac{nm - m - m \Lambda}{m - 1 - \Lambda}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}_{{}_{[4]}total}
:=
\mathcal{W}_{{}_{[4]}post}
+
\mathcal{W}_{{}_{[4]}inter}
+
\mathcal{W}_{{}_{[4]}pre}
=
0 + \frac{nm - m - m \Lambda}{m - 1 - \Lambda} + 0
=
\frac{nm - m - m \Lambda}{m - 1 - \Lambda}
\Bigg)
}
\end{cases}
\end{array}
$$

Part 36 :

- In this part, we compute the new total number of operations $\mathcal{W}'_{{}_{[4]}total}$ performed before, during and after the scan of the text $T$, by performing a pre-computation phase in which we 
  compute the "block jump" before the scan of the text $T$ 
	
	- Here, only a single operation (which is the call to function $\delta_{[3]}(\phi)$ ) is performed per block of text, because the tests for each block of text have already been performed during 
	  the pre-computation phase
	
	- By performing such a pre-computation phase, the total number of operations $\mathcal{W}'_{{}_{[4]}total}$ performed before, during and after the scan of the text $T$ is less than $\mathcal{W}_{{}_{[4]}total}$. 
	  It means that the algorithm does not need to perform as many operations as in the case with $\mathcal{W}_{{}_{[4]}total}$, which makes the algorithm more efficient

	- $\mathcal{W}'_{{}_{[4]}pre}$ is the new number of operations performed before the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[4]}inter}$ is the new number of operations performed during the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[4]}pos}$ is the new number of operations performed after the scan of the text $T$ 
	
	- $\mathcal{W}'_{{}_{[4]}total}$ is the new total number of operations performed before, during and after the scan of the text $T$ 
	
	- The table $\delta_{[3]}(\phi)$ is filled in during the pre-computation phase, and $\delta_{[3]}(\phi)$ is then consulted (during the scan of the text $T$) at each 
	  non-correspondence between the last character inspected of the current block and the last character inspected of the pattern $P$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\overbrace{
\left(
\underbrace{
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \phi \in \{0, \dots, m - 2\}, \quad
\delta_{[3]}(\phi)
=
\begin{cases}
\bigg(
P_{suffixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
max\Big(
P_{suffixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
max\Big(
P_{prefixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
m
\bigg)
\end{cases}
\right)
}_{
\text{Here, since the number of operations is equal to the number of calls to } \delta_{[3]}(\phi)
\text{ , and since } \delta_{[3]}(\phi) \text{ is called for every } \phi \text{ in } \{0, \dots, m - 2\} \text{ and for each case, }
\delta_{[3]}(\phi) \text{ is called } Card(\{0, \dots, m - 2\}) + Card(\{0, \dots, m - 2\}) + Card(\{0, \dots, m - 2\}) \text{ times (case 1 + case 2 + case 3)}
}
\Rightarrow
\boxed{
\bigg(
\mathcal{W}'_{{}_{[4]}pre}
:=
Card(\{0, \dots, m - 2\})
+
Card(\{0, \dots, m - 2\})
+
Card(\{0, \dots, m - 2\})
=
m - 1 + m - 1 + m - 1
=
3m - 3
\bigg)
}
\right)
}^{
\text{Performed before the algorithm}
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}'_{{}_{[4]}inter}
:=
\overset{\frac{n - m}{m - 1 - \Lambda}}{\underset{\Psi = 0}{\sum}}{
\Big(
\mathbb{1}\Big[
\delta_{[3]}(t_{(\mathcal{J}_{{}_{[4]}{min}_{(\Psi)}} + m - 1)})
\Big]
\Big)
}
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\mathcal{W}'_{{}_{[4]}inter}
=
\overset{\frac{n - m}{m - 1 - \Lambda}}{\underset{\Psi = 0}{\sum}}{
\Big(
\mathbb{1}\Big[
\delta_{[3]}(t_{(\mathcal{J}_{{}_{[4]}{min}_{(\Psi)}} + m - 1)})
\Big]
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}'_{{}_{[4]}inter}
=
\overset{\frac{n - m}{m - 1 - \Lambda}}{\underset{\Psi = 0}{\sum}}{
\Big(
1
\Big)
}
\bigg)
\iff
\bigg(
\mathcal{W}'_{{}_{[4]}inter}
=
\Big(
\big( (\frac{n - m}{m - 1 - \Lambda}) - 0 \big) + 1
\Big)
\cdot
\Big(
1
\Big)
\bigg)
\iff
\boxed{
\bigg(
\mathcal{W}'_{{}_{[4]}inter}
=
\frac{n - 1 - \Lambda}{m - 1 - \Lambda}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\mathcal{W}'_{{}_{[4]}total}
:=
\mathcal{W}'_{{}_{[4]}post}
+
\mathcal{W}'_{{}_{[4]}inter}
+
\mathcal{W}'_{{}_{[4]}pre}
=
0 + \frac{n - 1 - \Lambda}{m - 1 - \Lambda} + 3m - 3
=
\frac{n - 1 - \Lambda}{m - 1 - \Lambda}
+
\frac{(3m - 3) \cdot (m - 1 - \Lambda)}{m - 1 - \Lambda}
=
\frac{n - 1 - \Lambda}{m - 1 - \Lambda}
+
\frac{(3m^{2} - 3m - 3m \Lambda - 3m + 3 + 3 \Lambda)}{m - 1 - \Lambda}
=
\frac{n + 2 + 2 \Lambda + 3m^{2} - 6m - 3m \Lambda}{m - 1 - \Lambda}
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
\frac{n + 2 + 2 \Lambda + 3m^{2} - 6m - 3m \Lambda}{m - 1 - \Lambda}
<
\frac{nm - m - m \Lambda}{m - 1 - \Lambda}
\bigg)
\iff
\bigg(
\frac{nm - m - m \Lambda}{m - 1 - \Lambda}
>
\frac{n + 2 + 2 \Lambda + 3m^{2} - 6m - 3m \Lambda}{m - 1 - \Lambda}
\bigg)
\iff
\bigg(
\frac{nm - m - m \Lambda}{m - 1 - \Lambda}
-
\frac{n + 2 + 2 \Lambda + 3m^{2} - 6m - 3m \Lambda}{m - 1 - \Lambda}
>
0
\bigg)
\iff
\bigg(
\frac{nm - m - m \Lambda + ( - n - 2 - 2 \Lambda - 3m^{2} + 6m + 3m \Lambda )}{m - 1 - \Lambda}
>
0
\bigg)
\\[1em]
\quad
\iff
\bigg(
\frac{nm + 5m + 2m \Lambda - n - 2 - 2 \Lambda - 3m^{2}}{m - 1 - \Lambda}
>
0
\bigg)
\iff
\bigg(
\frac{(nm - n) + (- 3m^{2} + 5m - 2) + (2m \Lambda - 2 \Lambda)}{m - 1 - \Lambda}
>
0
\bigg)
\iff
\bigg(
\frac{n \cdot (m - 1) + (-3m + 2) \cdot (m - 1) + 2 \Lambda \cdot (m - 1)}{m - 1 - \Lambda}
>
0
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
m - 1 - \Lambda \neq 0
\Big)
\iff
\Big(
- \Lambda \neq 1 - m
\Big)
\iff
\Big(
\beta'
\neq
m - 1
\Big)
\bigg)
\land
\bigg(
\Big(
m - 1 - \Lambda < 0
\Big)
\iff
\Big(
- \Lambda < 1 - m
\Big)
\iff
\Big(
\Lambda > m - 1
\Big)
\bigg)
\land
\bigg(
\Big(
m - 1 - \Lambda > 0
\Big)
\iff
\Big(
- \Lambda > 1 - m
\Big)
\iff
\Big(
\Lambda < m - 1
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\frac{n \cdot (m - 1) + (-3m + 2) \cdot (m - 1) + 2 \Lambda \cdot (m - 1)}{m - 1 - \Lambda}
>
0
\bigg)
\iff
\bigg(
\Big(
\Lambda < m - 1
\Big)
\land
\Big(
n \cdot (m - 1) + (-3m + 2) \cdot (m - 1) + 2 \Lambda \cdot (m - 1) > 0
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda < m - 1
\Big)
\land
\Big(
n \cdot (m - 1) > - (-3m + 2) \cdot (m - 1) - 2 \Lambda \cdot (m - 1)
\Big)
\bigg)
\\[1em]
\quad
\iff
\bigg(
\Big(
\Lambda < m - 1
\Big)
\land
\Big(
n
>
\frac{
- (-3m + 2) \cdot (m - 1) - 2 \Lambda \cdot (m - 1)
}
{
(m - 1)
}
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda < m - 1
\Big)
\land
\Big(
n
>
- (-3m + 2) - 2 \Lambda
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda < m - 1
\Big)
\land
\Big(
n
>
3m - 2 - 2 \Lambda
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\frac{n \cdot (m - 1) + (-3m + 2) \cdot (m - 1) + 2 \Lambda \cdot (m - 1)}{m - 1 - \Lambda}
>
0
\bigg)
\iff
\bigg(
\Big(
\Lambda > m - 1
\Big)
\land
\Big(
n \cdot (m - 1) + (-3m + 2) \cdot (m - 1) + 2 \Lambda \cdot (m - 1) < 0
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda > m - 1
\Big)
\land
\Big(
n \cdot (m - 1) < - (-3m + 2) \cdot (m - 1) - 2 \Lambda \cdot (m - 1)
\Big)
\bigg)
\\[1em]
\quad
\iff
\bigg(
\Big(
\Lambda > m - 1
\Big)
\land
\Big(
n
<
\frac{
- (-3m + 2) \cdot (m - 1) - 2 \Lambda \cdot (m - 1)
}
{
(m - 1)
}
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda > m - 1
\Big)
\land
\Big(
n
<
- (-3m + 2) - 2 \Lambda
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda > m - 1
\Big)
\land
\Big(
n
<
3m - 2 - 2 \Lambda
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
\underbrace{
\frac{n + 2 + 2 \Lambda + 3m^{2} - 6m - 3m \Lambda}{m - 1 - \Lambda}
}_{\mathcal{W}'_{{}_{[4]}total}}
<
\underbrace{
\frac{nm - m - m \Lambda}{m - 1 - \Lambda}
}_{\mathcal{W}_{{}_{[4]}total}}
\bigg)
\iff
\bigg(
\Big(
\Lambda < m - 1
\Big)
\land
\Big(
n
>
3m - 2 - 2 \Lambda
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda > m - 1
\Big)
\land
\Big(
n
<
3m - 2 - 2 \Lambda
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 38 :

- In this part, we conclude

$$
\begin{array}{l}
\boxed{
\therefore
\begin{cases}
(P1) \quad
\Bigg(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\bigg(
\forall t_{(0)}, \dots, t_{(n - 1)} \in \varsigma, \quad
\exists! T \in \varsigma^{n}, \quad
T
=
(t_{(0)}, \dots, t_{(n - 1)})
\bigg)
\Rightarrow
\bigg(
\forall m \in \{1, \dots, n\}, \quad
\forall p_{(0)}, \dots, p_{(m - 1)} \in \varsigma, \quad
\exists! P \in \varsigma^{m}, \quad
P
=
(p_{(0)}, \dots, p_{(m - 1)})
\bigg)
\Bigg)
\\[1em]
(P2) \quad
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{suffixpos_{(\xi)}}
=
\underbrace{
\bigg\{
\lambda
\ \bigg| \
\bigg(
\psi \in \{0, \dots, \xi - Card(B_{P_{suffix_{(1)}}}) + 1\}
\bigg)
\land
\bigg(
\lambda \in \{0 + Card(B_{P_{suffix_{(1)}}}) - 1, \dots, \xi\}
\bigg)
\land
\bigg(
P_{suffix_{(2)}}
=
(p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)})
=
(p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)})
=
P_{suffix_{(1)}}
\bigg)
\land
\bigg(
\Big(
\psi - 1 \geq 0
\Big)
\Rightarrow
\Big(
p_{(\psi - 1)} \neq p_{(\xi)}
\Big)
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{suffixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{suffix_{(2)}} \text{, where } P_{suffix_{(2)}}
\text{ can be preceded by at least one character in } P \text{, or can be flushed with the left edge of } P
}
\ \
\Bigg)
\\[1em]
(P3) \quad
\Bigg(
\ \
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \xi \in \{0, \dots, m - 2\}, \quad
P_{prefixpos_{(\xi)}}
=
\underbrace{
\bigg\{
\lambda'
\ \bigg| \
\bigg(
\psi' \in \{m - 1 - Card(P) + 1 - Card(B_{P_{suffix_{(1)}}}) + 1, \dots, (0) - 1\}
\bigg)
\land
\bigg(
\lambda' \in \{0, \dots, (0 + Card(B_{P_{suffix_{(1)}}}) - 1) - 1\}
\bigg)
\land
\bigg(
P_{prefix_{(1)}}
=
(p_{(0)}, \dots, p_{(\lambda')})
=
(p_{(m - \lambda' - 1)}, \dots, p_{(m - 1)})
\bigg)
\land
\bigg(
Card(B_{P_{prefix_{(1)}}})
<
Card(B_{P_{suffix_{(1)}}})
\bigg)
\bigg\}
}_{
\text{For an arbitrary boundary position } \xi \text{ , }
P_{prefixpos_{(\xi)}}
\text{ is the set of all the positions of the last letter of each } P_{prefix_{(1)}} \text{, where } P_{prefix_{(1)}}
\text{ has a length exactly less than that of } P_{suffix_{(1)}}
}
\ \
\Bigg)
\\[1em]
(P4) \quad
\Bigg(
\bigg(
B_{P_{suffix_{(1)}}}
=
\Big\{\Big\{ p_{(\xi + 1)}, p_{(\xi + 2)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\land
\underbrace{
\bigg(
B_{P_{suffix_{(2)}}}
=
\Big\{\Big\{ p_{(\psi)}, p_{(\psi + 1)}, \dots, p_{(\lambda - 1)}, p_{(\lambda)} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{suffix_{(2)}} \text{ (= one possible occurrence of } P_{suffix_{(1)}} \text{ )}
}
\\
{
\text{ in the current block and each } P_{suffix_{(2)}} \text{ can also be viewed as a multiset of characters in } P
}
}
}
\land
\bigg(
Card(B_{P_{suffix_{(1)}}})
=
Card(B_{P_{suffix_{(2)}}})
=
m - 1 - \xi
\bigg)
\land
\underbrace{
\bigg(
B_{P_{prefix_{(1)}}}
=
\Big\{\Big\{ p_{(0)}, p_{(1)}, \dots, p_{(\lambda' - 1)}, p_{(\lambda')} \Big\}\Big\}_{M}
\bigg)
}_{
\substack{
{
\text{There is at least one possible } P_{prefix_{(1)}} \text{ (= one possible pattern suffix)}
}
\\
{
\text{ in the current block and each } P_{prefix_{(1)}} \text{ can be viewed as a multiset of characters in } P
}
}
}
\land
\bigg(
Card(B_{P_{prefix_{(1)}}})
=
\lambda' + 1
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
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\delta_{[2]}(\alpha)
=
\begin{cases}
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\bigg(
\beta'
=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
\alpha
\land
\gamma < m - 1
\Big\}
\Big)
\bigg)
\Rightarrow
\bigg(
\delta_{[2]}(\alpha)
=
m - 1 - \beta'
\bigg)
\\[1em]
\bigg(
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta_{[2]}(\alpha)
=
m
\bigg)
\end{cases}
\right)
\\[1em]
(P6) \quad
\left(
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \phi \in \{0, \dots, m - 2\}, \quad
\delta_{[3]}(\phi)
=
\begin{cases}
\bigg(
P_{suffixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
max\Big(
P_{suffixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
max\Big(
P_{prefixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\delta_{[3]}(\phi)
=
m
\bigg)
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
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\underbrace{
\exists! {\iota}_{max} \in \mathbb{N}
}_{
\text{We assume that the algorithm stops}
}
, \quad
\forall \iota \in \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max}\}, \quad
\mathcal{J}_{min} : \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max}\} \to \{0, \dots, n - m\}, \quad
\iota \mapsto \mathcal{J}_{{min}_{{\big({\iota}\big)}}}, \quad
\begin{cases}
\mathcal{J}_{{min}_{{\big({0}\big)}}}
=
0
\\[1em]
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
:=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)}
\land
\gamma < m - 1
\Big\}
\Big)
\\[1em]
\forall \xi \in \{0, \dots, m - 2\}, \quad
\exists! \Lambda \in \{0, \dots, m\}, \quad
\Lambda
:=
\begin{cases}
\bigg(
P_{suffixpos_{(\xi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
max\Big(
P_{suffixpos_{(\xi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
max\Big(
P_{prefixpos_{(\xi)}}
\Big)
\bigg)
\\[1em]
\bigg(
P_{suffixpos_{(\xi)}} = \emptyset
\land
P_{prefixpos_{(\xi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\Lambda
=
m
\bigg)
\end{cases}
\\[1em]
\forall \iota \in \{0, 1, 2, 3, \dots, \iota', \dots, {\iota}_{max} - 1\}, \quad
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
:=
\begin{cases}
\bigg(
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)} \neq p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
=
\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1 - \beta'
\bigg)
\\[1em]
\bigg(
t_{(\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1)} = p_{(m - 1)}
\bigg)
\Rightarrow
\bigg(
\mathcal{J}_{{min}_{{\big({\iota + 1}\big)}}}
=
\mathcal{J}_{{min}_{{\big({\iota}\big)}}} + m - 1 - \Lambda
\bigg)
\end{cases}
\end{cases}
\ \
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
\forall n \in \mathbb{N}_{\geq 1}, \quad
\forall m \in \{1, \dots, n\}, \quad
\forall \alpha \in \varsigma, \quad
\forall \phi \in \{0, \dots, m - 2\}, \quad
\delta : \varsigma \times \{0, \dots, m - 2\} \to \{0, \dots, m\}, \quad
(\alpha, \phi) \mapsto \delta(\alpha, \phi), \quad
\delta(\alpha, \phi)
:=
\begin{cases}
\text{(Property 1)} \quad
\bigg(
\Big(
\alpha \neq p_{(m - 1)}
\Big)
\land
\Big(
\forall \gamma \in \{0, \dots, m - 2\}, \quad
\exists! \beta' \in \{0, \dots, m - 2\}, \quad
\beta'
:=
max\Big(
\Big\{
\gamma
\ \Big| \
p_{(\gamma)}
=
\alpha
\land
\gamma < m - 1
\Big\}
\Big)
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m - 1 - \beta'
\bigg)
\\[1em]
\text{(Property 2)} \quad
\bigg(
\alpha \neq p_{(m - 1)}
\land
\alpha \notin \Big\{\Big\{ p_{(0)}, \dots, p_{(m - 2)}, p_{(m - 1)} \Big\}\Big\}_{M}
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m
\bigg)
\\[1em]
\text{(Property 3)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
max\Big(
P_{suffixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\text{(Property 4)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} \neq \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
max\Big(
P_{prefixpos_{(\phi)}}
\Big)
\bigg)
\\[1em]
\text{(Property 5)} \quad
\bigg(
\alpha = p_{(m - 1)}
\land
P_{suffixpos_{(\phi)}} = \emptyset
\land
P_{prefixpos_{(\phi)}} = \emptyset
\bigg)
\Rightarrow
\bigg(
\delta(\alpha, \phi)
=
m
\bigg)
\end{cases}
\ \
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
\Bigg(
\underbrace{
\frac{n}{m} + Card(\varsigma)
}_{\mathcal{W}'_{{}_{[2]}total}}
<
\underbrace{
n
}_{\mathcal{W}_{{}_{[2]}total}}
\Bigg)
\\[1em]
(P10) \quad
\Bigg(
\bigg(
\underbrace{
\frac{n - 1 - \beta'}{m - 1 - \beta'} + 2 \cdot Card(\varsigma)
}_{\mathcal{W}'_{{}_{[3]}total}}
<
\underbrace{
\frac{nm - m - m \beta'}{m - 1 - \beta'}
}_{\mathcal{W}_{{}_{[3]}total}}
\bigg)
\iff
\bigg(
\Big(
\beta' < m - 1
\Big)
\land
\Big(
n >
\beta' + 2 \cdot Card(\varsigma) - \frac{2 \cdot Card(\varsigma) \cdot \beta'}{(m - 1)} + 1
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\Bigg)
\\[1em]
(P11) \quad
\Bigg(
\bigg(
\underbrace{
\frac{n + 2 + 2 \Lambda + 3m^{2} - 6m - 3m \Lambda}{m - 1 - \Lambda}
}_{\mathcal{W}'_{{}_{[4]}total}}
<
\underbrace{
\frac{nm - m - m \Lambda}{m - 1 - \Lambda}
}_{\mathcal{W}_{{}_{[4]}total}}
\bigg)
\iff
\bigg(
\Big(
\Lambda < m - 1
\Big)
\land
\Big(
n
>
3m - 2 - 2 \Lambda
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\iff
\bigg(
\Big(
\Lambda > m - 1
\Big)
\land
\Big(
n
<
3m - 2 - 2 \Lambda
\Big)
\land
\Big(
m \neq 1
\Big)
\bigg)
\Bigg)
\end{cases}
}
\end{array}
$$



