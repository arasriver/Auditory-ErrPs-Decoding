# Auditory Error Potential Decoding — Praktikum 2

## Description

Analysis of whether auditory error-related potentials (ErrP, MMN, FRN, N400) can be
decoded from EEG recorded during the AID (Auditory Intention Decoding) paradigm.
The main project is here:
https://ucrisportal.univie.ac.at/en/publications/auditory-tagging-improving-performance-of-auditory-brain-computer/

In this project I tried to keep the base project code and use them as much as possible and just modify or 
write new code regarding to my purpose for finding ErrPs, MMN, FRN, N400 components.

In the AID paradigm, participants watch the prime numbers at the beginning on the screen, then 
listen to three numbers in sequence and identify target word. 
But in our project we want to know whether the brain's response
to non-target ("option") words, error trials, and attention check trials, violation of expectation
show something different from normal trials or not 
and whether that information is decodable or not.

The analysis contains approaches:
- ERP analysis: Grand Average Event Related Potentials with cluster based
  permutation testing, effect sizes (Cohen's d), and topographies.
- Single trial decoding: EEGNet classification with leave one subject out
  cross validation and within subject permutation testing.

This work was as part of Praktikum 2 in the Neuroinformatics group,
University of Vienna, supervised by Michal Robert Žák (Prof. Grosse-Wentrup's group).

## Data

Preprocessing of EEG data produced onset-locked and offset-locked epochs
with metadata (trial type, word position, target position, tagger type).
Behavioural responses (button presses) were extracted from
the log files of experiment to identify commission and omission errors.

I saved and read the EEG and Epoch files in my personal google drive and used google colab and GPU of colab for 
Traninig with EEGNet. Then it is independent of our personal system, that could be old
or slow to process data.

## Requirements

- Python 3.10+
- MNE-Python
- TensorFlow / Keras
- scikit-learn
- NumPy, pandas, matplotlib, seaborn

The EEGNet implementation is the ARL version (Lawhern et al.), imported from the
`external` module.

## Usage

Each notebook is an independent scenario:

- `PrePostTarget_Scenario_P2.ipynb` — options heard before target vs options heard after target word.
- `Option2_PrePost_Target_P2.ipynb` — options in position 2, in different role: pre target vs. post target.
- `AttCheck_P2.ipynb` — Attention Check trials vs control options that are in normal trials.
- `PressButtonWrong_P2.ipynb` — When subjects press the button wrongly in correct trials, instead of attention check trials.

There are also two other files for building epochs, with and without ICA filtering.
Each notebook in cells: data construction, model/statistics, and plotting.
Subjects can be included or excluded by editing the `SUBJECTS` list at the top of the
first cell. File paths at the top of each notebook must be adjusted accroding to 
google drive.

## Methods

- Epoching, filtering, and ICA artifact removal with MNE Python.
- ERP statistics: cluster based permutation test (`permutation_cluster_1samp_test`),
  with Cohen's d and 95% confidence intervals.
- Decoding: EEGNet with leave one subject out cross validation.
- Decoding significance assessed via within subject label shuffling permutation test
  (10,000 permutations), following Žák et al. (SMC 2025).

## Summary of findings

ERP analyses didn't show reliable Error Related Components or violation of expectation in their expected time
windows. Single trial decoding distinguished before vs after target options above
chance even under a position controlled design.
Behavioural error trials were too few (17 across all participants) for single trial
analysis.

## Author

Aras Saeidian, University of Vienna.

## Acknowledgment

Supervised by Michal Robert Žák, Neuroinformatics group (Prof. Grosse-Wentrup),
University of Vienna.
