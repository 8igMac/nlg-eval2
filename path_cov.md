# Argument Tree Evaluation Metrics

$$
\tag{1}
ArgumentTreeSimilarity(t,\hat{t})=\frac{\sum_{p_i \in Path(\hat{t})}^{} PathInTree(p_i,t)}{\left|{Path(\hat{t})}\right|},
$$

$$
\tag{2}
PathInTree(p_i, t)=
\begin{cases}
  1, & \text{if } MostSimilarPathScore(p_i,t) \geq \epsilon \\
  0, & \text{otherwise,}
\end{cases}
$$

$$
\tag{3}
MostSimilarPathScore(p_i,t)=max(Similarity(p_i,p_j)), p_j \in Path(t),
$$