---
title       : Introduction to Stattleship API
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace. You can use it for several things:

devtools::install_github("stattleship/stattleship-r")
library(stattleshipR)
set_token('18efec0cec8943fa9f5397516e4a6809')

# 3. Create a plot in the viewer, that students can check out while reading the exercise
# ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

*** =sct
```{r}
# The sct section defines the Submission Correctness Tests (SCTs) used to
# evaluate the student's response. All functions used here are defined in the 
# testwhat R package

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be a very bad action movie in the dataset."

# Use test_mc() to grade multiple choice exercises. 
# Pass the correct option (Action, option 2 in the instructions) to correct.
# Pass the feedback messages, both positive and negative, to feedback_msgs in the appropriate order.
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad)) 
```

--- type:NormalExercise lang:r xp:100 skills:1
## More movies

In the previous exercise, you saw a dataset about movies. In this exercise, we'll have a look at yet another dataset about movies!

A dataset with a selection of movies, `movie_selection`, is available in the workspace.

*** =instructions
- Set your API token ... 
- set the params
- call ss_get_result

*** =hint
- Use `set_token()`
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`. 

*** =pre_exercise_code
```{r}
# Pre-load a package in the workspace
library(stattleshipR)

# You can prepare the data before the student starts:
#data(Movies)
#movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"),c("Genre", "Rating", "Run")]

# You can also clean up data so that it's not available in the student's workspace anymore:
#rm(Movies)
```

*** =sample_code
```{r}
# set API token

# set sport, league, ep and q_body

# query for the data

```

*** =solution
```{r}
# set API token
set_token("18efec0cec8943fa9f5397516e4a6809")

# set params
sport <- 'basketball'
league <- 'nba'
ep <- 'game_logs'
q_body <- list(since='1 day ago')

# call Stattleship API
gl <- ss_get_result(sport=sport, league=league, ep=ep, query=q_body, version=1, verbose=TRUE, walk=TRUE)

```

*** =sct
```{r}
# The sct section defines the Submission Correctness Tests (SCTs) used to
# evaluate the student's response. All functions used here are defined in the 
# testwhat R package. Documentation can also be found at github.com/datacamp/testwhat/wiki

# Test whether the function str is called with the correct argument, object
# If it is not called, print something informative
# If it is called, but called incorrectly, print something else
#test_function("str", args = "object",
#              not_called_msg = "You didn't call `str()`!",
#              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

# Test the object, good_movies
# Notice that we didn't define any feedback here, this will cause automatically 
# generated feedback to be given to the student in case of an incorrect submission
test_object("gl")

# Test whether the student correctly used plot()
# Again, we use the automatically generated feedback here
# test_function("plot", args = "x")
# test_function("plot", args = "y")
# test_function("plot", args = "col")

# Alternativeley, you can use test_function() like this
# test_function("plot", args = c("x", "y", "col"))

# It's always smart to include the following line of code at the end of your SCTs
# It will check whether executing the student's code resulted in an error, 
# and if so, will cause the exercise to fail
test_error()

# Final message the student will see upon completing the exercise
success_msg("Good work!")
```
