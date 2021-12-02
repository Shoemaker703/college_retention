# How Does College Academic and Athletic Spending Impact Retention Rates?

![UT Austin](https://github.com/Shoemaker703/college_retention/blob/main/Images/Austin_Stadium.jpeg)

**Author**: 

- [Scott Schumann](https://github.com/Shoemaker703)

## Overview

Retention rates are one of the most important student success metrics used by colleges in the US. Even a brief search on websites like [Inside Higher Ed](https://www.insidehighered.com/) or [The Chronicle of Higher Education](https://www.chronicle.com/) will return a number of articles describing the importance of retention rates and strategies for departments to increase student retention. Given that graduation is one of the primary goals of attending college, retention rates can be thought of as an early indicator of what graduation rates will be later down the road. Given the importance of retention rates, this project seeks to understand the relationship between retention rates and college spending patterns in both academics and athletics. The hope is that if there are patterns between spending and retention rates, that colleges can use that information to redirect funds to increase student retention.

## Business Understanding

[According to the National Center for Education Statistics (NCES)](https://nces.ed.gov/programs/coe/indicator/ctr), "Retention rates measure the percentage of first-time undergraduate students who return to the same institution the following fall, and graduation rates measure the percentage of first-time, full-time undergraduate students who complete their program at the same institution within a specified period of time." Figure 1 below is from the NCES website linked above, which shows retention rates for all college, public, private nonprofit, and private for-profit institutions. The figure also includes additional information for three different acceptance rates: all, open, and less than 25%. 

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

## Modeling

The target variable is a weighted retention rate described above, using values above 81% to represent "above average retention rates" and values at or below 81% to represent "below average retention rates." A 70%/20% train-test split was created along with a 10% holdout test set.

True Positive: A school is identified as having above average retention rates and in fact does\
False Positive: A school is identified as having above average retention rates but in fact does not\
True Negative: A school is identified as having below average retention rates and in fact does\
False Negative: A school is identified as having below average retention rates but in fact does not

In this instance, I think false positives are more problematic than false negatives given that it is more of a problem to identify a school as above average when it is not. Thus, I will try and maximize precision scores throughout the modeling process.

Seven different model types were run (logistic regression, KNN, decision tree, decision tree grid search, gradient boost, random forest, and random forest grid search). The final model selected was the random forest grid search, which had precision scores of .885 for the cross-validation process, .947 on the testing data, and .814 on the holdout test.

## Conclusions

According to the random forest model, the most significant features in this model are "Average Faculty Salary" and 'Total Academic Spending (University-Wide)', which account for 13.5% and 8.8% of the value of features in this model, respectively. This, along with the 'Academic Spending per FTE Student' and 'Endowment' columns being ranked as important features in this model, suggests that academic spending is more important to student retention than athletic spending. However, if we examine the other spending metrics in this notebook, we can see that universities have been increasing athletic spending at a greater rate than academic spending over the course of the 15 years included in this data. Thus, it might be beneficial for universities interested in increasing retention rates to find more of a balance between faculty salaries and football coaching salaries by either paying faculty more and/or paying football coaches less.

![Final Comparison Bar Chart](https://github.com/Shoemaker703/college_retention/blob/main/Images/feature_importances.png)

Based on the predictions from the random forest model, I was able to determine that FBS schools are likely to have better retention rates than their FCS and NFS counterparts. Furthermore, within the FBS, schools in the power 5 conferences seem to have a greater likelihood of having above average retention rates than others. Thus, one general comment regarding these results might be that the results of this model are more relevant to schools outside of the FBS power 5. However, one possible reason for this could be that schools in the FBS power 5 conferences tend to have larger budgets than other schools, and thus are able to spend enough money on academics and athletics to be able to maintain above average retention rates and quality athletics programs. Thus, one possible approach would be for colleges to spend less on their athletics departments since they will not make money from them anyway, and redirect that spending towards academic departments which could have a positive impact on student retention rates.

## Information

Check out our [notebook](https://github.com/Shoemaker703/college_retention/blob/main/Final%20Notebook.ipynb) for a more thorough discussion of our project, as well as our [presentation](https://github.com/Shoemaker703/time_series_project/blob/main/Presentation.pdf).

## Repository Structure

```

├── EDA Notebooks                       <- Folder containing additional notebooks for data exploration and modeling
│   └── ...
├── Images                              <- Folder containing images used in the notebook and this README
│   └── ...
├── .gitignore                          <- File specifying files/directories to ignore
├── Final Notebook.ipynb                <- Final Jupyter Notebook containing full code and narrative for this project
├── README.md                           <- Top-level README
└── utils.py                            <- Evaluation function used for modeling process throughout notebook

``` 
