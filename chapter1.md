---
title       : Introduction to Stattleship API
description : test description

--- type:NormalExercise lang:r xp:100 skills:1  key:ba6e1a41f2
## Loading stattleshipR and Calling the API
The first step to using the Stattleship API is downloading the package and loading it into your environment. 

The following code block can be copied and pasted to download `stattleshipR` and load it into your environment.

```
instal_packages("devtools")

instal_packages("install_github")

devtools::install_github("stattleship/stattleship-r")

library(stattleshipR)
```

The package has already been loaded on our server and is available in your environment. Now you can explore the API call syntax. 

You will need to set the token using the `set_token` function. You are given a temporary token `TEMPORARY_TOKEN` that can only be used in DataCamp, <a href="http://developers.stattleship.com/#introduction">click here</a> for more information about how to get a permanent token for using the API outside of DataCamp. 

A `query_list` object is defined to be used in the API call. This code determines a list of features for the API to call. A full list of the options can be found <a href="http://developers.stattleship.com/#introduction">here</a>.

The format for the API call has been included in the sample code but follow the instructions to define the missing arguments.

*** =instructions
- Use the `library` function to load the `stattleshipR` package.
- `set_token` using the key `TEMPORARY_TOKEN`.
- Set the `sport` argument in the API call to `'baseball'`.  
- Set the `league` argument in the API call to `'mlb'`. 
- Set the `ep` argument in the API call to `'game_logs'`.
- Run the API call and assign the results to `game_log_data`. 

*** =hint
- Don't change the code for the token or the `query_list`. Remember to use '' around the arguments you add to the API call.  

*** =pre_exercise_code
```{r}
library(stattleshipR)
set_token("416745fa271fa945c0834ecdbe8d5c08")
set_token <- function(x){
print("YOUR_TEMPORARY_TOKEN")}
```

*** =sample_code
```{r}

# The token to access the stattleshipR API
set_token(____)

# Create a query list for the API call
query_list <- list(team_id = 'mlb-bos', status = 'ended', interval_type ='regularseason', since = '1 week ago')

# The API call 
game_log_data <- ss_get_result(sport = ___, league = ___, ep = ___, query = query_list, walk = TRUE)  

```

*** =solution
```{r}
# The token to access the stattleshipR API
set_token("TEMPORARY_TOKEN")

# Create a query list for the API call
query_list <- list(team_id = 'mlb-bos', status = 'ended', interval_type = 'regularseason', since = '1 week ago')

# The API call 
game_log_data <- ss_get_result(sport = 'baseball', league= 'mlb', ep= 'game_logs' , query = query_list, walk=TRUE)  

```

*** =sct
```{r}
test_function("set_token", args_not_specified_msg = 'Make sure you add "TEMPORARY_TOKEN" to the `set_token` function.', 
              incorrect_msg = 'The `set_token` function is not working properly, take a look at the instructions again and make sure that your token exactly matches what you see in the instructions.')

test_object("query_list",incorrect_msg = "Don't make any changes to the `query_list` object. If you need to you can reset                 the sample code by clicking on the arrow near the `submit answer` button.")

test_function("ss_get_result", args_not_specified_msg = 'When running the AIP call, `ss_get_results`, make sure you fill in               the blanks according to the instructions.', 
              incorrect_msg = 'The `ss_get_results` function is not working properly, take a look at the instructions again and make sure the arguements exactly match what you see in the instructions.')

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:7e2208dfc7
## Exploring the API Data
You successfully called in data using the stattleshipR API. 

Since this course can be taken over and over many times we saved data from an API call a week before the All-Star break in 2016. This data will be used for the remaining exercises. It is the same data that was called from the previous exercise. 

To see what data you called in, run the precoded `lappy()` to summarize the sublists within the data. Use the `head()` function to print an abbreviated list of these summaries.  

The `game_log_data` sublists have their own variables. We have created a data frame `all_variables` for you that contains all the unique variables within the sublists of the `game_log_data` data set. It has already been loaded into the environment. 

Print the variable list and then find out how long it is to get a sense of the size of the data you called.

*** =instructions
- Add the data set to the `lapply()` function to create a summary of all the sublists within the `game_log_data`.
- Use the `head()` function to print the first 5 summaries.
- Print the data set `all_variables`.
- Use the `length()` function to find the number of variables you called in with the stattleshipR API call.  

*** =hint
- When using the `length` function, you need to include the `unlist()` so the length can count the number of names. Just fill in the data frame name `all_variables` into the two functions. 

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
test_function("lapply", args_not_specified_msg = 'Make sure you add the data frame to the `lappy` function.', 
              incorrect_msg = 'The `lapply` function is not working properly, take a look at the instructions again and make sure that your token exactly matches what you see in the instructions.')

test_object("summary",incorrect_msg = "The data set `summary` was not defined properly. Follow the instructions to               define the `summary` object.")

test_function("head", args_not_specified_msg = 'Make sure you add the name of the data set you want to print when using the               `head` function.', incorrect_msg = 'The `head` function was not called properly, take a look at the                         instructions again and make sure the arguments exactly match what you see in the instructions.')

test_output_contains("all_variables",incorrect_msg = "The data set `all_variables` was not printed. To print just type the                name in the script.R pane.")

test_function("length", args_not_specified_msg = 'Make sure you fill in the blanks for the `length` function according to                 the instructions.', 
              incorrect_msg = 'The `ss_get_results` function is not working properly, take a look at the instructions again and make sure the arguements exactly match what you see in the instructions.')

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:49df9c3d68
## Combining game log data  

As you saw the `game_log_data` data set is a group of repeated multidimensional lists. Each name you saw in the summary was its own list. 

You will only be using one of the sublists in the following exercises, but we want to collect the data from each of the 31 repeated lists. 

You will use the `do.call()`, the `lapply()` and the `rbind()` functions to combine rows of data that we want. The list you will first combine is the `game_log` list. 

In this exercise the `do.call()` function follows the following form:
```NEW_DATA_SET_NAME <- do.call('rbind', lapply(DATA_SET, function(x) x$LIST_NAME))```

The new data set contains 94 game log variables.

*** =instructions
- Create a new data set `game_logs_combined` by filling in the data set name (`game_log_data`) and the list name (`game_log`) for the `do.call()` function.
- Print the names of the `game_logs` data set.

*** =hint
- For the `do.call` function, simply add the data set in for the first blank and then the list name after the `$`. If you need to reset the sample code, click the circular arrow near the `submit answer` button. 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/game_log_data.RData"))
```

*** =sample_code
```{r}
# Create the game_logs_combined data set
game_logs_combined <- do.call('rbind', lapply(______, function(x) x$_____)) 

# Print the names of the new data set
names(____)
```

*** =solution
```{r}
# Create the game_logs_combined data set
game_logs_combined <- do.call('rbind', lapply(game_log_data, function(x) x$game_log)) 

# Print the names of the new data set
names(game_logs_combined)

```

*** =sct
```{r}
test_object("game_logs_combined", incorrect_msg = "The `game_logs_combined` data set is not correct. To run the the                       `do.call` fuction, simply add the data set in for the first blank and then the list name after the `$`.")

test_function("names", args_not_specified_msg = 'To print the names of the new data set, make sure you fill in the blanks                 according to the instructions.', 
              incorrect_msg = 'The `names` function is not working properly, take a look at the instructions again and make sure the arguments exactly match what you see in the instructions.')

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:831345cf7b
## Second API Call     
You will be using a second list of variables in later exercises so you will need to make a second call to the Stattleship API. 

Use the `set_token` function again and run the code to assign the `query_list` object just like the first API call.

The format for the API call has been included in the sample code but follow the instructions to define the missing arguments.

*** =instructions
- Set the `sport` argument in the API call to `'baseball'`.  
- Set the `league` argument in the API call to `'mlb'`. 
- Set the `ep` argument in the API call to `'players'`.
- Run the API call and assign the results to `player_data`. 

*** =hint
- Don't change the `query_list` function, just run the code and the use the API call after filling in the blank spaces. To reset the sample code, click the circular arrow near the `submit answer` button.

*** =pre_exercise_code
```{r}
library(stattleshipR)
set_token("416745fa271fa945c0834ecdbe8d5c08")
set_token <- function(x){
print("YOUR_TEMPORARY_TOKEN")}
```

*** =sample_code
```{r}
# The token to access the stattleshipR API
set_token("TEMPORARY_TOKEN")

# Create a query list for the API call
query_list <- list(team_id='mlb-bos')

# The API call 
player_data <- ss_get_result(sport='____', league='____', ep='____' , query=query_list, walk=TRUE)

```

*** =solution
```{r}
# The token to access the stattleshipR API
set_token("TEMPORARY_TOKEN")

# Create a query list for the API call
query_list <- list(team_id='mlb-bos')

# The API call 
player_data <- ss_get_result(sport='baseball', league='mlb', ep='players' , query=query_list, walk=TRUE)

```

*** =sct
```{r}
test_function("set_token", args_not_specified_msg = 'Make sure you add "TEMPORARY_TOKEN" to the `set_token` function.', 
              incorrect_msg = 'The `set_token` function is not working properly, take a look at the instructions again and make sure that your token exactly matches what you see in the instructions.')

test_object("query_list",incorrect_msg = "Don't make any changes to the `query_list` object. If you need to you can reset                 the sample code by clicking on the arrow near the `submit answer` button.")

test_function("ss_get_result", args_not_specified_msg = 'When running the AIP call, `ss_get_results`, make sure you fill in               the blanks according to the instructions.', 
              incorrect_msg = 'The `ss_get_results` function is not working properly, take a look at the instructions again and make sure the arguements exactly match what you see in the instructions.')

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:901ced8002
## Combining player data
As with the first API call, we have saved data from an API call to be used for the remaining exercises for consistency purposes, but the data is exactly the same as what you called in the previous exercise.

The `player_data` is a group of repeated multidimensional lists, just like the `game_log_data`. 

You will only be using one of the sublists in the following exercises, so you again want to collect the data from each of the 6 repeated lists. 

You will use the `do.call()`, the `lapply()` and the `rbind()` functions to combine rows of data that we want. The list you will first combine is the `players` list. 

In this exercise the `do.call()` function follows the following form:
```NEW_DATA_SET_NAME <- do.call('rbind', lapply(DATA_SET, function(x) x$LIST_NAME))```

The new data set contains 34 player attribute variables.

*** =instructions
- Create a new data set `players_combined` by filling in the data set name (`player_data`) and the list name (`players`) for the `do.call()` function.
- Use the `colnames()` function to rename the frist players variable, `'player_id'`.
- Print the names of the `players_combined` data set.


*** =hint
- For the `do.call` function, simply add the data set in for the first blank and then the list name after the `$`. If you need to reset the sample code, click the circular arrow near the `submit answer` button. 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/player_data.RData"))

```

*** =sample_code
```{r}
# Create the players_combined data set
players_combined <- do.call('rbind', lapply(_____, function(x) x$____)) 

# Set the column names to 'player_id'
colnames(players_combined)[1] <- '____'

# Print the names of the variables in the new data set
names(____)

```

*** =solution
```{r}
# Create the players_combined data set
players_combined <- do.call('rbind', lapply(player_data, function(x) x$players)) 

# Set the column names to 'player_id'
colnames(players_combined)[1] <- 'player_id'

# Print the names of the variables in the new data set
names(players_combined)

```

*** =sct
```{r}
test_object("players_combined", incorrect_msg = "The `players_combined` data set is not correct. To run the the                       `do.call` fuction, simply add the data set in for the first blank and then the list name after the `$`.")

test_function("names", args_not_specified_msg = 'To print the names of the new data set, make sure you fill in the blanks                 according to the instructions.', 
              incorrect_msg = 'The `names` function is not working properly, take a look at the instructions again and make sure the arguments exactly match what you see in the instructions.')

test_error()
success_msg("Good work!")

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:7651cbecc4
## Game Logs  
You have now created two lists, one with game log data and another with player attribute data. If we combine them we can link performance data from game logs with player attributes like their full name, the school they attended and salary.

You will use the combined data set to find the player with the highest Runs Over Replacement per thousand dollars of salary.

The `merge()` function follows the following format:
```
NEW_DATA_SET_NAME <- merge(DATA_SET_1, DATA_SET_2, by='COMMON_COLUMN')
```

*** =instructions
- Use the `merge()` function to combine the two datasets, `game_logs_combined` and `players_combined`, using the common variable `'player_id'` and assign it to `game_logs`.
- Print the `game_logs` variables names. 

*** =hint
- Make sure that the data set names are added to the `merge` function exactly as they are in the instructions. 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/players.RData"))
players_combined <- players
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/game_logs_combined.RData"))
```

*** =sample_code
```{r}
# Create the game_logs  
game_logs <- merge(____, ____, by='____')

# Print the variable names of the game_log data set
names(____)

```

*** =solution
```{r}
# Create the game_logs  
game_logs <- merge(players_combined, game_logs_combined, by='player_id')

# Print the variable names of the game_log data set
names(game_logs)
```

*** =sct
```{r}
test_function("merge", incorrect_msg = 'The `merge` function is not working properly, take a look at the instructions                 again and make sure that the arguments exactly match what you see in the instructions.')

test_object("game_logs",incorrect_msg = "Looks like the `game_logs` data set didn't merge correctly. Chek the instructions                for the correct arugements for the `merge` function.")


test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:46ddcad271
## Stats    

Now that you have created a combined data set, you will manipulate some of the variables to create the following new variables:
<p>- `totalRuns`</p>
<p>- `meanBA`</p>
<p>- `totalBases`</p>
<p>- `salary`</p>

The code for the data manipulation is provided in the sample code. It follows the function from the `dplyr` package. If you want to learn more take a look at the premium <a href="https://www.datacamp.com/courses/dplyr-data-manipulation-r-tutorial">dplyr course</a>.

*** =instructions
- Manipulate the `game_logs` data set to create the following variables.
- `totalRuns` is the `sum()` of the `runs` variable
- `meanBA` is the `mean()` of the `batting_average` variable
- `totalBases` is the `sum()` of the `total_bases` variable
- `salary` is the `max()` of the `salary` variable
- Print the variable names of the new data set `stats`

*** =hint
- To create the `stats` data set, just fill in the blanks according to the instructions. 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/game_logs.RData"))
library(dplyr)
```

*** =sample_code
```{r}
# Manipulate the game_logs data set
stats <- game_logs %>%
  filter(game_played == TRUE) %>%
  group_by(name) %>%
  summarise(totalRuns = sum(___), meanBA = mean(___), totalBases=sum(___), salary=max(___))

# Print the variable names of the stats data set
names(___)
```

*** =solution
```{r}
# Manipulate the game_logs data set
stats <- game_logs %>%
  filter(game_played == TRUE) %>%
  group_by(name) %>%
  summarise(totalRuns = sum(runs), meanBA = mean(batting_average), totalBases=sum(total_bases), salary=max(salary))

# Print the variable names of the stats data set
names(stats)

```

*** =sct
```{r}
test_object("stats",incorrect_msg = "The `stats` object is not correct. Check to make sure that you followed the directions             and filled the blanks with the correct variables.")

test_function("names", 
              incorrect_msg = 'The `names` function is not working properly, take a look at the instructions again and make sure the arguments exactly match what you see in the instructions.')

test_error()
success_msg("Good work!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:3 key:6d4d29437c
## Plot 

Using the `stats` data set you created in the previous exercise we calculated the Runs over Replacement metric. It identifies the number of runs a player gives their team when compared to an average replacement player. 

We calulated this using the general formula:
```
Runs over Replacement = Player_runs - ReplPlayer_runs = (Player_runs - AvgPlayer_runs) + (AvgPlayer_runs - ReplPlayer_runs)
```
You can see this metric in the plot to the right which was generated using `ggplot2`.

If you want to learn more about `ggplot2`, try our course on <a href="http://www.datacamp.com/courses/data-visualization-with-ggplot2-1">ggplot2</a>.

Use the plot to answer the following question:

Which player has the highest Runs Over Replacement per thousand dollars of salary (`ROR_per_dollar_thousand`)?

*** =instructions
- Mookie Betts
- David Ortiz
- Dustin Pedroia

*** =hint
The player with the highest Runs Over Replacement per thousand dollars of salary (`ROR_per_dollar_thousand`) will be in the lightest blue.

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


