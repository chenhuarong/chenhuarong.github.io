# Patch-ANN Results and Analysis
**Chen Huarong <i@chr.asia>** *11/08/14*

<!-- 
{Syntax quick reference}
Link: [Text](link)  <a target="_blank" href=""></a>
Image: ![Title](link)
-->

## Construct an existing image using Patch-ANN result

User Input | Style Input | Matched Patch's Centers | Construct Using Matched Patches |
--- | --- | --- | --- |
![farm](img/src/farm/nymph_in.jpg) | ![farm](img/src/farm/style_in.jpg) | ![farm](img/patch-ann/construct/farm/pm_prob.jpg) | ![farm](img/patch-ann/construct/farm/pm_result.jpg) |
![flower](img/src/flower/nymph_in.jpg) | ![flower](img/src/flower/style_in.jpg) | ![flower](img/patch-ann/construct/flower/pm_prob.jpg) | ![flower](img/patch-ann/construct/flower/pm_result.jpg) |
![fruit](img/src/fruit/nymph_in.jpg) | ![fruit](img/src/fruit/style_in.jpg) | ![fruit](img/patch-ann/construct/fruit/pm_prob.jpg) | ![fruit](img/patch-ann/construct/fruit/pm_result.jpg) |
![hand](img/src/hand/nymph_in.jpg) | ![hand](img/src/hand/style_in.jpg) | ![hand](img/patch-ann/construct/hand/pm_prob.jpg) | ![hand](img/patch-ann/construct/hand/pm_result.jpg) |
![sea](img/src/sea/nymph_in.jpg) | ![sea](img/src/sea/style_in.jpg) | ![sea](img/patch-ann/construct/sea/pm_prob.jpg) | ![sea](img/patch-ann/construct/sea/pm_result.jpg) |

* The patch size is set to 11.
* The distance is RGB distance.
* The number of iterations is 5.
* The results above can prove the correctness of my implementation of Patch-ANN.

## Different patch size
### About the elapsed time
Patch Size | Elapsed Seconds |
--- | --- |
3 | 4 |
7 | 13 |
11 | 28 |
21 | 133 |

* The distance is RGB distance.
* The number of iterations is 5.
* Most time was consumed to calculate the distance.

### Construct with different patch size
User Input: ![fruit](img/src/fruit/nymph_in.jpg)
Style Input: ![fruit](img/src/fruit/style_in.jpg)

Patch Size | Matched Patch's Centers | Construct Using Matched Patches |
--- | --- | --- |
3 | ![fruit](img/patch-ann/patch-size/3/pm_prob.jpg) | ![fruit](img/patch-ann/patch-size/3/pm_result.jpg) |
7 | ![fruit](img/patch-ann/patch-size/7/pm_prob.jpg) | ![fruit](img/patch-ann/patch-size/7/pm_result.jpg) |
11 | ![fruit](img/patch-ann/patch-size/11/pm_prob.jpg) | ![fruit](img/patch-ann/patch-size/11/pm_result.jpg) |
21 | ![fruit](img/patch-ann/patch-size/21/pm_prob.jpg) | ![fruit](img/patch-ann/patch-size/21/pm_result.jpg) |

* The distance is RGB distance.
* The number of iterations is 5.
* For the given image, patch size 11 is suitable for the rest algorithm.

## Different number of iterations
### About the elapsed time
Iterations | Elapsed Seconds |
--- | --- |
1 | 6 |
4 | 21 |
6 | 33 |

### Construct with different number of iterations
Iterations | Matched Patch's Centers | Construct Using Matched Patches |
--- | --- | --- |
1 | ![fruit](img/patch-ann/iterations/1/pm_prob.jpg) | ![fruit](img/patch-ann/iterations/1/pm_result.jpg) |
4 | ![fruit](img/patch-ann/iterations/4/pm_prob.jpg) | ![fruit](img/patch-ann/iterations/4/pm_result.jpg) |
6 | ![fruit](img/patch-ann/iterations/6/pm_prob.jpg) | ![fruit](img/patch-ann/iterations/6/pm_result.jpg) |

* 3-5 iterations are enough.

## Different distance functions
Distance Function | Matched Patch's Centers | Construct Using Matched Patches |
--- | --- | --- |
RGB | ![fruit](img/patch-ann/energy/rgb/pm_prob.jpg) | ![fruit](img/patch-ann/energy/rgb/pm_result.jpg) |
Luminance | ![fruit](img/patch-ann/energy/luminance/pm_prob.jpg) | ![fruit](img/patch-ann/energy/luminance/pm_result.jpg) |