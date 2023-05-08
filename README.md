# Tagging-StackOverflow-Questions-NLP

#	Problem Statement

* The problem says that we will be provided a bunch of questions. A question in Stack Overflow contains three segments Title, Description and Tags. By using the text in the title and description we should suggest the tags related to the subject of the question automatically. These tags are extremely important for the proper working of Stack Overflow. The project is based on a multi-label classification problem in NLP.

# Business Objectives and Constraints

* Predict as many tags as possible with high precision and recall.
So for this problem we should get high precision and high recall rates. For example, let’s assume that we have a title, description with 4 tags. If we want to predict any of the tags we should have a high precision value i.e, we have to be really sure that the predicted tag belongs to the given question. Also, we want to have a high Recal rate, which means If the tag actually supposed to be present, we want it to be present most number of times.

* Incorrect tags could impact customer experience on Stack Overflow
So from the above mentioned cases, If we predict an incorrect tag then Precision will decrease and If we missed out an important tag then Recall will decrease. So both are impacting customer experience very badly. To understand it in a better way, lets say If we predict ‘C#’ tag to a question which is related to C language, People who get the message or notification from Stack Overflow may not be an expert in C language or If the question is actually related to ‘C#’ and If we missed out stating the tag then we could send the question to a wrong person, this will create a mess and impacts the business of Stack Overflow.

* No Strict Latency Constraints
We don’t have a strict latency constraints. For example, let’s say somebody posts a question with title and description. We don’t have to provide all the tags or predict all the tags in milliseconds. We can have a couple of seconds to provide/predict right tags. Even 5 minutes should be fine. The most important thing is to increase the Rates of Precision and Recall.

# Datasets

Source: https://www.kaggle.com/datasets/stackoverflow/stacksample

Data Overview:
All of the data is in 2 files, Questions and Tags.
i. Questions.csv contains 7 columns: Id, OwnerUserID,    CreationDate, ClosedDate, Score, Title, Body,.
ii. Tags.csv contains 2 columns: Id, Tag 
iii. Size of Questions.csv: 1.92GB
iv. Size of Test.csv: 65.48MB

The columns in the table are:
Id : Unique identifier for each question
Title: The question’s title
Body: The body of the question
Tags: The tags associated with the question in a space separated format 

*	We will be using F1 score as a Performance metric for this problem. F1 score is the harmonic mean of precision and recall values.
*	Precision It is defined as ratio of true positives by (true positives + false positives)  
*	Recall It is defined as ratio of true positives by (true positives + false negatives)  
*	F1 Score = 2* Precision * Recall / (Precision + Recall)

# METHODOLOGY 

*	We choose the 10% StackOverflow questions dataset and use the Python Pandas library to import the dataset from the CSV file. Then we create two files, i.e., the questions.csv file and the Tags.csv file, in which we get the title body and tags related to the question
*	The first step of pre-processing involves consolidating the questions and tags into single data from the input dataset and mapping the labels according to the question id given in the dataset.
*	The next step involved the grouping of tags and removal of repeated tags. • Then we filtered the data in the questions data frame, and we dropped the columns such as ’ownerUserId’, ’CreationDate’, ’ClosedDate’.
*	Then we further disregarded the rows having scores less than 5. The score is the sum of up- votes and negative downvotes for a question.
*	After filtering based on id and score, we dropped these columns because they are not needed for model training.
•	Then we processed the tags and filtered unique tags; we ran frequency distribution using NLTK and found that more than 14000+ tags occurred more than 220000+ times. So, using this data, we extracted the top 100 tags in the dataset, which came out to be primarily related to the tech stack.
*	The next task was to filter the content, body, and title column data. We need to remove HTML tags and unnecessary elements from the text,and we used the bs4 library for this purpose.
*	Then we do the essential part of the project, which is pro- cessing the ’body’ column. Here, we first clean the data, i.e., remove the redundant spaces between the words, and then we clean the punctuation in which we removed the special characters, if any, present in the data. 
* Then we perform lemmatization on the data. Lemmatization refers to reduce the word to simplest form , such that its vo-cabulary and morphological analysis
*	Then we applied StopWords removal using Natural Language Toolkit, where the stopwords in NLTK refers to word in documents which occur frequently. Also stopwords are the word which do not define the context to the document so it is essential to remove them.
*	Then we used Mulilabel binarizer to convert the tags into binary data. The step is also called Bucketization.
*	Then we used the TF-IDF vectorizer to obtain scores of different words in the documents, and then we applied the vectorization to the dataset.
*	After processing the dataset, we train the model on 80% of the dataset and then test it on the remaining 20%. Then, we compare the results given by different models based on hamming loss and Precision.

# Performance of the model

*	After training and testing the model on Six different algorithms separately, we compared them based on hamming loss and Precision. The result is shown in the following figures:

*	The best model is the SGDClassifier model because it has the lowest hamming loss (0.9572) and highest Precision (83.53%). Based on hamming loss alone, the LinearSVC and SGDClassifier model gives the best result with the lowest score of (0.95).

# REFERENCES

•	https://www.ijert.org/tagging-stack-overflow-questions-using-supervised-machine-learning-techniques
•	https://medium.datadriveninvestor.com/predicting-tags-for-the-questions-in-stack-overflow-29438367261e
•	https://github.com/kushagra2103/Auto-Tagging-System
