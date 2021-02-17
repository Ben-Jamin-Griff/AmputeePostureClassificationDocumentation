<h1 align="center">Prosthesis-Physical-Behaviour-Monitoring-Description</h1>

## Project Introduction
The work is part of the Low Cost Through Knee Prosthesis Takeup project, which is an EPSRC funded project with a collaboration effort between Exceed Worldwide, DPO, UOS & ICL (Department of Prosthetics and Orthotics in the Faculty of Prosthetic and Orthotic Engineering at the National Institute of Social Affairs). The main objective of the project is to evaluate the use of a new, low-cost, knee joint design within developing countries. The reason for this project is that vast amount of R&D on both the design and evaluation of P&O devices is concentrated to Europe and North America and therefore devices often inappropriate for use in developing countries. So the P&O research group at ICL have come up with a new knee design with a focus specifically on the application within developing countries. Current low-cost designs have some major limitations such as they can’t be locked in extension, they compromise on aesthetics which could result in social exclusion, and a very low prosthetic knee joint center producing other functional issues. These are all things that the project aims at addressing, while focusing on making the design suitable for manufacture and maintence in developing countries and you can see there a prototype of the design.

## Why is This Work Import?
Lets look at Cambodia where this evaluation project is focused, Cambodia is one of the world's most landmine affected countries and as a result has had over 25,000 amputations recorded since 1979. Added to this, the rise in the number of amputations resulting from road traffic accidents and you have a serious need for P&O services. It’s estimated that 10 million people in South East Asia, India and Sri Lanka need but do not have access to these kind of services. This project is directly targeted at improving resources for end-users, both prosthetists and amputees, by creating a design that will reduce both the manufacture and maintenance costs of this technology.

## Project Objective 
The aim of the study is to recruit 20 lower limb amputees within Cambodia, give them access to the new ICL knee design for 3 weeks and then at the end of this period evaluate the design. There are 2 methods we are going to use as part of this evaluation. The first being a user satisfaction questionnaire, where we are going to follow a standard prosthesis evaluation protocol and assess their general satisfaction with the design. The other side of the evaluation is monitoring their physical behaviours during the 3 week period. To do this we’ll be using a typical event based method looking at assessing the patterns and duration of their physical behaviours. So we’ll be specifically looking at how much time they spend sitting, standing, walking and also wear-time. This is important because it will give us a measure of how much they used their new device and the specific activities they performed while using the device. This can help by not only supporting the feeback we get from the questionnaires but also giving us an objective measure of usage and could be used to identify areas where the design could be improved.

## Traditional Physcial Behaviour Monitoring Methods
Typically, we monitor physical behaviours using an activity monitor and the ActivPal is a device commonly used for this purpose. For those that don’t know, this is a device that contains an accelerometer which is mounted on the thigh of the user. It uses it’s reference to gravitational acceleration to classify postures such sitting and standing based on thigh orientation and then looks at other acceleration features, like signal frequency, to classify activities like stepping. It does this throughout the measurement period until eventually we build a picture of the wearers physical behaviours which gives a rich dataset to analyse
So we could use this device to monitor the amputees physical behaviours.

<p align="center">
  <img width="500" src="https://github.com/Ben-Jamin-Griff/Prosthesis-Physical-Behaviour-Monitoring-Description/blob/main/ap-description.PNG">
</p>

## Summary

  - [Project Objective](#project-objective)
  - [Getting Started](#getting-started)
  - [Authors](#authors)

## Project Objective
The aim of this project is to create software that processes activity monitor data for the purpose of analysing the physical behaviours of lower limb prosthesis users and prosthesis use.

### Partners
* University of Salford
* Southampton University

### Technologies
* MATLAB
* Python
  * Pandas, Numpy, Matplotlib, Seaborn, Jupyter Notebook, Scikit-Learn
* PAL Technologies - ActivPAL

## Getting Started

Clone this repo (for help see this [tutorial](https://help.github.com/articles/cloning-a-repository/)).

The data for this project are confidential, but may be obtained with Data Use Agreements. Researchers interested in access to the data may contact Benjamin Griffiths (b.n.griffiths@salford.ac.uk). The author will assist with any reasonable replication attempts.

A sample dataset has been provided by the author for use as open access.

Dataset list
------------

| Data file | Notes    |
|-----------|----------|
| `example_data/example_data/shank-AP870085 202a 1Sep20 10-30am for 5h.datx` | datafile from shank mounted activpal |
| `example_data/example_data/shank-AP870085 202a 1Sep20 10-30am for 5h-CREA-PA08110254-AccelDataUncompressed.csv` | shank raw accelerations (3-axis 20Hz) exported from PAL Analysis |
| `example_data/example_data/shank-AP870085 202a 1Sep20 10-30am for 5h-CREA-PA08110254-Events.csv` | shank events exported from PAL Analysis |
| `example_data/example_data/thigh-AP472387 202a 1Sep20 10-30am for 5h.datx` | datafile from thigh mounted activpal |
| `example_data/example_data/thigh-AP472387 202a 1Sep20 10-30am for 5h-CREA-PA08110254-AccelDataUncompressed.csv` | thigh raw accelerations (3-axis 20Hz) exported from PAL Analysis |
| `example_data/example_data/thigh-AP472387 202a 1Sep20 10-30am for 5h-CREA-PA08110254-Events.csv` | thigh events exported from PAL Analysis |

Each data directory should be structured as above with data from 2 devices.

*TBC processing for 1 device only*

Computational requirements
---------------------------

### Software Requirements
- MATLAB (2019a)
  - `Statistics and Machine Learning Toolbox`

### Memory and Runtime Requirements

The code was last run on an **Intel(R) Core(TM) i5-7200U CPU**.

Instructions
------------

### Description of programs

- The program `prosthesis-physical-behaviour-monitoring/exploratoryDataAnalysis.m` will extract, reformat and save all datasets selected during execution. On running the program, select the directory containing the example data `example_data/example_data/`, with access to more datasets this function will continue to collate data by providing additional selection boxes, but if using example data select cancel.  After the initial program terminates there are sections of code that explore potential predictor features, run each block after the keyboard interupt or run them all by selecting continue and inspecting the visualisations.

- The program `prosthesis-physical-behaviour-monitoring/modelDevelopment.m` will extract, reformat and save all datasets selected during execution. On running the program, select the directory containing the example data `example_data/example_data/`, with access to more datasets this function will continue to collate data by providing additional selection boxes, but if using example data select cancel.  After the initial program terminates there is placeholder code commented at the bottom of the file which can be used to access the classicication learner toolbox. Here you will need to run through the process of creating a ML model. After exiting the toolbox and exporting the model to the workspace, there is more placeholder code to assess the model and save the model for making predictions.

- The programs `prosthesis-physical-behaviour-monitoring/evaluatingDataHeuristic.m` and `prosthesis-physical-behaviour-monitoring/evaluatingDataML.m`  will extract, reformat and save a selected datasets. On running the program, select the directory containing the example data `example_data/example_data/`, you will be required to create a reference for this analysis. (**Note:** when running the ML model you first need to select the folder containing the model you want to use, this can be found in the output folder after creating the model using the previous function). Once the program has extracted the data it will compare the original values from both activtiy monitors before applying the relevant algorithm and comparing the new values. Throughout this process the program will present visualisations and ask if you would like to save these to the figures directory.

- All other programs within the directory `prosthesis-physical-behaviour-monitoring/` are class definitions that are used by the previously described programs. The class definitions (objects) are collections of related function that are executed by calling the name of the class followed by the function and parameters e.g. Process.someFunction(x, y).

### Recommended Execution

- First run `exploratoryDataAnalysis.m` to look over your entire dataset and analyse potential features. Although this program is not nessesary it is useful for exploring the data.
- Next run `modelDevelopment.m` this will process your example data and enable you to create a ML model to evaluate your data (**Note:** With only the example dataset you will be training and testing your data on a single dataset. There are many issues with this but the example data is presented only for the purpose of demoing the program).
- Next run `evaluatingDataHeuristic.m` this will process your example data and compare your data before and after applying the rule-based algorithm.
- Next run `evaluatingDataML.m` this will process your example data and compare your data before and after applying the machine learning algorithm. First you need to select the directory containing the ML model before selecting your data to analyse. 

List of outcome resources
---------------------------

| Directory | Program | Note |
|-------------|-------------|-------------|
| prosthesis-physical-behaviour-monitoring/output/eda/*date*/ | `exploratoryDataAnalysis.m` | Contains data and figures from EDA process |
| prosthesis-physical-behaviour-monitoring/output/eda/*date*/ | `modelDevelopment.m` | Contains the model exported as during ML model development |
| prosthesis-physical-behaviour-monitoring/output/analysis/heuristic/*date*/*analysis-reference*/ | `evaluatingDataHeuristic.m` | Contains data and figures from rule based algorithm |
| prosthesis-physical-behaviour-monitoring/output/analysis/ml/*date*/*analysis-reference*/ | `evaluatingDataML.m` | Contains data and figures from ML algorithm |

Data structure (after processing)
----------------------------------
```
data    
│
└───file_001
│   │   Time (datetime)
│   │   xRaw (double)
│   │   yRaw (double)
│   │   zRaw (double)
│   │   accelLocation (char)
│   │   accelFileName (char)
│   │   samplingFrequecy (double)
│   │   eventTable (table)
│   │   eventLocation (char)
│   │   eventFileName (char)
│   │
│   └───summaryStatistics
│   │   │   totalTimeSedentary (double)
│   │   │   totalTimeStanding (double)
│   │   │   totalTimeStepping (double)
│   │   │   totalTimeLying (double)
│   │   │   totalTimeTransport (double)
│   │   │   totalSteps (double)
│   │
│   └───eventList
│       │
│       └────event_00001
│       │    │   activtiyCode (double)
│       │    │   xRaw (double)
│       │    │   yRaw (double)
│       │    │   zRaw (double)
│       │
│       └────...
│
└───file_002
```

<hr>

## Authors

  - **Benjamin Griffiths** - *Wrote the code* -
    [Ben-Jamin-Griff](https://github.com/Ben-Jamin-Griff)

[![](https://mermaid.ink/img/eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG4gICAgQWxpY2UtPj4rSm9objogSGVsbG8gSm9obiwgaG93IGFyZSB5b3U_XG4gICAgQWxpY2UtPj4rSm9objogSm9obiwgY2FuIHlvdSBoZWFyIG1lP1xuICAgIEpvaG4tLT4-LUFsaWNlOiBIaSBBbGljZSwgSSBjYW4gaGVhciB5b3UhXG4gICAgSm9obi0tPj4tQWxpY2U6IEkgZmVlbCBncmVhdCFcbiAgICAgICAgICAgICIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In0sInVwZGF0ZUVkaXRvciI6ZmFsc2V9)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG4gICAgQWxpY2UtPj4rSm9objogSGVsbG8gSm9obiwgaG93IGFyZSB5b3U_XG4gICAgQWxpY2UtPj4rSm9objogSm9obiwgY2FuIHlvdSBoZWFyIG1lP1xuICAgIEpvaG4tLT4-LUFsaWNlOiBIaSBBbGljZSwgSSBjYW4gaGVhciB5b3UhXG4gICAgSm9obi0tPj4tQWxpY2U6IEkgZmVlbCBncmVhdCFcbiAgICAgICAgICAgICIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In0sInVwZGF0ZUVkaXRvciI6ZmFsc2V9)
