# Impacts of Collegiate Spending Patterns on Student Retention Rates

![UT Austin](https://github.com/Shoemaker703/college_retention/blob/main/Images/Austin_Stadium.jpeg)

**Author**: 

- [Scott Schumann](https://github.com/Shoemaker703)

## Overview

Retention rates are one of the most important student success metrics used by colleges in the US. Even a brief search on websites like [Inside Higher Ed](https://www.insidehighered.com/) or [The Chronicle of Higher Education](https://www.chronicle.com/) will return a number of articles describing the importance of retention rates and strategies for departments to increase student retention. Given that graduation is one of the primary goals of attending college, retention rates can be thought of as an early indicator of what graduation rates will be later down the road. Given the importance of retention rates, this project seeks to understand the relationship between retention rates and college spending patterns in both academics and athletics. The hope is that if there are patterns between spending and retention rates, that colleges can use that information to redirect funds to increase student retention.

## Business Understanding

[According to the National Center for Education Statistics (NCES)](https://nces.ed.gov/programs/coe/indicator/ctr), "Retention rates measure the percentage of first-time undergraduate students who return to the same institution the following fall." Figure 1 below is from the NCES website linked above, which shows retention rates for all college, public, private nonprofit, and private for-profit institutions. The figure also includes additional information for three different acceptance rates: all, open, and less than 25%. 

The target variable in this project will be student retention rates. Given that this project focuses on all types of college institutions, we can take the 81% rate indicated by the "All institutions—All acceptance rates" on the NCES website to represent our average retention rate. This rate only includes full-time students, but many of the schools in this analysis have both full- and part-time students. Thus, I will create a "weighted retention rate" for each school calculated by adding the number of retained full- and part-time students, divided by the total number of students enrolled at the institution. [Part-time retention rates](https://nces.ed.gov/ipeds/TrendGenerator/app/build-table/7/33?rid=4&cid=1) are often much lower than full-time retention rates, which means many schools in this analysis will be below this 81% threshold. However, given the importance of retention rates for all students, I think it is okay to set a high bar for this metric.


## Data Understanding

The data used in this project comes from three sources:

1) [The Knight Commission on Intercollegiate Athletics](https://www.knightcommission.org/)
- Includes 'NCAA Subdivision' and 'FBS Conference' information
- Includes many columns about college athletic finances including expenses and revenues, as well as some academic spending metrics. 

2) [The US Department of Education Equity in Athletics Data Analysis](https://ope.ed.gov/athletics/#/)
- Total Revenue and Expenses of each athletic department
- Total number of male and female student athletes at each institution

3) [NCES (National Center for Education Statistics) IPEDS (Integrated Postsecondary Education Data System)](https://nces.ed.gov/ipeds/)
- Student enrollment data
- Average faculty salaries
- Endowment size

## Reproducibility

For more detailed instructions regarding how I collected and merged the data from these three sources, please check out my 'Data Collection' notebook in the ['Reproducibility' folder in this GitHub repository](https://github.com/Shoemaker703/college_retention/tree/main/Reproducibility). This notebook contains step-by-step instructions (including screenshots) of how I gathered the data for the analysis below, in case you are interested in recreating and/or building on any part of this project.

## Modeling

The target variable is a weighted retention rate described above, using values above 81% to represent "above average retention rates" and values at or below 81% to represent "below average retention rates." A 70%/20% train-test split was created along with a 10% holdout test set.

True Positive: A school is identified as having above average retention rates and in fact does\
False Positive: A school is identified as having above average retention rates but in fact does not\
True Negative: A school is identified as having below average retention rates and in fact does\
False Negative: A school is identified as having below average retention rates but in fact does not

In this instance, I think false positives are more problematic than false negatives given that it is more of a problem to identify a school as above average when it is not. Thus, I will try and maximize precision scores throughout the modeling process.

Seven different classification model types were run (logistic regression, KNN, decision tree, decision tree grid search, gradient boost, random forest, and random forest grid search). The final model selected was the random forest grid search, which had precision scores of .899 for the cross-validation process, .922 on the testing data, and .944 on the holdout test.

## Conclusions

![Final Comparison Bar Chart](https://github.com/Shoemaker703/college_retention/blob/main/Images/feature_importances.png)

According to the random forest grid search model, the most significant features in this model are "Average Faculty Salary" and 'Total Academic Spending (University-Wide)', which account for 20.8% and 10.5% of the value of features in this model, respectively. If we look at the features used in the training data, there are 62 total features, only 4 of them are clearly related to academic spending ('Total Academic Spending (University-Wide)', 'Average Faculty Salary', 'Endowment', 'Academic Spending per FTE Student'). The fact that all 4 of these features are in the top 6 most important features in the random forest model reinforces the idea that academic spending is more important to student retention rates than athletic spending. 
However, if we examine the other spending metrics in this notebook, we can see that universities have spent more on athletics and have increased athletic spending at a greater rate than academic spending over the course of the 15 years included in this data: 
We can also see based on the trends for above and below average predictions that athletic spending is the highest overall amount at above average schools (both for student athletes and football coaches).\
<br>
**Average Football Coach Salaries**\
    - Above Average Colleges: $337,245\
    - Below Average Colleges: $82,614\
**Average Faculty Salaries**\
    - Above Average Colleges: $91,076\
    - Below Average Colleges: $68,283\
**Athletic Spending per Student Athlete**\
    - Above Average Colleges: $99,830\
    - Below Average Colleges: $44,573\
**Academic Spending per FTE Student**\
    - Above Average Colleges: $30,059\
    - Below Average Colleges: $15,610\
<br>
<br>
Athletic spending rates have also been increasing at a greater rate than academic spending rates from 2005–2019.\
<br>
**Average Football Coach Salary Rate of Increase**\
    - Above Average Colleges: 236.6%\
    - Below Average Colleges: 98.2%\
**Average Faculty Salary Rate of Increase**\
    - Above Average Colleges: 24.2%\
    - Below Average Colleges: 26.8%\
**Athletic Spending per Student Athlete Rate of Increase**\
    - Above Average Colleges: 75.3%\
    - Below Average Colleges: 64.0%\
**Academic Spending per FTE Student Rate of Increase**\
    - Above Average Colleges: 44.7%\
    - Below Average Colleges: 45.5%\
<br>
<br>
Thus, it might be beneficial for universities interested in increasing retention rates to strike more of a balance between faculty salaries and football coaching salaries by either paying faculty more and/or paying football coaches less.

## Information

Check out my [notebook](https://github.com/Shoemaker703/college_retention/blob/main/Summary%20Notebook.ipynb) for a more thorough discussion of my project, as well as my [presentation](https://github.com/Shoemaker703/college_retention/blob/main/presentation.pdf).

## Repository Structure

```

├── EDA Notebooks                       <- Folder containing additional notebooks for data exploration and modeling
│   └── ...
├── Images                              <- Folder containing images used in the notebook and this README
│   └── ...
├── Reproducibility                     <- Folder containing steps for collecting the data used in the summary notebook
│   └── ...
├── .gitignore                          <- File specifying files/directories to ignore
├── README.md                           <- Top-level README
├── Summary Notebook.ipynb              <- Final Jupyter Notebook containing full code and narrative for this project
├── presentation.pdf                    <- Keynote presentation slides PDF
└── utils.py                            <- Evaluation function used for modeling process throughout notebook

``` 
