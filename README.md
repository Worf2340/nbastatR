# nbastatR
NBA Stats API Wrapper for R, formal description coming soon!!

This package is in it's extreme infancy but it should work if you have the necassary packages installed.  Formal vigentte's will come once the wrappers are complete but you please explore around.  Here is some sample code encompassing some of what nbastatR can do.

```{r}
devtools::install_github("abresler/nbastatR")
library("nbastatR")
get_nba_days_scores("10/06/15")
get_nba_franchise_data(return_franchises = c('all'))
get_nba_players_ids(active_only = F)
get_nba_teams_seasons_roster(team = 'Nets', include_coaches = F)
get_year_draft_combine(combine_year = 2009, return_message = T)
get_all_draft_combines(combine_years = 2000:2015) #draft combines
get_all_draft_data(draft_years = 1960:2015) # drafts
get_nba_player_injuries(filter_returning_today = T)
get_nba_synergy_stats(table_name = "Isolation",
                      include_defense = T,
                      include_offense = T,
                      type_table = 'player') # Player isolations
get_nba_synergy_stats(table_name = "Transition",
           include_defense = T,
           include_offense = T,
           type_table = "team",
           return_message = T)
  
```

## Salary Cap Data Example

```{r}
all_salaries <- 
  get_all_team_salaries()

non_guaranteed_players <- 
  all_salaries %>% 
  dplyr::filter(id.season %in% c("2015-16", "2016-17"),
                is.non.guaranteed == T)

non_guaranteed_players %>% 
  View()

team_2017_non_guaranteed_players <- 
  non_guaranteed_players %>% 
  group_by(id.season, team) %>% 
  summarise(players = n(),
            total.non_guaranteed.salary = sum(value, na.rm = T) %>% formattable::currency(digits = 0)
            ) %>% 
  ungroup() %>% 
  arrange(desc(total.non_guaranteed.salary))

team_2017_non_guaranteed_players %>% 
  View()
```
