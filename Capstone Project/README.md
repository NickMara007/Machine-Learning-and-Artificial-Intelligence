# Capstone Project – Black Box Optimisation Challenge

## Project Overview
This project forms a key segment of the Professional Certificate programme, and serves an opportunity to demonstrate the machine learning techniques learned on the course within the scope of a 
formally structured project.

The project focuses on utilising Bayesian Optimisation to maximise eight black-box functions of increasing dimensionality, to analyse function behaviour, model performance, and convergence. The project forms an essential part of the Professional Certificate in Machine Learning and Artificial Intelligence programme with Imperial College London.

## Project Objectives and Constraints

The objective of the project is to maximise these eight black-box functions, through any machine learning method of choice. 
Every week, we were required to submit one new set of inputs per function, and would receive the corresponding output values before the following week. Through a total of 13 submissions, over 13 weeks, the aim was to find an output value for each function that is as close to its global maximum as possible.

We were provided with a limited amount of initial data, from which we had to build our own models to approximate each function and strategically select a next data point to query each week. Bayesian Optimisation seemed the most fitting technique, and is the machine learning approach I opted for.

Note: this project is currently under completion, and is running from March 2026 date to June 2026.

## Features

- Implementation of Bayesian Optimisation using Gaussian Processes 
- Support for multiple acquisition functions:
  - Upper Confidence Bound (UCB)
  - Expected Improvement (EI)
  - Probability of Improvement (PI)
- Evaluation on eight benchmark functions
- Visualisation of optimisation process
- Visualisation of key metrics to track model performance over time
- Model iteration and development over time
- Integration of deep learning (neural networks) to aid the optimisation process

## Methodology

### 1) Bayesian Optimisation Framework

Bayesian Optimisation models the objective function using a Gaussian Process (GP), which provides:
- A mean prediction
- Uncertainty (variance) estimate

An acquisition function is then used to determine the next sampling point.

### 2) Acquisition Functions

The acquisition functions used in this project were:
- Upper Confidence Bound (UCB): Trades off mean and uncertainty using a confidence parameter κ (kappa).
- Expected Improvement (EI): Balances exploration and exploitation by estimating expected gain.

### 3) Optimisation Pipeline

- Initialise with random samples 
- Fit Gaussian Process to observed data 
- Maximise acquisition function 
- Sample new point 
- Update model 
- Repeat until convergence or budget reached

### 4) Overall strategy

With only a limited number of queries, 13 in total, it was important that I had an execution plan so that each submission provided as much value as possible.
My strategy was roughly to emphasise exploration over exploitation at the start of the project, allowing the models to gain an understanding of the overall topology of each of the response surfaces. The middle and later stages would take a much more exploitative approach, concentrating queries on high-performing regions to maximise the output.


In terms of model parameters:
- Used a Gaussian Process as the surrogate function for every objective function.
- Used a Radial Basis Function (RBF) kernel for smooth or unimodal functions.
- Used a Matern kernel, with nu = 2.5, for functions with many local optima.
- Started with UCB as the acquisition function.
- Began with a high kappa, so exploration is favoured.
- Slowly decayed kappa on a weekly basis until weeks 8/9.
- Used Expected Improvement (EI) as the acquisition function from then on, favouring exploitation.

Hyperparameters were tailored to each objective function to model them most accurately. 
My approach was open to adaptation as new information was gathered each week. 
For example, if results were promising for a given function, I may have switched the acquisition function from UCB to EI sooner than planned.


## Scripts and Documentation

***Data Sets***

This folder contains the data sets for each function, that were updated on a weekly basis to include the latest input and output data points for each of the objective functions.

***Capstone Week X.ipynb***

These are the notebooks that I used each week to run models and generate the next submission. 
Additional features were integrated and improvements were made on a rolling basis, so later scrips will be more polished and refined.  These include additional performance metrics, visualisation improvements, and increases in interpretability. This shows the natural development of my solutions and the week-by-week iteration that took place.

***00 Capstone Data Set Updater.ipynb***

The purpose of this script is to update the data sets for each function on a weekly basis, incorporating the new input values that I had submitted and their corresponding output value.
Input and output data was given as separate .npy files for each function.

After every submission, the updated data sets are returned as text files. 
This script imports the previous week’s .npy file data as numpy arrays; appends the new data to the end of the arrays; then saves back as a new .npy file, ready to use as the following week’s data.

***01 Capstone Project Script Template.ipynb***

This is a neutral template of the Jupyter notebook I would be using each week to update my model. 
It is based on the early iterations of the notebooks so may lack features that later scripts include.

***docs/Capstone Variable and Submission Tracker.xlsx***

An Excel file containing 3 spreadsheets:
1) Plans out the approach and model parameters for each week for every function, and compares it to the actual parameters that were used.
2) Tracks and stores weekly submissions for every function.
3) Logs key changes made to models each week.

***docs/Functions.md***

Provides key information about each of the objective functions used in the project.

## Real-world Application

This type of problem is representative of many real-world machine learning cases, where a system has to be optimised to produce the best possible output.
One way to do this is through a grid search, essentially trying every hyperparameter combination and choosing the set that returns the best result. 

The problem with such an approach comes when testing the system is expensive, either in terms of monetary cost, time, or computational power. 
Additionally, for many real-world models there are a near infinite number of potential hyperparameter permutations, and even if this is constrained, the number can still be extremely large. 
For both these reasons, a different, more efficient approach has to be taken.

Take, for example, another one of my machine learning projects that utilises decision trees to generate market predictions, which an options straddle strategy uses as trade signals (please see my other repository). 
To get the best trading performance there are many hyperparameters that could be tuned. Say we wanted to select ten of these, and for each one test five different values. 
This would result in $5^{10} ≈ 9.77$ million different permutations. 

Only with a vast amount of parallel computing power and enough time would it be possible to test these many permutations, but in any realistic sense this is not a practical approach. 
Bayesian Optimisation could reduce the number of combinations of hyperparameters to hundreds or a few thousand, significantly reducing costs.
