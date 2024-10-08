# O&O Scoring Definitions

## Score or Contributing Factor, Synonyms, and Definition

### Ordering Score 

**Synonyms:** Sugeno, Sugeno Integral, f-score

**Definition:** The **Ordering Score** is calculated as the Sugeno Integral, which is based on the concepts of "fuzzy measures" and "fuzzy integral", as described in Fuzzy Set Theory. The Ordering Score is based on three scoring factors: **Confidence Score**; **Clinical Evidence Score**; and **Novelty Score**. The fuzzy integral is used to aggregate those factors. The Ordering Score or Sugeno considers the aggregated importance of combinations of the scoring factors, where higher values are treated with greater importance than lower values, and it intuits that factors with low scores are not as relevant or important to the aggregation than factors with high scores. The Ordering Score is scaled 0 to 5.

**UI Concise Definition Display:** Multimodal calculation considering strength of relationships supporting the result. Scores range from 0 to 5 and may change as new results are added.

### Confidence Score

**Synonyms:** g-score	

**Definition:** The **Confidence Score** combines the scores assigned to a given result by multiple reasoning agents, with an expected range of [0,1] for each score. The Confidence Score invokes an algorithm that implements the following logic: let `score(ara[i])` represent the score returned by ARA `i` for a given answer; the Confidence Score is then given by `1 - \product_i (1 - score(ara[i]))`. In natural language, the algorithm treats `1 - score(ara[i])` as the "doubt" that ARA `i` had in the answer and then considers each ARA as independent from the others, so it multiplies these "doubts" together before subtracting from 1 to return a final Confidence Score. This is essentially equivalent to geometric (or logarithmic) pooling with constant weights as described [here](https://philsci-archive.pitt.edu/11349/1/OpinionPoolingReview.pdf).

### Clinical Information Score

**Synonyms:** Clinical	

**Definition:** The **Clinical Information Score** is calculated as a weighted average of the natural logarithm of the odds ratio for an observed real-world association between a drug exposure and a disease diagnosis, as asserted by Translator's clinical knowledge sources. The Clinical Information Score is thresholded as [0,1). For additional information, please see the associated [wiki page](https://github.com/NCATSTranslator/Translator-All/wiki/Translator-Clinical-Information-Score).

### Novelty Score

**Synonyms:** Novelty	

**Definition:** The **Novelty Score** is calculated using three factors: **Recency Factor**; **Molecular Similarity Factor**; and **FDA Approval Status**. The computation is performed for results that have been "inferred" by one or more reasoning agents; the computation is not performed for results that have been derived from curated knowledge sources and thus considered "fact". The Recency Factor refers to how current the publication support is for a given result; the Molecular Similarity Factor is based on chemical structure similarity between a predicted drug treatment and established drug treatments; and FDA Approval Status refers to the phase (Phase I, II, III, or IV) of US FDA approval for a predicted drug treatment. Note that the Novelty Score reflects the Translator System's assessment of the "novelty" of a given result, which may or may not align with a user's assessment of "novelty". The Novelty Score is represented as [0,1].

### Recency Factor

**Synonyms:** Recency	

**Definition:** The **Recency Factor** considers the number of supporting publications for a given result and the year of publication for the oldest supporting publication: these two values are combined into a sigmoid function to produce a value for recency of a given result. The Recency Factor is represented as a number within the interval [0,1], where a recency factor near 1 indicates that a drug has very recent publication support.

### Molecular Similarity Factor	

**Synonyms:** Molecular Similarity	

**Definition:** The **Molecular Similarity Factor** compares the chemical structure of a predicted drug treatment with that of established treatments, as asserted by curated knowledge sources. The Molecular Similarity Factor is calculated using a cheminformatics algorithm that applies a Jaccard coefficient to assess the pairwise similarity between two molecules. The factor is represented as [0,1], where a molecular similarity factor of 1 indicates that two molecules are structurally identical.

### FDA Approval Status		

**Synonyms:** Approval Status

**Defintion:** **FDA Approval Status** is provided for predicted drug treatments and refers to the clinical research phases required for US FDA approval of a new pharmaceutical or a new indication for an existing pharmaceutical. _This FDA Approval Status is specific to the disease that is part of the result._ For the Novelty Score, FDA approval Status is treated as a binary value of 0 (FDA Approval for Marketing / FDA Clinical Research Phase 4) or 1 (FDA Clinical Research Phase 1, 2, or 3). Note that the source from which the FDA Approval Status is derived is ChEMBL (https://www.ebi.ac.uk/chembl/), which does not distinguish between FDA Approval for Marketing and FDA Clinical Research Phase 4. If a predicted drug treatment is a chemical entity that is not in clinical trials, then FDA approval status is treated as null and does not factor into the Novelty Score.

![O O-graphic](https://github.com/NCATSTranslator/Ordering-Organizing/assets/26254388/34fd08ca-d9c9-45bf-8757-1045a3557555)

