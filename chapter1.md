---
title       : Getting to know your data
description : This exercise helps you get to know your data better
attachments :
  video_link : https://www.youtube.com/watch?v=P5M7ptDor6w

--- type:NormalExercise lang:r xp:100 skills:1 key:1ecca31bfa
## Intro to analyzing experimental data

Data from the Oregon Health Insurance Experiment, `OHIE`, is available in the workspace.

In this exercise, you will be manipulating the data by dividing it into a treatment group and control group for future analysis.

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


--- type:NormalExercise lang:r xp:100 skills:1
## Testing for balancedness across experimental groups

Data from the Oregon Health Insurance Experiment, `OHIE`, is available in the workspace. This has been divided into two separate dataframes: `trmt` and `ctrl` denoting the treatment and control groups, respectively.

In this exercise, you will be comparing means of demographic variables to see if the group of patients who did and did not receive health insurance have the same characteristics

*** =instructions
- Test that the treatment and control groups have the same average values for the following characteristics: 
- gender (variable `gender_inp`)
- age in 19-34 (variable `age_19_34_inp`)
- age in 35-49 (variable `age_35_49_inp`)
- age in 50-64 (variable `age_50_64_inp`)
- white (variable `race_white_inp`)
- black (variable `race_black_inp`)
- hispanic (variable `hispanic_inp`)

*** =hint
- Use `mean(x)-mean(y)` to compute the difference in the means of two vectors `x` and `y`
- For vectors that belong to different dataframes, use the $ to call the variable, e.g. `mean(df1$x)-mean(df2$x)` 

*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
OHIE <- OHIE[!is.na(OHIE$treatment),c("id","treatment","gender_inp","age_19_34_inp","age_35_49_inp","age_50_64_inp","race_white_inp","race_black_inp","hispanic_inp")]
trmt <- OHIE[OHIE$treatment==1 & !is.na(OHIE$treatment),]
ctrl <- OHIE[OHIE$treatment==0 & !is.na(OHIE$treatment),]
rm(OHIE)
```

*** =sample_code
```{r}
# trmt and ctrl are both available in your workspace

# Compute the mean difference in the proportion female (gender_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion between ages of 19-34 (age_19_34_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion between ages of 35-49 (age_35_49_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion between ages of 50-64 (age_50_64_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion white (race_white_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion black (race_black_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion hispanic (hispanic_inp==1) in the treatment and control groups


```

*** =solution
```{r}
# trmt and ctrl are both available in your workspace

# Compute the mean difference in the proportion female (gender_inp==1) in the treatment and control groups
mean(trmt$gender_inp)-mean(ctrl$gender_inp)

# Compute the mean difference in the proportion between ages of 19-34 (age_19_34_inp==1) in the treatment and control groups
mean(trmt$age_19_34_inp)-mean(ctrl$age_19_34_inp)

# Compute the mean difference in the proportion between ages of 35-49 (age_35_49_inp==1) in the treatment and control groups
mean(trmt$age_35_49_inp)-mean(ctrl$age_35_49_inp)

# Compute the mean difference in the proportion between ages of 50-64 (age_50_64_inp==1) in the treatment and control groups
mean(trmt$age_50_64_inp)-mean(ctrl$age_50_64_inp)

# Compute the mean difference in the proportion white (race_white_inp==1) in the treatment and control groups
mean(trmt$race_white_inp)-mean(ctrl$race_white_inp)

# Compute the mean difference in the proportion black (race_black_inp==1) in the treatment and control groups
mean(trmt$race_black_inp)-mean(ctrl$race_black_inp)

# Compute the mean difference in the proportion hispanic (hispanic_inp==1) in the treatment and control groups
mean(trmt$hispanic_inp)-mean(ctrl$hispanic_inp)

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("mean", args = "object",
              not_called_msg = "You didn't call `mean()`!",
              incorrect_msg = "You didn't call `mean(object = ...)` with the correct argument, `object`.")

test_error()

success_msg("Good work!")
```
