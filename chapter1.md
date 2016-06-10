---
title       : Introduction to Stattleship API
description : test description
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:NormalExercise lang:r xp:100 skills:1 key:65468e39a4
## Set API token and parameters

*** =instructions
- Set your API token. We've already done this for you, but if you'd like to continue to use the API outside of DataCamp, sign up for one at [stattleship.com](https://www.stattleship.com/). This is done with `set_token('YOUR-TOKEN-GOES-HERE')`.
- The Stattleship library has already been installed and loaded for you with `library(stattleshipR)`

The next step is to set the parameters needed to query the API. There are 4 main parameters: `sport`, `league`, `ep` and `q_body`. 
Let's query for yesterday's MLB team game logs. In order to do this, you will need to set the parameters like this:

```
sport <- 'baseball'
league <- 'MLB'
ep <- 'team_game_logs'
q_body <- list(since = '1 day ago', status='ended')

```

Now you try it!

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
sport <- 'baseball'
league <- 'mlb'
ep <- 'team_game_logs'
q_body <- list(since='1 day ago', status='ended')

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

# Test the that the params were set properly
# Notice that we didn't define any feedback here, this will cause automatically 
# generated feedback to be given to the student in case of an incorrect submission
test_object("sport")

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
