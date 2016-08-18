---
title       : Getting to know your data
description : This exercise helps you get to know your data better
attachments :
  video_link : https://www.youtube.com/watch?v=P5M7ptDor6w

--- type:NormalExercise lang:r xp:100 skills:1 key:1ecca31bfa
## Intro to analyzing experimental data

Data from the Oregon Health Insurance Experiment, `OHIE`, is available in the workspace.

In this exercise, you will be performing statistical tests to see if patients who received health insurance reported improved health outcomes 12 months after being granted access.

*** =instructions
- Examine the structure of `OHIE`
- Subset the `OHIE` data frame into treatment and control groups
- The treatment variable is a column in `OHIE` called `treatment`
- Call the treatment group `trmt` and the control group `ctrl`. 

*** =hint
- Use `str()` to examine the structure of the data

*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
OHIE <- OHIE[!is.na(OHIE$treatment),c("id","treatment","gender_inp","age_19_34_inp","age_35_49_inp","age_50_64_inp")]
```

*** =sample_code
```{r}
# OHIE is available in your workspace

# Check out the structure of OHIE


# Create a new data frame called `trmt` that contains only treated individuals 


# Create a new data frame called `ctrl` that contains only control individuals 

```

*** =solution
```{r}
# OHIE is available in your workspace

# Check out the structure of OHIE
str(OHIE)

# Create a new data frame called `trmt` that contains only treated individuals 
trmt <- OHIE[OHIE$treatment==1, ]

# Create a new data frame called `ctrl` that contains only control individuals 
ctrl <- OHIE[OHIE$treatment==0, ]
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("trmt")

test_object("ctrl")

test_error()

success_msg("Good work!")
```
