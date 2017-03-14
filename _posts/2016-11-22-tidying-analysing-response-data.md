---
layout: post
title: "Tidying and Analysing Response Data using R"
date: 2016-11-2
---
You have spent months collecting data, some participants turn up on time, some participants turn up late, and others do not show up at all. After all this, all you want to do is get down to analysing your data and writing up your results. However, before you do all that, you need to extract all the information you need from the output of your experiment. Until the last few weeks, the process of tidying my data took me around 10 minutes per participant as I would do it all manually through Excel. Even for a moderate sample size, this starts to take up a large chunk of time that could be spent doing other things like writing or having a beer. Inspired by the book ‘Python for experimental psychologists’ by Edwin Dalmaijer (which I recommend you buy if you are interested in learning about programming in psychology), I started to think how I could use R to do all the hard work for me. Hopefully this post will allow you to see how you can do this in R and be able to create your own data tidying script.

The example that I am using is a measure of attentional bias known as the dot probe task. The participant is presented with two cues, and when they disappear a small dot appears in the location of one of the cues. The participant has to provide a keyboard response to whether the cue is on the left or right. The idea behind the task is that if participants provide a faster response on average to a particular type of cue, it is assumed that their attention is already in the location of the cue. In this particular example, there are two within-subject IVs which are the stimulus response asynchrony (SOA or the duration the stimuli are presented on the screen for) and trial type. SOA has three levels which are whether the cues are presented for 200ms, 500ms, or 2000ms. Trial type has two levels for whether the dot probe replaces either a smoking or a neutral cue.

If we were to do this process manually, we would split it up into several stages. Firstly, we need to load the data file up so that we can see it. Secondly, we want to only analyse correct responses. Thirdly, we want to remove any extreme values. Finally, we want to calculate the averages for each condition in the experiment.

## Step one: importing the data file

For the script to work later on, we need to install some packages. I am a big fan of the tidyverse series of packages developed by Hadley Wickham and colleagues for data science. Therefore all of the packages we will be using can be imported using the tidyverse package. If you do not have this installed, you will need to do this first using the install.packages() function (e.g. install.packages(“tidyverse”) ).

Most experimental software will provide you with a spreadsheet of your data, and after you make sure this is a .csv file we want to import the data so that we can toy around with it. If you want to follow along with the example, you can find an example data set and the full R script on Github.
```R
#Load packages 
library(tidyverse)

#Read in example file 
data1<- read.csv("RT-screening-sample.csv", 
                 header=TRUE, stringsAsFactors = FALSE)
```
