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
### 1. **EEG Preprocessing**
Load .mat files for each subjects. Extract and preprocess EEG segments (baseline vs. event). Apply bandpass filtering and artifact removal (ICA for eye blinks). Compute power spectral density (PSD) for theta, alpha, beta, gamma bands. Baseline correction. Normalize features across trials.

### 2. **Model Training**
Support Vector Machines (SVM) for within-subject classification (replication).
Logistic regression and Random Forest for cross-subject classification.
K-means or hierarchical clustering on EEG features to group similar preference profiles.
t-tests and ANOVA for analyzing odor rating agreement across subjects.

### 3. **Visualization and Evaluation**
Classification accuracy (ROC/AUC, confusion matrix).
Heatmaps of average EEG power changes per odor and condition.
EEG electrode maps showing discriminative regions (Fisher Discriminant Ratio).
Preference similarity matrices (ratings vs. EEG patterns).

---

## Relevant Works
*Kroupi, E., Yazdani, A., Vesin, J.M., & Ebrahimi, T. (2014). EEG correlates of pleasant and unpleasant odor perception. ACM Transactions on Multimedia Computing, Communications, and Applications (TOMM), 11(1s), 1–17. [DOI: 10.1145/2637287]
*Koelstra, S. et al. (2011). DEAP: A Database for Emotion Analysis Using Physiological Signals. IEEE Transactions on Affective Computing, 3(1), 18–31.

---

## Future Exploration
If cross-subject generalization proves feasible, future work could work on larger and more diverse (including females, different ages, more odors) pools which would improve the model’s generalization. Cross-modal integration with physiological signals (GSR, heart rate) may also enhance prediction.
