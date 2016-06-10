---
title       : Introduction to Stattleship API
description : test description
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:NormalExercise lang:r xp:100 skills:1 key:65468e39a4
## first query

*** =instructions
- Set your API token. Sign up for one from www dot stattleship dot com.
- set the params
- call `ss_get_result()`

*** =hint
- Use `set_token()`

*** =pre_exercise_code
```{r}
# Pre-load a package in the workspace
library(stattleshipR)
set_token("416745fa271fa945c0834ecdbe8d5c08")

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
set_token("416745fa271fa945c0834ecdbe8d5c08")

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

# Test the object, gl
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
