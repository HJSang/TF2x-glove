# Implement Glove by TF2.x

* [GloVe: Global Vector for Word Representation](https://nlp.stanford.edu/pubs/glove.pdf)

* Model Details:
  - Notation: <img src="https://latex.codecogs.com/gif.latex?X"/> be the matrix of word-word co-occurence counts, where <img src="https://latex.codecogs.com/gif.latex?X_{ij}"/> is the number of times word ``j`` occurs in the context of word ``i``. Let <img src="https://latex.codecogs.com/gif.latex?X_i=\sum_k X_{ik}"/> be the number of times any word appears in the context ``i``. Let <img src="https://latex.codecogs.com/gif.latex?P_{ij}=P(j|i)=X_{ij}/X_i"/> be the probability that word ``j`` appears in the context of word ``i``.
  - The appropriate starting point should be with ratios of co-occurence proabbilities rather than the probabilities themselves. Noting that the ratio of <img src="https://latex.codecogs.com/gif.latex?P_{ik}/P_{jk}"/> depends on the three words ``i,j,k``, the most general model tasks:

  <img src="https://latex.codecogs.com/gif.latex?F(w_i,w_j,\tilde{w}_k)=\frac{P_{ik}}{jk}"/>.
  
  - Since vector spaces are inherently linear structures, the most nature way todo this with vector differences:

  <img src="https://latex.codecogs.com/gif.latex?F(w_i-w_j,\tilde{w}_k)=\frac{P_{ik}}{P_{jk}}"/>

  - ``F`` could to be a complicated function but it would obfuscate the linear structure. To avoid this issue, 

  <img src="https://latex.codecogs.com/gif.latex?F((w_i-w_j)^T\tilde{w}_k)=\frac{P_{ik}}{P_{jk}}"/>

  - ``F=exp``

  <img src="https://latex.codecogs.com/gif.latex?P_{ik}=F(w_i^T\tilde{w}_k)=\frac{X_{ik}}{X_i}"/>

  - Finally, adding an additional bias:

  <img src="https://latex.codecogs.com/gif.latex?w_i^T\tilde{w}_k+b_i+\tilde{b}_k=\log(X_{ik})"/>

  - The cost function:

  <img src="https://latex.codecogs.com/gif.latex?J=\sum_{i,j=1}^Vf(X_{ij})(w_i^T\tilde{w}_j+b_i+\tilde{b}_j-\log X_{ij})^2"/>
  
  ``V`` is the size of the vocabulary. The weighting function should obey the following properties:
    -  ``f(0)=0``. It should vanish as ``x->0`` fast enough that ``lim f(x)log^2(x)`` is finite.
    -  ``f(x)`` is non-decreasing 
    -  ``f(x)`` should be relatively small for large values, so that frequent co-occurences are not overweighted.
    -  For example:

    ![image](./imgs/weights.png)

    ![image](./imgs/plot.png)

