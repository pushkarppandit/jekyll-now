---
layout: post
title: Algorithmically generating natural looking trees
---
## NOW!
### here is something

Reading [this](http://www.nbtindia.gov.in/books_detail__11__popular-science__1074__chaos-fractals-and-self-organisation.nbt) excellent book got me thinking on fractals in nature and how many natural structures could be modeled as neat fractals. I decided to try my hand at visually representing the most obvious choice for fractal structures in nature, which is trees, using python. 

A tree can be thought of as a recursively generated object, with the main trunk splitting into a number of branches, and each branch further splitting in a similar way. 
To start simple, I write the following two functions to create a binary tree
```python
def binary_tree(n,seed,changes):
    lines = []
    lines.append(seed)
    if n>1:
        new_seed1 = [(seed[0][0]+seed[1][0]*np.cos(seed[1][1]),seed[0][1]+seed[1][0]*np.sin(seed[1][1])),(seed[1][0]*changes[0],seed[1][1]+changes[1])]
        new_seed2 = [(seed[0][0]+seed[1][0]*np.cos(seed[1][1]),seed[0][1]+seed[1][0]*np.sin(seed[1][1])),(seed[1][0]*changes[0],seed[1][1]-changes[1])]
        lines.extend(binary_tree(n-1,new_seed1,changes))
        lines.extend(binary_tree(n-1,new_seed2,changes))
    return lines
def transform_tree_to_coord(tree_lines):
    tree_transf = [[(pt[0][0],pt[0][1]),(pt[0][0]+pt[1][0]*np.cos(pt[1][1]),pt[0][1]+pt[1][0]*np.sin(pt[1][1]))] for pt in tree_lines]
    return(tree_transf)
```

The function `binary_tree` is used to define a tree. Each tree is defined as a set of segments, with the segments defined recursively starting from the main trunk. Each segment is defined like a vector by $(x,y)$ coordinates for a point and $(l,\theta)$ for a length and direction. These are captured in the parameter `seed` which is `[[x,y],[l,theta]]`


![saitama]({{ site.baseurl }}/images/saitama.jpg)
