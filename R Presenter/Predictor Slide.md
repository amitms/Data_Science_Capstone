TheNextWord 
========================================================
author: Amit Man Singh
date: 30 May 2016

Next Word Predictor
========================================================

An Intuitive Application that Predicts the next Word!

**Word Predictor** can be implemented on mobile devices and offers advantages over standard text typing:

* Improved typing speed
* Improved spelling and accuracy

Predict Next Word
========================================================


**Word Predictor** is an interactive Shiny R application that can predict the word based on the phrase/sentence/word you enter.


IT'S INTUITIVE AND EASY TO USE

How does it work?
========================================================

* **Word Predictor** uses the n-grams data set determining word frequency.

Here are the steps of how it works:

1. The user enters the required phrase, sentence or word.
2. The application utilizes its trained Decision Tree to figure out which word occurs next.
3. The application outputs the results

The Internal of the application
========================================================

The application, at the core, uses N-Gram model for prediction.

Please try the the accuracy of the application youself. I hope to increase its accuracy in the next release.

Getting my hands at the Application
========================================================

Shiny word predictor application
<a href="https://amitms.shinyapps.io/WordPrediction">https://amitms.shinyapps.io/WordPrediction/</a>

Other source codes<br>
<a href="https://github.com/amitms/Data_Science_Capstone">other source codes</a>

References:<br>
[1] http://www.ngrams.info/
