---
title: "ANA 515 Assignment 2"
author: "Melissa Jayawardane"
output: word_document
date: "2023-06-13"
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE,message = FALSE,warning = FALSE)
```

## Section 1
The gathered data in this dataset provides tremendous value to those seeking knowledge regarding job salaries within the domain of data science. The compiled information includes vast amounts of detail about various facets of salary payment across sectors like work year, experience level and employment type - all critical indicators of earning potential. Any potential user could analyze this comprehensive table's rows and columns - 11 columns to be exact - which breaks down everything from job title to remote work allowances amongst various companies across countless industries. Of note, this abundant repository's CSV file format affords those interested ease-of-use flexibility -the ability to hash-out relevant figures- via specialized software packages available in several modern programming languages like R.

## Section 2
```{r Loading Data}
# Read the dataset into R using read.csv() function
df<-read.csv("C:/Users/user/Documents/ds_salaries.csv") 
```

## Section 3
```{r Data Cleaning}
# Load the required packages
library(tidyverse)
library(knitr)
library(dplyr)
library(kableExtra)
# Rename columns
df <- df %>%
  rename(year = work_year,
         experience_level = experience_level,
         employment = employment_type,
         job_title = job_title,
         salary = salary,
         currency = salary_currency,
         salary_usd = salary_in_usd,
         employee_residence = employee_residence,
         remote_ratio = remote_ratio,
         company_location = company_location,
         company_size = company_size)

# Subset to keep at least 4 columns
sub_df <-  df %>%
  select(year, experience_level, job_title, salary, remote_ratio, salary_usd)
```

## Section 4
This dataframe has `r nrow(sub_df)` rows and `r ncol(sub_df)` columns. The names of the columns and a brief description of each are in the table below
```{r}


# Define the column names and descriptions as a data frame
column_description <- data.frame(Column = colnames(sub_df), Description = c("The year the salary was paid",
                                                                        "The experience level in the job",
                                                                        "The job title",
                                                                        "The total gross salary amount",
                                                                        "The overall amount of work done remotely",
                                                                        "The salary in USD"))
# Display the table
knitr::kable(column_description, format = "markdown", col.names = c("Column", "Description")) 
```

## Section 5
```{r Summary Statistics}
# Select three columns
selected_columns <- sub_df[, c("remote_ratio", "salary_usd", "salary")]
names(sub_df)
# Calculate summaries for each column
summary_data <- summary(selected_columns)
min_values <- sapply(selected_columns, min, na.rm = TRUE)
max_values <- sapply(selected_columns, max, na.rm = TRUE)
mean_values <- sapply(selected_columns, mean, na.rm = TRUE)
num_missing <- sapply(selected_columns, function(x) sum(is.na(x)))

# Assign the summaries to a new object
column_summaries <- data.frame(Column = colnames(selected_columns),
                               Minimum = min_values,
                               Maximum = max_values,
                               Mean = mean_values,
                               "Number of Missing Values" = num_missing)

# Display the column summaries
column_summaries
```
