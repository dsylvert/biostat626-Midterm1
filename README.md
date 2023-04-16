## General Information
An introduction to the data used can be found within the READ.md file here: [https://github.com/xqwen/bios626.git](https://github.com/xqwen/bios626.git). The training data set consists of 7,767 observations, and the testing data set consists of 3,162 observations, each consisting of 561 features. All code used can be viewed in either `Midterm_code.Rmd` or `Midterm_code.html`. Note that the .html document shows some expected output and must be downloaded locally and opened in a browser for access. All of the data can be accessed at the Github repository in the link above.

There were two tasks given, as seen in the above link. Task 1 corresponds to treating the response variable as binary, and Task 2 corresponds to treating the response variable as a multiclass variable.

## Objectives
1. Compute maximum likelihood estimates based on a model approapriate for the data. 
2. Address the multicollinearity issue in the potential predictors.
3. Utilize methods that prevent overfitting the model. 
4. Investigate methoods to improve accuracy during the cross validation procedure.

## Programming language and Necessary Packages
R/Rstudio was used to perform all methods. There are multiple packages required to run `Midterm_code.Rmd` to reproduce results. The following are the require packages:
- **dplyr**: for easy manipulation of data (often use to access `select()`, `mutate()`)
- **stat**: used to access the `cor()` function
- **FactoMineR**: used to perform PCA without manual coding (used to access `princomp()`)
- **utils**: used to read in the data (used to access `read.table()`)
- **nnet**: used to perform multinomial regression (used to access `multinom()`)
- **ggplot2**: for data visualization (used to access `ggplot()` and corresponding aesthetics and additional features)

## Methods
The outcome is split into two different categories and multiple categories for Task1 and Task2, respectively. The following is the baseline algorithm for both:
	(i) Depending on the Task, categorize the activity variable as described in the midterm Github repository. This will be referred to when evaluating the accuracy of my methods.
	(ii) To address (a), principal component analysis (PCA) is used to transform the training data. In the first step of PCA, the data set is typically standardized. However, the data appeared to be given in a standardized form.
	(iii) The covariance matrix of the dataset is then calculated, excluding the response variable and subject variable. 
	(iv) Using the covariance matrix of the features, the characteristic equation is used to retrieve eigenvalues and eigenvectors.
	(v) The eigenvalues are then sorted with their corresponding eigenvectors.
	(vi) The top 3 eigenvalues are chosen, and their corresponding eigenvectors are used to transform the original training data (only including the features).
	(vii) Using the transformed data and the corresponding responses logistic regression and multinomial regression are used to obtain model estimates for Task1 and Task2, respectively.
	(viii) Predictions are made using the training data. Steps (vii) is done as well for the testing data set using the trained eigenvectors.
	(ix) To test the accuracy for the training data set, the predictions are compared with the observed responses (# of correct predictions/ # of observations).

For the final algorithm of Task1 and Task2, the only change made was how many top eigenvalues are chosen (chose 7 for Task1 and chose 11 for Task2), which changes the number of eigenvectors used to transform the data, as described in problem 4 (vi). This results in a different number of transformed features used for step (vii) in problem 4 of this assignment. This is decided based on the proportions of variance obtained during PCA.


