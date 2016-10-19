# Data Insights

## General
- Input is the decays signature of a particule collision
- Ouput is a classification on whether the particle is a Higg's Boson or not
- There are 30 features in total
- All variables are floating point except PRI_jet_num which is an integer
- Variables prefixed with DER are quantites computed from primitive features
- -999 represents values that cannot be computed or are meaningless
- training set is comprised of 250'000 events

## Possible plots
- Range of each feature
- Count number of -999 per feature.
- Rank attributes per correlation with output feature

## Ideas for feature engineering
- Bin separation of data to see its distribution
- Convert features with -999 into binary classification

## Observations
-There appears to be no direct link between any feature and classification output at a cursory glance
-Features:0,4,5,6,12,23,24,25,26,27,28 had invalid values.
-tX:In initial dataset: Features 14, 15, 17, 18, 24, 25, 27, 28 display minimal correlation to the output classification
-X1:Upon performing binary classification of valid versus invalid values, features 14, 15, 17, 18 only were uncorrelated out of 33.
-X2:Upon performing mean_replacement and standardizations features [14, 15, 17, 18, 23, 24, 26, 27] were uncorrelated out of 33 which correspond to initial features [14, 15, 17, 18, 24, 25, 27, 28]
-X3:Upon performing median_replacement and standardizations features, same results were observed as X2

Experiment 1: Best
Stochastic gradient descent on X2 
max_iters = 100
gamma = 0.2
obtained score=0.74506

Experiment 2: Perform LSE instead of gradient descent on X1 results in  0.73651
Performs worst as lambda is smaller (clear overfitting)

Conclusions so far: Stick to stochastic gradient descent instead of LSE/ridge regression

Experiment 3:
Eliminate columns with low correlation and perform gradient descent
[14, 15, 17, 18, 24, 25, 27, 28] performed worst than initial. 	0.72028

Experiment 4:
Eliminate only columns 14,15,17,18 obtains 0.72031

Thoughts: Perform gradient descent using X1 and all features

