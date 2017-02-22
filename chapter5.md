  ---
  title       : Experiments 5: Practice with Published Experiments - The Oregon Health Insurance Experiment
  description : These videos and exercises will allow you to practice skills used in analyzing experimental data
  attachments :
  video_link :


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:46fda452f0
## The Design of the Oregon Health Experiment.
*** =video_link
//player.vimeo.com/video/198212086

--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:47f92415c5
## Reading Average Treatment Effect & Confidence Intervals in a Table: Depression in the Oregon Health Experiment
*** =video_link
//player.vimeo.com/video/198212094


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:533b160157
## Multiple Choice: Significance
What is the difference between a statistically significant effect and a clinically (or "substantively") significant effect?

*** =instructions
- Statistically significant effects are bigger than clinically significant effects
- Statistically significant effects don't necessarily matter, whereas clinically significant effects do matter
- Statistically significant effects have smaller confidence intervals than clinically significant effects
- Statistically significant effects always matter, whereas clinically significant effects sometimes don't matter
*** =sct
```{r}
msg1 = "This might be true in some individual cases, but it's not true in general, so try again"
msg2 = "Correct! Statistical significance indicates whether an effect is real, but it does not necessarily indicate whether it is meaningful. With enough data, a study might find a statistically significant effect of season on people's preference to buy tissue paper, but the effect might not be important (for example, if people were 0.2% more likely to buy tissue paper in the spring over the fall)."
msg3 = "This might be true in some individual cases, but it's not true in general, so try again"
msg4 = "This is not how you should interpret treatment effects, so look again!"
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:0fa656dc08
## Practice Reading Tables (Part I)
Now let's practice reading tables from the Oregon Health Experiment. As described in the previous video, the Oregon Health Experiment studies the effect of getting Medicaid coverage on respondent's health, so let's look at some mental health results in the data.

The dataframe "OregonHealthResults" indicates results from the Oregon Health Experiment (in percentages) pertaining to depression, and to get a good sense of how this was affected in the experiment, you decide to review some results and then calculate some new numbers for yourself. 

One of the most interesting results of any experiment is the Average Treatment Effect relative to the mean value of a parameter. Therefore, With this dataframe, you decide to first look at two basic items: The average positive screen value in the control group, and the Average Treatment Effect of Medicaid on positive screen values. These calculations will give you a deeper sense of the impact of health insurance on basic mental health.


*** =instructions
- What is the mean value of positive screening in the control group?
- What is the average treatment effect of medicaid coverage on positive screening? 
- Given the mean value of positive screening in the control group and the average treatment effect of medicaid coverage on positive screening, estimate the mean value of positive screening in the treatment group.

*** =pre_exercise_code
```{r}
OregonHealth<-data.frame(c("Blood pressure - Systolic (mm Hg)","Blood pressure - Diastolic (mm Hg)","Blood pressure - Elevated (%)","Hypertension - Diagnosis after lottery (%)","Hypertension - Current use of medication for hypertension (%)","Cholesterol - Total level (mg/dl)","Cholesterol - High total level (%)","Cholesterol - HDL level (mg/dl)","Cholesterol - Low HDL level (%)","Hypercholesterolemia - Diagnosis after lottery (%)","Hypercholesterolemia - Current use of medication for high cholesterol level (%)","Glycated hemoglobin - Level (%)","Glycated hemoglobin - Level ???6.5% (%)","Diabetes - Diagnosis after lottery (%)","Diabetes - Current use of medication for diabetes (%)","Depression - Positive screening result (%)","Depression - Diagnosis after lottery (%)","Depression - Current use of medication for depression (%)","Framingham risk score - Overall","Framingham risk score - High-risk diagnosis","Framingham risk score - Age 50-65 yr"),
              c(119.3,76,16.3,5.6,13.9,204.1,14.1,47.6,28,6.1,8.5,5.3,5.1,1.1,6.4,30,4.8,16.8,8.2,11.6,13.9),
              c(-0.52,-0.81,-1.33,1.76,0.66,2.2,-2.43,0.83,-2.82,2.39,3.8,0.01,-0.93,3.83,5.43,-9.15,3.81,5.49,-0.21,1.63,-0.37),
              c(-2.97,-2.65,-7.16,-1.89,-4.48,-3.44,-7.75,-1.31,-10.28,-1.52,-0.75,-0.09,-4.44,1.93,1.39,-16.7,0.15,-0.46,-1.56,-1.11,-2.64),
              c(1.93,1.04,4.49,5.4,5.8,7.84,2.89,2.98,4.64,6.29,8.35,0.11,2.59,5.73,9.48,-1.6,7.46,11.45,1.15,4.37,1.9),
              c(0.68,0.39,0.65,0.34,0.8,0.45,0.37,0.45,0.46,0.23,0.1,0.82,0.61,0.001,0.008,0.02,0.04,0.07,0.76,0.24,0.75))
names(OregonHealth)<-c("Variable","Mean Value in Control Group","Change with Medicaid Coverage","95% Confidence Interval (lower bound)","95% Confidence Interval (Upper Bound)","P Value")
OregonHealthResults<-OregonHealth[16:18,]
OregonHealthResults$Variable<-c("Positive_Screening","Diagnosis_After_Lottery","Current_Use_Of_Medication")
rm(OregonHealth)
```
*** =sample_code
```{r}
str(OregonHealthResults) # Dataframe

print(Solution1<- ) # Write mean value of positive screening in the control group

print(Solution2<- ) # Write average treatment effect of medicaid coverage on positive screening

print(Solution3<- ) # Write mean value of positive screening in the treatment group

```

*** =solution
```{r}
print(Solution1<-OregonHealthResults[OregonHealthResults$Variable=="Positive_Screening",]$`Mean Value in Control Group`)
print(Solution2<-OregonHealthResults[OregonHealthResults$Variable=="Positive_Screening",]$`Change with Medicaid Coverage`)
print(Solution3<-Solution1+Solution2)

```

*** =sct
```{r}
test_object("Solution1")
test_object("Solution2")
test_object("Solution3")
success_msg("Good work!")
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:5fa7d35f25
## Practice Reading Tables (Part II)
Now that we know how an Average Treatment Effect is related to mean values in the treatment and control groups, we should examine the reliability of these results. Therefore, you decide to examine the 95% confidence interval lower bound, and statistical significance for one of the table's Average Treatment Effects.

*** =instructions
- What is the the 95% confidence interval lower bound for the treatment effect of medicaid coverage on current use of medication?
- Which average treatment effect of medicaid coverage on depression was not statistically significant? You can write this out as a line of text.

*** =pre_exercise_code
```{r}
OregonHealth<-data.frame(c("Blood pressure - Systolic (mm Hg)","Blood pressure - Diastolic (mm Hg)","Blood pressure - Elevated (%)","Hypertension - Diagnosis after lottery (%)","Hypertension - Current use of medication for hypertension (%)","Cholesterol - Total level (mg/dl)","Cholesterol - High total level (%)","Cholesterol - HDL level (mg/dl)","Cholesterol - Low HDL level (%)","Hypercholesterolemia - Diagnosis after lottery (%)","Hypercholesterolemia - Current use of medication for high cholesterol level (%)","Glycated hemoglobin - Level (%)","Glycated hemoglobin - Level ???6.5% (%)","Diabetes - Diagnosis after lottery (%)","Diabetes - Current use of medication for diabetes (%)","Depression - Positive screening result (%)","Depression - Diagnosis after lottery (%)","Depression - Current use of medication for depression (%)","Framingham risk score - Overall","Framingham risk score - High-risk diagnosis","Framingham risk score - Age 50-65 yr"),
              c(119.3,76,16.3,5.6,13.9,204.1,14.1,47.6,28,6.1,8.5,5.3,5.1,1.1,6.4,30,4.8,16.8,8.2,11.6,13.9),
              c(-0.52,-0.81,-1.33,1.76,0.66,2.2,-2.43,0.83,-2.82,2.39,3.8,0.01,-0.93,3.83,5.43,-9.15,3.81,5.49,-0.21,1.63,-0.37),
              c(-2.97,-2.65,-7.16,-1.89,-4.48,-3.44,-7.75,-1.31,-10.28,-1.52,-0.75,-0.09,-4.44,1.93,1.39,-16.7,0.15,-0.46,-1.56,-1.11,-2.64),
              c(1.93,1.04,4.49,5.4,5.8,7.84,2.89,2.98,4.64,6.29,8.35,0.11,2.59,5.73,9.48,-1.6,7.46,11.45,1.15,4.37,1.9),
              c(0.68,0.39,0.65,0.34,0.8,0.45,0.37,0.45,0.46,0.23,0.1,0.82,0.61,0.001,0.008,0.02,0.04,0.07,0.76,0.24,0.75))
names(OregonHealth)<-c("Variable","Mean Value in Control Group","Change with Medicaid Coverage","95% Confidence Interval (lower bound)","95% Confidence Interval (Upper Bound)","P Value")
OregonHealthResults<-OregonHealth[16:18,]
OregonHealthResults$Variable<-c("Positive_Screening","Diagnosis_After_Lottery","Current_Use_Of_Medication")
rm(OregonHealth)
```
*** =sample_code
```{r}
str(OregonHealthResults) # Dataframe

print(Solution1<- ) # Write the 95% confidence interval lower bound for the treatment effect of medicaid coverage on current use Of medication

print(Solution2<-"") # Write name of variable whose average treatment effect was not statistically significant

```

*** =solution
```{r}
print(Solution1<-OregonHealthResults[OregonHealthResults$Variable=="Current_Use_Of_Medication",]$`95% Confidence Interval (lower bound)`)
print(Solution2<-OregonHealthResults[OregonHealthResults$`P Value`>.05,]$Variable)

```

*** =sct
```{r}
test_object("Solution1")
ex() %>% check_output('"[C|c]urrent.*"',
missing_msg = "Solution2 is incorrect. Please write out your answer. Make sure it is in string format and printed in the console") 
success_msg("Good work!")
```
--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:743f5494ef
## A Note on Heteroskedasticity
*** =video_link
//player.vimeo.com/video/205124690

--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:6a474387e6
## Reading Average Treatment Effect & Confidence Intervals in a Table: Cholesterol in the Oregon Health Experiment
*** =video_link
//player.vimeo.com/video/198212098


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:5765daa781
## Multiple Choice: Interpreting effect sizes
The head of marketing at Bizer, Inc. is trying to decide whether to include a new cholesterol medicine's average treatment effect in the company's advertisements for that medicine. He knows that on average, the medicine reduces cholesterol in respondents by about 1mg/dL and knows that the effect is statistically different from zero. However, he's not sure whether that number is large or small; that is, whether the medicine's average treatment effect is worth advertising. 

If cholesterol is highly variable in the population (about 70% of the population has cholesterol between 160mg/dL and 240mg/dL), does an average treatment effect of 1mg/dL seem relatively small or relatively large? In other words, when an average treatment effect is substantially smaller than the standard error of the mean for a parameter, how would we tyipcally interpret the size of that average treatment effect?


*** =instructions
- The average treatment effect is large
- The average treatment effect is small
*** =sct
```{r}
msg1 = "Although a 1mg/dL reduction in cholesterol is statistically significant and might be substantial for some members of the population, it is not a very large reduction relative to the amount of variance in cholesterol in the population. Try again."
msg2 = "Correct! When an average treatment effect is small relative to the standard error of a sample mean, it suggests that the average treatment effect is small, relative to the amount of variance typically found in that parameter. This thought process is especially helpful when deciding if an estimated effect is clinically significant (even if it is statistically significant)."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:82150d848b
## Practice working with the Oregon Health Experiment
Let's say you're wondering how much mens' and womens' health differed in the experiment, and what the data says about Medicaid's effects on those differences, so you decide to look at some of the basic health numbers in the data. A simulated version of the Oregon Health Insurance Experiment data, `OHIE`, is available in the workspace. With this dataframe, you make some quick calculations to learn about any differences that might be linked to gender by looking at:

*** =instructions
- Test if there is a statistically significant difference in gender between the treament and control groups (i.e. whether gender is balanced between the treatment and control group). 
- Determine if the treatment and control groups have significantly different average values for the following health outcomes: systolic blood pressure (variable `bp_sar_inp`), and diastolic blood pressure (variable `bp_dar_inp`).

*** =hint
- For the first question, you will need to `subset` the `OHIE` data frame by treatment. 
- It may help to create a new dataframe called `TreatmentGroup` that contains only WePhones in the treatment group, and a new data frame called `ControlGroup` that contains only WePhones in the control group.
- For each of the following questions, use the `t.test` function where (mu=0) to statistically test whether the treatment and control group are different from each other.


*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
OHIE <- OHIE[!is.na(OHIE$treatment),c("id","treatment","gender_inp","bp_sar_inp","bp_dar_inp")]

```

*** =sample_code
```{r}
str(OHIE) #Dataframe

print(Solution1a<- ) # Use a t.test to determine whether gender is balanced between the treatment and control groups 

print(Solution1b<-"" ) # Based on your t.test, is gender balanced? Answer with "Yes" or "No" 

print(Solution2a<- ) # Use a t.test to determine if the treatment had a statistically significant effect on systolic blood pressure 

print(Solution2b<-"" ) # Based on your t.test, does the treatment have a statistically significant effect on systolic blood pressure? Answer with "Yes" or "No" 

print(Solution3a<- ) # Use a t.test to determine if the treatment had a statistically significant effect on diastolic blood pressure 

print(Solution3b<-"" ) # Based on your t.test, does the treatment have a statistically significant effect on diastolic blood pressure? Answer with "Yes" or "No" 

```

*** =solution
```{r}
TreatmentGroup <- OHIE[OHIE$treatment==1, ]
ControlGroup <- OHIE[OHIE$treatment==0, ]
print(Solution1a<- t.test(TreatmentGroup$gender_inp,ControlGroup$gender_inp,mu=0))
print(Solution1b<-"Yes")
print(Solution2a<- t.test(TreatmentGroup$bp_sar_inp,ControlGroup$bp_sar_inp,mu=0))
print(Solution2b<-"No")
print(Solution3a<- t.test(TreatmentGroup$bp_dar_inp,ControlGroup$bp_dar_inp,mu=0))
print(Solution3b<-"Yes")

```

*** =sct
```{r}
test_object("Solution1a")
test_object("Solution1b")
test_object("Solution2a")
test_object("Solution2b")
test_object("Solution3a")
test_object("Solution3b")

success_msg("Good work!")
```



--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:4f3ebb92a2
## Practice working with eGulf
To increase their commissions, the popular online auctioneer, eGulf, wants to help its sellers increase the final sales prices of their merchandise. For each auction on eGulf, sellers are allowed to post up to 10 pictures of an item that they are selling. Past studies suggest that customer's appraisals of merchandise (and subsequently, final bids of merchandise) improve when sellers include more pictures of their merchandise; therefore, eGulf considers raising the number of pictures that a seller can post on an auction's webpage. 

To test whether eGulf should allow sellers to post more than 10 pictures of their items, eGulf conducts an experiment: eGulf finds a random sample of dedicated used WePhone sellers that typically post 10 pictures of their used WePhones, and temporarily allows them to post up to 15 pictures for each auction of their WePhones. Using the results of this experiment, listed in dataset `eGulf`, test whether there is an added benefit to posting more than 10 pictures on WePhone auctions. Specifically:

*** =instructions
- Statistically test whether sellers who posted more than 10 pictures (`Seller_Opted_Into_Treatment`==1) on their WePhone auctions (`Final_Sales_Price`) sold their WePhones at higher prices than sellers who posted 10 or less pictures on their WePhone auctions (`Seller_Opted_Into_Treatment`==0)

*** =hint
- For the first question, you will need to `subset` the `eGulf` data frame by treatment. 
- It may help to create a new dataframe called `TreatmentGroup` that contains only WePhones in the treatment group, and a new data frame called `ControlGroup` that contains only WePhones in the control group.
- Use the `t.test` function where (mu=0) to statistically test whether the treatment and control group are different from each other.

*** =pre_exercise_code
```{r}
# Initialize dataframe
set.seed(1)
n <- 1000
eGulf <- as.data.frame(matrix(0, ncol=5,nrow=n))
colnames(eGulf) <- c("Seller_Offered_Treatment","Seller_Opted_Into_Treatment","Seller_Feedback_Count","Seller_Feedback_Score","Auction_Final_Sales_Price")
# Simulate baseline data
  # Make seller feedback count
    eGulf$Seller_Feedback_Count<-as.integer(abs(round(rnorm(n,200,100))))
  # Make feedback score loosely correlated with feedback count 
    eGulf$Seller_Feedback_Score<-round(.9+.1*eGulf$Seller_Feedback_Count/max(eGulf$Seller_Feedback_Count)-rbeta(100,1,10),2)
  # Make seller offered treatment loosely correlated with with feedback count 
    eGulf$Seller_Offered_Treatment<-rbinom(n,1,.5+eGulf$Seller_Feedback_Count/max(eGulf$Seller_Feedback_Count)/5)
  # Make seller opted_into_treatment correlated with seller_feedback_score
    eGulf$Seller_Opted_Into_Treatment<-ifelse(eGulf$Seller_Offered_Treatment==0,0,rbinom(n,1,eGulf$Seller_Feedback_Score^5)) #
  # Make final sales price also correlated with seller_feedback_score
    eGulf$Final_Sales_Price<-round(rlnorm(n, meanlog=log(400), sdlog = log(1.2))*eGulf$Seller_Feedback_Score)
```
*** =sample_code
```{r}
str(eGulf) #Dataframe
Solution1<- # Use a t.test to determine whether opting into treatment (i.e. posting more than 10 pictures) increased final sales prices
```
*** =solution
```{r}
Solution1<-t.test(eGulf$Final_Sales_Price[eGulf$Seller_Opted_Into_Treatment==1],eGulf$Final_Sales_Price[eGulf$Seller_Opted_Into_Treatment==0])
```
*** =sct
```{r}
test_object("Solution1")
success_msg("Good work! It looks like posting more photos was positively associated with final WePhone sales prices.")
```
--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:ad358b17bb
## Where the Chapter Will Go From Here
*** =video_link
//player.vimeo.com/video/205124618
