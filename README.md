# Implement Glove by TF2.x

* [GloVe: Global Vector for Word Representation](https://nlp.stanford.edu/pubs/glove.pdf)

* Model Details:
  - Notation: <img src="https://latex.codecogs.com/gif.latex?X"/> be the matrix of word-word co-occurence counts, where <img src="https://latex.codecogs.com/gif.latex?X_{ij}"/> is the number of times word ``j`` occurs in the context of word ``i``. Let <img src="https://latex.codecogs.com/gif.latex?X_i=\sum_k X_{ik}"\> be the number of times any word appears in the context ``i``. Let <img src="https://latex.codecogs.com/gif.latex?P_{ij}=P(j|i)=X_{ij}/X_i"/> be the probability that word ``j`` appears in the context of word ``i``.
  - The appropriate starting point should be with ratios of co-occurence proabbilities rather than the probabilities themselves. Noting that the ratio of <img src="https://latex.codecogs.com/gif.latex?P_{ik}/P_{jk}"/> depends on the three words ``i,j,k``, the most general model tasks: <img src="https://latex.codecogs.com/gif.latex?F(w_i,w_j,\tilde{w}_k)=\frac{P_{ik}}{jk}"/>.

