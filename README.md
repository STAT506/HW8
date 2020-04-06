# HW8

```
knitr::opts_chunk$set(echo = TRUE)
library(readr)
library(dplyr)
library(arm)
seattle <- read_csv("http://math.montana.edu/ahoegh/teaching/stat408/datasets/SeattleHousing.csv") %>% filter(zipcode %in% c(98070, 98102)) %>% mutate(zipcode = factor(zipcode)) %>% filter(zipcode ==98070 & waterfront == 1 | zipcode == 98102)
```

### 1. Separation (12 points)

#### a. (4 points)
Assume y ~ Binomial(n,p), what is the MLE of p? Using your MLE what is the point estimate and confidence interval for p when y = n?

#### b. (4 points)
Now consider a logistic regression model 
\begin{eqnarray*}
y_i &\sim& Bernoulli(p_i) \\
logit(p_i) &=& \beta_0 + \beta_1 I(zipcode = group2) 
\end{eqnarray*}

If all of the $y_i$ values for group 1 are equal to 0 and all the $y_i$ values for group 2 are equal to 1, what should be the MLE for $\beta_0$? Hint: you can use the `invlogit` function in the `arm` package to explore this. 

#### c. (4 points)
Diagnose the model
```
seattle %>% group_by(zipcode) %>% summarise(mean(waterfront))
glm_separation <- glm(waterfront ~ zipcode, data = seattle, family = binomial)
display(glm_separation)

```


### 2. Diagnostics / Simulation (8 points)

#### a. (4 points)
Simulate data and fit a logistic regression model to this data. Comment on your results.

#### b. (4 points)
Repeat this simulation many times and create diagnostics plots to look at the residuals. Present one plot and comment on the results 


### 3. Titanic Prediction ( 10 points)

The `titanic` package in R contains survival data on passengers from the Titanic. Use the titanic_train dataset to fit a logistic regression model for passenger survival. Then report your classification error on the titanic_test dataset. Look at a few different model specifications and summarize what you found to work best.
```
library(titanic)
tibble(titanic_train)
tibble(titanic_test)
```

