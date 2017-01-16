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
- Examine the provided phone specifications and name the specification that has the `largest ratio` between the WePhone 10S and the Universe S10
- What is the `size` of this ratio (expressed as a quotient)?
*** =pre_exercise_code
```{r}
PhoneSpecifications<-data.frame(WePhone10S=c(190,4000,5.5,64,800),UniverseS10=c(180,3500,5.2,64,550))
row.names(PhoneSpecifications)<-c("Weight (g)","Battery Capacity (mAh)","Diagonal Length (in)","Storage (Gb)","Luminance (cd/m2)")
PhoneSpecifications<-t(PhoneSpecifications)
```
*** =sample_code
```{r}
print(Solution1<-   )#Write Column name of specification with the largest ratio between the WePhone 10S and the Universe S10

print(Solution2<-   )#Write quotient of phone specifications selected in Solution1

```
*** =solution
```{r}
Ratios<-vector(length=5)
for(i in 1:length(PhoneSpecifications[1,])){
Ratios[i]<-PhoneSpecifications[1,i]/PhoneSpecifications[2,i]
}
print(Solution1<-dimnames(PhoneSpecifications)[[2]][match(max(Ratios),Ratios)])

print(Solution2<-max(Ratios))

```
*** =sct
```{r}
test_object("Solution1")
test_object("Solution2")

success_msg("Good work!")
```



--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1
## Randomized Experiments
*** =video_link
//player.vimeo.com/video/198212082


