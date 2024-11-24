# Dependence of NBA Free Throws

# Purpose
The goal of this project was to determine if the result of the first free throw affects the probability of making the second free throw, and if it does, how does it affect it?

If a player makes the first free throw, does it lead to overconfidence and result in a lower probability of making the second free throw? Or does making the first free throw indicate that the player is in the 'zone' and has a higher probability of making the second free throw?

# Tools
This project was completed using the pandas, NumPy, SciPy, and Lmer libraries in Python.

# Sources
The dataset was comprised of information for over 600 thousand NBA free throws from 2006 to 2016. The dataset was obtained from Kaggle:

Mantey, S. (2017). NBA Free Throws. Kaggle. https://www.kaggle.com/datasets/sebastianmantey/nba-free-throws 


The test statistic used to calculate the p-value for each player was obtained from NIST:

7.3.3. How can we determine whether two processes produce the same proportion of defectives?. National Institute of Standards and Technology. 
(n.d.). https://www.itl.nist.gov/div898/handbook/prc/section3/prc33.htm 

Information about the multiple testing correction that was found on Statistics How To:
Benjamini-Hochberg Procedure. Statistics How To. (n.d.). https://www.statisticshowto.com/benjamini-hochberg-procedure/

# Process
# [Preprocessing](https://github.com/CurtisBender/Dependence-of-NBA-Free-Throws/blob/main/Reports/Preprocessing.pdf)
I started this project by downloading the dataset and importing the csv as a DataFrame in Python. As a result of an error by the NBA or the Kaggle member that scraped the data, there were instances of free throw 1 of 2 appearing twice or not having free throw 2 of 2. As a result, some data cleaning was required. From there, I reconfigured the DataFrame to allow me to perform statistical analysis. 

# [Individual Player Analysis](https://github.com/CurtisBender/Dependence-of-NBA-Free-Throws/blob/main/Reports/Individual%20Player%20Analysis.pdf)
The first part of the analysis focussed on evaluating the effect of making or missing the first free throw for individual players.

When performing multiple hypothesis tests, the significance level needs to be adjusted to account for the increased likelihood of making a Type I error (false positive) across multiple tests. 

Adjusting the significance level reduces the power of the individual hypothesis tests. Therefore, the testing was limited to the 50 players with the largest total number of free throws.

For each of the 50 players, the analysis involved calculating their p-values with the null hypothesis that consecutive free throws are independent events.

# [General Player Analysis](https://github.com/CurtisBender/Dependence-of-NBA-Free-Throws/blob/main/Reports/General%20Player%20Analysis.pdf)
In addition to the analysis of individual players, the overall trend amongst players in general was also investigated.

Mixed effects logistic regression was used to model the probability of a player making free throw 2 of 2 given the result of free throw 1 of 2, while accounting for differences in overall free throw abilities amongst different player's.

# Results
For the individual player analysis, only 2 of the 50 players provided sufficient evidence to reject the null hypothesis the consecutive free throws are independent events. 
These two players were Dwight Howard and Josh Smith.

Dwight Howard is approximately 6.4% more likely to make the second free throw if he makes the first.

Josh Smith is approximately 9.1% more likely to make the second free throw if he makes the first.

For the general player analysis, it was found that knowing the result of free throw 1 of 2 improved the model's ability to predict the probability of making 2 of 2 at a statistically significant level. 

The model was used to predict the 2nd free throw probability for 4 different players with varying average free throw percentages:

```
Estimated second free throw probabilities:

Ben Wallace missed first free throw: 0.4507
Ben Wallace made first free throw: 0.4857
Difference: 0.0350

Shaquille O'Neal missed first free throw: 0.5590
Shaquille O'Neal made first free throw: 0.5933
Difference: 0.0343

LeBron James missed first free throw: 0.7611
LeBron James made first free throw: 0.7857
Difference: 0.0246

Stephen Curry missed first free throw: 0.9041
Stephen Curry made first free throw: 0.9156
Difference: 0.0115
```

From the model predictions, it can been seen that making the first free throw increases the probability of making the second free throw by roughly 1.2-3.5% depending on the player's average free throw percentage.
