---
title: "M8 SPAM Example"
author: "Salimah Mokhtar"
date: "December 16, 2015"
output: html_document
---

## Load library, ensure e1071 is also installed
```{r}
library(caret)
library(kernlab)
```

## Split data into training and test set
```{r}
data(spam)
inTrain <- createDataPartition(y=spam$type, p=0.75, list=FALSE) #75% training
training <- spam[inTrain, ] 
testing <- spam[-inTrain, ]
dim(training) # 3451 training, 58 testing, dim returns dimension of training
set.seed(32343) # ensure similar seed to get reproducible results when try on your own
```

## Fitting phase using a Generalized Linear Model (glm)
```{r}
modelFit <- train(type ~ ., data=training, method="glm")
modelFit
```

## Final model
```{r}
modelFit$finalModel # gives predictions vector
```

## Predictions on testing data
```{r}
predictions <- predict(modelFit, newdata=testing) 
predictions
```

## Evaluate prediction using error measures 
```{r}
confusionMatrix(predictions, testing$type)
```

