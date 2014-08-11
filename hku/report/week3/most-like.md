# Approximate "Most Like" Results and Analysis
**Chen Huarong <i@chr.asia>** *11/08/14*

<!-- 
{Syntax quick reference}
Link: [Text](link)  <a target="_blank" href=""></a>
Image: ![Title](link)
-->

* The found "most like" region was marked with red border.

## Different Inputs

Number of Patches | User Input | Style Input |
--- | --- | --- |
25 | ![farm](img/most-like/images/farm/most_match_src.jpg) | ![farm](img/most-like/images/farm/most_match_cor.jpg) |
245 | ![flower](img/most-like/images/flower/most_match_src.jpg) | ![flower](img/most-like/images/flower/most_match_cor.jpg) |
78 | ![fruit](img/most-like/images/fruit/most_match_src.jpg) | ![fruit](img/most-like/images/fruit/most_match_cor.jpg) |
362 | ![hand](img/most-like/images/hand/most_match_src.jpg) | ![hand](img/most-like/images/hand/most_match_cor.jpg) |
183 | ![sea](img/most-like/images/sea/most_match_src.jpg) | ![sea](img/most-like/images/sea/most_match_cor.jpg) |

* The distance is RGB distance - 150 * total of pixels.
* The number of pre-selected seeds is 1024. 

## Different number of pre-selected seeds
### About the elapsed time
Number of Seeds | Elapsed Seconds |
--- | --- |
1024 | &lt;1 |
16384 | 1 | 
65536 | 2 |
131072 | 4 |
262144 | 9 |
524288 | 17 |

* It seems to be $O(n)$.

### Results
Number of Seeds | Number of Patches | User Input | Style Input |
--- | --- | --- | --- |
1024 | 60 | ![fruit](img/most-like/seeds/1024/most_match_src.jpg) | ![fruit](img/most-like/seeds/1024/most_match_cor.jpg) |
65536 | 37 | ![fruit](img/most-like/seeds/65536/most_match_src.jpg) | ![fruit](img/most-like/seeds/65536/most_match_cor.jpg) |
524288 | 107 | ![fruit](img/most-like/seeds/524288/most_match_src.jpg) | ![fruit](img/most-like/seeds/524288/most_match_cor.jpg) |

* The results are similar.

## Different distance functions
Distance Function | Number of Patches | User Input | Style Input |
--- | --- | --- | --- |
RGB | 21 | ![farm](img/most-like/energy/rgb/most_match_src.jpg) | ![farm](img/most-like/energy/rgb/most_match_cor.jpg) |
Luminance | 74 | ![farm](img/most-like/energy/luminance/most_match_src.jpg) | ![farm](img/most-like/energy/luminance/most_match_cor.jpg) |

* The result with luminance distance is better.