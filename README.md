# Project: Population genomics project for *Salmonella* Monophasic ST34.

### Objectives
* To identify and rank the most discriminative genomic features (AMR genes, shell genes, and plasmid genes) associated with different sources or epidemiological clusters of Salmonella ST34 using Random Forest classification.
* To evaluate the distribution patterns and clustering of shell genes across isolates to uncover potential hidden population structures within epidemiological clusters.
* To assess the predictive value of top-ranked genes through proportion-based confusion matrix analysis, identifying features with the highest discriminatory power across different training/test splits.

### Workflow
![GitHub Workflow](https://github.com/user-attachments/assets/ad481f7b-3922-467e-9f69-a9be7d830609)

### Methods
**2.1 Cleaning the data**

Preprocessing pipeline for three epidemiological datasets. Each dataset's metadata was individually imported into Pandas, cleaned, and merged with biosample and genomic data (MLST, SISTR). Geographic data were standardized to country-level, focusing on the U.S. and U.K., and isolation sources were categorized (Human, Swine, Poultry, Bovine, Others). Genomes were filtered to retain only ST34 monophasic strains (serovar: 'I 1,4,[5],12:i:-') relevant to each dataset's specific criteria. Gene presence/absence data from Rtab files was filtered to retain unique genomes, exclude hypothetical and overly frequent shell genes, and merged back with the metadata. Additional cleaning was applied to plasmid and antimicrobial resistance (AMR) gene datasets (from ResFinder and ARG-ANNOT), filtering out genes with low identity or coverage and duplicates. All data were finally merged by genome ID to create clean, analysis-ready datasets for each set.

**2.2 Clustermap**

Clustermaps were generated using Random Forests on cleaned datasets (plasmid, AMR genes from ResFinder and ARG-ANNOT, and shell genes) to determine key features differentiating groups (source or cluster). Each dataset was split into features (genes) and labels (source or cluster), then into training and testing subsets using varying ratios (60–40%, 70–30%, 80–20%). After training, the top 10 most important features were retained, and the model was re-evaluated for accuracy. Features with importance > 0.01 across runs were kept. For visualization, feature presence was displayed as a seaborn clustermap using the Jaccard metric, grouped by source (set 1) or epidemiological cluster (sets 2 and 3).

**2.3 Random Forest Feature Importance**

Random Forest classifiers were used on cleaned datasets (plasmid, AMR, shell genes) to rank gene importance in classifying source (set 1) or epidemiological cluster (sets 2 and 3). Datasets were split into feature sets and target variables, and evaluated with multiple train-test splits. Models were retrained using the top 10 genes to assess post-selection accuracy. The final list of genes with importance > 0.01 was visualized using seaborn bar plots, color-coded by split ratio. This method highlighted the most influential genetic features in distinguishing epidemiological groups. 

**2.4 Heavy Metals**

The heavy metal gene analysis used similar preprocessing steps as section 2.1: metadata was cleaned, relevant genomes (monophasic ST34) selected by isolation source and country, and merged with gene presence data. Shell genes were filtered, and only genes linked to heavy metal resistance were retained. For sets 2 and 3, this process was repeated per epidemiological cluster and later combined. Gene presence/absence data was visualized using seaborn clustermap (Jaccard distance), anchored by source (set 1) or cluster (sets 2 and 3).

**2.5 Jaccard**

This section employed logistic PCA and multidimensional scaling (MDS) on cleaned metadata and shell gene datasets to assess gene pattern similarity using Jaccard distances. For set 1, data was split by Human vs. Swine, while for sets 2 and 3, all genomes were analyzed by cluster. K-means clustering was used, and the optimal number of clusters was identified via the elbow method (WSS, using kneed). Results were visualized in 2D (elbow plot using Matplotlib) and 3D (scatterplot using Plotly), with clusters color-coded.

**2.6 Confusion Matrix Proportion**

This analysis quantified how well top gene features could predict source or cluster by evaluating confusion matrix proportions for each gene. Starting with cleaned datasets, Random Forests were run to extract top features (importance > 0.01), with training/test split variations. Unique features were annotated by source or cluster, and proportions from confusion matrices were calculated for each gene. Results were visualized via seaborn bar plots showing each gene's predictive power. This method offered insight into individual gene contributions beyond aggregate model accuracy.

**2.7 Random Forest Combined Feature importance**

In this section, a combined analysis of feature (gene) importance was performed using the plasmid, AMR genes from ResFinder, and shell genes cleaned datasets. For datasets in sets 2 and 3, the data for each epidemiological cluster was merged before analysis. The data was divided into two categories: features (genes) and the target variable (source for set 1, and epidemiological cluster for sets 2 and 3). The datasets were split into training and testing sets to train and evaluate a Random Forest Classifier model for accuracy. Feature importances were then extracted and ranked.

The top 10 features were selected, and the model was retrained using only these features to assess the accuracy of the model post-feature selection. This process was conducted with a test-train split of 70-30% and only the top 20 features were retained. Finally, the importance of each feature was visualized in a horizontal bar plot using seaborn, color-coded by data source (shell genes, plasmids, or AMR genes from ResFinder). 

### Hypothesis Tested
This work has one central hypothesis: that population-based analysis of the accessory genome content of S. Monophasic will enhance genomic resolution in epidemiological research and reveal hidden zoonotic variants. Given the clonal nature of S. Monophasic and the anticipated nonrandom inheritance of accessory loci (often reflective of ecological adaptation), we expect to identify previously undetected cryptic variants these datasets.

### Outcomes
* Feature importance selection (AMR Genes, Shell Genes, Plasmids)
* Mean proportion distribution of most discriminating features
* Shell Gene based hidden clusters

<!-- ### Journal
Open Life Sciences-->

## How to Read
This repository is divided by sets, each corresponding to a specific scenario proposed in the paper. 
Each folder contains 7 Jupyter Notebooks (one for each figure and one with the full code) and one folder containing all the files used by the codes (these files can also be found here for [set 1](https://figshare.com/s/ee922a1d35c031908978), [set 2](https://figshare.com/s/208104531264a3db6366) and [set 3](https://figshare.com/s/91557c6cf134885d08ff)).
