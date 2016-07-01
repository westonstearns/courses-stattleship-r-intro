---
title       : Introduction to Stattleship API
description : test description

--- type:NormalExercise lang:r xp:100 skills:1  key:ba6e1a41f2
## Loading stattleshipR and Calling the API
The first step to using the Stattleship API is loading the package into your environment. 

Use the standard `library` function to make the package available to use. 

Now that you have loaded the package, its time for you to explore the API call syntax. 

You will need to set the token using the `set_token` function. The token here can only be used in DataCamp, <a href="http://developers.stattleship.com/#introduction">click here</a> for more information about how to get a perminant token for using the API outside of DataCamp. 

A `query_list` object is defined to be used in the API call. This code determines a list of features for the API to call. A full list of the options can be found <a href="http://developers.stattleship.com/#introduction">here</a>. ## Add description of `query`.

The format for the API call has been included in the sample code but follow the instructions to define the missing arguements.

*** =instructions
- Use the `library` function to load the `stattleshipR` package.
- Set the `sport` arguement in the API call to `'baseball'`.  
- Set the `league` argument in the API call to `'mlb'`. 
- Set the `ep` argument in the API call to `'game_logs'`.
- Run the API call and assign the results to `game_log_data`. 

*** =hint
- Don't change the code for the token or the `q_body`. Remember to use '' around the arugments you add to the API call.  

*** =pre_exercise_code
```{r}
library(dplyr)
library(ggplot2)
```

*** =sample_code
```{r}
# Load stattleshipR package
library(___)

# The token to access the stattleshipR API
set_token("416745fa271fa945c0834ecdbe8d5c08")

# Create a query list for the API call
query_list <- list(team_id = 'mlb-bos', status = 'ended', interval_type ='regularseason')

# The API call 
game_log_data <- ss_get_result(sport = ___, league = ___, ep = ___, query = query_list, walk = TRUE)  

```

*** =solution
```{r}
# Load stattleshipR package
library(stattleshipR)

# The token to access the stattleshipR API
set_token("416745fa271fa945c0834ecdbe8d5c08")

# Create a query list for the API call
query_list <- list(team_id = 'mlb-bos', status = 'ended', interval_type = 'regularseason')

# The API call 
#game_log_data <- ss_get_result(sport = 'baseball', league= 'mlb', ep= 'game_logs' , query = query_list, walk=TRUE)  

```

*** =sct
```{r}




test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:7e2208dfc7
## Exploring the API Data

You successfully called in data using the stattleshipR API, running the precoded `lappy()` function can give you a sence of the data you called in. Use the `head()` fucntion to print an abrieveated list of the `game_log_data` summaries.  

The `game_log_data` containes sublists that each have their own variables. We have created a data frame `all_variables` for you that contains all the unique variables within the sublists of the `game_log_data` data set. It has already been loaded into the environment. 

Print the variable list and then find out how long it is to get a sence of the size of the data you called.

*** =instructions
- Add the data set to the `lapply()` function to create a summary of all the sublists within the `game_log_data`.
- Use the `head()` function to print the first 5 summaries.
- Print the data set `all_variables`.
- Use the `length()` function to find the number of variables you called in with the stattleshipR API call.  

*** =hint
- When using the `length` function, you need to unclude the `unlist()` so the length can cound the number of names. Just fill in the data frame name `all_variables` into the two functions. 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/all_variables.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/game_log_data.RData"))
```

*** =sample_code
```{r}
# Summarising each data list within the game_log_data object
summary <- lapply(_____, function(x) summary(x))

# Print out the first 5 summaries
head(_____)

# Print the data set all_variables


# Find the total number of variables that were called using the API
length(unlist(___))
```

*** =solution
```{r}
# Summarising each data list within the game_log_data object
summary <- lapply(game_log_data, function(x) summary(x))

# Print out the first 5 summaries
head(summary)

# Print the data set all_variables
all_variables

# Find the total number of variables that were called using the API
length(unlist(all_variables))

```

*** =sct
```{r}



test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:49df9c3d68
## Game logs 1    

Explain the `do.call` function 
```
[NEW_DATA_SET] <- do.call('rbind', lapply([NAME OF DATASET], function(x) x$[NAME OF COLOMN])) 
```
*** =instructions
- fill in the dataset name and the column name for the `do.call` function
- print the names of the `game_logs` data set

*** =hint
- 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/game_log_data.RData"))
```

*** =sample_code
```{r}
game_logs_combined <- do.call('rbind', lapply(______, function(x) x$_____)) 
names(game_logs_combined)
```

*** =solution
```{r}
game_logs_combined <- do.call('rbind', lapply(game_log_data, function(x) x$game_logs)) 
names(game_logs_combined)
```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:831345cf7b
## Second Call     

*** =instructions
- 

*** =hint
- 

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Load stattleshipR package
library(stattleshipR)

# The token to access the stattleshipR API
set_token("416745fa271fa945c0834ecdbe8d5c08")

# Create a query list for the API call
query_list <- list(team_id='mlb-bos')

# The API call 
player_data <- ss_get_result(sport='baseball', league='mlb', ep='players' , query=query_list, walk=TRUE)

```

*** =solution
```{r}
#
# Load stattleshipR package
library(stattleshipR)

# The token to access the stattleshipR API
set_token("416745fa271fa945c0834ecdbe8d5c08")

# Create a query list for the API call
query_list <- list(team_id='mlb-bos')

# The API call 
player_data <- ss_get_result(sport='baseball', league='mlb', ep='players' , query=query_list, walk=TRUE)

```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:901ced8002
## Players    

Explain the `do.call` function 
```
[NEW_DATA_SET] <- do.call('rbind', lapply([NAME OF DATASET], function(x) x$[NAME OF COLOMN])) 
```
*** =instructions
- fill in the dataset name and the column name for the `do.call` function
- print the names of the `players` data set


*** =hint
- 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/player_data.RData"))
```

*** =sample_code
```{r}
players <- do.call('rbind', lapply(_____, function(x) x$____)) 
colnames(players)[1] <- 'player_id'
names(players)


```

*** =solution
```{r}
players <- do.call('rbind', lapply(player_data, function(x) x$players)) 
colnames(players)[1] <- 'player_id'
names(players)


```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:7651cbecc4
## Game Logs   

*** =instructions
- 

*** =hint
- 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/players.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/game_logs_combined.RData"))
```

*** =sample_code
```{r}
game_logs <- merge(players, game_logs_combined, by='player_id')
names(game_logs)

```

*** =solution
```{r}
game_logs <- merge(players, game_logs_combined, by='player_id')
names(game_logs)

```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:46ddcad271
## Stats    

*** =instructions
- 

*** =hint
- 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/game_logs.RData"))
library(dplyr)
```

*** =sample_code
```{r}
stats <- 
  game_logs %>%
  filter(game_played == TRUE) %>%
  group_by(name) %>%
  summarise(totalRuns = sum(runs), meanBA = mean(batting_average), totalBases=sum(total_bases), salary=max(salary))

names(stats)


```

*** =solution
```{r}
stats <- 
  game_logs %>%
  filter(game_played == TRUE) %>%
  group_by(name) %>%
  summarise(totalRuns = sum(runs), meanBA = mean(batting_average), totalBases=sum(total_bases), salary=max(salary))

names(stats)

```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```
--- type:MultipleChoiceExercise lang:r xp:50 skills:3 key:6d4d29437c
## Plot 

Using the `stats` data set you created in the previous exercise we calculated the Runs over Replacement metric. It identifies the number of runs a player gives their team when compared to an average replacemnt player. 

We calulated this using the general formula:
```
Runs over Replacement = Player_runs - ReplPlayer_runs = (Player_runs - AvgPlayer_runs) + (AvgPlayer_runs - ReplPlayer_runs)
```
You can see this metric in the plot to the right which was generated using `ggplot2`.

If you want to learn more about `ggplot2`, try our course on <a href="http://www.datacamp.com/courses/data-visualization-with-ggplot2-1">ggplot2</a>.

Use the plot to answer the following question:

Which player has the highest Runs Over Replacement per thousand dollars of salary (`ROR_per_dollar_thousand`)?

*** =instructions
- Xander Bogaerts
- David Ortiz
- Dustin Pedroia

*** =hint
The player with the hightest Runs Over Replacement per thousand dollars of salary (`ROR_per_dollar_thousand`) will be in the lightest blue.

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/stats.RData"))
library(ggplot2)
library(dplyr)
stats <- stats %>%
    mutate(avg_player_runs = mean(totalRuns)) %>%
  group_by(name) %>%
    mutate(Player_runs = (totalRuns - avg_player_runs), ReplPlayer_runs = (avg_player_runs - 20.5), Runs_Over_Replacement = Player_runs - ReplPlayer_runs, ROR_per_dollar_thousand = 1000*(Runs_Over_Replacement/salary))
ggplot(stats, aes(x = meanBA, y = Runs_Over_Replacement, size = totalBases, label = name, color = ROR_per_dollar_thousand)) + geom_text()
```

*** =sct
```{r}
msg1 = 'You got it! We hoped you enjoyed your intro to the stattleshipR package. This API gives you access to a tremendous amount of Sports information and we showed you just a fraction of what you can do with the data at your fingertips. Please explore the <a href="http://developers.stattleship.com/#introduction">stattleshipR package</a> and DataCamp to help get you moving toward becoming a Sports Data Scientist.'
msg2 = "Try again."
msg3 = "Not quite."
test_mc(correct = 1, feedback_msgs = c(msg1,msg2,msg3))

```






