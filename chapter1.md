---
title       : Introduction to Stattleship API
description : test description

---
title       : For loops
description : A brief intro to writing for loops

--- type:NormalExercise lang:r xp:100 skills:1 key:e20287ea44
## Getting started with stattleshipR

Before we get started with the demo of the `stattleshipR` API, we want to recap how to install a package and load it into the environement. 

The `stattleshipR` package along with the accessory packages `dplyr` and `ggplot2` are installed and loaded on the DataCamp servers. The following code can be used to install it on your personal computer outside of the DataCamp platform.  

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

test_function("library", index = 1, , not_called_msg = "Did you load `stattleshipR`? Check out the hint if you need help.", args_not_specified_msg = "Did you load `stattleshipR`? Check out the hint if you need help.", incorrect_msg = "Something's not right with how you loaded `stattleshipR`? Check out the hint if you need help.")

test_function("library", index = 2, not_called_msg = "Did you load `dplyr`? Check out the hint if you need help.", args_not_specified_msg = "Did you load `dplyr`? Check out the hint if you need help.", incorrect_msg = "Something's not right with how you loaded `dplyr`? Check out the hint if you need help.")

test_function("library", index = 3, not_called_msg = "Did you load ggplot2? Check out the hint if you need help.", args_not_specified_msg = "Did you load ggplot2? Check out the hint if you need help.", incorrect_msg = "Something's not right with how you loaded `ggplot2`? Check out the hint if you need help.")

test_error()
success_msg("Good work!")
```




set_token("your-api-token")

sport <- 'baseball'  
league <- 'mlb'  
ep <- 'game_logs'  
q_body <- list(team_id='mlb-bos', status='ended', interval_type='regularseason')

gls <- ss_get_result(sport=sport, league=league, ep=ep, query=q_body, walk=TRUE)  
game_logs<-do.call('rbind', lapply(gls, function(x) x$game_logs)) 

sport <- 'baseball'  
league <- 'mlb'  
ep <- 'players'  
q_body <- list(team_id='mlb-bos')

pls <- ss_get_result(sport=sport, league=league, ep=ep, query=q_body, walk=TRUE)  
players<-do.call('rbind', lapply(pls, function(x) x$players)) 

colnames(players)[1] <- 'player_id'
game_logs <- merge(players, game_logs, by='player_id')

stats <- 
  game_logs %>%
  filter(game_played == TRUE) %>%
  group_by(name) %>%
  summarise(totalRuns = sum(runs), meanBA = mean(batting_average), totalBases=sum(total_bases), salary=max(salary))

ggplot(stats, aes(x=totalRuns, y=meanBA, size=totalBases, label=name, color=salary)) + geom_text()


--- type:NormalExercise lang:r xp:100 skills:1  key:ba6e1a41f2
##     

*** =instructions
- 

*** =hint
- 

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}


```

*** =solution
```{r}



```

*** =sct
```{r}

test_error()
success_msg("Good work!")
```



