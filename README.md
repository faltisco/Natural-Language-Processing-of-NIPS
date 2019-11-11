## Natural_Language_Processing_NeurIPS_Papers
The purpose this project is to do a topic based analysis of the content in papers submitted at an annual conference for  computational neuroscience (ie. neural networks,AI and related topics) known as  NeurIPS.  (see: https://en.wikipedia.org/wiki/Conference_on_Neural_Information_Processing_Systems). 

Over 7200 papers were obtained from Kaggle as CSV files. The papers were presented at NeurIPS between 1987 and 2017. The papers were explored via NLP techniques and Latent Dirichlet Allocation (LDA) models. LDA modeling is a form of probabalistic, unsupervised deep learning that reveals topics. The findings are presented in graphical and topic descriptions which show the importance certain terms have within these LDA topics. It's important to note that these topics are often not easily understood by humans (NLP research hopes to improve this issue). Rather, the findings allow for a better view into the data of interest: human language and it's meaning and how machines are beginning to tackle the notion of meaning in natural language.

## NeurIPS Data and EDA

The papers were read into a Pandas dataframe and early EDA completed. The data was quite clean, and no imputation necessary. Here is a plot showing the number of papers per yearly conference. 
https://github.com/faltisco/Natural_Language_Processing_NeurIPS_Papers/blob/master/images/papers_year_bar.png

In NLP, word clouds seem quite useful because analysts can  graphically see what words are most frequent. The topics for papers presented seem well represented in the titles of the papers. As part of EDA, a word cloud of the frequency of terms in the titles is here:
https://github.com/faltisco/Natural_Language_Processing_NeurIPS_Papers/blob/master/images/word_cloud_titles.png

A new column was created from the papers' text called "text_processed" which stores the data after stop words were removed.  The following bar graph showing the most frequent terms in the overall corpus of papers taken together.
https://github.com/faltisco/Natural_Language_Processing_NeurIPS_Papers/blob/master/images/Most_Com_W_in_Text.png

## Analyzing Time Periods

NLP modeling results require significant post-modeling analysis. Presentation of findings can be cumbersome because the findings are non-labeled topics found in quantitative ways. So, rather than analyzing each year's conference separately, a decision was made to analyze and present topics per decade of papers. The findings from each of the 1980s, the 1990s, the 2000s and the 2010's are presented using LDA modeling. The LDA topics can be viewed by coefficients that represent how important that term is in the formation of that un-labeled topic. For example, the following output from LDA:

[(0,
  '0.105*"kernel" + 0.086*"estimator" + 0.067*"estimate" + 0.064*"estimation" '
  '+ 0.049*"regression" + 0.038*"density" + 0.029*"gaussian" + '
  '0.029*"function" + 0.027*"covariance" + 0.018*"sample"'),
  
 (1,
  '0.194*"sequence" + 0.144*"prediction" + 0.110*"game" + 0.072*"predict" + '
  '0.051*"expert" + 0.051*"strategy" + 0.035*"future" + 0.034*"action" + '
  '0.027*"play" + 0.025*"frame"')]
  
  can be understood as showing topics 0 and 1. Within topic 0, the term "kernel" has a coefficient 0.105 and the next term "estimator" has a coefficient 0.086. These are the two most important terms in topic 0. Note that the values are best read as relative strengths. 
  
# Measuring The Coherence Values in LDA Models

The common understanding of the modeling term "coherent" applies. It means the terms within the LDA topic support that topic.  So, the coherency measure in LDA modeling shows how well terms within topics support their shared topic. For a good discussion of coherency, see the following article written by Shashank Kapadia
Shashank Kapadia:
https://towardsdatascience.com/evaluate-topic-model-in-python-latent-dirichlet-allocation-lda-7d57484bb5d0

The models in this analysis used herein utilized the "C_v" measure. Mathematically, it is a measure that uses "normalized pointwise mutual information (NPMI)" and the cosine similarity. It compares the distances between topics. This information was plotted to decide the hyperparameter of "tuning" the 4 LDA models (recall each represents a decade of papers). Here is one plot revealing the coherence scores for models of differing number of topics:
https://github.com/faltisco/Natural_Language_Processing_NeurIPS_Papers/blob/master/images/opt_coh_top_90s.png

Choosing the number of topics the LDA model tries to find is an important parameter to decide upon in LDA modeling. As the plot shows, the coherence value begins to stop increasing around 8 topics, and then certainly levels off at 14. For the 1990s papers, 14 was chosen as the number of topics for the LDA model to find. If computational resources become an issue, it seems also feasible to choose 8. 
  
## LDAvis

LDAvis is an interactive visualization tool with an interactive graphical representation of LDA models, described here:  (https://www.aclweb.org/anthology/W14-3110.pdf). After choosing a coherence value of 14 for papers in 1980s, 1990s and 2000s, and a coherence value of 20 for 2010s, the model results were visualized using LDAvis. The output was placed in the interactive HTML files, available here at a later date.

The LDA models can also be viewed by the frequency of terms within the topics. Four frequency wordclouds are shown per decade in the following images:

https://github.com/faltisco/Natural_Language_Processing_NeurIPS_Papers/blob/master/images/Cloud_1980s.png

https://github.com/faltisco/Natural_Language_Processing_NeurIPS_Papers/blob/master/images/Cloud_1990s.png

https://github.com/faltisco/Natural_Language_Processing_NeurIPS_Papers/blob/master/images/Cloud_2000s.png

https://github.com/faltisco/Natural_Language_Processing_NeurIPS_Papers/blob/master/images/Cloud_2000s.png

## Conclusions

Topic coherence measures were calculated for each of the four period models. The "C_v" coherence score for each LDA model follows:
1980s: 0.4589252522391932
1990s: 0.4938471029084987
2000s: 0.4964968134408346
2010s: 0.4964169876394429

