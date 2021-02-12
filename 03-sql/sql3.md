__Question 1:__ Which team scored the most points when playing at home?  

"SELECT home_team_api_id AS home_teamID, SUM(home_team_goal) AS total_goals \
            FROM Match \
            GROUP BY home_teamID \
            ORDER BY total_goals DESC\
            LIMIT 10;"

The team with __ID 8633__ scored the most goals with 505 over the period

__Question 2:__ Did this team also score the most points when playing away?  

"SELECT away_team_api_id AS away_teamID, SUM(away_team_goal) AS total_goals \
            FROM Match \
            GROUP BY away_teamID \
            ORDER BY total_goals DESC \
            LIMIT 10;"

No, the team with __ID 8634__ scored the most away goals

__Question 3:__ How many matches resulted in a tie? 

"SELECT COUNT(id) AS count_game_ties \
            FROM Match \
            WHERE home_team_goal == away_team_goal;"

__6596__ games resulted in ties

__Question 4:__ How many players have Smith for their last name? How many have 'smith' anywhere in their name?

"SELECT COUNT() \
            FROM Player \
            WHERE player_name LIKE '%Smith';"
"SELECT COUNT() \
            FROM Player \
            WHERE player_name LIKE '% smith';"
            
__15__ people have Smith as their last name and a further __3__ have smith anywhere in their name for a total of 18

__Question 5:__ What was the median tie score? Use the value determined in the previous question for the number of tie games.

"WITH med_ties AS ( \
            SELECT id, home_team_api_id, away_team_api_id, home_team_goal, away_team_goal \
            FROM Match \
            WHERE home_team_goal == away_team_goal) \
          SELECT * FROM ( \
              SELECT \
                  ROW_NUMBER() OVER ( \
                      ORDER BY home_team_goal DESC) \
                      RowNum, id,  home_team_api_id, away_team_api_id,home_team_goal, away_team_goal \
              FROM med_ties \
              ) t \
              WHERE RowNum = 3298 OR RowNum = 3299"

The median score is __1__

__Question 6:__ What percentage of players prefer their left or right foot?

"WITH player_foot AS ( \
            SELECT player_api_id, preferred_foot \
            FROM Player_Attributes \
            GROUP BY player_api_id) \
        SELECT COUNT(player_api_id) AS number_players, preferred_foot \
            FROM player_foot \
            GROUP BY preferred_foot;"
            
__75.7%__ prefer their right foot
