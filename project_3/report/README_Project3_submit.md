# Project 3 - Reddit API

## Introduction


The objective of this project is to train our model to classify a subreddit post into one of two categories. The subreddits chosen are [World news] ['www.reddit.com/worldnews'] and [Funny] ['www.reddit.com/funny].

Given the discrete nature of the target classes, a classification model is needed. The different models used are evaluated based on the (default) accuracy score.

The best model resulted in a 94% accuracy, based on the _countVectorizer_ and Multinomial Naive Bayes_ models.

Steps toward reaching that best model will be described. The best model will be the focus of analysis in this technical report. However, subsequent attempts to improve the model will be described, when relevant.

### Scope of the project:

**The outline below covers the scope of the steps taken:**
  - Data collection
  - Data cleaning and EDA
  - Model setting
  - Model evaluation
  - Problem address and conclusion

### Data collection

About 3400 unique posts were collected from reddit's API.
The data extraction was limited to the last 1000 posts at any point in time. the data was extracted over 3 days. 61.5% of the data consisted of 'funny' titles and 38.5% were 'worldnews' titles.


### Exploratory Data analysis

the categories that were retained at the data extraction stage were mostly empty. others, on a second thought, were dismissed for lack of relevance for the problem at hand, which is the successful  classification of subreddits, one way or another. For example, the author's name or the subreddit id would help locate the subreddit but were deemed irrelevant in this particular problem.
In fact, only the title subreddit was retained as the predicting feature.

### Data cleaning

**dropping duplicates**

Given that the data extraction is limited to 1000 posts and that for every inquiry the latest 1000 posts are extracted, when there were no new 1000 posts within the 24 hours, duplicate posts are extracted. At a later stage of the process those duplicates were not dropped, in attempt to boost the score by bootstrapping. the result was a stuggering 99.15% score on the test data! But then, I realized that the model might have been trained on data that also appeared in the test data.

**resetting the index **

given that for each extraction the index resets to 0 and that for each subreddit the index starts at 0, several indeces shared the same index, which needed cleaning.

**filtering text for certain patterns, using the regex module** However, this did not improve the model's score.

### Setting the model:

The problem has been defined as a classification problem. Accordingly, several models have been considered. As for the 'text extraction' technique, the **countVectorizer** and the **TfidfVectorizer** were put to compete. As for the classification model, the **Multitnomial Naive Bayes** and the **logistic regression** were put to compete.

#### Feature creation:

As a first step, only the title of the subreddit was used as a predictor. The name of the subreddit, was  set as the target to be predicted. When the model evaluated strongly, it was decided that it was not worth increasing the number of predictors.

The data was, then, split into a training set and test set for model validation.

#### Setting the pipeline and the Gridsearch:

The pipeline was a convenient way to commingle the use of several modules in addition to the Gridsearch tool to iterate through the parameters of each one of these modules, thereby optimizing not only each module on a standalone basis but take into consideration their interaction.

### Model evaluation and iteration

The first model that was run was the Logistic Regression, which resulted in a 89% accuracy score on the test data. Starting at a baseline performance of 61.5%, the model's score could be considered strong. However, the training set scored over 98%, which indicated a high variance and an overfit to the training data.
The Multinomial Naive Bayes model was used to attempt to reduce the variance, which it did, bringing the test score to 94% while the training score also went up to 99%, partially offsetting the reduction in the overfit.
The TF-IDF was used in lieu of the countVectorizer but did not improve the result.
**Here is the confusion matrix resulting from the best model:**
![Confusion Matrix]('./images/ConfusionMatrix.png')

### Testing the model:
The model tested well with live data except with the expression "school shooting" which was taken as a 'funny' subject when it is clearly not!
**Here is a snapshot of the live data test:**
![Examples Vs. Predictions]('./images/ExampleVsPrediction.png')

### Final recommendations and future steps

This report highlighted the steps undertaken in reaching the best model possible in this reddit classification exercise. The report also described the steps undertaken to strengthen the model, mainly through trying more than one classification model and trying more than one text/feature extraction technique.

**An extension of this work would be to:**
- increase the amount of data to reduce the variance/overfit to training data
- Have a closer look at the origin of the False predictions, in an attempt to visualize the origin of the errors.
- Try other models, including the KNN, SVM, or others.
- add another subreddit category to challenge the model


## Attachments:
please find attached to
- this executive summary:
- the latest Jupyter notebook with the model code
- other notebooks retracing the effort to improve the model
- the csv files
- Presentation slides
