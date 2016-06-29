---
title       : Introduction to Stattleship API
description : test description
---

--- type:NormalExercise lang:r xp:100 skills:1 key:e20287ea44
## Getting started with stattleshipR

Before we get started with the demo of the `stattleshipR` API, we want to recap how to install a package and load it into the environement. 

The `stattleshipR` package along with the accessory packages `dplyr` and `ggplot2` are installed on the DataCamp servers. The following code can be used to install it on your personal computer outside of the DataCamp platform.  

```
install.packages("devtools")  
devtools::install_github("stattleship/stattleship-r")
install.packages('dplyr')
install.packages('ggplot2')
```

Now we will have you can install each of those three packages.

*** =instructions
- Load the `stattleshipR` package
- Load the `dplyr` package
- Load the `ggplot2` package

*** =hint
- To load a package use the `library()` function

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Load the stattleshipR package
library(___)  

# Load the dplyr package
library(___)

# Load the ggplot2 package
library(___)


```

*** =solution
```{r}
# Load the stattleshipR package
library(stattleshipR)  

# Load the dplyr package
library(dplyr)

# Load the ggplot2 package
library(ggplot2)

```

*** =sct
```{r}

test_function("library", index = 1, not_called_msg = "Did you load `stattleshipR`? Check out the hint if you need help.", args_not_specified_msg = "Did you load `stattleshipR`? Check out the hint if you need help.", incorrect_msg = "Something's not right with how you loaded `stattleshipR`? Check out the hint if you need help.")

test_function("library", index = 2, not_called_msg = "Did you load `dplyr`? Check out the hint if you need help.", args_not_specified_msg = "Did you load `dplyr`? Check out the hint if you need help.", incorrect_msg = "Something's not right with how you loaded `dplyr`? Check out the hint if you need help.")

test_function("library", index = 3, not_called_msg = "Did you load ggplot2? Check out the hint if you need help.", args_not_specified_msg = "Did you load ggplot2? Check out the hint if you need help.", incorrect_msg = "Something's not right with how you loaded `ggplot2`? Check out the hint if you need help.")

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:ba6e1a41f2
## Calling the API

Now that you have loaded the packages that you will need, its time for you to explore the API call syntax. 

You will need to set the token using the `set_token` function. The token here can only be used in DataCamp, click here for more information about who to get a perminant token for using the API outside of DataCamp. 

A `q_body` object is defined to be used in the API call. This code determines....

The format for the API call has been included in the sample code but follow the instructions to define the missing arguements. 

*** =instructions
- Set the `sport` arguement in the API call to `'baseball'`  
- Set the `league` argument in the API call to `'mlb'` 
- Set the `ep` argument in the API call to `'game_logs'`

*** =hint
- Don't change the code for the token or the `q_body`. Remember to use '' around the arugments you add to the API call.  

*** =pre_exercise_code
```{r}
# library(stattleshipR)  
library(dplyr)
library(ggplot2)

```

*** =sample_code
```{r}
# The token to access the stattleshipR API
set_token("416745fa271fa945c0834ecdbe8d5c08")

# 
q_body <- list(team_id = 'mlb-bos', status = 'ended', interval_type ='regularseason')

# The API call 
gls <- ss_get_result(sport = ___, league = ___, ep = ___, query = q_body, walk = TRUE)  

```

*** =solution
```{r}
# The token to access the stattleshipR API
set_token("416745fa271fa945c0834ecdbe8d5c08")

# 
q_body <- list(team_id = 'mlb-bos', status = 'ended', interval_type = 'regularseason')

# The API call 
gls <- ss_get_result(sport = 'baseball', league= 'mlb', ep= 'game_logs' , query = q_body, walk=TRUE)  

```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:ba6e1a41f2
## First API Call

You successfully called in data using the stattleshipR API. Let's have a look at the data. 

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




