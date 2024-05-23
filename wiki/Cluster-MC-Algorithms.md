Clustering Monte Carlo Algorithms
===

Wolff Algorithm
---


```
Wolff( v_0, beta, J )
  S = { v_0 }
  while |S| > 0:
    v = pop(S)
    foreach neighbor u of v:
      if (spin(u) != spin(v)): continue
      if rand() < (1 - exp( - 2 * beta * J )):
        push(S,u)
    flip(v)

for (iter < max_iter) or (E < E_threshold):
  v = random site
  Wolff( v, beta, J )
```

References
---

* [Introduction to Cluster Monte Carlo Algorithms](https://csml.northwestern.edu/resources/Reprints/lnp_color.pdf)


###### 2024-05-22
