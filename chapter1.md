  ---
  title       : Introduction to Experiments
  description : This exercise helps you get to know your data better
  attachments :
  video_link :


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1
## Controlled Experiments
*** =video_link
//player.vimeo.com/video/198212077

--- type:MultipleChoiceExercise lang:r xp:50 skills:1
## Problem 1
Laurel wants to know which phone is more durable: The WePhone 10S or the Universe S10. To determine which phone is more durable, he buys one of each phone and tests how much force is needed to crush each phone with his hydraulic press. Assuming that each phone is made exactly according to specification and that each phone is tested under exactly the same condition, would this controlled experiment be able to determine which phone is more durable?

*** =instructions
- Yes
- No
*** =sct
```{r}
msg1 = "Correct, if all experimental conditions between the phones are identical (i.e. if all other factors that could influence the outcome are controlled for) only two observations are needed to determine whether there is a causal effect between the treatment (phone type) and outcome (durability)"
msg2 = "Try again"
test_mc(correct = 1, feedback_msgs = c(msg1,msg2))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1
## Problem 2
Laurel's experiment determines that the WePhone 10S is more durable than the Universe S10. Laurel is now interested in what factors caused the WePhone 10S to be more durable than the Universe S10. Laurel examines the model specifications of each phone, and incorrectly assumes that whichever specification is most different between the phones is the cause of their different durabilities.
*** =instructions
- Examine the provided phone specifications in dataframe`PhoneSpecifications` and name the specification that has the `largest ratio` between the WePhone 10S and the Universe S10
- What is the `size` of this ratio (expressed as a quotient)?
*** =pre_exercise_code
```{r}
PhoneSpecifications<-data.frame(WePhone10S=c(190,4000,5.5,64,800),UniverseS10=c(180,3500,5.2,64,550))
row.names(PhoneSpecifications)<-c("Weight (g)","Battery Capacity (mAh)","Diagonal Length (in)","Storage (Gb)","Luminance (cd/m2)")
PhoneSpecifications<-t(PhoneSpecifications)
```
*** =sample_code
```{r}
PhoneSpecifications #Dataframe

print(Solution1<-" "  ) #Write column name of specification with the largest ratio between the WePhone 10S and the Universe S10

print(Solution2<-     ) #Write quotient of phone specifications selected in Solution1

```
*** =solution
```{r}
#loop through specification ratios to find max ratio
Ratios<-vector(length=5)
for(i in 1:length(PhoneSpecifications[1,])){
Ratios[i]<-PhoneSpecifications[1,i]/PhoneSpecifications[2,i]
}
print(Solution1<-dimnames(PhoneSpecifications)[[2]][match(max(Ratios),Ratios)])

print(Solution2<-max(Ratios))

```
*** =sct
```{r}
#I use regular expressions to allow for multiple spellings of answers. 

ex() %>% check_output('"[L|l]uminance+?"',
missing_msg = "Solution1 is incorrect. Make sure it is in string format and printed in the console") 

ex() %>% check_output("1.45+?",
missing_msg = "Solution2 is incorrect. Make sure to divide the WePhone10S's specification by the UniverseS10's specification")

success_msg("Good work! Keep in mind, even though there is a correlation between the treatment (luminance) and outcome (durability), this correlation is spurious; in reality, a phone's luminance (brightness) does not have a causal effect on its durability.
")
```


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1
## Randomized Experiments
*** =video_link
//player.vimeo.com/video/198212082


--- type:MultipleChoiceExercise lang:r xp:50 skills:1
## Problem 3
Laurel is now interested in determining whether the WePhone 10S is more bendable than the Universe S10. He tests this by having four of his friends try to bend one of the two phones for a duration of 1 minute each. Two of his friends really want to try to bend the Universe S10, so Laurel assigns those two friends to bend the Universe S10, whereas his other two friends are assigned to trying to bend the WePhone 10S. He finds that the average treatment effect of the WePhone 10S on bendability is -2 degrees (i.e. on average, his friends bent the WePhone 10S 2 degrees less less than his friends bent the Universe S10). Of the following, which is the most problematic design error in this experiment?


*** =instructions
- Noncompliance
- Ethics
- Random assignment
- Data visualization

*** =sct
```{r}
msg1 = "Try again"
msg2 = "Try again"
msg3 = "Correct, Laurel's friends were not randomly assigned to each treatment. Instead, he assigned them based on their own preferences, which could lead to confounded results."
msg4 = "Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1
## Problem 4
If Laurel was interested in what proportion of the U.S. population could bend a WePhone 10S with their hands, which group would serve as a better sample?


*** =instructions
- Perfect strangers in Laurel's neighborhood
- Perfect strangers across the world
- Perfect strangers in Laurel's town
- Perfect strangers across the U.S.

*** =sct
```{r}
msg1 = "Try again"
msg2 = "This answer may be tempting, but Laurel wants a sample that is reflective of the U.S. population"
msg3 = "Try again"
msg4 = "Correct"
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```
