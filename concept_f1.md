# Concept F1 Evaluation Metrics

Traditional similarity-based metrics for natural language
generation like ROUGE ([Lin, 2004](https://www.microsoft.com/en-us/research/publication/rouge-a-package-for-automatic-evaluation-of-summaries/)) 
and BLEU ([Papineni et al., 2002](https://aclanthology.org/P02-1040/)) only compare
system answer and gold answer from a surface-form like n-gram and can not
capture the semantic concept within the output of long-form answer. 
Thus, we proposed a new evaluation metric for comparing long 
form sentences, concept F1, that focuses
on the mapping of semantic concepts.

## Definition
Given an output $y$ of the system, we define 
$C(y)=\{c_1, c_2, ... ,c_i, ... ,c_n\}$
as a set of $n$ unique concepts that is contained in $y$. 
Let $\hat{y}$ be the gold answer with unique concepts 
$C(\hat{y})=\{c_1, c_2, ... ,c_j, ... ,c_m\}$. 
Define $ConceptHits(y,\hat{y})$ as a function that calculates  
the number of concepts $c_i$ in system output $y$ that appears in gold 
answer $\hat{y}$ as Equation (1):

$$
\tag{1}
ConceptHits(y,\hat{y})=\sum_{c_i \in C(y)}^{} ConceptInSentence(c_i,\hat{y}),
$$

where $ConceptInSentence(c_i,\hat{y})$ indicates if concept $c_i$ appear in 
gold answer $\hat{y}$ (see Equation 2).

$$
\tag{2}
ConceptInSentence(c_i,\hat{y})=
\begin{cases}
  1, & \text{if } MostSimilarConceptScore(c_i,\hat{y}) \geq \epsilon \\
  0, & \text{otherwise,}
\end{cases}
$$

where $\epsilon$ is the threshold, and $MostSimilarConceptScore(c_i,\hat{y})$ 
is the maximum similarity score between concept $c_i$ 
and each of the concepts $c_j$ in the gold answer $C(\hat{y})$,
which is defined in Equation (3).

$$
\tag{3}
MostSimilarConceptScore(c_i,\hat{y})=max(Similarity(c_i,c_j)), c_j \in C(\hat{y}),
$$

where $Similarity(c_i,c_j)$ is defined as the cosine similarity between the 
concept embedding of concept $c_i$ and $c_j$. 

Finally, we can calculate $ConceptPrecision_c(y,\hat{y})$, 
$ConceptRecall_c(y,\hat{y})$, and $ConceptF1_c(y,\hat{y})$ as follows:

$$
\tag{4}
ConceptPrecision_c(y,\hat{y})=\frac{ConceptHits(y,\hat{y})}{\left|{C(y)}\right|},
$$

$$
\tag{5}
ConceptRecall_c(y,\hat{y})=\frac{ConceptHits(y,\hat{y})}{\left|{C(\hat{y})}\right|},
$$

$$
\tag{6}
ConceptF1_c(y,\hat{y})=2\times\frac
{ConceptPrecision_c(y,\hat{y}) \times ConceptRecall_c(y,\hat{y})}
{ConceptPrecision_c(y,\hat{y}) + ConceptRecall_c(y,\hat{y})}
.
$$
