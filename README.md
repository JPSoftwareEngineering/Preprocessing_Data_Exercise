# Preprocessing_Data_Exercise

## Importing the Data Set

**data = read.csv("Data.csv")**

## Taking Care of Missing Data

**data$Auto = ifelse(is.na(data$Age), mean(data$Age, na.rm = TRUE), data$Age)**

Parameters:

1. First parameter is the condition.
2. What to do when the condition is true.
3. What to do when the condition is false.

is.na checks if there is a missing value or not in the specified data set vector.

is.na checks if there is a missing value or not in the specified data set vector.

na.rm refers to the logical parameter that tells the function whether or not to remove NA values from the calculation. It literally means NA remove and is a parameter not a function.

we do this again for salary column:

**data$Salary = ifelse(is.na(data$Salary), mean(data$Salary, na.rm = TRUE), data$Salary)**

## Working with Categorical Data

To categorise data in R, we make our category data column into a column of factors.

**data$Country = factor(data$Country, levels = c("France", "Spain", "Germany"), labels = c(1, 2, 3))**

The c function returns a vector.

We use labels to assign numbers in order to the vector in levels.

We also do this for the purchased column:

**data$Purchased = factor(data$Purchased, levels = c("No", "Yes"), labels = c(0, 1))**

## Splitting the Data Set into Training and Test Data Sets

**install.packages("caTools")**
**library(caTools)**
**set.seed(123)**

**split = sample.split(data$Purchased, SplitRatio = 0.8)**

Parameters:

1. The response variable.
2. The ratio for the training data set.

What sample.split does is return a vector of true or false values for each of your observations, true being the observation is part of the training data set and false it is not.

**training = subset(data, split == TRUE)**
**test = subset(data, split == FALSE)**

## Feature Scaling

Feature scaling is a method used to normalise the range of independent variables or features of data. Normalisation means adjusting values measured on different scales to a notionally common scale, often prior to averaging.

training = scale(training)
test = scale(test)

One thing to note is that all the data in x, i.e. the data set passed in as the parameter, needs to be numerical. Now, remember that we transformed our categorical data into factors, which are not numerical in R, they are objects. So in this case we would not scale our factors, just the columns with numerical data in them, which in our case would be columns two and three:

**training[, 2:3] = scale(training[, 2:3])**
**test[, 2:3] = scale(test[, 2:3])**

So the scale function, with default settings, will calculate the mean and standard deviation of the entire vector, then "scale" each element by those values by subtracting the mean and dividing by the sd (if you use scale(x, scale=FALSE), it will only subtract the mean but not divide by the std deviation). Basically, the data is normalised to the number of sd away from the mean.
