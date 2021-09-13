# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Capstone Project: Whisk(e)y & Food Pairing Recommender


## Introduction ##
Our objective is to build a recommendation system that will guide users into making a data-based decision about whiskies and food to go with it. It's a system designed to help people who wish to try whisky but don't know where to begin, and people who would like to find similar whiskies to the ones that they enjoy.


## Methodology ##
We will be utilizing Machine Learning to train a model that will make recommendations based on the whiskies' flavour profiles.



## Data Cleaning ##
The whisky dataset had a lot of word and alphabet based columns that had to be changed to numerical or dummified columns in order for the machine learning model to make more accurate predictions.

Single Malt and Blended Whiskies:
- A - Full-bodied, sweet, pronounced sherry – with fruity, honey and spicy notes
- B - Full-bodied, sweet, pronounced sherry – with fruity, floral and malty notes, some honey and spicy notes
- C - Full-bodied, sweet, pronounced sherry – with fruity, floral, nutty, and spicy notes, some smoky notes
- E - Medium-bodied, medium-sweet – with fruity, honey, malty and winey notes, some smoky and spicy notes
- F - Full-bodied, sweet and malty – with fruity, spicy, and smoky notes
- G - Light-bodied, sweet, apéritif-style – with honey, floral, fruity and spicy notes, but rarely any smoky notes
- H - Very light-bodied, sweet, apéritif-style – with malty, fruity and floral notes
- I - Medium-bodied, medium-sweet, quite smoky – with some medicinal notes and spicy, fruity and nutty notes
- J - Full-bodied, dry, very smoky, pungent – with medicinal notes and some spicy, malty and fruity notes

Bourbons and American Whiskies:
- R0 - “No Rye” whisky with 0 rye gain (pure corn whiskies and "wheaters")
- R1 - “Low Rye” whisky of 10% or less rye grain
- R2 - “Standard Rye” whisky of 10-15% rye grain (classic bourbons)
- R3 - “High Rye” whisky of more 15% rye
- R4 - “Rye” whisky of more than 51% rye (straight rye whiskies)

All these clusters (A - R4) were numbered 1 - 14, and whiskies with a blank cell under the 'cluster' column were assigned a new cluster "0".

The flavour notes were broken down into Winey, Fruity, Floral, Honey, Malty, Nutty, Spicy, Smoky, Medicinal representing the primary notes, and Some Fruity, Some Honey, Some Malty, Some Nutty, Some Spicy, Some Smoky, Some Medicinal representing the secondary notes in the whiskies. 
 
As for the Food dataset, which we created using research from the internet, each food was matched to one or more whisky clusters based on the food's flavour profile.




## Brief Summary of Analysis ##
Scotch whiskies made up more than 50% of the dataset which was unsurprising given that Scotland is the largest producer of whiskies in the world. As far as different types of whiskies go, Malts made up about 60% of the dataset, with more Sweet whiskies than Medium-Sweet and Dry whiskies put together. Sherry cask were the dominant Base Flavour to feature in the dataset, with the combination of Quite Smoky and Very Smoky whiskies coming in close behind. Fruity notes were far more prominent in the dataset in almost 900 whiskies compared to the other Flavour Notes with Spicy and Some Spicy still some distance behind, only being present in 520 and 600 whiskies respectively.

## Modelling Process ##
The modelling process was made simple thanks to the use of the Pycaret Library which is able to run a comparison between several different classification models. The default train-test split for running models through Pycaret is 70% - 30%, and we also stratified the data so as to have more fair results given the dominance of whiskies from Scotland in the dataset compared to whiskies from other countries.

The ranking of the training models is as follows:

1. Gradient Boosting Classifier
2. Ridge Classifier
3. Random Forest Classifier
4. Decision Tree Classifier
5. Logistic Regression Classifier
6. Extra Trees Classifier
7. K Neighbors Classifier
8. Light Gradient Bosting Machine
9. SVM - Linear Kernel
10. Naive Bayes
11. Linear Discriminant Analysis
12. Ada Boost Classifier
13. Quadratic Discriminant Analysis

The Gradient Boosting Classifier finished top in almost every category with training scores of:
 - Accuracy - 96.64%
 - AUC - 99.83%
- Recall - 93.84%
- Precision - 96.82%
- F1 - 96.19%
- Kappa - 96.27%
- MCC - 96.34%

The highest AUC score went to Logistic Regression at 99.84% with Gradient Boosting Classifier coming in a close second at 99.83%.

Due to being the overall top model, and also due to the importance of F1 scores outweighing AUC scores in multi-class classification, we decided to go with the Gradient Boosting Classifier to base our recommender system on.

We ran our prediction on the Gradient Boosting Classifier with the all the test scores outperforming the training scores:
- Accuracy - 96.65%
- AUC - 99.87%
- Recall - 94.01%
- Precision - 97.03%
- F1 - 96.26%
- Kappa - 96.28%
- MCC - 96.34%

## Recommendation - Whisky Flavour Profile ##

### Option A: Recommend Whiskies Similar to User's Chosen Whisky
This option allows users to input a whisky name from the database, and the recommender system generates a random output of 5 whiskies from the same cluster.

### Option B: Recommend Whiskies based on User's Chosen Flavour Profile
This option allows users to input the cluster number of his/her preferred flavour profile from the database, and the recommender system generates a random output of 5 whiskies from the same cluster.

## Conclusion ##
These basic recommendation systems have given expected results thus far.


## Limitations ##
Since the majority of whiskies are from Scotland, the recommender is more likely to recommend whiskies from Scotland compared to whiskies from other regions.

The food database might be inadequate as it was a self-created file based on internet research.


## Future Steps ##
The recommendation system could be further improved to perhaps display 3 whiskies from Scotland and 2 from other regions to give the rest of the world's whiskies a more significant representation when making recommendations to users.

Perhaps a price filter could be built in to help users pick whiskies that they find more affodable or that possible offer more "value-for-money" options.

It would also be beneficial to have a proper data source with diverse food options to match with the flavour profiles of the whiskies.
