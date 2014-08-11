# Weekly Report: Week 3 (04/08/14 - 10/08/14)
**Chen Huarong <i@chr.asia>** *11/08/14*

<!-- 
{Syntax quick reference}
Link: [Text](link)  <a target="_blank" href=""></a>
Image: ![Title](link)
-->

## Summary
* (Papers) I read the paper <a target="_blank" href="http://gfx.cs.princeton.edu/pubs/Barnes_2009_PAR/index.php">PatchMatch: A Randomized Correspondence Algorithm for Structural Image Editing</a> [\[1\]](#ref1), and implemented the approximate nearest-neighbor algorithm (for patches, referred to as Patch-ANN) introduced in the paper.
* (Project) I designed the pipeline of my stylization algorithm and finished part of it with the help of Patch-ANN(Approximate nearest-neighbor algorithm for patches).
* (Experiments) I managed to construct an existing image using Patch-ANN result to confirm the correctness of my implementation of the paper. Also, I tested several images using my algorithm to find out their "most like part".

## Completions
### Patch-ANN
I failed to find out a 3rd-party library of the ANN algorithm introduced in PatchMatch [\[1\]](#ref1) , so I implemented the algorithm according to the algorithm description.

The Patch-ANN algorithm introduced in the paper is commonly used in image inpainting and usually based on a Gaussian Pyramid to build the matching map(coarse to fine). Here I choose Patch-ANN to help selecting a number of seeds and later grow them to "most like" parts in the image.

I choose the user input image $I$ as source image and want to find every patch's correspondence to the style input image $S$. So the input of Patch-ANN algorithm includes $I$, $S$ and a customed distance function $d$. 

To confirm the correctness of my implementation of Patch-ANN, I constructed $I$ using the corresponding patches in $S$.

Results and Analysis: <a href="patch-ann.html" target="_blank">open</a>.

### Finding the "most like" part in images
I want to find out a connected region in $I$ that satisfying:

1. Its area is as large as possible.
2. For given distance function $d$, the distance between the region and its corresponding region in $S$ is as small as possible.

Combining the above two conditions, $d$ will be area-related.

I designed an algorithm to find the approximate "most like" part in images. The steps of the algorithm are as following:

1. Build the corresponding map $C$ between $I$ and $S$ using the Patch-ANN algorithm and distance function $d$. That is, for every patch $p\in I$, we have $q=C(p)\in S$, and $d(p, q)$ has an approximate minimum value.
2. Select $N$ patches as seeds in $I$ randomly.
3. For every seed $t$, calculate $t_d = d(t, C(t))$.
4. Screen out $\dfrac{N}{2}$ seeds that has larger $t_d$. Let $N=\dfrac{N}{2}$.
5. For every seed $t$, grow it. That is, find out an adjacent patch $u$ that satisfying $d(t\cup\{u\}, C(t\cup\{u\}))>d(t, C(t))$, then let $t=t\cup\{u\}$. If no adjacent patch satisfied the condition, $t$ will not grow.
6. If $N>1$, goto step 3. If $N==1$, goto step 5 until the sole seed stop growing.
7. The sole seed is the output.

Results and Analysis: <a href="most-like.html" target="_blank">open</a>.

## Observations & Thoughts
The size of patch, the iterations in Patch-ANN, the number of pre-selected seeds, the distance function, all above terms will affect the result of the "approximate most-like" algorithm.
	
### The size of patch
Too large patch will result in a leap of processing time and too small patch will result in an unsatisfying "most-like" result.

For the moment, a acceptable size of patch can be calculated by the formula: $\sqrt{\dfrac{Rows*Cols}{40000}}$, where $Rows$ and $Cols$ are the number of rows and columns of $I$.

### The iterations in Patch-ANN and the number of pre-selected seeds
According to the Patch-ANN results and analysis above, I think 3-5 iterations in Patch-ANN is a good choice.

In the same way, $N=1024$ pre-selected seeds can achieve acceptable results.

### The distance function
I only tried two naive distance functions(RGB distance, luminance distance) and they only consider the patches in given region.

To find a good "most-like" part, or to synthesis a good stylized result, the adjacent regions will help a lot, but I haven't tried it out.

## Difficulties & Plans
In my plan, finding the approximate "most-like" region in images is the first step of the whole algorithm.

I want to find out an approximate "most-like" rect in images and found that it is hard to "grow" a rect. So I compromised with such "most-like" region algorithm.

The three steps of my stylization algorithm are:

1. Find an approximate "most-like" region in given input image and style input image.
2. Synthesize the corresponding region in the output image.
3. Break the input image up into some "like" region and synthesize them using the algorithm in step 1 and 2, and combine the results after that.

I will implement my stylization algorithm with less considerations of efficiency at first, and speed it up later.

## References
<b id="ref1">[1]</b> Barnes C, Shechtman E, Finkelstein A, et al. PatchMatch: A randomized correspondence algorithm for structural image editing[J]. ACM Transactions on Graphics-TOG, 2009, 28(3): 24.