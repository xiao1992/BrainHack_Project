# EEG-Based Odor Preference Modeling 🌹🧀️🪷🍃

## Overview
The human sense of smell plays a crucial role in emotional experience, yet remains underexplored in brain-computer interface research. EEG recordings provide a non-invasive technique for neural responses during olfactory perception. Previous research has shown that EEG can distinguish between pleasant and unpleasant odors at an individual level (Kroupi et al.,2014), but the consistency of these preferences across individuals and their potential for predictive modeling remain open questions.

---

## Project Motivation
This project investigates whether individuals share common EEG response patterns to odors they find pleasant or unpleasant, and whether these patterns can be generalized across subjects to predict preferences. The goal is to assess both subject-specific and cross-subject odor pleasantness classification and identify potential for real-world olfactory recommendation systems. Specifically, we seek to:
1) replicate existing within-subject classification of odor pleasantness.
2) determine if some odors are commonly preferred across subjects.
3) analyze whether EEG response patterns reflect those shared preferences.
4) develop and evaluate models that generalize odor preference prediction across individuals.

## Literature Review
Kroupi et al. (2014) demonstrated that EEG signals could classify pleasant vs. unpleasant odor perception with high accuracy in a subject-specific manner. However, subject-independent classification yielded lower performance, suggesting significant individual variation. The study did not explicitly test preference consistency across subjects or analyze EEG similarity among individuals who prefer the same odors. 

## Expected Outcomes
- Replication of Kroupi et al. (2014)'s within-subject EEG classification results of pleasant vs. unpleasant odors.
- Statistical analysis of cross-subject odor pleasantness agreement.
- Clustering of EEG responses among individuals with similar preferences.
- Development of simple classifiers to predict preference class from EEG, including cross-subject generalization.
- A set of visualizations mapping EEG response patterns to odors.

---

## Dataset: OPPD
We use the OPPD (Odor Pleasantness Perception Database) delopved by Kroupi et al. (2014) from EPFL [OPPD dataset](https://www.epfl.ch/labs/mmspg/downloads/page-119131-en-html/):
The dataset includes EEG recordings from 5 male participants (ages 26–32), each exposed to four odors: valerian, lotus flower, cheese, and rosewater. For each subject, both eyes-open and eyes-closed conditions were tested. Each odor trial includes a baseline segment and an event segment (odor presentation). The EEG signals were recorded with a 256-electrode EGI system at 250 Hz. Participants rated each odor on intensity and pleasantness. The most and least pleasant odors were identified per subject.

---

## Methodology
### 1. **EEG Data Processing**
The EEG data for each subject will be loaded from .mat files corresponding to the eyes-open and eyes-closed conditions. Within each file, the X_event segments, which represent EEG recordings during odor exposure, and the baseline segments preceding them will be extracted. EEG preprocessing will include bandpass filtering to isolate relevant frequency bands, followed by artifact removal using ICA. After filtering, each trial will be baseline-corrected by subtracting the power spectral density (PSD) of the corresponding pre-stimulus baseline segment. The PSD will be computed for standard EEG frequency bands: theta (4–7 Hz), alpha (8–13 Hz), beta (14–29 Hz), and gamma (30–47 Hz). The resulting band power values will be normalized across trials to reduce inter-trial variability and prepare the data for classification and clustering. Channels with poor signal quality or muscle contamination will be discarded, and the remaining data will be re-referenced to the common average.

### 2. **Model Training**
We will first replicate part of the original study with support vector machines (SVMs) using a radial basis function (RBF) kernel for within-subject classification of pleasant vs. unpleasant odors. We will also incorporate logistic regression and random forest models for exploratory comparison. For subject-independent analysis, we will explore transfer learning methods and cross-subject classifiers using leave-one-subject-out validation. To explore EEG preference consistency, clustering methods (k-means, hierarchical clustering, and spectral clustering) will be applied to the PSD feature space. Additionally, linear discriminant analysis (LDA) and principal component analysis (PCA) will be used to reduce dimensionality and highlight separable patterns. We will use Fisher Discriminant Ratio (FDR), Hilbert-Schmidt Independence Criterion (HSIC), t-tests, ANOVA, and Kendall’s W to evaluate the discriminability of features and agreement in odor preference across subjects.

### 3. **Visualization and Evaluation**
The effectiveness of the classification models will be assessed using multiple evaluation metrics including accuracy, precision, recall, F1-score, and ROC-AUC. For both within-subject and cross-subject settings, confusion matrices will be used to visualize misclassification patternss. To understand the spatial distribution of EEG feature importance, we will visualize scalp topographies using Fisher Discriminant Ratio (FDR) values, highlighting brain regions that contribute most to odor discrimination. Additionally, heatmaps of averaged EEG power changes will be created for each odor and frequency band, allowing direct comparison between conditions (eyes open vs. eyes closed). For exploring the consistency of odor preferences across subjects, we will generate preference similarity matrices comparing EEG-derived clusters to self-reported ratings. Dimensionality reduction techniques such as t-SNE or UMAP will be employed to visualize the structure of the EEG feature space and reveal whether trials cluster meaningfully by odor class or by individual preference profiles. These visualizations will support both interpretability and communication of the model’s performance and insights.

---

## Relevant Works
*Kroupi, E., Yazdani, A., Vesin, J.M., & Ebrahimi, T. (2014). EEG correlates of pleasant and unpleasant odor perception. ACM Transactions on Multimedia Computing, Communications, and Applications (TOMM), 11(1s), 1–17. [DOI: 10.1145/2637287]
*Koelstra, S. et al. (2011). DEAP: A Database for Emotion Analysis Using Physiological Signals. IEEE Transactions on Affective Computing, 3(1), 18–31.

---

## Future Exploration
If cross-subject generalization proves feasible, future work could work on larger and more diverse (including females, different ages, more odors) pools which would improve the model’s generalization. Cross-modal integration with physiological signals (GSR, heart rate) may also enhance prediction.
