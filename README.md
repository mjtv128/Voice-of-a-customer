# Voice of the Policygenius Customer <img width=90 align="right" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/Duke_University_logo.svg/1024px-Duke_University_logo.svg.png">



## Project status
*complete*

## Description
The project utilises customer feedback reviews to identify key customer themes and trends over time. The motivation behind this project is to provide Policygenius with a reliable and scalable way to analyze customer feedback, saving time and resources. The aim of this project is to develop an automated text analysis pipeline that can identify key topics from customer surveys. 

This project leverages structured and unstructured information to gain an understanding of the customers’ reviews on Policygenius products and establish key themes that can be actioned to improve customer retention and overall satisfaction. Different unsupervised natural language models, including Latent Dirichlet Allocation (LDA), Latent Semantic Analysis (LSA), Non-negative Matrix-Factorization (NMF), and deep learning models - Bidirectional Encoder Representations from Transformers (BERT), were explored to achieve these goals.

Extensive model evaluations using coherence scores and intertropical distance maps were utilized to compare the different models and ultimately BERTopic model was chosen to identify the key themes from customer surveys. BERTopic was applied to the customer feedback data, which was divided into 4 segments based on varying customer sentiment levels: promoters, passives, detractors, and CSAT.

## Data
We were provided with four data sources by our client, namely, a customer demographics dataset, a CSAT survey dataset, an NPS survey dataset, and an Application ID customer mapping table. The customer demographics dataset contains over 62 million records with 12 demographic features, such as gender and BMI, while the mapping table provides keys (application ID, application user ID, and product type) for merging different datasets. The CSAT and NPS survey datasets contain 6,372 and 27,066 historical customer responses, respectively.

To maintain privacy and confidentiality while also ensuring transparency, we generated synthetic data that mimics the patterns and distributions of the original datasets mentioned above but does not include any personal or confidential information. Long Short-Term Memory (LSTM), a language model that can generate tabular data with mixed categorical, numeric, time-series, and text fields, were utilized to produce synthetic data sets consisting of 5000 records for both the NPS and CSAT datasets. The main variables we used in our project included timestamps, reviewer comments, survey response IDs, and application IDs. 

## Directory structure
```
├── README.md
├── code
│   ├── 001_data_pull_preprocess
│   │   ├── Csat_data.ipynb
│   │   └── NPS_data.ipynb
│   ├── 002_model_comparison
│   │   ├── BERT
│   │   │   └── BERTopic_NPS.ipynb
│   │   ├── LDA
│   │   │   ├── LDA_results.ipynb
│   │   │   └── LDA_with_TF_IDF.ipynb
│   │   ├── NNMF
│   │   │   └── 00_NNMF_v2.ipynb
│   │   ├── STM
│   │   │   ├── Policygenius.Rproj
│   │   │   └── STM.Rmd
│   │   └── comparison.ipynb
│   ├── 003_bert_training
│   │   ├── BERTopic_CSAT.ipynb
│   │   ├── BERTopic_NPS_Passives.ipynb
│   │   ├── BERTopic_NPS_Promoters.ipynb
│   │   └── Results_detractors.ipynb
│   └── 004_bert_scoring
│       └── BERTopic_scoring.ipynb
├── data
│   ├── intermediary_data
│   │   ├── NNMF_coherence_scores.csv
│   │   ├── Numoftopics_Bertopic.csv
│   │   ├── STM_coherence_score.csv
│   │   ├── lda_cohernece.csv
│   │   └── lda_tfi_coherence.csv
│   ├── synthetic_csatdata.csv
│   └── synthetic_npsdata.csv
├── model_checkpoints
│   ├── checkpoints.zip
├── requirements.txt
└── results
    ├── decks
    │   ├── PPT_Capstone Symposium 2023_v2.pptx
    │   └── PPT_client_presentation.pdf
    └── report
        └── finalreport_1.0.pdf
```
## Usage
This project is built with Python 3, and the visualizations are created using Jupyter Notebooks. The following steps can be followed to replicate the analysis:

* Clone repo with SSH key
```
git clone git@github.com:mjtv128/Voice-of-a-customer.git
```

* Install the necessary dependencies:
```
pip install -r requirements.txt
```

* After pulling survey reponses from Pg's database, some preliminary steps are carried out to reduce the raw data into a format, which is unique at the level of survey responses. Some synthetic datasets that mimic this format can be found in `/data/`.

* To run the different topic models that were tried out on the NPS dataset for comparison, head to `code/002_model_comparison/`. Currently, this project supports running LDA, STM, NNMF models, in addition to BERTopic.

* To run the BERTopic model (which was our model of choice), head to `code/003_bert_training/`. Here, each script fits BERTopic on the four individual segments. To load our pre-trained models, head to `model_checkpoints/` and unzip the file. This should give four model checkpoints corresponding to each segment.

* To score the BERTopic model to generate predictions on new data,  head to `code/004_bert_scoring/` and run the script on the dataset you would like to generate predictions for. Update the paths to your dataset in this script accordingly.

The draft report for this project can be found under `results/report`. 

Please note that the above instructions are for demonstration purposes only and may need to be modified for your specific use case. Additionally, the accuracy and performance of the model may vary depending on the dataset.

## Results
The chief objective of this project was to develop an automated text analysis pipeline that can efficiently identify key topics from customer feedback received by Policygenius in the surveys they send out. We tried different unsupervised natural language methods, including LDA, STM, NMF, and BERTopic. BERTopic models achieved the highest coherence score of over 0.7, while the rest of the models have coherence scores lower than 0.4.

Our fine-tuned BERTopic models then extracted 7, 4, 5, and 7 commonly mentioned topics within promoters, passives, detractors and the CSAT group respectively. Together with the comments corresponding to each topic, the general themes were summarized using human interpretation. Moreover, we explored the historical trends (yearly, quarterly, and monthly) over the past seven years by plotting the proportion of each theme relative to the rest. Policygenius can gain useful insights into how different segments of customers feel about their products and services, as well as track how they change over time. 

With models in hand, we created a production-ready pipeline, allowing Policygenius to score new reviews every month. The outputs from this pipeline can be visualized in the form of a Tableau dashboard we built, which was handed over to Policygenius.

Overall, we managed to automate the topic identification process from customer text reviews. The models, pipeline, and dashboard are expected to significantly reduce the effort required for the original manual extraction process and enhance the analysis accuracy at the same time. This project provides businesses with an effective and efficient way to analyze textual feedback and gain valuable insights into the needs and preferences of their customers.

## Authors and acknowledgment

We would also like to acknowledge the guidance, support, and expertise provided by the following individuals from Policygenius:

- Brenna Hayes, Director of Marketing Strategy
- Emily Nightingale, Senior Data Scientist
- Dustin Tucker, Senior Director of Data Science and Engineering

## Contributing
Contributions are welcome! Please open a pull request and we will respond at the earliest.


## References
1. D. Godes and D. Mayzlin, “Using online conversations to study word-of-mouth communication”, Marketing science, vol. 23, no. 4, pp. 545–560, 2004.
2. C. Dellarocas, “The digitization of word of mouth: Promise and challenges of online feedback mechanisms”, JSTOR, 2003.
3. S.-C. Chu and Y. Kim, “Determinants of consumer engagement in electronic word-of-mouth
(ewom) in social networking sites”, International Journal of Advertising, vol. 30, pp. 47–75, 01 2011.
4. S.-J. Doh and J.-S. Hwang, “How consumers evaluate ewom (electronic word-of-mouth) messages,” CyberPsychology & Behavior, vol. 12, pp. 193–197, 2023/04/03 2008.
5. T. Hennig-Thurau and G. Walsh, “Electronic word-of-mouth: Motives for and consequences of reading customer articulations on the internet”, International Journal of Electronic Commerce, vol. 8, pp. 51–74, 12 2003.
6. W. Duan, B. Gu, and A. Whinston, “The dynamics of online word-of-mouth and product sales: An empirical investigation of the movie industry”, Journal of Retailing, vol. 84, pp. 233–242, 05 2011.
7. K. Floyd, R. Freling, S. Alhoqail, H. Y. Cho, and T. Freling, “How online product reviews affect retail sales: A meta-analysis”, Journal of Retailing, vol. 90, no. 2, pp. 217–232, 2014.
8. K. P. Gu Bin, Park Jaehong, “Research note: The impact of external word-of-mouth sources on retailer sales of high-involvement products”, JSTOR, 2012.  
9. J. A. Chevalier and D. Mayzlin, “The effect of word of mouth on sales: Online book reviews”,Journal of Marketing Research, vol. 43, pp. 345–354, 2023/04/03 2006.  
10. R. Hallowell, “The relationships of customer satisfaction, customer loyalty, and profitability: an empirical study”, International journal of service industry management, 1996.  
11. A. Baquero, “Net promoter score (nps) and customer satisfaction: Relationship and efficient management”, Sustainability, vol. 14, no. 4, p. 2011, 2022.
12. C. Balan, “Net promoter score: Key metric of customer loyalty”, Quality-Access to Success, vol. 13, 2012.
13. B. Cheng, I. Ioannou, and G. Serafeim, “Corporate social responsibility and access to finance”, Strategic management journal, vol. 35, no. 1, p. 1–23, 2014.
14. P. Xie and E. P. Xing, “Integrating document clustering and topic modeling”, arXiv preprint, arXiv:1309.6874, 2013.
15. T. Hofmann, “Probablistic latent semantic indexing proceedings of the 22nd annual international acm sigir conference on research and development in information retrieval”, ACM Press: Berkeley, CA, USA;, 1999.
16. S. Deerwester, S. T. Dumais, G. W. Furnas, T. K. Landauer, and R. Harshman, “Indexing
by latent semantic analysis”, Journal of the American society for information science, vol. 41, no. 6, p. 391–407, 1990.
17. D. M. Blei, A. Y. Ng, and M. I. Jordan, “Latent dirichlet allocation”, Journal of machine Learning research, vol. 3, no. Jan, pp. 993–1022, 2003.23
18. D. Maier, A. Waldherr, P. Miltner, G. Wiedemann, A. Niekler, A. Keinert, B. Pfetsch, G. Heyer, U. Reber, T. H ̈aussler, H. Schmid-Petri, and S. Adam, “Applying lda topic modeling in communication research: Toward a valid and reliable methodology”,Communication Methods and Measures, vol. 12, pp. 93–118, 04 2018.
19. H. Chen, M. Gao, Y. Zhang, W. Liang, and X. Zou, “Attention-based multi-nmf deep neural network with multimodality data for breast cancer prognosis model,” BioMed Research International, vol. 2019, p. 9523719, May 2019.
20. M. Grootendorst, “Bertopic: Neural topic modeling with a class-based tf-idf procedure”, arXiv preprint, arXiv:2203.05794, 2022.
21. D. Angelov, “Top2vec: Distributed representations of topics,” arXiv preprint arXiv:2008.09470, 2020.
22. D. M. Blei and J. D. Lafferty, “A correlated topic model of science”, 2007.
23. J. Devlin, M.-W. Chang, K. Lee, and K. Toutanova, “Bert: Pre-training of deep bidirectional transformers for language understanding,” 2018.
24. N. Hu, T. Zhang, B. Gao, and I. Bose, “What do hotel customers complain about? text analysis using structural topic model,” Tourism Management, vol. 72, pp. 417–426, 2019.
25. J. Li, X. Zhou, and Z. Zhang, “Lee at semeval-2020 task 12: A bert model based on the maximum self-ensemble strategy for identifying offensive language”, in Proceedings of the Fourteenth Workshop on Semantic Evaluation, pp. 2067–2072, 2020.
26. Y. Liu, M. Ott, N. Goyal, J. Du, M. Joshi, D. Chen, O. Levy, M. Lewis, L. Zettlemoyer,
and V. Stoyanov, “Roberta: A robustly optimized bert pretraining approach”, arXiv preprint
arXiv:1907.11692, 2019.
27. Z. Lan, M. Chen, S. Goodman, K. Gimpel, P. Sharma, and R. Soricut, “Albert: A lite bert for self-supervised learning of language representations”, arXiv preprint arXiv:1909.11942, 2019
