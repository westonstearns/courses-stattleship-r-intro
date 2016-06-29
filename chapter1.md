---
title       : Introduction to Stattleship API
description : test description
---

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
game_log_data <- ss_get_result(sport = ___, league = ___, ep = ___, query = q_body, walk = TRUE)  

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
game_log_data <- ss_get_result(sport = 'baseball', league= 'mlb', ep= 'game_logs' , query = query_list, walk=TRUE)  

```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:7e2208dfc7
## First API Call

You successfully called in data using the stattleshipR API. Let's have a look at the data. 

We have created a data frame 'all_variables' that contains a list of all the variables that were contained in the API call.

The code provided manipulates the data that you called in to help you see the size and completixty of the data that you can get from stattleshipR. There variety and size of the data mean that there countless of projects and potential uses for the data. Remember this was just one specific API call from many other options. 

At the end of the course you can download a list of all the options and datasets that can be accessed through stattleshipR.

Run the code and follow the instructions below to get a better sense of the data and possibilites you have in using the stattleship API.  

*** =instructions
- Run the first code block to find all the variables within the dataset.
- Use the `length` function to find the number of `variables` you called in with the stattleshipR API call.  

*** =hint
- 

*** =pre_exercise_code
```{r}
library(stattleshipR)  
library(dplyr)
library(ggplot2)

set_token("416745fa271fa945c0834ecdbe8d5c08")
q_body <- list(team_id = 'mlb-bos', status = 'ended', interval_type = 'regularseason')
gls <- ss_get_result(sport = 'baseball', league= 'mlb', ep= 'game_logs' , query = q_body, walk=TRUE)  

for (x in 1:31){
  for(i in 1:12){
    data <- as.data.frame(gls[[x]][i])
    data_names <- names(data)
    data_names_edit = unlist(regmatches(data_names,gregexpr("(?<=\\.).*",data_names, perl = TRUE)))
    nam <- paste("df", i, sep = "")
    assign(nam, as.data.frame(data_names_edit))
  }
}

all_variables <-  unique(Reduce(function(x, y) merge(x, y, all=TRUE), list(df1,df2,df3,df4, df5,df6,df7,df8,df9,df10,df11,df12)))
names(all_variables) <- c("variables")


```

*** =sample_code
```{r}
# 
length(unlist(all_variables$variables))
```

*** =solution
```{r}

length(unlist(all_variables$variables))


```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```




