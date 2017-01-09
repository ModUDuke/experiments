<!-- Course information --> 
  ---
  title       : Exercise Title
  description : This exercise does something
  attachments :
  video_link : https://vimeo.com/179938122

<!-- First Exercise - Video--> 
    <!-- set type to video --> 
        --- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:bfc8a2d235
    <!-- Title --> 
        ## Introduction to Experiments
    <!-- Link to video --> 
        *** =video_link
        //player.vimeo.com/video/179938122

<!-- Second Exercise - Multiple Choice--> 
    <!-- set type to multiple choice --> 
        --- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:1ecca31bfa
    <!-- Title --> 
        ## Problem 1: Something
    <!-- Problem text --> 
This is a question
    <!-- Choices --> 
      *** =instructions
      - Answer 1
      - Answer 2
      - Answer 3
      - Answer 4
    <!-- Hints --> 
      *** =hint
      - Here is a useful hint: Answer 3 is the right answer
    <!-- Not clear whether this syntax is necessary -->   
      *** =pre_exercise_code
      ```{r}
      #none
      ```
    <!-- Feedback dependent on answer. test_mc identifies which is correct  -->   
      *** =sct
      ```{r}
      msg1 = "Try again"
      msg2 = "Try again"
      msg3 = "Well done"
      msg4 = "Try again"
      test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
      ```

<!-- Third Exercise -  Coding with R--> 
    <!-- set type to Normal --> 
        --- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:bfc8a2d235
    <!-- Title --> 
        ## Problem 2: Something Different
      <!-- Problem text -->
          This describes (in general terms) what you need to do.
    <!-- Specific Instructions -->
        *** =instructions
        - Do this something with `variable`
        - Do  something else with `key term` 
    <!-- Hint -->
        *** =hint
        - This is a useful hint
    <!-- Data for exercise -->
        *** =pre_exercise_code
        ```{r}
        load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
        ```
    <!-- Initial code written in R workspace -->
        *** =sample_code
        ```{r}
        # Useful initial code
        ```
    <!-- Ideal way to solve problem -->
        *** =solution
        ```{r}
        # Solution and ideal way to solve problem. For example, imagine we want the user to add 2+2 and store result in "x"
        x <- 2+2
        ```
    <!-- Check to determine if student was correct -->
        *** =sct
        ```{r}
            test_object("x")
            success_msg("Good work!")

          # The above tests if x contains the right value. If we don't care how they arrive at the solution (i.e. x<-4 would be an accurrate solution), then this is enoughThe
          # More options and detail for syntax described at: https://github.com/datacamp/testwhat/wiki
          #The following is an example of specific feedback for a wrong answer. The example below tests whether a result is written as a string rather than as a number, and provides a message to the user saying as much.
            test_function("print", args = "x")
          
        ```

