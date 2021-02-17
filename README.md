<h1 align="center">Prosthesis-Physical-Behaviour-Monitoring-Description</h1>

## Summary

  - [Project Introduction](#project-introduction)
  - [Why is This Work Import?](#why-is-this-work-import)
  - [Project Objective](#project-objective)
  - [Traditional Physcial Behaviour Monitoring Methods](#traditional-physcial-behaviour-monitoring-methods)
  - [The Problem](#the-problem)
  - [The Method](#the-method)
  - [The Results](#the-results)
  - [Future Work](#future-work)
  - [Authors](#authors)

### Technologies
* MATLAB
* Python
  * Pandas, Numpy, Matplotlib, Seaborn, Jupyter Notebook, Scikit-Learn
* PAL Technologies - ActivPAL
 
## Project Introduction
The work is part of the Low Cost Through Knee Prosthesis Takeup project, which is an EPSRC funded project with a collaboration effort between Exceed Worldwide, DPO, UOS & ICL (Department of Prosthetics and Orthotics in the Faculty of Prosthetic and Orthotic Engineering at the National Institute of Social Affairs). The main objective of the project is to evaluate the use of a new, low-cost, knee joint design within developing countries. The reason for this project is that vast amount of R&D on both the design and evaluation of P&O devices is concentrated to Europe and North America and therefore devices often inappropriate for use in developing countries. So the P&O research group at ICL have come up with a new knee design with a focus specifically on the application within developing countries. Current low-cost designs have some major limitations such as they can’t be locked in extension, they compromise on aesthetics which could result in social exclusion, and a very low prosthetic knee joint center producing other functional issues. These are all things that the project aims at addressing, while focusing on making the design suitable for manufacture and maintence in developing countries and you can see there a prototype of the design.

## Why is This Work Import?
Lets look at Cambodia where this evaluation project is focused, Cambodia is one of the world's most landmine affected countries and as a result has had over 25,000 amputations recorded since 1979. Added to this, the rise in the number of amputations resulting from road traffic accidents and you have a serious need for P&O services. It’s estimated that 10 million people in South East Asia, India and Sri Lanka need but do not have access to these kind of services. This project is directly targeted at improving resources for end-users, both prosthetists and amputees, by creating a design that will reduce both the manufacture and maintenance costs of this technology.

## Project Objective 
The aim of the study is to recruit 20 lower limb amputees within Cambodia, give them access to the new ICL knee design for 3 weeks and then at the end of this period evaluate the design. There are 2 methods we are going to use as part of this evaluation. The first being a user satisfaction questionnaire, where we are going to follow a standard prosthesis evaluation protocol and assess their general satisfaction with the design. The other side of the evaluation is monitoring their physical behaviours during the 3 week period. To do this we’ll be using a typical event based method looking at assessing the patterns and duration of their physical behaviours. So we’ll be specifically looking at how much time they spend sitting, standing, walking and also wear-time. This is important because it will give us a measure of how much they used their new device and the specific activities they performed while using the device. This can help by not only supporting the feeback we get from the questionnaires but also giving us an objective measure of usage and could be used to identify areas where the design can be improved.

## Traditional Physcial Behaviour Monitoring Methods
Typically, we monitor physical behaviours using an activity monitor and the ActivPal is a device commonly used for this purpose. For those that don’t know, this is a device that contains an accelerometer which is mounted on the thigh of the user. It uses it’s reference to gravitational acceleration to classify postures such sitting and standing based on thigh orientation and then looks at other acceleration features, like signal frequency, to classify activities like stepping. It does this throughout the measurement period until eventually we build a picture of the wearers physical behaviours which gives a rich dataset to analyse
So we could use this device to monitor the amputees physical behaviours.

<p align="center">
  <img width="450" src="https://github.com/Ben-Jamin-Griff/Prosthesis-Physical-Behaviour-Monitoring-Description/blob/main/ap-description.PNG">
</p>

## The Problem
The limitation is that for lower limb amputees, mounting an activity monitor on the participants thigh means we will not be able to also collect non-wear data because the device has no interface with the prosthesis and therefore no way of knowing when it has been removed. Also, because of the method used to mount the activPAL on the thigh, which involves a sticky covering plaster, this can cause skin irritation, which means the participant will be more inclined to remove the device. So instead we thought we should try mounting an accelerometer onto the prosthesis itself and then we can monitor both the physical behaviours of the amputees (while they are wearing the prosthesis) and non-wear time. With the added benefit of having no impact on the wearers comfort. One other bonus is that mounting the device on the prosthesis gives us the opportunity to eventually develop a robust (maybe waterproof) casing that would protect the device from the environment. But we don’t have any plans for this yet. Now we can’t rely on the activPAL’s native algorithm for detecting events because it’s going to miss classify sitting events as standing events because it’s orientation will be the same. So we needed to develop a new method for classifying events from a shank mounted accelerometer and this has been my role in the project to date.

<p align="center">
  <img width="400" src="https://github.com/Ben-Jamin-Griff/Prosthesis-Physical-Behaviour-Monitoring-Description/blob/main/problem-description.PNG">
</p>

## The Method
I used the ActivPal located in the normal thigh mounted location to collect events and considered these events to be true and my validation dataset. Then I used another ActivPal mounted onto the anterioror aspect of my shank which is the same location we plan to mount the activPAL on the prosthesis. Doing so enabled me to collect a full week of data and plenty of examples of the events we want to try and classify and the corresponding raw acceleration data from the shank. And as you can see this data was collected on myself in my flat and I’ve even got washing hanging up in the background to make it look like an authentic home lab. However, the ActivPal defines events without specific durartions and instead, the event classification changes when it detects some sort of transition. Therefore each event could be seconds or minutes long. This is a problem because I might not be able to accurately detect event transitions using the shank data in the same way the activPAL does and therefore I needed to separate out my raw data differently

<p align="center">
  <img width="500" src="https://github.com/Ben-Jamin-Griff/Prosthesis-Physical-Behaviour-Monitoring-Description/blob/main/method-description.PNG">
</p>

I separated out the data into epochs of 15 seconds in length. Each epoch contained the an event code that corresponded to the event detected by the thigh mounted ActivPal and also contained the corresponded raw data from the shank mounted activPAL and the thigh mounted activPAL. The reasons I also collected the raw thigh data was to perform some checks on the processing which I’ll explain in a moment The 15 epoch was moved along the data in 5 second intervals to create and overlap in the data collected. This was done to increase the amount of unique epochs for creating the algorithm. If the window spanned multiple activities, the event code was assigned based on the activity with the longest duration in that window. This method generated up to 17280 epochs per day but then a lot of these were removed if they were not spanning either a sitting, standing or stepping event. For example, sleeping.

<p align="center">
  <img width="600" src="https://github.com/Ben-Jamin-Griff/Prosthesis-Physical-Behaviour-Monitoring-Description/blob/main/method2-description.PNG">
</p>

Before the raw acceleration data had been separated out into epochs it was low pass filtered at a frequency of 10 Hz. This was done to remove any noise or high frequency artifact. Then for each epoch I used the raw acceleration data to create a few additional signals, I combined the acceleration axis to create a vector magnitude signal and differentiated the raw acceleration data to calculate jerk for each axis and again combined these to create a jerk magnitude signal. From these signals, within each epoch I calculated 136 values that were to be my features I would use to make predictions of the events. These features were made up of time domain and frequency domain features
All of this processing was found in the 2017 paper by Zhu et al who was trying to predict activities using several accelerometers and the features were common among other similar papers.

`Zhu, J., San-Segundo, R. & Pardo, J.M. Feature extraction for robust physical activity recognition. Hum. Cent. Comput. Inf. Sci. 7, 16 (2017).`

I had an idea of which algorithm I wanted to test first,  a K nearest neighbour. The way the KNN works, is by taking in labelled training data (like this) and simply stores it in memory. Then whenever a new value is presented to the data, it simply looks for K nearest values to itself using simple geometry. The reason I wanted to use this algorithm is because it is simple to interpret, it works well with large labelled datasets and the data did not need to meet any specific distribiution assumptions. However, it works best on data with low dimensions, by that I mean only has a few predictor features `and I have 136`. So I used a method call linear discriminate analysis to reduce the number of dimensions I have down to 2. This is like principle component analysis but it uses labelled data and tries to increase the variation between the classes at each step. After this process I was left with 2 features to make my predictions, which make it easy to plot and show the separation between classes

I was also lucky enough to get out of my flat and visit the team down in ICL in December and I was able to collect a few hours of data on several amputees. So the results include both data collected on myself and data on an amputee from ICL (5 days).

## The Results
Let us first look at the predictions made using the shank data, on the left I have all the epochs collected from the shank and I partitioned this data so that 80% of the data was used to train the algorithm and 20% was used for testing. The results and corresponding confusion matrix are displayed. On the right I have `Pure EPOCHs` which is a subset of the data where any EPOCHs that contain overlapping events were removed.

<p align="center">
  <img width="900" src="https://github.com/Ben-Jamin-Griff/Prosthesis-Physical-Behaviour-Monitoring-Description/blob/main/results-description.PNG">
</p>

I also conducted the same analysis using the raw data from the thigh. This was to validate my methodology as we can assume the data will be far better at seperating out sitting and standing events due to the reference to gravitational acceleration. 

<p align="center">
  <img width="900" src="https://github.com/Ben-Jamin-Griff/Prosthesis-Physical-Behaviour-Monitoring-Description/blob/main/results-description2.PNG">
</p>

One more point I wanted to make about the results is that the 80/20 split probably isn’t the most fair way of testing the algorithm because I’m using data collected on a participant to make predictions about that very same participant, and this isn’t something that would happen when this algorithm meets new data. So I performed a leave one group out cross validation using the participant as the grouping. I wanted to keep both analysis results in because at the moment this method isn’t exactly fair too as I only have 2 participants. Just my data is being used to make predictions on an amputee and vice versa. These results show only a small drop in prediction accuracy using this method. For the shank data its around 3 percentage points both mixed EPOCHs and pure EPOCHs and for the thigh it doesn’t change.

## Future Work
And this is where I’m currently up to... I have some short datasets from ICL (a few hours) where other amputees were testing out the new ICL knee joint and I want to test the algorithm on these datasets. I also was to compare the results in the context of analysing the physical behaviour data so using the activPAL and my method to see differences in predicted standing time, stepping time and sitting time per day for example. There is also the potential to test different algorithms, I used the KNN but you could use a SVM or neural network and with this you could test using all 136 features or a subset of features without using dimensionality reduction. Also, you could try calculating different features to see if they are better at distinguishing between the sit and stand events which is where the problem lies. You could even use deep learning with something like Tensor Flow to feed in the raw accelerometer data and remove the feature engineering step. Finally, we’re prepping for the main data collection which will be conducted in Cambodia in April.

### Thanks for reading, if you have any questions please get in touch with me via email, which can be found on my profile page.

<hr>

## Authors

  - **Benjamin Griffiths** - *Wrote the code* -
    [Ben-Jamin-Griff](https://github.com/Ben-Jamin-Griff)
