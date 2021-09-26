# INLs Meet IR V 2.0

## 																														Group Political-Bias

## 															

---

Our goal is to train a classifier that can recognize whether a sentence is politically related or not through machine learning. To do this, we need to collect data, preprocess the data, extract features, select models, train models, adjust parameters, model evaluation, and save. Model.
The following documents will record the entire process, and instructions for usage.

#### Dataset

> Overview of dataset:

| Sentence                                                     | Label         |
| :----------------------------------------------------------- | ------------- |
| It is also long overdue recognition of the work of the Capitol Police, the sacrifices that they and their families have made, and the changes they need. | Political     |
| an army officer who spotted the assailant hit him with his vehicle but the palestinian escaped and troops launched a search the military said | Political     |
| an anonymous insider tells radar that kardashian is convinced her concept will succeed because she thinks shes in the best shape of her life after having two children | Non-Political |
| More than a dozen states have introduced measures this year to allow residents to carry guns in public without a license, according to Brady, a gun control advocacy group. | Political     |
| paramount scooped up the rights to the film back in august with dicaprio slated to star in and coproduce the film which will require him to grow his revenant beard to unprecedented lengths | Non-Political |
|                                                              |               |

> Data Overview

<img src="https://github.com/zzuisa/inls-ir/blob/master/img/1.png" alt="image-20210923220928545" style="zoom:30%;" />

> Train-Set

<img src="https://github.com/zzuisa/inls-ir/blob/master/img/2.png" alt="image-20210923220950206" style="zoom:30%;" />

> Test-Set

<img src="https://github.com/zzuisa/inls-ir/blob/master/img/3.png" alt="image-20210923221009862" style="zoom:30%;" />

#### Data Collection:

- **origin dataset** (from moodle) [https://moodle.uni-due.de/mod/resource/view.php?id=1461332&redirect=1]

- **edition** [https://edition.cnn.com]

- **google news**: [https://news.google.com]

**About 3000 columns of data that have been manually modified**

<img src="https://github.com/zzuisa/inls-ir/blob/master/img/4.png" alt="image-20210926170752983" style="zoom:50%;" />







#### Model

> **support vector machine** (SVM)

In machine learning, support-vector machines (SVMs, also support-vector networks[1]) are supervised learning models with associated learning algorithms that analyze data for classification and regression analysis. . SVM maps training examples to points in space so as to maximise the width of the gap between the two categories. New examples are then mapped into that same space and predicted to belong to a category based on which side of the gap they fall.

<img src="https://gitee.com/internet_plus/inls-meet-ir/blob/master/img/5.png" alt="img" style="zoom:18%;" />

> Logistic Regression

Logistic regression is a statistical model that in its basic form uses a logistic function to model a binary dependent variable, although many more complex extensions exist. In regression analysis, logistic regression (or logit regression) is estimating the parameters of a logistic model (a form of binary regression). Mathematically, a binary logistic model has a dependent variable with two possible values, such as pass/fail which is represented by an indicator variable, where the two values are labeled "0" and "1". 





> Naive-Bayes

In statistics, naive Bayes classifiers are a family of simple "probabilistic classifiers" based on applying Bayes' theorem with strong (naïve) independence assumptions between the features (see Bayes classifier). They are among the simplest Bayesian network models, but coupled with kernel density estimation, they can achieve higher accuracy levels.

**Gaussian Naive Bayes:**

![{\displaystyle p(x=v\mid C_{k})={\frac {1}{\sqrt {2\pi \sigma _{k}^{2}}}}\,e^{-{\frac {(v-\mu _{k})^{2}}{2\sigma _{k}^{2}}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/685339e22f57b18d804f2e0a9c507421da59e2ab)

**Buernoulli naive Bayes:** 

![{\displaystyle p(\mathbf {x} \mid C_{k})=\prod _{i=1}^{n}p_{ki}^{x_{i}}(1-p_{ki})^{(1-x_{i})}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b23b8affe1fa31b1ce499d5d2944d9763ff2e6e)

> TF-IDF

In information retrieval, tf–idf, TF*IDF, or TFIDF, short for term frequency–inverse document frequency, is a numerical statistic that is intended to reflect how important a word is to a document in a collection or corpus.[1] It is often used as a weighting factor in searches of information retrieval, text mining, and user modeling. The tf–idf value increases proportionally to the number of times a word appears in the document and is offset by the number of documents in the corpus that contain the word, which helps to adjust for the fact that some words appear more frequently in general.

**Term frequency**, tf(*t*,*d*), is the frequency of term *t*:

![{\displaystyle \mathrm {tf} (t,d)={\frac {f_{t,d}}{\sum _{t'\in d}{f_{t',d}}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dd4f8a91dd0d28a11c00c94a13a315a5b49a8070)

 **Inverse document frequency** is a measure of how much information the word provides:

![ \mathrm{idf}(t, D) =  \log \frac{N}{|\{d \in D: t \in d\}|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac67bc0f76b5b8e31e842d6b7d28f8949dab7937)

Then tf–idf is calculated as:

![{\displaystyle \mathrm {tfidf} (t,d,D)=\mathrm {tf} (t,d)\cdot \mathrm {idf} (t,D)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/10109d0e60cc9d50a1ea2f189bac0ac29a030a00)

> BERT

Bidirectional Encoder Representations from Transformers (BERT) is a transformer-based machine learning technique for natural language processing (NLP) pre-training developed by Google.

![image](https://habrastorage.org/getpro/habr/post_images/2bd/0ba/1c4/2bd0ba1c4fb80fe4d771f555168c9ff0.png)



#### Result

---

| data:2880           | precision | F1-score | Recall |
| ------------------- | --------- | -------- | ------ |
| SVM                 | 0.83      | 0.84     | 0.85   |
| Logistic regression | 0.83      | 0.83     | 0.84   |
| GaussianNB          | 0.72      | 0.75     | 0.78   |
| BernoulliNB         | 0.81      | 0.80     | 0.79   |
| BERT                | 0.838     | 0.838    | 0.839  |



#### Theresholding

> Thresholding with 0.6/0.7/0.8

| data: 2880          | Threshold | dropped | precision | F1-score | Recall |
| ------------------- | --------- | ------- | --------- | -------- | ------ |
| SVM                 | 0.60      | 271     | 0.86      | 0.87     | 0.87   |
| Logistic regression | 0.60      | 237     | 0.85      | 0.86     | 0.87   |
| GaussianNB          | 0.60      | 15      | 0.73      | 0.75     | 0.78   |
| BernoulliNB         | 0.60      | 34      | 0.81      | 0.80     | 0.80   |
| BERT                | 0.60      | 36      | 0.85      | 0.85     | 0.85   |



| data: 2880          | Threshold | dropped | precision | F1-score | Recall |
| :------------------ | --------- | ------- | --------- | -------- | ------ |
| SVM                 | 0.70      | 618     | 0.89      | 0.89     | 0.90   |
| Logistic regression | 0.70      | 479     | 0.88      | 0.89     | 0.89   |
| GaussianNB          | 0.70      | 54      | 0.73      | 0.75     | 0.78   |
| BernoulliNB         | 0.70      | 74      | 0.81      | 0.81     | 0.80   |
| BERT                | 0.70      | 84      | 0.86      | 0.86     | 0.86   |



| data: 2880          | Threshold | dropped | precision | F1-score | Recall   |
| ------------------- | --------- | ------- | --------- | -------- | -------- |
| SVM                 | 0.80      | 1220    | **0.92**  | **0.92** | **0.91** |
| Logistic regression | 0.80      | 774     | 0.89      | 0.90     | 0.91     |
| GaussianNB          | 0.80      | 73      | 0.73      | 0.76     | 0.78     |
| BernoulliNB         | 0.80      | 117     | 0.82      | 0.81     | 0.80     |
| BERT                | 0.80      | 122     | 0.86      | 0.86     | 0.86     |



#### Install requirement:

- download  pre-trained models and dataset from kaggle: https://www.kaggle.com/zzuisa/praxisprojekt-inls-meet-ir-v-20-political-bias , and move them into data folder and models folder.

```bash
git clone https://github.com/zzuisa/inls-ir
cd ./inls-ir
pip install -r requirement.txt
# (python3.8.5)  
jupyter notebook
```

> Notebooks list:

| Version | Description                                    |
| ------- | ---------------------------------------------- |
| V1      | [TF-IDF] initial, try multi models             |
| V2      | [TF-IDF] correct dataset and adjust parameters |
| V3      | [TF-IDF] new dataset, more data                |
| V4      | [BERT] pure bert                               |
| V5      | [BERT] bert with traditional models            |
| V6      | [BERT] rebuild dataset and ROC                 |
| V7      | [BERT] work with threshold                     |
| V8      | [BERT] merged none-political and left,right    |
| V9      | [BERT] Chi square                              |



