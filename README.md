# Projects
Data Science Project - Diabetes Prediction Model building 
```{r}
# Load necessary libraries
library(readr)
library(ISLR)
```
```{r}
# Load the dataset
data<-read.csv("diabetes_prediction_dataset.csv")

```
```{r}
# Display the first few rows of the data
head(data)
```
```{r}
# Split the data into training and testing sets
set.seed(42) 
sample <- sample.int(n = nrow(data), size = floor(0.8 * nrow(data)), replace = FALSE)
train <- data[sample, ]
test <- data[-sample, ]
```

```{r}
# Fit the GLM model with binomial family
model <- glm(diabetes ~ ., data = train, family = binomial())
```
```{r}
# Summary of the model
summary(model)
```
```{r}
# Make predictions on the test set
predictions <- predict(model, newdata = test, type = "response")
```
```{r}
# Convert probabilities to binary outcomes
predicted_classes <- ifelse(predictions > 0.5, 1, 0)
```
```{r}
# Evaluate the model
conf_matrix <- table(test$diabetes, predicted_classes)
accuracy <- sum(diag(conf_matrix)) / sum(conf_matrix)
```
```{r}
print("Confusion Matrix:")
print(conf_matrix)
print(paste("Accuracy:", round(accuracy, 4)))
```
