# 📊 Prosthesis-Physical-Behaviour-Monitoring-Description 📈

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
