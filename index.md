## About Me

Hi, my name is Will, and I'm a Senior at Lehigh University. I expect to graduate this May with a degree in Finance, and I also have minors in Real Estate and Business Information Systems. After graduation, I will be working in Real Estate Development at Matrix Development Group in New Jersey. While at Lehigh, I spent several semesters learning how to code in Java, R, SQL, and Python. Below, I would like to showcase some of my work!

<img src="images/dummy_thumbnail.jpg?raw=true"/>

---

## My Python Portfolio

<!-- You can link to other websites, PDFs in this repo, and other pages in this repo -->

_**[Measuring Sentiment in S&P 500 Company 10Ks](report/report.md)**_

This report is a cross-sectional event study that attempts to answer the question of whether positive or negative sentiment in a 10-K is associated with better or worse stock returns. Specifically, I attempted to determine the tone of each 10-K filing by scanning the documents for words with positive or negative sentiment that I defined using the Machine Learning positive and negative sentiment datasets and the Loughran McDonald, or LM, Master Dictionary which can be found in the inputs file. In addition to this question, I also scanned through each 10-K to find out how often words related to my three research topics - Countries facing conflict, the COVID pandemic, and cryptocurrencies - appeared next to positive and negative sentiment words, and how this correlated to the firm's stock returns at the time.

From my analysis, I found that there is little or no relationship between the overall document sentiment as well as my contextual sentiment variables and the 2- and 10-day returns around the firm's filing date. As seen in the report, there is a fairly even distribution among sentiment scores when plotted against 2- and 10-day returns. The primary thing that stood out to me from my contextual analysis was that when countries in conflict were talked about with positive sentiment, it had a significantly higher correlation to the returns around the filing date than when they were discussed with negative sentiment. Please open and read my report linked above to learn more about my findings and analysis process
 
---

_**[Using Machine Learning Regression](report/best_model.md)**_

The goal of this report was to predict housing prices on a "holdout" sample using a machine learning approach. To answer this question, I preprocessed the dataset using pipelines, including the assignment of missing values, standardization of numerical variables, and one-hot encoding of categorical variables. Additionally, I used a Gradient Boosting Regressor model on the preprocessed data using Grid Search to optimize hyperparameters. I chose the Gradient Boosting Regressor model for this project after considering other regression models, such as Linear Regression, Random Forest Regressor, and Support Vector Regressor. After some research, I found that this model supposedly has superior performance in terms of predictive accuracy and speed compared to other similar models. Also, this model is well-suited for predicting non-linear relationships and interactions among numerous features, which is required when trying to accurately predict housing prices. I used this model to successfully capture the complex patterns in the data and produce accurate predictions on the holdout dataset. Furthermore, I evaluated the model using cross-validation and tried to maximize my R-squared scores. Then, I used this best model to predict my holdout dataset housing prices and saved the results as a CSV file that can be viewed below. Please also click the title above to view how I used machine learning to make my prediction.

<a href="https://williamroth82.github.io/report/MY_PREDICTIONS.csv">Click Here to See My Prediction</a> 

---

## Career Objectives

My main goal in life and my career is to do the best I can in whatever I set my mind to and to make sure to have fun along the way.

I am still unsure about what I want to do for my career, but currently I want to work in real estate developmet and learn how to invest in, add value to, and then sell properties. My ultimate goal would be to start my own firm and be able to work on my own investment projects later in life.

---

## Hobbies

My main hobbies include horseback riding, lifting weights, playing video games, listening to music, and spendig time with friends and famimly!

---

## Thanks for stopping by!
<p style="font-size:11px">Page template forked from <a href="https://github.com/evanca/quick-portfolio">evanca</a></p>
<!-- Remove above link if you don't want to attibute -->
