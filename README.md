# LST-course-project

This project aims to find the best variant classification model by testing different NLP preprocessing techniques and classification algorithms. It used data from kaggle competition https://www.kaggle.com/c/msk-redefining-cancer-treatment/overview

## Description of files

- ```Variation_preprocessing.ipynb``` (by Tien) aims to convert variation information into numerical feature. This file requires inputs: ```training_variants``` and ```test_variants``` which can be downloaded from original kaggle competition. It need to be run twice, one for train sample and one for test sample, which will be done by manually commenting out unused file as following:

```
## INPUT FILE IS MANUALLY ADJUSTED
## This setup is for training sample

training_set = pd.read_csv('training_variants')
final_file = "training_variants_cleaned.csv"

# training_set = pd.read_csv('test_variants')
# final_file = "test_variants_cleaned.csv"
```
and
```
## INPUT FILE IS MANUALLY ADJUSTED
## This setup is for test sample

# training_set = pd.read_csv('training_variants')
# final_file = "training_variants_cleaned.csv"

training_set = pd.read_csv('test_variants')
final_file = "test_variants_cleaned.csv"
```

The two output files ```training_variants_cleaned.csv``` and ```test_variants_cleaned.csv``` include 1 column for substitution score, 4 columns for mutation groups. 

- ```Word embedding for clinical text and Classification.ipynb``` (by Tien) aims to find numerical representation of clinical text and perform logistic regression on it. This file requires inputs: ```training_variants``` and ```test_variants``` and ```training_text``` and ```test_text``` and ```stage1_solution_filtered.csv``` which can be downloaded from original kaggle competition, ```training_variants_cleaned.csv``` and ```test_variants_cleaned.csv``` which are produced by running ```Variation_preprocessing.ipynb```. 

This notebook is recommended to be run with GPU since Longformer will take days to be finished. Chosen values of alpha (regularization parameter) in this notebook result the best performance of classification in term of log-loss. Four heatmaps are provided at the end to visualize predictive performance between base model and extended model.

- ```Pre_preprocessing and variant exploration.ipynb``` (by Huy) can be utilized to clean the text on both document and sentence level, as well as provide a report displaying variations' distribution on a target document. The function ```clean``` aims to remove stopwords, captions, references, and sentences contaminated with lengthy or collection of smaller words. The input for ```clean``` require any string document and can be iteratively call to return a new dataframe/training set with clean results. Extensions to the processed data are a new column containing only information about the target variation and the fixing of UTF-8 encodings. These expansions can be run with the function ```expansion``` which requires a dataframe with attributes: 'Gene','Variation','Class, and 'Text' in order. An example of such dataframe is the variable ```combine_train``` but one can modify the expansion to run with any dataframe since the function ```expansion``` create and clean new features based on only variation names and clinical text.     

In addition, ```Pre_preprocessing and variant exploration.ipynb``` also provides two functions ```report_dup``` and ```dis_report```
