# nlg-eval2
Large language model (LLM) like [GPT-4](https://openai.com/product/gpt-4)
are getting more and more powerful. The advancement of evaluation metrics 
for natural language generation (NLG) tasks have seems to fall behind. 
This repo aims to collect different modern evaluation metrics for NLG 
in the post LLM era.

## Updates
- 2023.07.25 Paper worth reading[Beyond Statistical Similarity: Rethinking Metrics for Deep Generative Models in Engineering Design](https://arxiv.org/abs/2302.02913): How do you evaluate the design
that ChatGPT generated compare to human design? Which was better?
- 2023.07.01 Add new evaluation metrics: [Concept F1](./concept_f1.md).

## Evaluation Method in Pre-LLM Era
- BLEU ([Papineni et al., 2002. Bleu: a Method for Automatic Evaluation of Machine Translatio](https://aclanthology.org/P02-1040/))
- ROUGE ([Chin-Yew Lin, 2004](https://www.microsoft.com/en-us/research/publication/rouge-a-package-for-automatic-evaluation-of-summaries/))
- METEOR ([Satanjeev Banerjee and Alon Lavie. 2005. Meteor: An automatic metric for mt evaluation with improved correlation with human judgments.](https://aclanthology.org/W05-0909/))
- BERTScore ([Zhang et al., 2019. BERTScore: Evaluating Text Generation with BERT](https://arxiv.org/abs/1904.09675))
    - Criticism
        - [Michael Hanna and Ondřej Bojar, 2021. A Fine-Grained Analysis of BERTScore](https://aclanthology.org/2021.wmt-1.59/)
        - [Sun et al., 2022. BERTScore is Unfair: On Social Bias in Language Model-Based Metrics for Text Generation](https://aclanthology.org/2022.emnlp-main.245/)
    - [BertScore on HuggingFace](https://huggingface.co/spaces/evaluate-metric/bertscore)

## Evaluation Method in Post-LLM Era
- [Concept F1](./concept_f1.md)
- GPT-based (See [this repo](https://github.com/THU-KEG/EvaluationPapers4ChatGPT#31-metrics) for more related paper.)
    - [DERA: Enhancing Large Language Model Completions with Dialog-Enabled Resolving Agents, Nair et al., 2023](https://arxiv.org/abs/2303.17071)
    - GPT-exact
    ```
    Question :{ question }

    Do the following two answers refer to the same medical concept ? Respond with an
    answer (" Answer : True " or " Answer : False ") followed by an explanation ("
    Explanation :")

     { answer_text }
     { predicted_answer_text }

     Answer :
    ```
    - GPT-similarity
    ```
    Assign a dxSimilarityScore to each of the following pairs where the first diagnosis
    is an " expectedDx " and the second diagnosis is the " providedDiagnosis ".

    Expected Vs Provided Dx Pairs :
    { answer_text } | { predicted_answer_text }
    { answer_text } | { zero_shot_option_index }

    Output each pair in one line using this format " dx1 " "|" " dx2 " "|" "
    dxSimilarityScore "
    output :
    ```
    - GPT-F1

## Qestion: How to evaluate information richness (i.e., informativeness) in semantic level?
What we are looking for is "relevant" and "diverse" information. (orthogonal in semantic space)
- Approach 1: Use GPT-based method to extract "information point" and use clustering algorithm
to calculate degree of seperation.
- Approach 2: Develop another GPT-based method, GPT-orthogonal, that prompt GPT to spot different
information point in a text. (**How to prove robustness of this method?**)

## Types of evaluation metrics
- Similarity-based: Require preparation of gold reference and use some kind of mechansim
to perform similarity comparison between the predicted answer and the gold reference. 
(e.g., BERTScore, GPT-F1, BLEU)
- Reference-free: Don't need to prepare gold reference. (e.g., As a human evaluator to vote
for different indicators, like fluency, consistency, etc.)
