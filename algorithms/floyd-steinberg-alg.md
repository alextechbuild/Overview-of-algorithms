
Definition of the property of the Floyd-Steinberg algorithm :




- The $\boxed{\text{pixel currently visited}}$ (by the algorithm) is located at the $i$-th row and $j$-th column of the $\boxed{\text{original}}$ image (= the input image of the algorithm) 
  (similar to a matrix of pixels). Thus, this pixel can be viewed as being located at position $\boxed{(i, j)}$ 

- $\boxed{a_{(i, j)}}$ represents the color (between $0$ and $255$) of one single pixel located at the $i$-th row and $j$-th column of the $\boxed{\text{original}}$ image

- $\boxed{\eta_{(i, j)}}$ represents the color (either black $0$ or white $255$) of one single pixel located at the $i$-th row and $j$-th column of the $\boxed{\text{final}}$ image (= the output image of the algorithm) 
  (= the dithered digital image in black and white $\{0, 255\}$ )

- $\boxed{\eta_{(i, j)}}$ determines if the color $a_{(i, j)}$ of the currently visited pixel is either "blackish" or "whitish" (based on the value of $\bar{x}$, which provides an uniform distribution of white and black pixels in 
  the dithered image). 
  For example, the value $200$ is considered “whitish” because it is closer to $255$ (white) than to $0$ (black). Therefore, we replace it with $255$, because the dithered image in our case needs 
  to contain either white or black $\{0, 255\}$ 

- The gap $\boxed{e_{(i, j)}}$ is the difference in brightness between the original color $a_{(i, j)}$ of the pixel (the one currently being visited) in the original image $M'$ and white or black 
  (depending on whether the color is considered "whitish" or "blackish")
  For example, the value $200$ is considered “whitish” because it is closer to $255$ (white) than to $0$ (black). Therefore, we replace it with $255$, because the dithered image in our case needs 
  to contain either white or black $\{0, 255\}$ 

	- If the gap is positive $e_{(i, j)} > 0$, then we add clarity to the neighbouring pixels
	- If the gap is negative $e_{(i, j)} < 0$, then we add shade to the neighbouring pixels
	
	- If we did not distribute the difference in brightness with a gap $e_{(i, j)}$, then we would have black and / or white blocks in the dithered image :
		
		- All blackish details in a blackish area would be hidden because they would all be black
		- And / or all whitish details in a whitish area would be hidden because they would all be white


- At the currently visited pixel $(i, j)$, we transmit the gap $e_{(i, j)}$ to the colors of the neighboring pixels $(i + \Delta_{y}, j + \Delta_{x})$. The pixel at $(i, j)$ can be viewed as the $\boxed{\text{"giver"}}$ , and the other pixels 
  can be viewed as the $\boxed{\text{"receivers"}}$ :
  
	- Thus, from the “giver” point of view, we have : $e_{(i, j)} \xrightarrow{\text{gives to}} (i + \Delta_{y}, j + \Delta_{x})$ (process called $\boxed{\text{“diffusion”}}$ )

	- We can also change the perspective (i.e., switch from the “giver” point of view to a “receiver” point of view chosen from among all possible receivers) by performing a change of 
	  variables : $(\alpha = i + \Delta_{y} \iff \alpha - \Delta_{y} = i) \land (\beta = j + \Delta_{x} \iff \beta - \Delta_{x} = j)$ 
		- Thus, from the "receiver" point of view (which is a receiver chosen from among all possible receivers), we have : $e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})} \xrightarrow{\text{given by}} (\alpha - \Delta_{y}, \beta - \Delta_{x})$ 

- $\boxed{a_{(i + \Delta_{y}, j + \Delta_{x})}}$ can be viewed as the receiver that receives $\boxed{1}$ gap from its giver, which is the gap $e_{(i, j)}$ of its giver at $(i, j)$ 

- $\boxed{a_{(\alpha, \beta)}}$ can be viewed as the receiver that $\boxed{\text{has already}}$ received $\boxed{\text{all}}$ the possible gaps $e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}$ from all its neighboring pixels at $(\alpha - \Delta_{y}, \beta - \Delta_{x})$ 
  (and its neighboring pixels are not necessarily the neighbors of the giver at $(i, j)$ )


- $\Delta_{x}$ and $\Delta_{y}$ can be viewed together as displacement vector $\begin{pmatrix}\Delta_{x} \\\Delta_{y}\end{pmatrix}$ from the currently visited pixel at $(i, j)$ to a neighboring pixel at $(i + \Delta_{y}, j + \Delta_{x})$ :
	- This displacement vector can be used with the Tchebychev norm ${\|\cdot\|}_{\infty}$ to obtain as many $\Delta_{x}$ and $\Delta_{y}$ as possible, since :
	
		- The Tchebychev norm considers diagonal vectors (characterizing diagonal neighboring pixels at $(i + \Delta_{y}, j + \Delta_{x})$ ) to be at the same distance (from the currently visited pixel 
		  at $(i, j)$ ) as horizontal and vertical vectors (characterizing the nearest horizontal and vertical neighboring pixels at different $(i + \Delta_{y}, j + \Delta_{x})$ )

	- Then, the found $\Delta_{x}$ and $\Delta_{y}$ values will be filtered by the row-major lexicographical order to obtain the final values $\Delta_{x}$ and $\Delta_{y}$ 

- $S_{{o}_{(x)}}$ ("$o$" for "offset") denote the set of all possible final values of $\Delta_{x}$, and $S_{{o}_{(y)}}$ ("$o$" for "offset") denote the set of all possible final values of $\Delta_{y}$.
  The elements of the set $S_{o}$ (with $o$ for "offset") are called "offset vectors"


- The Floyd-Steinberg algorithm uses the row-major lexicographical order because it corresponds to the row-major order (denoted 'C') in computer science, and because 
  when a CPU reads a pixel from memory, the CPU does not just retrieve that single pixel : the CPU loads a “cache line”, which is a block of adjacent data in a single line. 
  In row-major order, the next pixel in the loop of the algorithm ($j+1$) is right next to it in memory. It is therefore already in the CPU’s cache, and access is instantaneous (which is optimal)


- For any image larger than a postage stamp (16×16 pixels), the dithered image is visually coherent




Context of the algorithm property (part 1) :

$$
\begin{array}{l}
\exists! W, H \in \mathbb{N}_{\geq 1}, \quad
\Bigg(
\bigg(
Width_{pixels} := W
\bigg)
\land
\bigg(
Height_{pixels} := H
\bigg)
\Bigg)
\Rightarrow
\Bigg(
\bigg(
(a_{(k, l)})_{
\substack{{ 1 \leq k \leq H } \\ { 1 \leq l \leq W }}
}
\in
\mathcal{M}_{H, W}(\{0, 1, 2, \dots, 255\})
\bigg)
\land
\bigg(
(\eta_{m, p})_{
\substack{{ 1 \leq m \leq H } \\ { 1 \leq p \leq W }}
}
\in
\mathcal{M}_{H, W}(\{0, 255\})
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\left(
\exists! \bar{A}, \bar{N} \in \mathbb{R}, \quad
\left(
\bar{A}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ k = H } \\ { l = W }}}
{\underset{\substack{{ k = 1 } \\ { l = 1 }}}{\sum}}
{a_{k, l}}
\right)
\right)
\land
\left(
\bar{N}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ m = H } \\ { p = W }}}
{\underset{\substack{{ m = 1 } \\ { p = 1 }}}{\sum}}
{\eta_{m, p}}
\right)
\right)
\right)
\Rightarrow
\Bigg(
S_{pixels}
:=
\Big\{
(x,y, a_{(i, j)})
\ \Big| \
0 \leq x \leq W - 1
\land
0 \leq y \leq H - 1
\land
1 \leq i \leq H
\land
1 \leq j \leq W
\Big\}
\Bigg)
\\[1em]
\Rightarrow
\left(
\exists! M' \in \mathcal{M}_{H, W}(S_{pixels}), \quad
\left(
M'
=
\begin{bmatrix}
(0, 0, a_{(1, 1)}) & (1, 0, a_{(1, 2)}) & \dots & (W - 1, 0, a_{(1, W)}) \\
(0, 1, a_{(2, 1)}) & (1, 1, a_{(2, 2)}) & \dots & (W - 1, 1, a_{(2, W)}) \\
\vdots & \vdots & \ddots & \vdots \\
(0, H - 1, a_{(H, 1)}) & (1, H - 1, a_{(H, 2)}) & \dots & (W - 1, H - 1, a_{(H, W)}) \\
\end{bmatrix}
\ \
\right)
\land
\Big(
Image_{pixels} := M'
\Big)
\right)
\\
\hspace{750pt}
\end{array}
$$

Context of the algorithm property (part 2) :

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg\{
\\[1em]
\quad \quad
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\exists! a_{{(\alpha, \beta)}_{(\iota)}} \in \{0, 1, 2, \dots, 255\}, \quad
\exists! \eta_{(i, j)} \in \{0, 255\}, \quad
\exists! \iota_{max} \in \mathbb{N}_{\geq 1}, \quad
\\[1em]
\quad \quad
\forall \iota \in \{1, \dots, \iota', \dots, \iota_{max}\}, \quad
\exists! e_{(i, j)} \in \{-127, \dots, 127\}, \quad
\forall \Delta_{x} \in S_{{o}_{(x)}}, \quad
\forall \Delta_{y} \in S_{{o}_{(y)}}, \quad
a_{(i + \Delta_{y}, j + \Delta_{x})} : \mathbb{N} \to \mathbb{N}, \quad
\iota \mapsto a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}, \quad
\\[1em]
\quad \quad
\Bigg[
\\[1em]
\quad \quad \quad \quad
\left(
\eta_{(i, j)}
=
\begin{cases}
a_{{(i, j)}_{(\iota)}} < 128
\Rightarrow
\eta_{(i, j)} = 0
\\[1em]
a_{{(i, j)}_{(\iota)}} \geq 128
\Rightarrow
\eta_{(i, j)} = 255
\end{cases}
\ \
\right)
\land
\bigg(
a_{{(i, j)}_{(\iota)}} = \eta_{(i, j)}
\bigg)
\land
\bigg(
e_{(i, j)}
=
a_{{(i, j)}_{(\iota)}} - \eta_{(i, j)}
\bigg)
\land
\left(
w_{(\Delta_{x}, \Delta_{y})}
=
\begin{cases}
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
1 \\
0
\end{pmatrix}
\right)
\Rightarrow
\Big(
w_{(\Delta_{x}, \Delta_{y})}
=
\frac{7}{16}
\Big)
\\[1em]
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
\right)
\Rightarrow
\Big(
w_{(\Delta_{x}, \Delta_{y})}
=
\frac{3}{16}
\Big)
\\[1em]
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
0 \\
1
\end{pmatrix}
\right)
\Rightarrow
\Big(
w_{(\Delta_{x}, \Delta_{y})}
=
\frac{5}{16}
\Big)
\\[1em]
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
1 \\
1
\end{pmatrix}
\right)
\Rightarrow
\Big(
w_{(\Delta_{x}, \Delta_{y})}
=
\frac{1}{16}
\Big)
\end{cases}
\ \
\right)
\\[1em]
\quad \quad \quad \quad
\land \
\bigg(
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{w_{(\Delta_{x}, \Delta_{y})}}
=
\frac{7}{16} + \frac{3}{16} + \frac{5}{16} + \frac{1}{16}
=
1
\bigg)
\land
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\\[1em]
\quad \quad
\Bigg]
\\[1em]
\Bigg\}
\end{cases}
\\
\hspace{750pt}
\end{array}
$$

Algorithm property :

$$
\begin{array}{l}
\boxed{
\Bigg(
\bigg(
e_{(H, W)} = - 127
\bigg)
\Rightarrow
\bigg(
\bar{N}
>
\bar{A}
\bigg)
\Bigg)
\land
\Bigg(
\bigg(
e_{(H, W)} = 0
\bigg)
\Rightarrow
\bigg(
\bar{N}
=
\bar{A}
\bigg)
\Bigg)
\land
\Bigg(
\bigg(
e_{(H, W)} = + 127
\bigg)
\Rightarrow
\bigg(
\bar{N}
<
\bar{A}
\bigg)
\Bigg)
\land
\Bigg(
\bar{N}
\underset{H \cdot W \to +\infty}{=}
\bar{A}
\Bigg)
}
\end{array}
$$


Proof of the algorithm property :

Part 1 :

- In this part, we start from the arithmetic mean brightness $\bar{A}$ of an original digital image $M'$ in grayscale and from the arithmetic mean brightness $\bar{N}$ of the final image 
  (= dithered digital image in black and white $\{0, 255\}$ ) to show where the gap $e_{(i, j)}$ (and the sum of the gaps $e$) and the threshold value $\bar{x}$ (used for $\eta_{(i, j)}$) come from

- The $\boxed{\text{pixel currently visited}}$ (by the algorithm) is located at the $i$-th row and $j$-th column of the $\boxed{\text{original}}$ image (= the input image of the algorithm) 
  (similar to a matrix of pixels). Thus, this pixel can be viewed as being located at position $\boxed{(i, j)}$ 

- $\boxed{a_{(i, j)}}$ represents the color (between $0$ and $255$) of one single pixel located at the $i$-th row and $j$-th column of the $\boxed{\text{original}}$ image

- $\boxed{\eta_{(i, j)}}$ represents the color (either black $0$ or white $255$) of one single pixel located at the $i$-th row and $j$-th column of the $\boxed{\text{final}}$ image (= the output image of the algorithm) 
  (= the dithered digital image in black and white $\{0, 255\}$ )

- The gap $\boxed{e_{(i, j)}}$ is the difference in brightness between the original color $a_{(i, j)}$ of the pixel (the one currently being visited) in the original image $M'$ and white or black 
  (depending on whether the color is considered "whitish" or "blackish")
  For example, the value $200$ is considered “whitish” because it is closer to $255$ (white) than to $0$ (black). Therefore, we replace it with $255$, because the dithered image in our case needs 
  to contain either white or black $\{0, 255\}$ 

	- If the gap is positive $e_{(i, j)} > 0$, then we add clarity to the neighbouring pixels
	- If the gap is negative $e_{(i, j)} < 0$, then we add shade to the neighbouring pixels
	
	- If we did not distribute the difference in brightness with a gap $e_{(i, j)}$, then we would have black and / or white blocks in the dithered image :
		
		- All blackish details in a blackish area would be hidden because they would all be black
		- And / or all whitish details in a whitish area would be hidden because they would all be white

- $\boxed{\bar{x}}$ is the threshold value which provides an uniform distribution of white and black pixels in the dithered image

$$
\begin{array}{l}
\exists! W, H \in \mathbb{N}_{\geq 1}, \quad
\left(
\ \
\bigg(
\Big(
Width_{pixels} := W
\Big)
\land
\Big(
Height_{pixels} := H
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\boxed{
(a_{(k, l)})_{
\substack{{ 1 \leq k \leq H } \\ { 1 \leq l \leq W }}
}
}
\in
\underline{
\mathcal{M}_{H, W}(\{0, 1, 2, \dots, 255\})
}
\Big)
\land
\Big(
\boxed{
(\eta_{m, p})_{
\substack{{ 1 \leq m \leq H } \\ { 1 \leq p \leq W }}
}
}
\in
\underline{
\mathcal{M}_{H, W}(\{0, 255\})
}
\Big)
\bigg)
\Rightarrow
\left(
\exists! \bar{A}, \bar{N} \in \mathbb{R}, \quad
\left(
\bar{A}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ k = H } \\ { l = W }}}
{\underset{\substack{{ k = 1 } \\ { l = 1 }}}{\sum}}
{a_{k, l}}
\right)
\right)
\land
\left(
\bar{N}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ m = H } \\ { p = W }}}
{\underset{\substack{{ m = 1 } \\ { p = 1 }}}{\sum}}
{\eta_{m, p}}
\right)
\right)
\right)
\Rightarrow
\boxed{
\bigg(
S_{pixels}
:=
\Big\{
(x,y, a_{(i, j)})
\ \Big| \
\Big(
0 \leq x \leq W - 1
\Big)
\land
\Big(
0 \leq y \leq H - 1
\Big)
\land
\Big(
1 \leq i \leq H
\Big)
\land
\Big(
1 \leq j \leq W
\Big)
\Big\}
\bigg)
}
\Rightarrow
\left(
\exists! M' \in \mathcal{M}_{H, W}(S_{pixels}), \quad
\left(
M'
=
\begin{bmatrix}
(0, 0, a_{(1, 1)}) & (1, 0, a_{(1, 2)}) & \dots & (W - 1, 0, a_{(1, W)}) \\
(0, 1, a_{(2, 1)}) & (1, 1, a_{(2, 2)}) & \dots & (W - 1, 1, a_{(2, W)}) \\
\vdots & \vdots & \ddots & \vdots \\
(0, H - 1, a_{(H, 1)}) & (1, H - 1, a_{(H, 2)}) & \dots & (W - 1, H - 1, a_{(H, W)}) \\
\end{bmatrix}
\ \
\right)
\land
\Big(
Image_{pixels} := M'
\Big)
\right)
\ \
\right)
\\[1em]
\Rightarrow
\begin{cases}
\left(
\ \
\left(
\bar{A}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ k = H } \\ { l = W }}}
{\underset{\substack{{ k = 1 } \\ { l = 1 }}}{\sum}}
{a_{k, l}}
\right)
\right)
\land
\left(
\left(
\bar{N}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ m = H } \\ { p = W }}}
{\underset{\substack{{ m = 1 } \\ { p = 1 }}}{\sum}}
{\eta_{m, p}}
\right)
\right)
\Rightarrow
\Big(
\forall \kappa_{1} \in \{1, \dots, H\}, \quad
\forall \kappa_{2} \in \{1, \dots, W\}, \quad
\eta_{(\kappa_{1}, \kappa_{2})} \in \{0, 255\}
\Big)
\right)
\right)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\exists! e \in \mathbb{R}, \quad
\bigg(
\Big(
\bar{A}
=
\bar{N} + e
\Big)
}
\because
\Big(
\forall \kappa_{1} \in \{1, \dots, H\}, \quad
\forall \kappa_{2} \in \{1, \dots, W\}, \quad
\underline{
\big(
a_{(\kappa_{1}, \kappa_{2})} \in \{0, 1, 2, \dots, 255\}
\big)
\land
\big(
\eta_{(\kappa_{1}, \kappa_{2})} \in \{0, 255\}
\big)
}
\Big)
\bigg)
\Rightarrow
\boxed{
\bigg(
\bar{A} \underset{e \to 0}{=} \bar{N}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\left(
\ \
\bigg(
\bar{A}
=
\bar{N} + e
\bigg)
\iff
\boxed{
\bigg(
e
=
\bar{A} - \bar{N}
\bigg)
}
\iff
\left(
e
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ k = H } \\ { l = W }}}
{\underset{\substack{{ k = 1 } \\ { l = 1 }}}{\sum}}
{a_{k, l}}
\right)
-
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ m = H } \\ { p = W }}}
{\underset{\substack{{ m = 1 } \\ { p = 1 }}}{\sum}}
{\eta_{m, p}}
\right)
\right)
\iff
\left(
e
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ k = H } \\ { l = W }}}
{\underset{\substack{{ k = 1 } \\ { l = 1 }}}{\sum}}
{a_{k, l}}
-
\overset{\substack{{ m = H } \\ { p = W }}}
{\underset{\substack{{ m = 1 } \\ { p = 1 }}}{\sum}}
{\eta_{m, p}}
\right)
\right)
\iff
\left(
e
=
\frac{1}{W \cdot H}
\cdot
\overset{\substack{{ i = W \cdot H } \\ { j = W \cdot H }}}
{\underset{\substack{{ i = 1 } \\ { j = 1 }}}{\sum}}
{
\Big(
\underbrace{
\boxed{
a_{(i, j)}
-
\eta_{(i, j)}
}
}_{\boxed{e_{(i, j)}}}
\Big)
}
\right)
\ \
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists! \bar{x} \in \mathbb{R}, \quad
\boxed{\bar{x}}
=
\underbrace{
\left\lceil
\frac{min(\{0, 1, 2, \dots, 255\}) + max(\{0, 1, 2, \dots, 255\})}{2}
\right\rceil
=
\left\lceil
\frac{0 + 255}{2}
\right\rceil
=
\left\lceil
127.5
\right\rceil
=
\boxed{128}
}_{\boxed{\text{rounding of the value}}}
\Bigg)
\end{cases}
\end{array}
$$

Part 2 :

- In this part, we first identify the global loop variant of the algorithm based on the general formula (and on the loops present in the algorithm). This guarantees that variables whose values 
  change from their previous values are changed a finite number of times (because the algorithm stops)

- $\boxed{\eta_{(i, j)}}$ determines if the color $a_{(i, j)}$ of the currently visited pixel is either "blackish" or "whitish" (based on the value of $\bar{x}$, which provides an uniform distribution of white and black pixels in 
  the dithered image). 
  For example, the value $200$ is considered “whitish” because it is closer to $255$ (white) than to $0$ (black). Therefore, we replace it with $255$, because the dithered image in our case needs 
  to contain either white or black $\{0, 255\}$ 

- $\boxed{\xi}$ represents the $\xi$-th time a variable changes its value from its previous value in the algorithm (similar to a recurrent sequence of order 1) (it can be viewed as a "state")

- Then, we examine what happens when we express the color $a_{(i, j)}$ of one and the same pixel in the next state $a_{{(i, j)}_{(\xi + 1)}}$ in terms of its color in the current state $a_{{(i, j)}_{(\xi)}}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
V_{g} : \mathbb{N}^{2} \to \mathbb{N}, \quad
(i, j) \mapsto V_{g}(i, j), \quad
\underbrace{
\boxed{
V_{g}(i,j)
:=
max\Big(
0,
\Big\lfloor
W \cdot (H - 1 - i) + 1 \cdot (W - 1 - j)
\Big\rfloor
\Big)
}
}_{\text{global loop variant } V_{g} \text{ formula}}
\bigg)
\Rightarrow
\boxed{
\bigg(
\text{the algorithm stops}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\underbrace{
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \eta_{(i, j)} \in \{0, 255\}, \quad
\overbrace{\exists! \xi_{max} \in \mathbb{N}_{\geq 1}}^{\text{maximum number because the algorithm stops}}, \quad
\forall \xi \in \{1, \dots, \xi', \dots, \xi_{max}\}, \quad
}_{
\text{quantifiers placed in the order in which each variable is initialized in the algorithm}
}
\Bigg(
\eta_{(i, j)}
=
\begin{cases}
a_{{(i, j)}_{\boxed{(\xi)}}} < \bar{x}
\Rightarrow
\eta_{(i, j)} = 0
\\[1em]
a_{{(i, j)}_{\boxed{(\xi)}}} \geq \bar{x}
\Rightarrow
\eta_{(i, j)} = 255
\end{cases}
\ \
\Bigg)
\\[1em]
\quad \quad
\because
\Bigg(
\bigg(
\Big(
Pixels_{blackish}
:=
\Big\{
a_{(i, j)}
\ \Big| \
\Big(
1 \leq i \leq H
\Big)
\land
\Big(
1 \leq j \leq W
\Big)
\land
\Big(
0 \leq a_{(i, j)} < \bar{x}
\Big)
\Big\}
\Big)
\land
\Big(
Pixels_{whitish}
:=
\Big\{
a_{(i, j)}
\ \Big| \
\Big(
1 \leq i \leq H
\Big)
\land
\Big(
1 \leq j \leq W
\Big)
\land
\Big(
\bar{x} \leq a_{(i, j)} \leq 255
\Big)
\Big\}
\Big)
\bigg)
\\[1em]
\quad \quad
\Rightarrow
\bigg(
\Big(
\underbrace{
\quad \quad \quad \quad \quad \quad
P_{blackish} = \frac{127}{255} \approx \boxed{0.5}
\quad \quad \quad \quad \quad \quad
}_{\text{Probability of the pixel value } a_{(i, j)} \text{ being in the interval of blackish pixels}}
\Big)
\land
\Big(
\underbrace{
\quad \quad \quad \quad \quad \quad
P_{whitish} = \frac{128}{255} \approx \boxed{0.5}
\quad \quad \quad \quad \quad \quad
}_{\text{Probability of the pixel value } a_{(i, j)} \text{ being in the interval of whitish pixels}}
\Big)
\bigg)
\Rightarrow
\boxed{
\bigg(
\text{uniform distribution of white and black pixels in the dithered image}
\bigg)
}
\Bigg)
\ \
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\ \
\underbrace{
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \eta_{(i, j)} \in \{0, 255\}, \quad
\overbrace{\exists! \xi_{max} \in \mathbb{N}_{\geq 1}}^{\text{maximum number because the algorithm stops}}, \quad
\forall \xi \in \{1, \dots, \xi', \dots, \xi_{max}\}, \quad
\exists! e_{(i, j)} \in \{-127, \dots, 127\}, \quad
}_{
\text{quantifiers placed in the order in which each variable is initialized in the algorithm}
}
\Bigg(
\boxed{
\bigg(
a_{{(i, j)}_{(\xi)}}
=
\eta_{(i, j)}
\bigg)
\because
\bigg(
a_{(i, j)}
\underset{e \to 0}{=}
\eta_{(i, j)}
\bigg)
}
\Bigg)
\\[1em]
\quad \quad
\land
\Bigg(
\boxed{
\bigg(
e_{(i, j)}
=
a_{{(i, j)}_{\boxed{(\xi)}}}
-
\eta_{(i, j)}
\bigg)
}
\iff
\bigg(
\Big(
a_{{(i, j)}_{\boxed{(\xi)}}}
=
\eta_{(i, j)}
+
e_{(i, j)}
\Big)
\Rightarrow
\Big(
a_{{(i, j)}_{\boxed{(\xi + 1)}}}
=
a_{{(i, j)}_{\boxed{(\xi)}}}
+
e_{(i, j)}
\iff
\boxed{
a_{{(i + 0, j + 0)}_{(\xi + 1)}}
=
a_{{(i + 0, j + 0)}_{(\xi)}}
+
e_{(i, j)}
}
\iff
\boxed{
a_{{(i + \Delta_{x}, j + \Delta_{y})}_{(\xi + 1)}}
=
a_{{(i + \Delta_{x}, j + \Delta_{y})}_{(\xi)}}
+
e_{(i, j)}
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
P_{1} :
\Bigg(
(\Delta_{x}, \Delta_{y})
=
(0, 0)
\Bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 3 :

- In this part, we examine what happens if $(\Delta_{x}, \Delta_{y}) = (0, 0)$ 

- If pixels are viewed as cases and the original image $M'$ as a grid (or matrix), then $\Delta_{x}$ and $\Delta_{y}$ indicate how many cases you can move from the currently visited pixel at $(i, j)$ on the grid

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
P_{1}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underline{
\bigg(
a_{{(i + \Delta_{x}, j + \Delta_{y})}_{(\xi + 1)}}
=
a_{{(i + \Delta_{x}, j + \Delta_{y})}_{(\xi)}}
+
e_{(i, j)}
\bigg)
}
\iff
\bigg(
a_{{(i + 0, j + 0)}_{(\xi + 1)}}
=
a_{{(i + 0, j + 0)}_{(\xi)}}
+
e_{(i, j)}
\bigg)
\iff
\bigg(
a_{{(i, j)}_{(\xi + 1)}}
=
a_{{(i, j)}_{(\xi)}}
+
e_{(i, j)}
\bigg)
\iff
\bigg(
a_{{(i, j)}_{(\xi + 1)}}
=
a_{{(i, j)}_{(\xi)}}
+
a_{{(i, j)}_{(\xi)}}
-
\eta_{(i, j)}
\bigg)
\iff
\boxed{
\bigg(
a_{{(i, j)}_{(\xi + 1)}}
=
2a_{{(i, j)}_{(\xi)}}
-
\eta_{(i, j)}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
0 \leq a_{{(i, j)}_{(\xi = 0)}} < 128
\bigg)
}
\Rightarrow
\bigg(
\eta_{(i, j)} = 0
\bigg)
\Rightarrow
\bigg(
a_{{(i, j)}_{(\xi = 1)}}
=
2a_{{(i, j)}_{(\xi = 0)}}
=
2a_{(i, j)}
=
a_{{(i, j)}_{(\xi = \iota_{max})}}
=
\eta_{(i, j)}
\bigg)
\Rightarrow
\boxed{
\bigg(
\bar{N} = 2 \bar{A}
\bigg)
}
\Rightarrow
\bigg(
\bar{N} \gg \bar{A}
\bigg)
\Rightarrow
\boxed{
\bigg(
\text{Not a dithered image}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\left(
\boxed{
\bigg(
128 \leq a_{{(i, j)}_{(\iota = 0)}} \leq 255
\bigg)
}
\Rightarrow
\bigg(
\eta_{(i, j)} = 255
\bigg)
\Rightarrow
\bigg(
a_{{(i, j)}_{(\iota = 1)}}
=
2a_{{(i, j)}_{(\iota = 0)}} - 255
=
2a_{(i, j)} - 255
=
a_{{(i, j)}_{(\iota_{max})}}
=
\eta_{(i, j)}
\bigg)
\Rightarrow
\left(
\left(
\bar{N}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ m = H } \\ { p = W }}}
{\underset{\substack{{ m = 1 } \\ { p = 1 }}}{\sum}}
{\Big(2a_{(m, p)} - 255\Big)}
\right)
\right)
\iff
\left(
\bar{N}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ m = H } \\ { p = W }}}
{\underset{\substack{{ m = 1 } \\ { p = 1 }}}{\sum}}
{\Big(2a_{(m, p)}\Big)}
- W \cdot H \cdot 255
\right)
\right)
\iff
\left(
\bar{N}
=
\frac{1}{W \cdot H}
\cdot
\left(
\overset{\substack{{ m = H } \\ { p = W }}}
{\underset{\substack{{ m = 1 } \\ { p = 1 }}}{\sum}}
{2a_{(m, p)}}
\right)
- 255
\right)
\iff
\boxed{
\Big(
\bar{N}
=
2 \bar{A} - 255
\Big)
}
\right)
\Rightarrow
\bigg(
\Big(
\bar{N} \leq \bar{A}
\Big)
\oplus
\Big(
\bar{N} > \bar{A}
\Big)
\bigg)
\Rightarrow
\boxed{
\bigg(
\text{Not a dithered image}
\bigg)
}
\right)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\neg P_{1}
\Bigg)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
(\Delta_{x}, \Delta_{y})
\neq
(0, 0)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 4 :

- In this part, we examine what happens if $(\Delta_{x}, \Delta_{y}) \neq (0, 0)$ 

- We distribute the gap $e_{(i, j)}$ of the currently visited pixel to one or more neighboring pixels (for now, the number of neighbors and their distances from the currently visited pixel are chosen 
  “randomly”)

- At the currently visited pixel $(i, j)$, we transmit the gap $e_{(i, j)}$ to the colors of the neighboring pixels $(i + \Delta_{y}, j + \Delta_{x})$. The pixel at $(i, j)$ can be viewed as the $\boxed{\text{"giver"}}$ , and the other pixels 
  can be viewed as the $\boxed{\text{"receivers"}}$ :
  
	- Thus, from the “giver” point of view, we have : $e_{(i, j)} \xrightarrow{\text{gives to}} (i + \Delta_{y}, j + \Delta_{x})$ (process called $\boxed{\text{“diffusion”}}$ )

	- We can also change the perspective (i.e., switch from the “giver” point of view to a “receiver” point of view chosen from among all possible receivers) by performing a change of 
	  variables : $(\alpha = i + \Delta_{y} \iff \alpha - \Delta_{y} = i) \land (\beta = j + \Delta_{x} \iff \beta - \Delta_{x} = j)$ 
		- Thus, from the "receiver" point of view (which is a receiver chosen from among all possible receivers), we have : $e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})} \xrightarrow{\text{given by}} (\alpha - \Delta_{y}, \beta - \Delta_{x})$ 

- $\boxed{a_{(i + \Delta_{y}, j + \Delta_{x})}}$ can be viewed as the receiver that receives $\boxed{1}$ gap from its giver, which is the gap $e_{(i, j)}$ of its giver at $(i, j)$ 

- $\boxed{a_{(\alpha, \beta)}}$ can be viewed as the receiver that $\boxed{\text{has already}}$ received $\boxed{\text{all}}$ the possible gaps $e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}$ from all its neighboring pixels at $(\alpha - \Delta_{y}, \beta - \Delta_{x})$ 
  (and its neighboring pixels are not necessarily the neighboring pixels of the giver at $(i, j)$ )

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\exists \Delta_{x}, \Delta_{y} \in \mathbb{Z}, \quad
(\Delta_{x}, \Delta_{y})
\neq
(0, 0)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\exists! a_{{(\alpha, \beta)}_{(\xi)}} \in \{0, 1, 2, \dots, 255\}, \quad
\exists! \xi_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \xi \in \{1, \dots, \xi', \dots, \xi_{max}\}, \quad
\exists \Delta_{x}, \Delta_{y} \in \mathbb{Z}, \quad
a_{(i + \Delta_{y}, j + \Delta_{x})} : \mathbb{N} \to \mathbb{N}, \quad
\xi \mapsto a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi)}}, \quad
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi - 1)}}
+
e_{(i, j)}
=
a_{{(\alpha, \beta)}_{(\xi)}}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
\alpha
=
\alpha(i)
\Big)
\land
\Big(
\beta
=
\beta(j)
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\alpha
=
i + \Delta_{y}
\Big)
\land
\Big(
\beta
=
j + \Delta_{x}
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\alpha(i(\alpha)) = \alpha \land i(\alpha(i)) = i
\Big)
\land
\Big(
\beta(j(\beta)) = \beta \land j(\beta(j)) = j
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\exists! \alpha \in \{1, \dots, H\}, \quad
\alpha^{-1} : \{1, \dots, H\} \to \{1, \dots, H\}, \quad
\alpha \mapsto i(\alpha), \quad
i(\alpha)
=
\alpha - \Delta_{y}
=
i
\Big)
\land
\Big(
\exists! \beta \in \{1, \dots, W\}, \quad
\beta^{-1} : \{1, \dots, W\} \to \{1, \dots, W\}, \quad
\beta \mapsto j(\beta), \quad
j(\beta)
=
\beta - \Delta_{x}
=
j
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
(\alpha, \beta)
=
(i + \Delta_{y}, j + \Delta_{x})
\bigg)
\iff
\bigg(
(\alpha, \beta)
=
(i, j)
+
(\Delta_{y}, \Delta_{x})
\bigg)
\iff
\bigg(
(i, j)
=
(\alpha, \beta)
-
(\Delta_{y}, \Delta_{x})
\bigg)
\iff
\bigg(
(i, j)
=
(\alpha - \Delta_{y}, \beta - \Delta_{x})
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi - 1)}}
+
e_{(i, j)}
\bigg)
\iff
\bigg(
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\exists! a_{{(\alpha, \beta)}_{(\iota)}} \in \{0, 1, 2, \dots, 255\}, \quad
\exists! \xi_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \xi \in \{1, \dots, \xi', \dots, \xi_{max}\}, \quad
\exists \Delta_{x}, \Delta_{y} \in \mathbb{Z}, \quad
a_{{(\alpha, \beta)}_{(\xi)}}
=
a_{{(\alpha, \beta)}_{(\xi - 1)}}
+
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\left(
\Bigg(
a_{{(\alpha, \beta)}_{(\xi_{max})}}
=
\bigg(
\overbrace{
\Big(
\overbrace{
\big(
\underbrace{
a_{{(\alpha, \beta)}_{(0)}}
+
e_{(\alpha - \Delta_{{y}_{(0)}} \ , \ \beta - \Delta_{{x}_{(0)}} )}
}_{a_{{(\alpha, \beta)}_{(1)}}}
\big)
+
e_{(\alpha - \Delta_{{y}_{(1)}} \ , \ \beta - \Delta_{{x}_{(1)}} )}
}^{a_{{(\alpha, \beta)}_{(2)}}}
\Big)
+
\dots
}^{a_{{(\alpha, \beta)}_{(\xi_{max} - 1)}}}
\bigg)
+
e_{(\alpha - \Delta_{{y}_{(\xi_{max} - 1)}} \ , \ \beta - \Delta_{{x}_{(\xi_{max} - 1)}} )}
\Bigg)
\oplus
\dots
\oplus
\Bigg(
a_{{(\alpha, \beta)}_{(\xi_{max})}}
=
\bigg(
\overbrace{
\Big(
\overbrace{
\big(
\underbrace{
a_{{(\alpha, \beta)}_{(0)}}
+
e_{(\alpha - \Delta_{{y}_{(\xi_{max} - 1)}} \ , \ \beta - \Delta_{{x}_{(\xi_{max} - 1)}} )}
}_{a_{{(\alpha, \beta)}_{(1)}}}
\big)
+
e_{(\alpha - \Delta_{{y}_{(0)}} \ , \ \beta - \Delta_{{x}_{(0)}} )}
}^{a_{{(\alpha, \beta)}_{(2)}}}
\Big)
+
\dots
}^{a_{{(\alpha, \beta)}_{(\xi_{max} - 1)}}}
\bigg)
+
e_{(\alpha - \Delta_{{y}_{(1)}} \ , \ \beta - \Delta_{{x}_{(1)}} )}
\Bigg)
\right)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
a_{{(\alpha, \beta)}_{(\xi_{max})}}
=
a_{{(\alpha, \beta)}_{(0)}}
+
\underbrace{
e_{(\alpha - \Delta_{{y}_{(0)}} \ , \ \beta - \Delta_{{x}_{(0)}} )}
}_{
\text{Reception from sense } 0
}
+
\underbrace{
e_{(\alpha - \Delta_{{y}_{(1)}} \ , \ \beta - \Delta_{{x}_{(1)}} )}
}_{
\text{Reception from sense } 1
}
+
\dots
+
\underbrace{
e_{(\alpha - \Delta_{{y}_{(\xi_{max} - 1)}} \ , \ \beta - \Delta_{{x}_{(\xi_{max} - 1)}} )}
}_{
\text{Reception from sense } \xi_{max} - 1
}
\bigg)
\iff
\bigg(
a_{{(\alpha, \beta)}_{(\xi_{max})}}
=
a_{{(\alpha, \beta)}_{(0)}}
+
\underbrace{
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\Big)
}
}_{
E_{\alpha, \beta}
}
\bigg)
\iff
\bigg(
a_{{(\alpha, \beta)}_{(\xi_{max})}}
=
a_{{(\alpha, \beta)}_{(0)}}
+
E_{\alpha, \beta}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \eta_{(i, j)} \in \{0, 255\}, \quad
\exists! \xi_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \xi \in \{1, \dots, \xi', \dots, \xi_{max}\}, \quad
\exists! e_{(i, j)} \in \{-127, \dots, 127\}, \quad
\Big(
\big(
e_{(i, j)}
=
a_{{(i, j)}_{(\xi)}} - \eta_{(i, j)}
\big)
\iff
\big(
\eta_{(i, j)}
=
a_{{(i, j)}_{(\xi)}} - e_{(i, j)}
\big)
\Big)
\Rightarrow
\Big(
\eta_{(i, j)}
=
a_{{(i, j)}_{(\xi_{max})}} - e_{(i, j)}
\Big)
\bigg)
\Rightarrow
\bigg(
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\Big(
\eta_{(\alpha, \beta)}
=
a_{{(\alpha, \beta)}_{(\xi_{max})}} - e_{(\alpha, \beta)}
\Big)
\iff
\Big(
\eta_{(\alpha, \beta)}
=
a_{{(\alpha, \beta)}_{(0)}}
+
E_{\alpha, \beta} - e_{(\alpha, \beta)}
\Big)
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 5 :

- In this part, we conclude that the output image with the current relation $a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi)}} = a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi - 1)}} + e_{(i, j)} \iff a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi)}} = a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\xi - 1)}} + e_{(i, j)} \times \boxed{1}$ is not a dithered image. 
  We then choose to $\boxed{\text{test}}$ what happens if the current relation contains a $\boxed{\text{coefficient}}$ (which we arbitrarily choose to call $w_{(\Delta_{x}, \Delta_{y})}$) such that 
  $a_{(i + \Delta_{y}, j + \Delta_{x})} = a_{(i + \Delta_{y}, j + \Delta_{x})} + e_{(i, j)} \times \boxed{w_{(\Delta_{x}, \Delta_{y})}}$ (for testing)

- Supposing that this new relation gives a different result, we can choose (still for testing) to examine what happens if the sum of the coefficients $w_{(\Delta_{x}, \Delta_{y})}$ is equal to 1 and / or if the sum of the
  coefficients $w_{(\Delta_{x}, \Delta_{y})}$ is different from 1. 
  In $P_{2}$, we arbitrarily first choose to see if the result is “conclusive” if the sum of the coefficients $w_{(\Delta_{x}, \Delta_{y})}$ is equal to 1. Otherwise, we will see what happens if the sum of the 
  coefficients $w_{(\Delta_{x}, \Delta_{y})}$ is different from 1

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\bigg(
\eta_{(\alpha, \beta)}
=
a_{{(\alpha, \beta)}_{(0)}}
+
E_{\alpha, \beta} - e_{(\alpha, \beta)}
\bigg)
}
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\Big(
a_{{(\alpha, \beta)}_{(0)}}
+
E_{\alpha, \beta} - e_{(\alpha, \beta)}
\Big)
}
\right)
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
a_{{(\alpha, \beta)}_{(0)}}
}
+
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
E_{\alpha, \beta}
}
-
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
e_{(\alpha, \beta)}
}
\right)
\\[1em]
\quad \quad
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
a_{{(\alpha, \beta)}_{(0)}}
}
+
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\Big(
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{
\Big(
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\Big)
}
\Big)
}
-
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
e_{(\alpha, \beta)}
}
\right)
\Bigg)
\\[1em]
\Rightarrow
\left(
\ \
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
a_{{(\alpha, \beta)}_{(0)}}
}
+
\underbrace{
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\Big(
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{
\Big(
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\Big)
}
\Big)
}
-
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
e_{(\alpha, \beta)}
}
}_{\boxed{\zeta}}
\right)
\Rightarrow
\boxed{
\bigg(
\bar{N} = \bar{A} + \zeta
\bigg)
}
\Rightarrow
\bigg(
\Big(
\bar{N} \leq \bar{A}
\Big)
\oplus
\Big(
\bar{N} > \bar{A}
\Big)
\bigg)
\Rightarrow
\boxed{
\bigg(
\bar{N} \neq \bar{A}
\bigg)
}
\Rightarrow
\boxed{
\bigg(
\text{Not a dithered image}
\bigg)
}
\ \
\right)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
P_{2} :
\Bigg(
\exists w_{(\Delta_{x}, \Delta_{y})} \in \mathbb{R}, \quad
\bigg(
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{w_{(\Delta_{x}, \Delta_{y})}}
=
1
\bigg)
\land
\bigg(
a_{(i + \Delta_{y}, j + \Delta_{x})}
=
a_{(i + \Delta_{y}, j + \Delta_{x})}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\land
\bigg(
\bar{N} \to \bar{A}
\bigg)
\Bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 6 :

- In this part, we define the relation in $P_{2}$ : $a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi)}} = a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi - 1)}} + e_{(i, j)} \cdot w_{(\Delta_{x}, \Delta_{y})}$ by also defining $\psi$ to specifically identify this relation. 
  Since the algorithm uses the row-major lexicographical order (because it guarantees that the next pixel in the loop is already in the CPU’s cache (CPU optimization) ), 
  we will examine what happen

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
P_{2}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
V_{g} : \mathbb{N}^{2} \to \mathbb{N}, \quad
(i, j) \mapsto V_{g}(i, j), \quad
\underbrace{
V_{g}(i,j)
:=
max\Big(
0,
\Big\lfloor
W \cdot (H - 1 - i) + 1 \cdot (W - 1 - j)
\Big\rfloor
\Big)
}_{\text{global loop variant } V_{g} \text{ formula}}
\bigg)
\Rightarrow
\boxed{
\bigg(
\text{the algorithm stops}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\left(
\underbrace{
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \eta_{(i, j)} \in \{0, 255\}, \quad
\overbrace{\exists! \psi_{max} \in \mathbb{N}_{\geq 1}}^{\text{maximum number because the algorithm stops}}, \quad
\forall \psi \in \{1, \dots, \psi', \dots, \psi_{max}\}, \quad
\exists! e_{(i, j)} \in \boxed{\{-127, \dots, 127\}}, \quad
}_{
\text{quantifiers placed in the order in which each variable is initialized in the algorithm}
}
\left(
\eta_{(i, j)}
=
\begin{cases}
a_{{(i, j)}_{\boxed{(\psi)}}} < 128
\Rightarrow
\boxed{
\eta_{(i, j)} = 0
}
\\[1em]
a_{{(i, j)}_{\boxed{(\psi)}}} \geq 128
\Rightarrow
\boxed{
\eta_{(i, j)} = 255
}
\end{cases}
\ \
\right)
\Rightarrow
\bigg(
a_{{(i, j)}_{(\psi)}} = \eta_{(i, j)}
\bigg)
\Rightarrow
\bigg(
e_{(i, j)}
=
a_{{(i, j)}_{\boxed{(\psi)}}} - \eta_{(i, j)}
\bigg)
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists! \psi_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \psi \in \{1, \dots, \psi', \dots, \psi_{max}\}, \quad
\forall \Delta_{x} \in \boxed{\mathbb{Z}}, \quad
\forall \Delta_{y} \in \boxed{\mathbb{Z}}, \quad
\bigg(
\boxed{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(1)}}
}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(0)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\\[1em]
\quad
\Rightarrow
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(2)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\Rightarrow
\dots
\Rightarrow
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi')}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi' - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\Rightarrow
\bigg(
\boxed{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi_{max})}}
}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi_{max} - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\exists! a_{{(\alpha, \beta)}_{(\psi)}} \in \{0, 1, 2, \dots, 255\}, \quad
\exists! \psi_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \psi \in \{1, \dots, \psi', \dots, \psi_{max}\}, \quad
\forall \Delta_{x} \in \boxed{\mathbb{Z}}, \quad
\forall \Delta_{y} \in \boxed{\mathbb{Z}}, \quad
a_{(i + \Delta_{y}, j + \Delta_{x})} : \mathbb{N} \to \mathbb{N}, \quad
\psi \mapsto a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi)}}, \quad
\boxed{
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
=
a_{{(\alpha, \beta)}_{(\psi)}}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\boxed{\exists \Delta_{x}, \Delta_{y} \in \mathbb{Z}}, \quad
\bigg(
\boxed{
\Big(
(i, j) <_{RL} (i + \Delta_{y}, j + \Delta_{x})
\Big)
\iff
\Big(
(i < i + \Delta_{y})
\lor
(
i = i + \Delta_{y}
\land
j < j + \Delta_{x}
)
\Big)
}
\bigg)
\because
\bigg(
\text{next pixel in the loop already in the CPU’s cache (CPU optimization)}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 7 :

- In this part, we examine all the possible values of $\Delta_{x}$ and $\Delta_{y}$ which indicate by how many we can move from the currently visited pixel at $(i, j)$ to its neighboring pixels 
  (each being at a different $(i + \Delta_{y}, j + \Delta_{x})$ ). Since we assume that there is at least one $\Delta_{x}$ and one $\Delta_{y}$, then we need as many $\Delta_{x}$ and $\Delta_{y}$ as possible

- $\Delta_{x}$ and $\Delta_{y}$ can be viewed together as displacement vector $\begin{pmatrix}\Delta_{x} \\\Delta_{y}\end{pmatrix}$ from the currently visited pixel at $(i, j)$ to a neighboring pixel at $(i + \Delta_{y}, j + \Delta_{x})$ :
	- This displacement vector can be used with the Tchebychev norm ${\|\cdot\|}_{\infty}$ to obtain as many $\Delta_{x}$ and $\Delta_{y}$ as possible, since :
	
		- The Tchebychev norm considers diagonal vectors (characterizing diagonal neighboring pixels at $(i + \Delta_{y}, j + \Delta_{x})$ ) to be at the same distance (from the currently visited pixel 
		  at $(i, j)$ ) as horizontal and vertical vectors (characterizing the nearest horizontal and vertical neighboring pixels at different $(i + \Delta_{y}, j + \Delta_{x})$ )

	- Then, the found $\Delta_{x}$ and $\Delta_{y}$ values will be filtered by the row-major lexicographical order to obtain the final values $\Delta_{x}$ and $\Delta_{y}$ 

- As a side note, in physics, we can also use the Rayleigh threshold to determine visual consistency of a dithered image : $\underbrace{\frac{distanceBetweenTwoPixels}{observationDistance}\approx\overbrace{1.22 \cdot\frac{(\lambda = 550nm)}{pupilDiameter = 8mm}}^{\theta}}_{\text{Rayleigh threshold}}$ 

- $S_{{o}_{(x)}}$ ("$o$" for "offset") denote the set of all possible final values of $\Delta_{x}$, and $S_{{o}_{(y)}}$ ("$o$" for "offset") denote the set of all possible final values of $\Delta_{y}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\boxed{
\Big(
i
<
i + \Delta_{y}
\Big)
}
\Rightarrow
\Big(
\ \
\boxed{
\Big(
\big(
\Delta_{y} > 0
\land
\Delta_{x} \in \mathbb{Z}
\big)
\iff
\big(
\Delta_{y} \geq 1
\land
\Delta_{x} \in \mathbb{Z}
\big)
\Big)
}
\because
\Big(
\big(
\Delta_{y} \leq 0
\big)
\Rightarrow
\big(
i \geq i + \Delta_{y}
\big)
\Rightarrow
\big(
(i, j) \ \centernot{<}_{RL} \ (i + \Delta_{y}, j + \Delta_{x})
\big)
\Big)
\ \
\Big)
\bigg)
\lor
\bigg(
\boxed{
\Big(
i = i + \Delta_{y}
\land
j < j + \Delta_{x}
\Big)
}
\Rightarrow
\Big(
\ \
\boxed{
\Big(
\big(
\Delta_{y} = 0
\land
\Delta_{x} > 0
\big)
\iff
\big(
\Delta_{y} = 0
\land
\Delta_{x} \geq 1
\big)
\Big)
}
\because
\Big(
\Delta_{x} \leq 0
\Rightarrow
j \geq j + \Delta_{x}
\Rightarrow
(i, j) \ \centernot{<}_{RL} \ (i + \Delta_{y}, j + \Delta_{x})
\Big)
\ \
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\Big(
i
<
i + \Delta_{y}
\Big)
}
\Rightarrow
\Big(
\ \
\boxed{
\Big(
\big(
\Delta_{y} > 0
\land
\Delta_{x} \in \mathbb{Z}
\big)
\iff
\big(
\Delta_{y} \geq 1
\land
\Delta_{x} \in \mathbb{Z}
\big)
\Big)
}
\because
\Big(
\big(
\Delta_{y} \leq 0
\big)
\Rightarrow
\big(
i \geq i + \Delta_{y}
\big)
\Rightarrow
\big(
(i, j) \ \centernot{<}_{RL} \ (i + \Delta_{y}, j + \Delta_{x})
\big)
\Big)
\ \
\Big)
\bigg)
\lor
\bigg(
\boxed{
\Big(
i = i + \Delta_{y}
\land
j < j + \Delta_{x}
\Big)
}
\Rightarrow
\Big(
\ \
\boxed{
\Big(
\big(
\Delta_{y} = 0
\land
\Delta_{x} > 0
\big)
\iff
\big(
\Delta_{y} = 0
\land
\Delta_{x} \geq 1
\big)
\Big)
}
\because
\Big(
\Delta_{x} \leq 0
\Rightarrow
j \geq j + \Delta_{x}
\Rightarrow
(i, j) \ \centernot{<}_{RL} \ (j + \Delta_{y}, i + \Delta_{x})
\Big)
\ \
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\exists v \in V = \mathbb{R}^{2}, \quad
\bigg(
v
=
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
\bigg)
\land
\bigg(
{\|v\|}_{\infty} \neq 1
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
{\|v\|}_{\infty} \neq 1
\bigg)
\Rightarrow
\bigg(
\Big(
\big(
\Delta_{x} \gg \Delta_{y}
\lor
\Delta_{x} \geq \Delta_{y}
\big)
\oplus
\big(
\Delta_{y} \gg \Delta_{x}
\lor
\Delta_{y} \geq \Delta_{x}
\big)
\Big)
\Rightarrow
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\psi - 1)}}
+
\big(
\underbrace{
a_{{(i, j)}_{(\psi)}} - \eta_{(i, j)}
}_{
e_{(i, j)}
}
\big)
\cdot
w
\Big)
\Rightarrow
\Big(
a_{{(i + 1000, j + 2)}_{(\psi)}}
=
a_{{(i + 1000, j + 2)}_{(\psi - 1)}}
+
\big(
\underbrace{
\quad \quad
a_{{(i, j)}_{(\psi)}} - \eta_{(i, j)}
\quad \quad
}_{
e_{(i, j) \text{ redistributed from } a_{(i, j)} \text{ to } a_{(i + 1000, j + 2)} }
}
\big)
\cdot
w
\Big)
\Rightarrow
\Big(
(i, j) \ll_{RL} (i + 1000, j + 2)
\Big)
\Rightarrow
\boxed{
\Big(
\text{visually incoherent dithered image because } e_{(i,j)} \text{ would be redistributed to too far from } a_{(i, j)}
\Big)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
{\|v\|}_{\infty} = 1
\bigg)
}
\Rightarrow
\bigg(
\text{expressed for 1 unit and visually coherent dithered image because } e_{(i,j)} \text{ close to } a_{(i, j)}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
{\|v\|}_{\infty} = 1
\bigg)
}
\land
\bigg(
\Big(
\Delta_{y} = 1
\land
\Delta_{x} \in \{-1, 0, 1\}
\Big)
\Rightarrow
\Big(
i < i + \Delta_{y}
\Big)
\Rightarrow
\Big(
(i, j) <_{RL} (i + 1, j + \Delta_{x})
\Big)
\Rightarrow
\boxed{
\Big(
S_{1}
=
\left\{
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
, \
\begin{pmatrix}
0 \\
1
\end{pmatrix}
, \
\begin{pmatrix}
1 \\
1
\end{pmatrix}
\right\}
\subset V
\Big)
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
{\|v\|}_{\infty} = 1
\bigg)
}
\land
\bigg(
\Big(
\Delta_{y} = 0
\land
\Delta_{x} = 1
\Big)
\Rightarrow
\Big(
i = i + \Delta_{y}
\land
j < j + \Delta_{x}
\Big)
\Rightarrow
\Big(
(i, j) <_{RL} (i, j + \Delta_{x})
\Big)
\Rightarrow
\boxed{
\Big(
S_{2}
=
\left\{
\begin{pmatrix}
1 \\
0
\end{pmatrix}
\right\}
\subset V
\Big)
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
\forall v \in S_{o}, \quad
{\|v\|}_{\infty} = 1
\bigg)
}
\land
\bigg(
\underbrace{
\boxed{
S_{o}
:=
\left\{
\begin{pmatrix}
1 \\
0
\end{pmatrix}
, \
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
, \
\begin{pmatrix}
0 \\
1
\end{pmatrix}
, \
\begin{pmatrix}
1 \\
1
\end{pmatrix}
\right\}
}
=
\left\{
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
\ \bigg| \
\bigg(
\Delta_{x} \in S_{{o}_{(x)}}
\bigg)
\land
\bigg(
\Delta_{y} \in S_{{o}_{(y)}}
\bigg)
\right\}
}_{
\text{According to row-major lexicographical order in the algorithm}
}
=
S_{1} \cup S_{2}
\subset V
\bigg)
\land
\boxed{
\bigg(
S_{{o}_{(x)}}
:=
\{1, -1, 0, 1\}
\bigg)
}
\land
\boxed{
\bigg(
S_{{o}_{(y)}}
:=
\{0, 1, 1, 1\}
\bigg)
}
\Bigg)
\end{cases}
\end{array}
$$

Part 8 :

- In this part, we identify a relation similar to the one in $P_{2}$ (by also defining $\iota$ to specifically identify this relation), specifically using the final values of $\Delta_{x}$ and $\Delta_{y}$ found previously

- $\iota$ represents the $\iota$-th time a variable changes its value from its previous value in the algorithm (similar to a recurrent sequence of order 1)

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \eta_{(i, j)} \in \{0, 255\}, \quad
\exists! \iota_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \iota \in \{1, \dots, \iota', \dots, \iota_{max}\}, \quad
\exists! e_{(i, j)} \in \{-127, \dots, 127\}, \quad
\left(
\eta_{(i, j)}
=
\begin{cases}
a_{{(i, j)}_{\boxed{(\iota)}}} < 128
\Rightarrow
\eta_{(i, j)} = 0
\\[1em]
a_{{(i, j)}_{\boxed{(\iota)}}} \geq 128
\Rightarrow
\eta_{(i, j)} = 255
\end{cases}
\ \
\right)
\Rightarrow
\bigg(
a_{{(i, j)}_{\boxed{(\iota)}}} = \eta_{(i, j)}
\bigg)
\Rightarrow
\bigg(
e_{(i, j)}
=
a_{{(i, j)}_{(\iota)}} - \eta_{(i, j)}
\bigg)
\right)
\\[1em]
\Rightarrow
\Bigg(
\exists! \iota_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \iota \in \{1, \dots, \iota', \dots, \iota_{max}\}, \quad
\forall \Delta_{x} \in S_{{o}_{(x)}}, \quad
\forall \Delta_{y} \in S_{{o}_{(y)}}, \quad
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{\boxed{(1)}}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(0)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\\[1em]
\quad
\Rightarrow
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(2)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\Rightarrow
\dots
\Rightarrow
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota')}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota' - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\Rightarrow
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{\boxed{(\iota_{max})}}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota_{max} - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 9 :

- In this part, we define the relation : $a_{{(i + \Delta_{y}, j + \Delta_{x})}_{\boxed{(\iota)}}} = a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota - 1)}} + e_{(i, j)} \cdot w_{(\Delta_{x}, \Delta_{y})}$ (similar to the one in $P_{2}$ ) by also defining $\boxed{\iota}$ to specifically identify this relation. 

- We perform the same variable substitution involving $\alpha$ and $\beta$ as in part 4

- We distribute the gap $e_{(i, j)}$ of the currently visited pixel at $(i, j)$ to $\boxed{4 \text{ specific neighboring pixels}}$ , because :

	- The total number of possible combinations of $\Delta_{x}$ and $\Delta_{y}$ $\boxed{\text{following the row-major lexicographical order and visual consistency}}$ is $Card(S_{o}) = 4$ 

- $\boxed{a_{(i + \Delta_{y}, j + \Delta_{x})}}$ can be viewed as the receiver that receives $\boxed{1}$ gap from its giver, which is the gap $e_{(i, j)}$ of its giver at $(i, j)$ 

- $\boxed{a_{(\alpha, \beta)}}$ can be viewed as the receiver that $\boxed{\text{has already}}$ received $\boxed{\text{all}}$ the possible gaps $e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}$ from all its neighboring pixels at $(\alpha - \Delta_{y}, \beta - \Delta_{x})$ 
  (and its neighboring pixels are not necessarily the neighbors of the giver at $(i, j)$ )

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}}, \quad
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\exists! a_{{(\alpha, \beta)}_{(\iota)}} \in \{0, 1, 2, \dots, 255\}, \quad
\exists! \iota_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \iota \in \{1, \dots, \iota', \dots, \iota_{max}\}, \quad
\forall \Delta_{x} \in S_{{o}_{(x)}}, \quad
\forall \Delta_{y} \in S_{{o}_{(y)}}, \quad
a_{(i + \Delta_{y}, j + \Delta_{x})} : \mathbb{N} \to \mathbb{N}, \quad
\iota \mapsto a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}, \quad
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
=
a_{{(\alpha, \beta)}_{(\iota)}}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\exists! a_{{(\alpha, \beta)}_{(\iota)}} \in \{0, 1, 2, \dots, 255\}, \quad
\exists! \iota_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \iota \in \{1, \dots, \iota', \dots, \iota_{max}\}, \quad
\forall \Delta_{x} \in S_{{o}_{(x)}}, \quad
\forall \Delta_{y} \in S_{{o}_{(y)}}, \quad
\bigg(
a_{{(\alpha, \beta)}_{(\iota)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Big(
\alpha
=
\alpha(i)
\Big)
\land
\Big(
\beta
=
\beta(j)
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\alpha
=
i + \Delta_{y}
\Big)
\land
\Big(
\beta
=
j + \Delta_{x}
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\alpha(i(\alpha)) = \alpha \land i(\alpha(i)) = i
\Big)
\land
\Big(
\beta(j(\beta)) = \beta \land j(\beta(j)) = j
\Big)
\bigg)
\Rightarrow
\bigg(
\Big(
\exists! \alpha \in \{1, \dots, H\}, \quad
\alpha^{-1} : \{1, \dots, H\} \to \{1, \dots, H\}, \quad
\alpha \mapsto i(\alpha), \quad
i(\alpha)
=
\alpha - \Delta_{y}
=
i
\Big)
\land
\Big(
\exists! \beta \in \{1, \dots, W\}, \quad
\beta^{-1} : \{1, \dots, W\} \to \{1, \dots, W\}, \quad
\beta \mapsto j(\beta), \quad
j(\beta)
=
\beta - \Delta_{x}
=
j
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\underline{
\bigg(
(\alpha, \beta)
=
(i + \Delta_{y}, j + \Delta_{x})
\bigg)
}
\iff
\bigg(
(\alpha, \beta)
=
(i, j)
+
(\Delta_{y}, \Delta_{x})
\bigg)
\iff
\bigg(
(i, j)
=
(\alpha, \beta)
-
(\Delta_{y}, \Delta_{x})
\bigg)
\iff
\underline{
\bigg(
(i, j)
=
(\alpha - \Delta_{y}, \beta - \Delta_{x})
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\iff
\boxed{
\bigg(
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\exists! a_{{(\alpha, \beta)}_{(\iota)}} \in \{0, 1, 2, \dots, 255\}, \quad
\exists! \iota_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \iota \in \{1, \dots, \iota', \dots, \iota_{max}\}, \quad
\forall \Delta_{x} \in S_{{o}_{(x)}}, \quad
\forall \Delta_{y} \in S_{{o}_{(y)}}, \quad
a_{{(\alpha, \beta)}_{(\iota)}}
=
a_{{(\alpha, \beta)}_{(\iota - 1)}}
+
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\left(
\ \
\left(
\underline{
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
1 \\
0
\end{pmatrix}
\in S_{o}
\right)
}
\land
\Big(
(\alpha - \Delta_{y}, \beta - \Delta_{x})
=
(\alpha - 0, \beta - 1)
=
\boxed{
(\alpha, \beta - 1)
}
\Big)
\right)
\oplus
\left(
\underline{
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
\in S_{o}
\right)
}
\land
\Big(
(\alpha - \Delta_{y}, \beta - \Delta_{x})
=
(\alpha - 1, \beta - (-1))
=
\boxed{
(\alpha - 1, \beta + 1)
}
\Big)
\right)
\oplus
\left(
\underline{
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
0 \\
1
\end{pmatrix}
\in S_{o}
\right)
}
\land
\Big(
(\alpha - \Delta_{y}, \beta - \Delta_{x})
=
(\alpha - 1, \beta - 0)
=
\boxed{
(\alpha - 1, \beta)
}
\Big)
\right)
\oplus
\left(
\underline{
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
1 \\
1
\end{pmatrix}
\in S_{o}
\right)
}
\land
\Big(
(\alpha - \Delta_{y}, \beta - \Delta_{x})
=
\boxed{
(\alpha - 1, \beta - 1)
}
\Big)
\right)
\ \
\right)
\\[1em]
\Rightarrow
\Bigg(
\boxed{
\bigg(
\iota_{max}
=
Card(S_{o})
=
4
\bigg)
}
\because
\bigg(
\text{In the equation }
a_{{(\alpha, \beta)}_{(\iota)}}
\text{ , there is one unique fixed } \alpha \text{ and } \beta
\text{ and the total number of possible combinations of } \Delta_{x} \text{ and } \Delta_{y}
\text{ following the row-major lexicographical order and visual consistency is }
Card(S_{o})
=
4
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 10 :

- In this part, we examine the possible values of the coefficients $w_{(\Delta_{x}, \Delta_{y})}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\Bigg(
a_{{(\alpha, \beta)}_{(\iota_{max} = 4)}}
=
\bigg(
\overbrace{
\Big(
\overbrace{
\big(
\underbrace{
a_{{(\alpha, \beta)}_{(0)}}
+
e_{(\alpha, \beta - 1)}
\cdot
w_{(1, 0)}
}_{a_{{(\alpha, \beta)}_{(1)}}}
\big)
+
e_{(\alpha - 1, \beta + 1)}
\cdot
w_{(-1, 1)}
}^{a_{{(\alpha, \beta)}_{(2)}}}
\Big)
+
e_{(\alpha - 1, \beta)}
\cdot
w_{(0, 1)}
}^{a_{{(\alpha, \beta)}_{(3)}}}
\bigg)
+
e_{(\alpha - 1, \beta - 1)}
\cdot
w_{(1, 1)}
\Bigg)
\oplus
\dots
\oplus
\Bigg(
a_{{(\alpha, \beta)}_{(\iota_{max} = 4)}}
=
\bigg(
\overbrace{
\Big(
\overbrace{
\big(
\underbrace{
a_{{(\alpha, \beta)}_{(0)}}
+
e_{(\alpha - 1, \beta + 1)}
\cdot
w_{(-1, 1)}
}_{a_{{(\alpha, \beta)}_{(1)}}}
\big)
+
e_{(\alpha, \beta - 1)}
\cdot
w_{(1, 0)}
}^{a_{{(\alpha, \beta)}_{(2)}}}
\Big)
+
e_{(\alpha - 1, \beta - 1)}
\cdot
w_{(1, 1)}
}^{a_{{(\alpha, \beta)}_{(3)}}}
\bigg)
+
e_{(\alpha - 1, \beta)}
\cdot
w_{(0, 1)}
\Bigg)
\right)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
Card(\{w_{(\Delta_{x}, \Delta_{y})} \ | \ (\Delta_{x}, \Delta_{y}) \in V \})
=
Card(S_{o})
=
4
\bigg)
\land
\bigg(
\exists \Phi_{1}, \Phi_{2}, \Phi_{3}, \Phi_{4}, \varrho \in \mathbb{R}, \quad
\Big(
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{w_{(\Delta_{x}, \Delta_{y})}}
=
1
\Big)
\Rightarrow
\Big(
\big(
\frac{\Phi_{1}}{\varrho}
+
\frac{\Phi_{2}}{\varrho}
+
\frac{\Phi_{3}}{\varrho}
+
\frac{\Phi_{4}}{\varrho}
=
1
\big)
\iff
\big(
\frac{\Phi_{1} + \Phi_{2} + \Phi_{3} + \Phi_{4}}{\varrho}
=
1
\big)
\iff
\boxed{
\big(
\Phi_{1} + \Phi_{2} + \Phi_{3} + \Phi_{4}
=
\varrho
\big)
}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\varrho = 2^{Card(S_{o})} = 2^{4} = \boxed{16}
\bigg)
\because
\bigg(
\boxed{
\Big(
Card(S_{o}) = 4
\text{ and division = 20 CPU cycles (in 1976) whereas bitwise right-shift = 1 CPU cycle}
\Big)
}
\Rightarrow
\boxed{
\Big(
\left\lfloor \frac{\Phi_{c \in \{1, \dots, 4\}}}{2^{4}} \right\rfloor
=
\Phi_{c \in \{1, \dots, 4\}} \gg_{2} 4
\Big)
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\Phi_{1} = 7
\land
\Phi_{2} = 3
\land
\Phi_{3} = 5
\land
\Phi_{4} = 1
\bigg)
\because
\boxed{
\bigg(
\text{Coefficient values found by testing different values after rendering "test" dithered images}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\left(
\left(
w_{(\Delta_{x}, \Delta_{y})}
=
\begin{cases}
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
1 \\
0
\end{pmatrix}
\right)
\Rightarrow
\Big(
w_{(\Delta_{x}, \Delta_{y})}
=
\boxed{
\frac{7}{16}
}
\Big)
\\[1em]
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
\right)
\Rightarrow
\Big(
w_{(\Delta_{x}, \Delta_{y})}
=
\boxed{
\frac{3}{16}
}
\Big)
\\[1em]
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
0 \\
1
\end{pmatrix}
\right)
\Rightarrow
\Big(
w_{(\Delta_{x}, \Delta_{y})}
=
\boxed{
\frac{5}{16}
}
\Big)
\\[1em]
\left(
\begin{pmatrix}
\Delta_{x} \\
\Delta_{y}
\end{pmatrix}
=
\begin{pmatrix}
1 \\
1
\end{pmatrix}
\right)
\Rightarrow
\Big(
w_{(\Delta_{x}, \Delta_{y})}
=
\boxed{
\frac{1}{16}
}
\Big)
\end{cases}
\ \
\right)
\land
\boxed{
\bigg(
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{w_{(\Delta_{x}, \Delta_{y})}}
=
\frac{7}{16} + \frac{3}{16} + \frac{5}{16} + \frac{1}{16}
=
1
\bigg)
}
\ \
\right)
\end{cases}
\end{array}
$$

Part 11 :

- In this part, we express $\eta_{(\alpha, \beta)}$ in terms of $a_{{(\alpha, \beta)}_{(0)}}$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
a_{{(\alpha, \beta)}_{(\iota_{max})}}
=
a_{{(\alpha, \beta)}_{(0)}}
+
e_{(\alpha, \beta - 1)}
\cdot
w_{(1, 0)}
+
e_{(\alpha - 1, \beta + 1)}
\cdot
w_{(-1, 1)}
+
e_{(\alpha - 1, \beta)}
\cdot
w_{(0, 1)}
+
e_{(\alpha - 1, \beta - 1)}
\cdot
w_{(1, 1)}
\bigg)
\iff
\bigg(
a_{{(\alpha, \beta)}_{(\iota_{max})}}
=
a_{{(\alpha, \beta)}_{(0)}}
+
\underbrace{
e_{(\alpha, \beta - 1)}
\cdot
\frac{7}{16}
}_{\text{Left reception}}
+
\underbrace{
e_{(\alpha - 1, \beta + 1)}
\cdot
\frac{3}{16}
}_{\text{Top right reception}}
+
\underbrace{
e_{(\alpha - 1, \beta)}
\cdot
\frac{5}{16}
}_{\text{Top reception}}
+
\underbrace{
e_{(\alpha - 1, \beta - 1)}
\cdot
\frac{1}{16}
}_{\text{Top left reception}}
\bigg)
\\[1em]
\quad
\iff
\bigg(
a_{{(\alpha, \beta)}_{(\iota_{max})}}
=
a_{{(\alpha, \beta)}_{(0)}}
+
e_{(\alpha - (0), \beta - (+1))} \cdot w_{(1, 0)}
+
e_{(\alpha - (1), \beta - (-1))} \cdot w_{(-1, 1)}
+
e_{(\alpha - (1), \beta - (0))} \cdot w_{(0, 1)}
+
e_{(\alpha - (1), \beta - (1))} \cdot w_{(1, 1)}
\bigg)
\iff
\bigg(
a_{{(\alpha, \beta)}_{(\iota_{max})}}
=
a_{{(\alpha, \beta)}_{(0)}}
+
\underbrace{
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\Big)
}
}_{
\boxed{
E_{\alpha, \beta}
}
}
\bigg)
\iff
\boxed{
\bigg(
a_{{(\alpha, \beta)}_{(\iota_{max})}}
=
a_{{(\alpha, \beta)}_{(0)}}
+
E_{\alpha, \beta}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\forall i \in \{1, \dots, H\}, \quad
\forall j \in \{1, \dots, W\}, \quad
\exists! \eta_{(i, j)} \in \{0, 255\}, \quad
\exists! \iota_{max} \in \mathbb{N}_{\geq 1}, \quad
\forall \iota \in \{1, \dots, \iota', \dots, \iota_{max}\}, \quad
\exists! e_{(i, j)} \in \{-127, \dots, 127\}, \quad
\Big(
\big(
e_{(i, j)}
=
a_{{(i, j)}_{(\iota)}} - \eta_{(i, j)}
\big)
\iff
\big(
\eta_{(i, j)}
=
a_{{(i, j)}_{(\iota)}} - e_{(i, j)}
\big)
\Big)
\Rightarrow
\boxed{
\Big(
\eta_{(i, j)}
=
a_{{(i, j)}_{(\iota_{max})}} - e_{(i, j)}
\Big)
}
\bigg)
\Rightarrow
\bigg(
\exists! \alpha \in \{1, \dots, H\}, \quad
\exists! \beta \in \{1, \dots, W\}, \quad
\boxed{
\Big(
\eta_{(\alpha, \beta)}
=
a_{{(\alpha, \beta)}_{(\iota_{max})}} - e_{(\alpha, \beta)}
\Big)
}
\iff
\boxed{
\Big(
\eta_{(\alpha, \beta)}
=
a_{{(\alpha, \beta)}_{(0)}}
+
E_{\alpha, \beta} - e_{(\alpha, \beta)}
\Big)
}
\bigg)
\Bigg)
\end{cases}
\end{array}
$$

Part 12 :

- In this part, we use the sums from $\eta_{(\alpha, \beta)} = a_{{(\alpha, \beta)}_{(0)}} + E_{\alpha, \beta} - e_{(\alpha, \beta)}$ (found in part 11) to get closer to the equality $\bar{N} = \bar{A}$, in order to check if the final result $\boxed{\text{might}}$ be different from the 
  one in part 5, and to check if $P_{2}$ is true

- We perform in the sums a variable substitution involving $i$ and $j$ by using the relation $(\alpha = i + \Delta_{y} \iff \alpha - \Delta_{y} = i) \land (\beta = j + \Delta_{x} \iff \beta - \Delta_{x} = j)$ 

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\bigg(
\eta_{(\alpha, \beta)}
=
a_{{(\alpha, \beta)}_{(0)}}
+
E_{\alpha, \beta} - e_{(\alpha, \beta)}
\bigg)
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\Big(
a_{{(\alpha, \beta)}_{(0)}}
+
E_{\alpha, \beta} - e_{(\alpha, \beta)}
\Big)
}
\right)
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
a_{{(\alpha, \beta)}_{(0)}}
}
+
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
E_{\alpha, \beta}
}
-
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
e_{(\alpha, \beta)}
}
\right)
\\[1em]
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
a_{{(\alpha, \beta)}_{(0)}}
}
+
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\Big(
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{
\Big(
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\Big)
}
\Big)
}
-
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
e_{(\alpha, \beta)}
}
\right)
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
a_{{(\alpha, \beta)}_{(0)}}
}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{
\Big(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\Big(
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\cdot
\ \
\underbrace{
\quad \quad \quad \quad
w_{(\Delta_{x}, \Delta_{y})}
\quad \quad \quad \quad
}_{\text{Common factor in the current sum = identical}}
\ \
\Big)
}
\Big)
}
-
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
e_{(\alpha, \beta)}
}
\right)
\\[1em]
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
a_{{(\alpha, \beta)}_{(0)}}
}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{
\Big(
w_{(\Delta_{x}, \Delta_{y})}
\cdot
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\Big(
e_{(\alpha - \Delta_{y}, \beta - \Delta_{x})}
\Big)
}
\Big)
}
-
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
e_{(\alpha, \beta)}
}
\right)
\iff
\left(
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
\eta_{(i + \Delta_{y}, j + \Delta_{x})}
}
=
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(0)}}
}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{
\Big(
w_{(\Delta_{x}, \Delta_{y})}
\cdot
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
\Big(
e_{(i, j)}
\Big)
}
\Big)
}
-
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
e_{(i + \Delta_{y}, j + \Delta_{x})}
}
\right)
\Bigg)
\end{cases}
\end{array}
$$

Part 13 :

- In this part, we observe that the results are different from those in part 5, because the sum of the coefficients equal to 1, as specified by proposition $P_{2}$, provides a way to get out of the sum

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\left(
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
\eta_{(i + \Delta_{y}, j + \Delta_{x})}
}
=
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(0)}}
}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{
\Big(
w_{(\Delta_{x}, \Delta_{y})}
\cdot
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
\Big(
e_{(i, j)}
\Big)
}
\Big)
}
-
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
e_{(i + \Delta_{y}, j + \Delta_{x})}
}
\right)
\iff
\left(
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
\eta_{(i + \Delta_{y}, j + \Delta_{x})}
}
=
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(0)}}
}
+
\ \
\underbrace{
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{
\Big(
w_{(\Delta_{x}, \Delta_{y})}
\Big)
}
}_{\boxed{1}}
\ \ \ \
\cdot
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
\Big(
e_{(i, j)}
\Big)
}
-
\overset{\substack{{ i + \Delta_{y} = H } \\ { j + \Delta_{x} = W }}}
{\underset{\substack{{ i + \Delta_{y} = 1 } \\ { j + \Delta_{x} = 1 }}}{\sum}}
{
e_{(i + \Delta_{y}, j + \Delta_{x})}
}
\right)
\\[1em]
\iff
\left(
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
\eta_{(i + \Delta_{y}, j + \Delta_{x})}
}
=
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(0)}}
}
+
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
\Big(
e_{(i, j)}
\Big)
}
-
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
e_{(i + \Delta_{y}, j + \Delta_{x})}
}
\right)
\Bigg)
\\[1em]
\Rightarrow
\left(
\ \
\boxed{
\left(
\ \
\vartheta
:=
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
e_{(i, j)}
}
\ \
\right)
}
\Rightarrow
\bigg(
\boxed{
\Omega
}
:=
\bigg\{
(\underbrace{i + \Delta_{y}}_{\boxed{\alpha}}, \underbrace{j + \Delta_{x}}_{\boxed{\beta}})
\ \bigg| \
1 \leq \underbrace{i + \Delta_{y}}_{\boxed{\alpha}} \leq H
\land
1 \leq \underbrace{j + \Delta_{x}}_{\boxed{\beta}} \leq W
\bigg\}
\bigg)
\land
\bigg(
\boxed{
\Omega'
}
:=
\bigg\{
(\underbrace{i}_{\boxed{\alpha'}}, \underbrace{j}_{\boxed{\beta'}})
\ \bigg| \
1 - \Delta_{y} \leq \underbrace{i}_{\boxed{\alpha' = \alpha - \Delta_{y}}} \leq H - \Delta_{y}
\land
1 - \Delta_{x} \leq \underbrace{j}_{\boxed{\beta' = \beta - \Delta_{x}}} \leq W - \Delta_{x}
\bigg\}
=
\boxed{
\bigg\{
(\alpha - \Delta_{y}, \beta - \Delta_{x})
\ \bigg| \
(\alpha, \beta) \in \Omega
\bigg\}
}
\bigg)
\Rightarrow
\boxed{
\left(
\vartheta
=
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
e_{(i, j)}
}
=
{\underset{(\alpha', \beta') \in \Omega'}{\sum}}
{
e_{(\alpha', \beta')}
}
\right)
}
\ \
\right)
\end{cases}
\end{array}
$$

Part 14 :

- In this part, we examine what happens if we choose to cancel out the two terms in ${\sum}{e_{(i, j)}} - {\sum}{e_{(i + \Delta_{y}, j + \Delta_{x})}}$ (found in part 13)

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
\boxed{
\forall (\alpha, \beta) \notin \Omega, \quad
\bigg(
e_{(\alpha, \beta)} = 0
\bigg)
}
\because
\bigg(
\Big(
(\alpha, \beta) \notin \Omega
\Big)
\Rightarrow
\Big(
\big(
e_{(\alpha, \beta)}
=
a_{{(\alpha, \beta)}_{(\iota)}}
+
\eta_{(\alpha, \beta)}
\big)
\land
\big(
a_{{(\alpha, \beta)}_{(\iota)}}
\text{ not an element of the matrix }
\big)
\land
\boxed{
\big(
a_{{(\alpha, \beta)}_{(\iota)}} \text{ not in the picture}
\big)
}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
{\underset{(\alpha', \beta') \in \Omega'}{\sum}}
{
e_{(\alpha', \beta')}
}
=
{\underset{(\alpha', \beta') \in \Omega' \cap \Omega}{\sum}}
{
e_{(\alpha', \beta')}
}
+
\underbrace{
{\underset{(\alpha', \beta') \in \Omega' \backslash \Omega}{\sum}}
{
e_{(\alpha', \beta')}
}
}_{\boxed{0}}
\bigg)
\land
\bigg(
{\underset{(\alpha, \beta) \in \Omega}{\sum}}
{
e_{(\alpha, \beta)}
}
=
{\underset{(\alpha, \beta) \in \Omega \cap \Omega'}{\sum}}
{
e_{(\alpha, \beta)}
}
+
{\underset{(\alpha, \beta) \in \Omega \backslash \Omega'}{\sum}}
{
e_{(\alpha, \beta)}
}
\iff
{\underset{(\alpha, \beta) \in \Omega}{\sum}}
{
e_{(\alpha, \beta)}
}
=
{\underset{(\alpha, \beta) \in \Omega \cap \Omega'}{\sum}}
{
e_{(\alpha, \beta)}
}
+
\boxed{
\underbrace{
e_{(H, W)}
}_{\neq 0}
}
\bigg)
\land
\boxed{
\bigg(
\Omega \backslash \Omega'
=
\bigg\{
(\alpha, \beta)
\ \bigg| \
(\alpha - \Delta_{y}, \beta - \Delta_{x}) \notin \Omega'
\bigg\}
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\Big(
\Omega' \cap \Omega
=
\Omega \cap \Omega'
\Big)
}
\land
\Big(
{\underset{(\alpha', \beta') \in \Omega' \cap \Omega}{\sum}}
{
e_{(\alpha', \beta')}
}
=
{\underset{(\alpha, \beta) \in \Omega \cap \Omega'}{\sum}}
{
e_{(\alpha, \beta)}
}
\Big)
\bigg)
\Rightarrow
\underline{
\bigg(
\Big(
{\underset{(\alpha', \beta') \in \Omega'}{\sum}}
{
e_{(\alpha', \beta')}
}
=
{\underset{(\alpha', \beta') \in \Omega' \cap \Omega}{\sum}}
{
e_{(\alpha', \beta')}
}
=
{\underset{(\alpha, \beta) \in \Omega}{\sum}}
{
e_{(\alpha, \beta)}
}
=
{\underset{(\alpha, \beta) \in \Omega \cap \Omega'}{\sum}}
{
e_{(\alpha, \beta)}
}
+
e_{(H, W)}
\Big)
\iff
\Big(
{\underset{(\alpha', \beta') \in \Omega'}{\sum}}
{
e_{(\alpha', \beta')}
}
=
{\underset{(\alpha, \beta) \in \Omega}{\sum}}
{
e_{(\alpha, \beta)}
}
-
e_{(H, W)}
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\left(
\ \
\left(
\boxed{
\bigg(
{\underset{(\alpha', \beta') \in \Omega'}{\sum}}
{
e_{(\alpha', \beta')}
}
=
{\underset{(\alpha, \beta) \in \Omega}{\sum}}
{
e_{(\alpha, \beta)}
}
-
e_{(H, W)}
\bigg)
}
\iff
\left(
\vartheta
=
\overset{\substack{{ \alpha' = H - \Delta_{y} } \\ { \beta' = W - \Delta_{x} }}}
{\underset{\substack{{ \alpha' = 1 - \Delta_{y} } \\ { \beta' = 1 - \Delta_{x} }}}{\sum}}
{
e_{(\alpha', \beta')}
}
=
{\underset{(\alpha', \beta') \in \Omega'}{\sum}}
{
e_{(\alpha', \beta')}
}
=
{\underset{(\alpha, \beta) \in \Omega}{\sum}}
{
e_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
e_{(\alpha, \beta)}
}
-
e_{(H, W)}
\right)
\right)
\Rightarrow
\left(
\left(
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
\eta_{(i + \Delta_{y}, j + \Delta_{x})}
}
=
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(0)}}
}
+
\ \
\overbrace{
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
e_{(i + \Delta_{y}, j + \Delta_{x})}
}
-
e_{(H, W)}
}^{\boxed{\vartheta}}
\ \
-
\overset{\substack{{ i = H - \Delta_{y} } \\ { j = W - \Delta_{x} }}}
{\underset{\substack{{ i = 1 - \Delta_{y} } \\ { j = 1 - \Delta_{x} }}}{\sum}}
{
e_{(i + \Delta_{y}, j + \Delta_{x})}
}
\right)
\iff
\left(
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
\eta_{(\alpha, \beta)}
}
=
\overset{\substack{{ \alpha = H } \\ { \beta = W }}}
{\underset{\substack{{ \alpha = 1 } \\ { \beta = 1 }}}{\sum}}
{
a_{{(\alpha, \beta)}_{(0)}}
}
-
e_{(H, W)}
\iff
\boxed{
\overset{\substack{{ i = H } \\ { j = W }}}
{\underset{\substack{{ i = 1 } \\ { j = 1 }}}{\sum}}
{
\eta_{(i, j)}
}
=
\overset{\substack{{ i = H } \\ { j = W }}}
{\underset{\substack{{ i = 1 } \\ { j = 1 }}}{\sum}}
{
a_{(i, j)}
}
-
e_{(H, W)}
}
\right)
\right)
\ \
\right)
\end{cases}
\end{array}
$$

Part 15 :

- Since the result is $\bar{N} - \bar{A} = -\frac{e_{(H, W)}}{H \cdot W}$, and since $e_{(H, W)} \in \{-127, \dots, 127\}$, then for any image of size $HW$ larger than the bounds of $e_{(H, W)}$ (so either $-127$, or $127$), we have :
  $-\frac{e_{(H, W)}}{H \cdot W} \approx 0$ 

- It means that for any image larger than a postage stamp (16×16 pixels), the output image is a dithered image that is visually coherent. So $P_{2}$ is true

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\left(
\ \
\boxed{
\left(
\overset{\substack{{ i = H } \\ { j = W }}}
{\underset{\substack{{ i = 1 } \\ { j = 1 }}}{\sum}}
{
\eta_{(i, j)}
}
=
\overset{\substack{{ i = H } \\ { j = W }}}
{\underset{\substack{{ i = 1 } \\ { j = 1 }}}{\sum}}
{
a_{(i, j)}
}
-
e_{(H, W)}
\right)
}
\iff
\left(
\frac{1}{H \cdot W}
\cdot
\left(
\overset{\substack{{ i = H } \\ { j = W }}}
{\underset{\substack{{ i = 1 } \\ { j = 1 }}}{\sum}}
{
\eta_{(i, j)}
}
\right)
=
\frac{1}{H \cdot W}
\cdot
\left(
\overset{\substack{{ i = H } \\ { j = W }}}
{\underset{\substack{{ i = 1 } \\ { j = 1 }}}{\sum}}
{
a_{(i, j)}
}
-
e_{(H, W)}
\right)
\right)
\iff
\bigg(
\bar{N}
=
\bar{A}
-
\frac{e_{(H, W)}}{H \cdot W}
\bigg)
\iff
\boxed{
\bigg(
\bar{N}
-
\bar{A}
=
-
\frac{e_{(H, W)}}{H \cdot W}
\bigg)
}
\ \
\right)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\boxed{
\Big(
e_{(H, W)} = - 127
\Big)
}
\Rightarrow
\Big(
\big(
\bar{N}
=
\bar{A}
+
\frac{127}{H \cdot W}
\big)
\Rightarrow
\boxed{
\big(
\bar{N}
>
\bar{A}
\big)
}
\Big)
\bigg)
\land
\bigg(
\boxed{
\Big(
e_{(H, W)} = 0
\Big)
}
\Rightarrow
\Big(
\big(
\bar{N}
=
\bar{A}
-
\frac{0}{H \cdot W}
\big)
\Rightarrow
\boxed{
\big(
\bar{N}
=
\bar{A}
\big)
}
\Big)
\bigg)
\land
\bigg(
\boxed{
\Big(
e_{(H, W)} = + 127
\Big)
}
\Rightarrow
\Big(
\big(
\bar{N}
=
\bar{A}
-
\frac{127}{H \cdot W}
\big)
\Rightarrow
\boxed{
\big(
\bar{N}
<
\bar{A}
\big)
}
\Big)
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
\lim_{H \cdot W \to +\infty}
\left(
-
\frac{e_{(H, W)}}{H \cdot W}
\right)
=
0
\bigg)
\Rightarrow
\bigg(
\Big(
\bar{N}
-
\bar{A}
\underset{H \cdot W \to +\infty}{=}
0
\Big)
\iff
\boxed{
\Big(
\bar{N}
\underset{H \cdot W \to +\infty}{=}
\bar{A}
\Big)
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\exists w_{(\Delta_{x}, \Delta_{y})} \in \mathbb{R}, \quad
\bigg(
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}
{w_{(\Delta_{x}, \Delta_{y})}}
=
1
\bigg)
\land
\bigg(
a_{(i + \Delta_{y}, j + \Delta_{x})}
=
a_{(i + \Delta_{y}, j + \Delta_{x})}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\bigg)
\land
\bigg(
\bar{N} \to \bar{A}
\bigg)
\Bigg)
}
\\[1em]
\Rightarrow
\boxed{
\Bigg(
P_{2}
\Bigg)
}
\end{cases}
\end{array}
$$

Part 16 :

- In this part (optional), we examine from a "local" point of view whether $a_{{(i, j)}_{(\iota + 1)}}=a_{{(i, j)}_{(\iota)}}$ (just as we did with other variables from a "global" point of view with $\bar{N} = \bar{A}$ )

$$
\begin{array}{l}
\Rightarrow
\begin{cases}
\Bigg(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
=
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota - 1)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
S_{{(local)}_{(\iota)}}
:=
a_{{(i, j)}_{(\iota)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
}
\bigg)
\land
\bigg(
S_{{(local)}_{(\iota + 1)}}
:=
a_{{(i, j)}_{(\iota + 1)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota + 1)}}
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
S_{(local)_{(\iota + 1)}}
=
a_{{(i, j)}_{(\iota + 1)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota + 1)}}
}
\bigg)
\iff
\bigg(
S_{(local)_{(\iota + 1)}}
=
a_{{(i, j)}_{(\iota + 1)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
+
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\Big)
}
\bigg)
\iff
\bigg(
S_{(local)_{(\iota + 1)}}
=
a_{{(i, j)}_{(\iota + 1)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
\Big)
}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
e_{(i, j)}
\cdot
w_{(\Delta_{x}, \Delta_{y})}
\Big)
}
\bigg)
\\[1em]
\quad
\iff
\bigg(
S_{(local)_{(\iota + 1)}}
=
a_{{(i, j)}_{(\iota + 1)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
\Big)
}
+
\underbrace{
e_{(i, j)}
\cdot
}_{\ \because {\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}}
\ \
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
w_{(\Delta_{x}, \Delta_{y})}
}
\bigg)
\iff
\bigg(
S_{(local)_{(\iota + 1)}}
=
a_{{(i, j)}_{(\iota + 1)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
\Big)
}
+
e_{(i, j)}
\cdot
\Big(
\underbrace{
\frac{7}{16} + \frac{3}{16} + \frac{5}{16} + \frac{1}{16}
}_{1}
\Big)
\bigg)
\\[1em]
\quad
\iff
\bigg(
S_{(local)_{(\iota + 1)}}
=
a_{{(i, j)}_{(\iota + 1)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
\Big)
}
+
e_{(i, j)}
\bigg)
\iff
\bigg(
S_{(local)_{(\iota + 1)}}
=
\Big(
a_{{(i, j)}_{(\iota + 1)}}
+
e_{(i, j)}
\Big)
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
\Big)
}
\bigg)
\Bigg)
\\[1em]
\Rightarrow
\Bigg(
\bigg(
S_{(local)_{(\iota + 1)}}
=
S_{(local)_{(\iota)}}
\bigg)
\iff
\bigg(
\Big(
a_{{(i, j)}_{(\iota + 1)}}
+
e_{(i, j)}
\Big)
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
\Big)
}
=
a_{{(i, j)}_{(\iota)}}
+
{\underset{(\Delta_{x}, \Delta_{y}) \in V}{\sum}}{
\Big(
a_{{(i + \Delta_{y}, j + \Delta_{x})}_{(\iota)}}
\Big)
}
\bigg)
\iff
\bigg(
a_{{(i, j)}_{(\iota + 1)}}
+
\underbrace{
\quad \quad
e_{(i, j)}
\quad \quad
}_{
e_{(i, j)} = a_{{(i, j)}_{(\iota+1)}} - \eta_{(i, j)}
}
=
a_{{(i, j)}_{(\iota)}}
\bigg)
\iff
\boxed{
\bigg(
\Big(
S_{(local)_{(\iota + 1)}}
=
S_{(local)_{(\iota)}}
\Big)
\iff
\Big(
a_{{(i, j)}_{(\iota + 1)}}
=
a_{{(i, j)}_{(\iota)}}
-
\underbrace{
\quad \quad
e_{(i, j)}
\quad \quad
}_{
e_{(i, j)} = a_{{(i, j)}_{(\iota+1)}} - \eta_{(i, j)}
}
\Big)
\bigg)
}
\Bigg)
\\[1em]
\Rightarrow
\boxed{
\Bigg(
\bigg(
e_{(i, j)}
=
a_{{(i, j)}_{(\iota+1)}} - \eta_{(i, j)}
=
0
\bigg)
\Rightarrow
\bigg(
a_{{(i, j)}_{(\iota + 1)}}
=
a_{{(i, j)}_{(\iota)}}
\bigg)
\Bigg)
}
\end{cases}
\end{array}
$$

Part 17 :

- In this part, we conclude

$$
\begin{array}{l}
\boxed{
\therefore
\Bigg(
\bigg(
e_{(H, W)} = - 127
\bigg)
\Rightarrow
\bigg(
\bar{N}
>
\bar{A}
\bigg)
\Bigg)
\land
\Bigg(
\bigg(
e_{(H, W)} = 0
\bigg)
\Rightarrow
\bigg(
\bar{N}
=
\bar{A}
\bigg)
\Bigg)
\land
\Bigg(
\bigg(
e_{(H, W)} = + 127
\bigg)
\Rightarrow
\bigg(
\bar{N}
<
\bar{A}
\bigg)
\Bigg)
\land
\Bigg(
\bar{N}
\underset{H \cdot W \to +\infty}{=}
\bar{A}
\Bigg)
}
\end{array}
$$

