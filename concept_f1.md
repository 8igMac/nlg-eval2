# Concept F1 Evaluation Metrics

The final output of our system is a conclusion which might contain multiple semantic
concepts. However, traditional similarity-based metrics for natural language
generation like ROUGE ([Lin, 2004][https://www.microsoft.com/en-us/research/publication/rouge-a-package-for-automatic-evaluation-of-summaries/]) 
and BLEU ([Papineni et al., 2002](https://aclanthology.org/P02-1040/)) only compare
system conclusion and gold conclusion from a surface-form like n-gram and can not
capture the semantic concept within the conclusion. Thus, we proposed a new
evaluation metric for comparing long form sentences, concept F-measure, that focuses
on the mapping of semantic concepts.