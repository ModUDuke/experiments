  ---
  title       : Introduction to Experiments
  description : This exercise helps you get to know your data better
  attachments :
  video_link :


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:4745db858e
## Controlled Experiments
*** =video_link
//player.vimeo.com/video/198212077

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:ebe90c9c16
## Problem 1
Laurel cracked the screen on her old phone, and her next phone choice will be based on which is more durable: the WePhone 10S or the Universe S10. She looks at a YouTube channel that buys one of each phone and tests how much force is needed to crush each phone with a hydraulic press. If every WePhone or Universe is identical from the factory, and if the phones are tested under exactly the same condition, is just one crushing test enough to determine durability?

*** =instructions
- Yes
- No
*** =sct
```{r}
msg1 = "Correct, only two observations are needed to determine whether there is a causal effect between the treatment (phone type) and outcome (durability if all experimental conditions between the phones are identical (i.e. If all other factors that could influence the outcome are controlled for). That's assuming you think a crush test is a valid one for determining real-world durability, of course!"
msg2 = "Try again"
test_mc(correct = 1, feedback_msgs = c(msg1,msg2))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:e157142b3a
## Problem 2
Laurel's video showed that the WePhone 10S was stronger than the Universe S10. Laurel is now interested in what factors caused the WePhone 10S to be more durable than the Universe S10. Laurel examines the model specifications of each phone, and assumes that whichever specification is most different between the phones is the cause of their different durabilities.

*** =instructions
- Examine the provided phone specifications in dataframe`PhoneSpecifications` and identify the specification that has the `largest ratio` between the WePhone 10S and the Universe S10
- In the console window, a.) write out the `name` that specification, and b.) write out the `size` of this ratio (expressed as a quotient)
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
missing_msg = "Solution1 is incorrect. Please write out your answer. Make sure it is in string format and printed in the console") 

ex() %>% check_output("1.45+?",
missing_msg = "Solution2 is incorrect. Make sure to divide the WePhone10S's specification by the UniverseS10's specification")

success_msg("Good work! Keep in mind, even though there is a correlation between the treatment (luminance) and outcome (durability), this correlation is spurious; in reality, a phone's luminance (brightness) does not have a causal effect on its durability.
")
```


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:9e9326a35b
## Randomized Experiments
*** =video_link
//player.vimeo.com/video/198212082


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:243af9a90f
## Problem 3
Laurel is wondering if it would be more realistic to test phone durability through a bending test rather than a crushing test. To find out, she convinces four of her friends try to join her at an electronics store to bend one of the two phones for a duration of 1 minute each. 

Two of her friends really want to try to bend the Universe S10, so Laurel assigns those two friends to bend the Universe S10, and her other two friends try bending the WePhone 10S. They find the Universe S10 bent about 2 degrees more than the WePhone 10, so she concludes the average treatment effect of the WePhone 10S on bendability is -2 degrees. Of the following, which is the most problematic design error in this experiment?


*** =instructions
- Noncompliance
- Ethics
- Random assignment
- Data visualization

*** =sct
```{r}
msg1 = "Try again"
msg2 = "Try again"
msg3 = "Correct, Laurel's friends were not randomly assigned to each treatment. Instead, she assigned them based on their own preferences, which could lead to confounded results. For example, what if the Universe S10 testers hated Universe phones, so tried harder to damage them?."
msg4 = "Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:1c689745b7
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
msg4 = "Correct. A single neighborhood is unlikely to reflect the diversity of the whole country, and involving people across the world brings in a lot of complicating confounders. People in her town is closer to ideal, but really to get a true representation of the US population, you need to survey strangers across the US"
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```
