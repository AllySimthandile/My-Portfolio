This code demonstrates how to build a logistic regression model to predict whether an individual's income exceeds $50K/year using the Adult UCI dataset. The process includes data loading, model training, and evaluating the model's performance on a test dataset using a confusion matrix.

2. Dataset Overview
The Adult Income Dataset contains demographic information (such as age, education, marital status, occupation, etc.) about individuals. The goal is to predict whether a person earns more than $50K based on these features.

Target Variable (class): The dependent variable indicating whether an individual earns more than $50K/year.
>50K: Income greater than $50K.
<=50K: Income less than or equal to $50K.
The dataset is divided into:

Training data: Used to train the model.
Test data: Used to evaluate the model's performance.
3. Setup Instructions
Before starting, ensure that you have the following:

R Installed: Download and install R from CRAN.
RStudio (optional): A more user-friendly IDE for working with R.
Download the Adult UCI Dataset:
Training data: adult.data
Test data: adult.test
4. Data Preparation
1. Load the Data
You will need to load the training and test data into R using the read.csv() function. Specify the file paths where you saved the data.

r
Copy code
# Load the training data
adult.training <- read.csv("C:/Users/jenst/Downloads/adult.data", header=FALSE)

# Load the test data
adult.test <- read.csv("C:/Users/jenst/Downloads/adult.test", header=FALSE)
2. Create a Binary Response Variable
The dependent variable y will be created based on the target column in the training data. We will set y = 1 for individuals earning more than $50K and y = 0 for others.

r
Copy code
# Create binary response variable for training data
N.obs <- dim(adult.training)[1]  # Number of observations
y <- rep(0, N.obs)
y[adult.training$class == ">50K"] <- 1
3. Explore the Dataset
Before proceeding, it's a good idea to explore the data using basic summary functions.

r
Copy code
# Get a summary of the training dataset
summary(adult.training)

# Get the column names
names(adult.training)

# View the first few rows of the training data
head(adult.training)
5. Model Building
We will build a logistic regression model using the glm() function in R. The independent variables include age, education level, marital status, occupation, and others.

r
Copy code
# Create the logistic regression model
adultdatamodel <- glm(y ~ age + educationnum + hoursperweek + workclass + maritalstatus + occupation + relationship + race + sex, 
                      family = binomial("logit"), data = adult.training)
1. View the Model Coefficients
After fitting the model, examine the coefficients to understand the relationship between the predictor variables and the target variable.

r
Copy code
# Get the coefficients of the fitted model
resultstable <- summary(adultdatamodel)$coefficients

# Sort the coefficients by p-value
sorter <- order(resultstable[, 4])
resultstable <- resultstable[sorter, ]
6. Prediction and Evaluation
1. Make Predictions on the Test Data
Once the model is trained, you can use it to make predictions on the test data.

r
Copy code
# Predict the probabilities on the test data
pred <- predict(adultdatamodel, adult.test, type = "response")
N.test <- length(pred)  # Number of test observations
2. Apply Threshold to Predictions
We use a threshold of 0.5 to classify the predictions as either >50K (1) or <=50K (0).

r
Copy code
# Classify the predictions based on the threshold (0.5)
y.hat <- rep(0, N.test)
y.hat[pred >= 0.5] <- 1
3. Compare Predictions with True Labels
Create the actual labels for the test dataset and compare them with the predicted values to evaluate the model.

r
Copy code
# Get the true outcome of the test data
outcome <- levels(adult.test$class)
y.test <- rep(0, N.test)
y.test[adult.test$class == outcome[2]] <- 1

# Create a confusion matrix
confusion.table <- table(y.hat, y.test)

# Add meaningful labels to the confusion matrix
colnames(confusion.table) <- c(paste("Actual", outcome[1]), outcome[2])
rownames(confusion.table) <- c(paste("Predicted", outcome[1]), outcome[2])

# Display the confusion matrix
print(confusion.table)
7. Visualizing Results
The confusion matrix shows the number of correct and incorrect predictions made by the model. This can be used to calculate key performance metrics such as accuracy, precision, recall, and F1-score.

8. Conclusion
This process demonstrates how to build and evaluate a logistic regression model for predicting adult income levels using the Adult UCI dataset. By following these steps, you can predict whether an individual earns more than $50K/year based on demographic features, and evaluate the model's performance using a confusion matrix.

For further analysis, you can experiment with different features, apply different machine learning algorithms, or tune the model’s hyperparameters for better performance.

Code Summary
r
Copy code
# Load training and test data
adult.training <- read.csv("C:/Users/jenst/Downloads/adult.data", header=FALSE)
adult.test <- read.csv("C:/Users/jenst/Downloads/adult.test", header=FALSE)

# Create binary response variable
y <- rep(0, dim(adult.training)[1])
y[adult.training$class == ">50K"] <- 1

# Build logistic regression model
adultdatamodel <- glm(y ~ age + educationnum + hoursperweek + workclass + maritalstatus + occupation + relationship + race + sex, 
                      family = binomial("logit"), data = adult.training)

# Get model coefficients
resultstable <- summary(adultdatamodel)$coefficients
sorter <- order(resultstable[, 4])
resultstable <- resultstable[sorter, ]

# Make predictions on the test data
pred <- predict(adultdatamodel, adult.test, type = "response")
N.test <- length(pred)

# Apply threshold for prediction success
y.hat <- rep(0, N.test)
y.hat[pred >= 0.5] <- 1

# Create confusion matrix
outcome <- levels(adult.test$class)
y.test <- rep(0, N.test)
y.test[adult.test$class == outcome[2]] <- 1
confusion.table <- table(y.hat, y.test)
colnames(confusion.table) <- c(paste("Actual", outcome[1]), outcome[2])
rownames(confusion.table) <- c(paste("Predicted", outcome[1]), outcome[2])
print(confusion.table)