# Automated Fact-Checking System for Climate Science Claims

## Overview

This project addresses the urgent need for robust systems to combat misinformation in climate science. The developed system classifies climate-related claims by retrieving and evaluating evidence from a large corpus. It employs advanced machine learning (ML) techniques to ensure the accuracy and reliability of public discourse.

**Claim**: The Earth’s climate sensitivity is so low that a doubling of atmospheric CO2 will result in a surface temperature change on the order of 1°C or less.

**Evidence:**
1. In his first paper on the matter, he estimated that global temperature would rise by around 5 to 6 °C (9.0 to 10.8 °F) if the quantity of CO 2 was doubled.
2. The 1990 IPCC First Assessment Report estimated that equilibrium climate sensitivity to a doubling of CO2 lay between 1.5 and 4.5 °C (2.7 and 8.1 °F), with a "best guess in the light of current knowledge" of 2.5 °C (4.5 °F).

It should not be difficult to see that the claim is not supported by the evidence passages, and assuming the source of the evidence is reliable, such a claim is misleading. The challenge of the project is to develop an automated fact-checking system where given a claim, the goal is to find related evidence passages from a knowledge source and classify whether the claim is supported by the evidence.

This system include: 
(1) search for the most related evidence passages from the knowledge source given the claim; 
(2) classify the status of the claim given the evidence in the following 4 classes: {SUPPORTS, REFUTES, NOT_ENOUGH_INFO, DISPUTED}. 


## Files
Theres several files for the project:
- `main.ipynb`: Contains the main code implementation for the project, including:
	- Data preprocessing pipelines.
	- Model architecture definitions for both evidence retrieval and claim classification.
	- Training, evaluation, and result visualization scripts.
- `train-claims,dev-claims.json`: JSON files for the labelled training and development set;
- `train-claims,dev-claims.json`: JSON files for the labelled training and development set;
- `test-claims-unlabelled.json`: JSON file for the unlabelled test set;
- `evidence.json`: JSON file containing a large number of evidence passages (i.e. the “knowledge source”);
- `dev-claims-baseline.json`: JSON file containing predictions of a baseline system on the development set;
- `eval.py`: Python script to evaluate system performance (see “Evaluation” below for more details).
- `requirements.txt`: The project uses Python and several essential packages. Install the dependencies in your environment.


For the labelled claim files (`train-claims.json`, `dev-claims.json`), each instance contains the claim ID, claim text, claim label (one of the four classes: {SUPPORTS, REFUTES, NOT_ENOUGH_INFO, DISPUTED}), and a list of evidence IDs. The unlabelled claim file (test-claims-unlabelled.json) has a similar structure, except that it only contains the claim ID and claim text. 

**NOTE:** The system **NOT** use any pretrained word embeddings (e.g. `Word2Vec`), pretrained language model weights or checkpoints (e.g. `BERT` checkpoints), or any closed-source models (OpenAI GPT-3). In other words, **ONLY** train your system from scratch, using the data provided in the project. **NOT** use any rule-based techniques.


## Features

1. **Evidence Retrieval**:  
   - Uses a Siamese network to compute cosine similarity between claim-evidence pairs.
   - Trained with contrastive loss and a cyclical learning rate scheduler.
   - Achieved a **dev F1-score of 0.665**.

2. **Claim Classification**:  
   - Employs a Transformer-Encoder model.
   - Utilizes Sparse Categorical Focal Loss to handle class imbalances.
   - Achieved a **dev accuracy of 0.487**.

3. **Performance**:  
   - The system’s harmonic mean score of **0.546** significantly surpasses the baseline of **0.344**.

## Workflow

1. **Preprocessing**:  
   - Text normalization, tokenization, and stemming.  
   - Retention of stop words to preserve context for distinguishing class labels.

2. **Model Design**:  
   - Siamese Network for evidence retrieval with Bi-LSTM layers for contextual encoding.  
   - Transformer-Encoder for claim classification to manage long-distance dependencies.

3. **Training Techniques**:  
   - Contrastive Loss for learning discriminative embeddings.  
   - Cyclical learning rates for efficient training and regularization.

4. **Evaluation**:  
   - Top-k evidence retrieval for balancing precision and recall.  
   - Early stopping to prevent overfitting during model training.


## Results

- Evidence Retrieval: Precision ~0.53, Recall ~0.88.  
- Claim Classification: Bias towards certain classes but notable improvements over the baseline. Dev Accuracy: 0.487 (approximately 49% of true labels were correctly predicted). 

