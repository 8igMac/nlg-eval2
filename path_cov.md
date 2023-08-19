# Argument Tree Evaluation Metrics

$$
\tag{1}
Path(t)=\{p_1, p_2, ... ,p_i, ... ,p_n\},
$$

$$
\tag{2}
Path(\hat{t})=\{p_1, p_2, ... ,p_j, ... ,p_m\},
$$

$$
\tag{3}
ArgumentTreeSimilarity(t,\hat{t})=\frac{PathHits(t,\hat{t})}{\left|{Path(\hat{t})}\right|},
$$

$$
\tag{4}
PathHits(t,\hat{t})=\sum_{p_j \in Path(\hat{t})}^{} PathInTree(p_j,t),
$$

$$
\tag{5}
PathInTree(p_j, t)=
\begin{cases}
  1, & \text{if } MostSimilarPathScore(p_j,t) \geq \epsilon \\
  0, & \text{otherwise,}
\end{cases}
$$

$$
\tag{6}
MostSimilarPathScore(p_j,t)=max(Similarity(p_j,p_i)), p_i \in Path(t),
$$