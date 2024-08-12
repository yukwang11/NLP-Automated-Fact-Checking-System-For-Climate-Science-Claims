# NLP Automated Fact Checking System For Climate Science Claims
The impact of climate change on humanity is a significant concern. However, the increase in unverified statements regarding climate science has led to a distortion of public opinion, underscoring the importance of conducting fact-checks on claims related to climate science. Consider the following claim and related evidence:

Claim: The Earth’s climate sensitivity is so low that a doubling of atmospheric CO2 will result in a surface temperature change on the order of 1°C or less.

**Evidence:**
1. In his first paper on the matter, he estimated that global temperature would rise by around 5 to 6 °C (9.0 to 10.8 °F) if the quantity of CO 2 was doubled.
2. The 1990 IPCC First Assessment Report estimated that equilibrium climate sensitivity to a doubling of CO2 lay between 1.5 and 4.5 °C (2.7 and 8.1 °F), with a "best guess in the light of current knowledge" of 2.5 °C (4.5 °F).

It should not be difficult to see that the claim is not supported by the evidence passages, and assuming the source of the evidence is reliable, such a claim is misleading. The challenge of the project is to develop an automated fact-checking system where given a claim, the goal is to find related evidence passages from a knowledge source and classify whether the claim is supported by the evidence.

This system include: 
(1) search for the most related evidence passages from the knowledge source given the claim; and 
(2) classify the status of the claim given the evidence in the following 4 classes: {SUPPORTS, REFUTES, NOT_ENOUGH_INFO, DISPUTED}. 

Theres several files for the project:
- [train-claims,dev-claims].json: JSON files for the labelled training and development set;
- [test-claims-unlabelled].json: JSON file for the unlabelled test set;
- [evidence.json]: JSON file containing a large number of evidence passages (i.e. the “knowledge source”);
- [dev-claims-baseline].json: JSON file containing predictions of a baseline system on the development set;
- [eval.py]: Python script to evaluate system performance (see “Evaluation” below for more details).

For the labelled claim files (train-claims.json, dev-claims.json), each instance contains the claim ID, claim text, claim label (one of the four classes: {SUPPORTS, REFUTES, NOT_ENOUGH_INFO, DISPUTED}), and a list of evidence IDs. The unlabelled claim file (test-claims-unlabelled.json) has a similar structure, except that it only contains the claim ID and claim text. 

**NOTE:** The system **NOT** use any pretrained word embeddings (e.g. Word2Vec), pretrained language model weights or checkpoints (e.g. BERT checkpoints), or any closed-source models (OpenAI GPT-3). In other words, ONLY train your system from scratch, using the data provided in the project. NOT use any rule-based techniques.
	
This code achieves 0.5 accuracy without using pretrained techniques. 
