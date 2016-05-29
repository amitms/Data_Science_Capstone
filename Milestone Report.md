---
title: "Milestone Report"
author: "Amit Man Singh"
date: "May 30, 2016"
output: html_document
---

## Abstract
This report presents the basic summary statistics of the three data sets downloaded from https://www.corpora.heliohost.org. It also reports interesting finding that I have found so far and provide feedback on the plans for creating a prediction algorithm via a shiny application.

## Introduction
We look at the three data sets of US English text from a corpus called HC Corpora. The three data sets are : a set of internet blogs posts, a set of internet news articles, and a set of twitter messages

Following information are collected from the data sets
* File Size
* Number of Lines
* Number of Non-Empty Lines
* Number of Words
* Distribution of Words (Quantiles and Plot)
* Number of Characters
* Number of non-white Characters

In the following section we will describe the data collection process, the section after that gives the results of the data exploration, we finally present conclusions and give references.

For our analysis we use the R computing environment, as well as the libraries stringi and ggplot2 . In order to make the code more readable we use the pipe operator from the magrittr library . This report is compiled using the rmarkdown library . Finally during writing we used the RStudio IDE .

Data
The data is presented as a ZIP compressed archive, which is freely downloadable from www.corpora.heliohost.org. I have already downloaded the file given the large size of the file. 

```r
# specify the source and destination of the download
destination_file <- "Coursera-SwiftKey.zip"

# extract the files from the zip file
unzip(destination_file)
```

```
## Warning in unzip(destination_file): error 1 in extracting from zip file
```

Inspect the unzipped files

```r
# find out which files where unzipped
unzip(destination_file, list = TRUE )
```

```
## Error in unzip(destination_file, list = TRUE): zip file 'Coursera-SwiftKey.zip' cannot be opened
```


```r
# inspect the data
list.files("final")
```

```
## character(0)
```


```r
list.files("final/en_US")
```

```
## character(0)
```

The corpora are contained in three separate plain-text files, out of which one is binary, for more information on this see . We import these files as follows.


```r
# import the blogs and twitter datasets in text mode
blogs <- readLines("final/en_US/en_US.blogs.txt", encoding="UTF-8")
```

```
## Error in file(con, "r"): cannot open the connection
```

```r
twitter <- readLines("final/en_US/en_US.twitter.txt", encoding="UTF-8")
```

```
## Error in file(con, "r"): cannot open the connection
```

```r
con <- file("final/en_US/en_US.news.txt", open="rb")
```

```
## Error in file("final/en_US/en_US.news.txt", open = "rb"): cannot open the connection
```

```r
news <- readLines(con, encoding="UTF-8")
```

```
## Error in readLines(con, encoding = "UTF-8"): object 'con' not found
```

```r
close(con)
```

```
## Error in close(con): object 'con' not found
```

```r
rm(con)
```

## Basic Statistics

The before we analyse the files we look at their size (presented in MegaBytes / MBs).


```r
# file size (in MegaBytes/MB)
file.info("final/en_US/en_US.blogs.txt")$size   / 1024^2
```

```
## [1] NA
```

```r
file.info("final/en_US/en_US.news.txt")$size    / 1024^2
```

```
## [1] NA
```

```r
file.info("final/en_US/en_US.twitter.txt")$size / 1024^2
```

```
## [1] NA
```

For our analysis we need two libraries.


```r
# library for character string analysis
library(stringi)

# library for plotting
library(ggplot2)
```

```
## Warning: package 'ggplot2' was built under R version 3.2.5
```

We analyse lines and characters.

```r
stri_stats_general(blogs)
```

```
## Error in stri_stats_general(blogs): object 'blogs' not found
```

```r
stri_stats_general(news)
```

```
## Error in stri_stats_general(news): argument `str` should be a character vector (or an object coercible to)
```

```r
stri_stats_general(twitter)
```

```
## Error in stri_stats_general(twitter): object 'twitter' not found
```

Next we count the words per item (line). We summarise the distribution of these counts per corpus, using summary statistics and a distribution plot. we start with the blogs' corpus.


```r
words_blogs   <- stri_count_words(blogs)
```

```
## Error in stri_count_boundaries(str, opts_brkiter = stri_opts_brkiter(type = "word", : object 'blogs' not found
```

```r
summary( words_blogs )
```

```
## Error in summary(words_blogs): object 'words_blogs' not found
```

```r
qplot(words_blogs)
```

```
## Error in eval(expr, envir, enclos): object 'words_blogs' not found
```


Next we analyse the news corpus.


```r
words_news    <- stri_count_words(news)
```

```
## Error in stri_count_boundaries(str, opts_brkiter = stri_opts_brkiter(type = "word", : argument `str` should be a character vector (or an object coercible to)
```

```r
summary(words_news)
```

```
## Error in summary(words_news): object 'words_news' not found
```

```r
qplot(words_news)
```

```
## Error in eval(expr, envir, enclos): object 'words_news' not found
```

Finally we analyse the twitter corpus.

```r
words_twitter <- stri_count_words(twitter)
```

```
## Error in stri_count_boundaries(str, opts_brkiter = stri_opts_brkiter(type = "word", : object 'twitter' not found
```

```r
summary(words_twitter)
```

```
## Error in summary(words_twitter): object 'words_twitter' not found
```

```r
qplot(words_twitter)
```

```
## Error in eval(expr, envir, enclos): object 'words_twitter' not found
```

### Conclusions
* We analysed the three datasets of corpora of US English text. The file sizes are around 200 MegaBytes (MBs) per file.
* We find that the __blogs__ and __news__ corpora consist of about 1 million items each, and the __twitter__ corpus consist of over 2 million items. 
* Twitter messages have a character limit of 140 (with exceptions for links), this explains why there are some many more items for a corpus of about the same size.
* This result is further supported by the fact that the number of characters is similar for all three corpora (around 200 million each). 
* Finally we find that the frequency distributions of the blogs and news corpora are similar (appearing to be log-normal). The frequency distribution of the twitter corpus is again different, as a result of the character limit.
