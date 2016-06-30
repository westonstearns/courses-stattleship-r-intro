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
## First API Call

You successfully called in data using the stattleshipR API. Let's have a look at the data. 

We have created a data frame 'all_variables' for you that contains a list of all the variables that were contained in the API call. It has already been loaded into the environment. It has only one column titled `variables` that is the list of variable names. 

Print the list and then find out how long it is to get a sence of the size of the data you called.

*** =instructions
- Print the data set `all_variables`
- Use the `length` function to find the number of variables you called in with the stattleshipR API call.  

*** =hint
- When using the `length` function remember to call the variable name that you would to know the length of. In this data set it is `length$variables` 

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1256/datasets/all_variables.RData"))
```

*** =sample_code
```{r}
# Print the data set all_variables

# Find the total number of variables that were called using the API
length(unlist(all_variables$____))
```

*** =solution
```{r}
# Print the data set all_variables
all_variables

# Find the total number of variables that were called using the API
length(unlist(all_variables$variables))

```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:49df9c3d68
## Game logs 1    

*** =instructions
- 

*** =hint
- 

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
game_logs <- do.call('rbind', lapply(game_log_data, function(x) x$game_logs)) 
names(game_logs)
```

*** =solution
```{r}
game_logs <- do.call('rbind', lapply(game_log_data, function(x) x$game_logs)) 
names(game_logs)
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

*** =instructions
- 

*** =hint
- 

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
players <- do.call('rbind', lapply(player_data, function(x) x$players)) 
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

```

*** =sample_code
```{r}
game_logs <- merge(players, game_logs, by='player_id')
names(game_logs)

```

*** =solution
```{r}
game_logs <- merge(players, game_logs, by='player_id')
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
--- type:NormalExercise lang:r xp:100 skills:1  key:6d4d29437c
## Plot    

*** =instructions
- 

*** =hint
- 

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
ggplot(stats, aes(x=totalRuns, y=meanBA, size=totalBases, label=name, color=salary)) + geom_text()

```

*** =solution
```{r}
ggplot(stats, aes(x=totalRuns, y=meanBA, size=totalBases, label=name, color=salary)) + geom_text()

```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```






