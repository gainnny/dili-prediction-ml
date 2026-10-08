# Drug-Induced Liver Injury (DILI)

This project explores molecular representations and machine-learning approaches for classifying DILI labels in the DILIst dataset. The five notebooks document dataset provenance, Morgan fingerprints, RDKit descriptors, feature/model comparisons, and exploratory neural and hybrid analyses. This notebook series uses ordinary stratified cross-validation. 

## Dataset and scope

The accepted modeling file is `DILIst_Final.csv`, with 1,198 rows: 463 class 0 and 735 class 1. RDKit parses 1,197 structures; DILIST_ID 397 is excluded from structure-based modeling, leaving 462 class 0 and 735 class 1 records.

The notebooks also refer to `DILIst_SMILES_Completed.csv` and saved result/audit reference files under `results/`. The source data are not included in this repository. Dataset reuse must follow the source dataset's terms; this project does not claim that the data are freely redistributable.

## Notebook sequence

Run the notebooks in this order, with the project root as the working directory:

1. `notebooks/final/01_dataset_construction.ipynb` — checks the accepted dataset and documents the available source-to-cohort evidence.
2. `notebooks/final/02_morgan_fingerprint_analysis.ipynb` — generates radius-2, 2,048-bit Morgan fingerprints and evaluates the listed classifier configurations with five-fold `StratifiedKFold` cross-validation. It also contains out-of-fold error analysis and exploratory PCA/t-SNE visualizations.
3. `notebooks/final/03_rdkit_descriptor_modeling.ipynb` — evaluates Random Forest and MLP models using 217 RDKit descriptors with five-fold stratified CV and pooled out-of-fold summaries.
4. `notebooks/final/04_feature_and_model_comparison.ipynb` — compares molecular feature representations and several tree-based classifiers using five-fold stratified CV.
5. `notebooks/final/05_exploratory_neural_and_hybrid_modeling.ipynb` — presents descriptor-based neural analyses, selected audit references, and exploratory model comparisons using a reused holdout where identified in the notebook.


## Evaluation limitations

- The modeling notebooks use shuffled five-fold `StratifiedKFold` rather than a structure-grouped split. The accepted data contain five duplicate-SMILES groups (10 rows); one group has conflicting labels. Because the folds are not grouped by canonical SMILES, identical structures may be split between training and validation folds.
- Therefore, the CV scores do not establish generalization to unseen molecular structures or chemical scaffolds. Possible duplicate-structure leakage may make some estimates optimistic; its effect on the reported scores was not isolated in this notebook series.
- Notebook 03 performs descriptor cleanup on the full valid cohort before cross-validation. Its fold-local imputation/scaling does not make that earlier cohort-wide cleanup fold-local.
- Notebook 05 labels its reused holdout analyses as exploratory. The same holdout was used in model comparisons and selection-related analyses, so it is not an untouched independent test set.
- Some historical neural/hybrid results are reference values rather than newly reproduced results. Notebook 05 documents that several neural/hybrid reruns were unavailable in its audited environment.
- This project is an educational computational analysis. It does not establish clinical validity, external validation, or real-world deployment performance.


## Results

Notebook-specific fold results, pooled out-of-fold summaries, and exploratory outputs are reported in the notebooks and saved tables under `results/`. Cross-validation, pooled OOF, historical reference, and reused-holdout values are different evaluation results and should not be combined or presented as independent test performance.
