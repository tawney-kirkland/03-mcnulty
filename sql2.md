__Question 1__: What was the total spent on salaries by each team, each year?

SELECT yearID, teamID, sum(salary) \
        FROM salaries \
        GROUP BY teamID, yearID;"
        
__Question 2__: What is the first and last year played for each player?

"SELECT playerID, MIN(yearID) AS first_year, MAX(yearID) AS final_year \
            FROM fielding \
            GROUP BY playerID;"
            
__Question 3__: Who has played the most all star games?

"SELECT playerID, count(awardID) AS number_awards\
            FROM awardsplayers \
            GROUP BY playerID \
            ORDER BY number_awards DESC;"
 
 __bondsba01__ has won the most all star games with 47 games
 
 __Question 4__: Which school has generated the most distinct players?
 
 "SELECT COUNT(DISTINCT(playerID)) AS unique_players,schoolID \
            FROM collegeplaying \
            GROUP BY schoolID \
            ORDER BY unique_players DESC;"

__Texas__ has created the most unique players with 107

__Question 5__: Which players have the longest career? Assume that the debut and finalGame columns comprise the start and end, respectively, of a player's career.

"SELECT playerID, debut AS first_game, finalGame AS final_game, (DATE(finalGame) - DATE(debut)) AS career \
            FROM people \
            ORDER BY career DESC;"

__altroni01__ had the longest career at 35 years

__Question 6__: What is the distribution of debut months?

"WITH months AS ( \
             SELECT strftime('%m', DATE(debut)) AS debut_month \
             FROM people) \
          SELECT MIN(debut_month) AS Min_month, \
          AVG(debut_month) AS Mean_month, \
          MAX(debut_month) AS Max_month \
          FROM months;"
          
__Question 7__: What is the effect of table join order on mean salary for the players listed in the main (master) table?

"WITH avg_salary AS ( \
            SELECT playerID, AVG(salary) AS average_salary \
            FROM salaries \
            GROUP BY playerID) \
        SELECT * FROM people \
            LEFT JOIN avg_salary \
            ON people.playerID = avg_salary.playerID \
            ORDER BY average_salary DESC;"
            
 "WITH avg_salary AS ( \
            SELECT playerID, AVG(salary) AS average_salary \
            FROM salaries \
            GROUP BY playerID) \
        SELECT * FROM avg_salary \
            LEFT JOIN people \
            ON avg_salary.playerID = people.playerID \
            ORDER BY average_salary DESC;"
  
  Because there is not salary data for every player, when you merge avg_salary onto the people data table, you end up with lots of NaNs. However, when you join in the reverse order, it only adds rows from people that also exist in avg_salary 
            
            
            
            
