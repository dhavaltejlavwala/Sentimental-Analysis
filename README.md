# Sentimental-Analysis

This program to perform sentiment classification for movie reviews. I have used a large movie review dataset containing a set of 25,000 movie reviews for training, and 25,000 for testing. You can visit the following website for more information about the dataset and the downloading link to the zip file. 

http://ai.stanford.edu/~amaas/data/sentiment/ 

Download the dataset and unzip it to the local directory. Enter the aclImdb/ directory created by the zip file, you will find five items 

#train/ - feature files and raw text files for the training set 
test/ - feature files and raw text files for the testing set 
imdb.vocab - expected rating for each token 
imdbEr.txt - text tokens for each feature index 
README - the readme file for more information on the dataset 

train/labeledBow.feat feature vector file for the training set 
test/labeledBow.feat feature vector file for the testing set 

Each feature vector file contains 25,000 lines, each line represents label value and feature vector of word occurrences for the corresponding movie review in the training/testing set. 

For e.g., the following is the first line of train/labeledBow.feat 

9 0:9 1:1 2:4 … 47304:1 

This means that the first review gets a rating of 9, 0:9 for 9 occurrences of the word "the" (the first token in imdb.vocab), 1:1 for 1 occurrence of the word "and", 2:4 for 4 occurrences of the word "a", where "the", "and", "a" are the first three tokens in imdb.vocab file, and the last token 47304:1 for one occurrence of the word "pettiness", the 47305th token in imdb.vocab. 

The above input vector basically calculates the number of occurrences for each word/token appearing in the raw text. The features are highly sparse, i.e. the majority of the entries are zero with only a few non-zero values. 

This program is able to read data from the training/testing files and parse them into the label vector and feature vectors for all 25,000 input examples. The input files (*.feat) are in a format called libsvm / svmlight and can be read into a matrix using the sklearn.datasets.load_svmlight_files function (see http://scikitlearn.org/stable/modules/generated/sklearn.datasets.load_svmlight_files.html). To then use the data for training classification model, I need to perform feature normalisation to the feature vectors. A recommended normalisation scheme for text data is the TF-IDF scheme. After reading the file, parsing the data and computing the TF-IDF metric, I need to train a classification model to differentiate between movies with positive and negative feedbacks depending on the reviews and ratings. This is a standard binary classification problem by treating all reviews with >5 rating scores as the positive class and those with <=5 rating scores as the negative class. 

I have implemented 3 classification models Logistic regression, linear SVM with and without parameter selection and random forest. Also program shows accuracy and time for each classification model. 
