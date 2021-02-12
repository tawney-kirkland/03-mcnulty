__Question 1:__ Using the same tennis data, find the number of matches played by each player in each tournament.

'WITH plays AS (\
            SELECT "Player1" AS name,COUNT(*) AS count \
            FROM aus_men \
            GROUP BY "Player1" \
            UNION ALL \
            SELECT "Player2" AS name, COUNT(*) AS count \
            FROM aus_men \
            GROUP BY "Player2") \
            SELECT name, SUM(count) AS games \
            FROM plays \
            GROUP BY name \
            ORDER BY games DESC;'

__Nadal__ played the most games in the AUS Mens Open
__Na Li and Dominika Cibulkova__ and tied for most games in AUS Women Open
__Nadal__ played the most games in the US Mens Open
__V Azarenka__ played the most games in the US Mens Open
__A Murray and N. Djokovic__ tied for most games played in Wimbledon Mens
__S.Lisicki and M.Bortoli__ tied for most games in Wimbledon womens
__Nadal and Ferrer__ tied for most games in the French Mens Open
__Serena Willians and Maria Sharapova__ tied for most games in French Womens


__Question 2:__ Who has played the most matches total in all of US Open, AUST Open, French Open? Answer this both for men and women.

'''

WITH plays AS (\
    SELECT "Player1" AS name,COUNT(*) AS count FROM french_womens GROUP BY "Player1" \
    UNION ALL \
    SELECT "Player2" AS name, COUNT(*) AS count FROM french_womens GROUP BY "Player2" \
    UNION ALL \
    SELECT "Player1" AS name,COUNT(*) AS count FROM french_men GROUP BY "Player1" \
    UNION ALL \
    SELECT "Player2" AS name, COUNT(*) AS count FROM french_men GROUP BY "Player2" \
    UNION ALL \
    SELECT "Player1" AS name,COUNT(*) AS count FROM aus_men GROUP BY "Player1" \
    UNION ALL \
    SELECT "Player2" AS name, COUNT(*) AS count FROM aus_men GROUP BY "Player2"
    UNION ALL \
    SELECT "Player1" AS name,COUNT(*) AS count FROM aus_women GROUP BY "Player1" \
    UNION ALL \
    SELECT "Player2" AS name, COUNT(*) AS count FROM aus_women GROUP BY "Player2" \
    UNION ALL \
    SELECT "Player1" AS name,COUNT(*) AS count FROM us_men GROUP BY "Player1" \
    UNION ALL \
    SELECT "Player2" AS name, COUNT(*) AS count FROM us_men GROUP BY "Player2"
    UNION ALL \
    SELECT "Player 1" AS name,COUNT(*) AS count FROM us_women GROUP BY "Player 1" \
    UNION ALL \
    SELECT "Player 2" AS name, COUNT(*) AS count FROM us_women GROUP BY "Player 2") \
    SELECT name, SUM(count) AS games \
        FROM plays \
        GROUP BY name \
        ORDER BY games DESC;'''

__Nadal__ played in the most Opens with 21 games

__Question 3:__ Who has the highest first serve percentage? (Just the maximum value in a single match.)

'''

WITH serves AS (\
    SELECT "Player1" AS name, "FSP.1" AS fsp FROM french_womens \
    UNION ALL \
    SELECT "Player2" AS name, "FSP.2" AS fsp FROM french_womens \
    UNION ALL \
    SELECT "Player1" AS name,"FSP.1" AS fsp FROM french_men \
    UNION ALL \
    SELECT "Player2" AS name, "FSP.2" AS fsp FROM french_men \
    UNION ALL \
    SELECT "Player1" AS name,"FSP.1" AS fsp FROM aus_men \
    UNION ALL \
    SELECT "Player2" AS name, "FSP.2" AS fsp FROM aus_men \
    UNION ALL \
    SELECT "Player1" AS name,"FSP.1" AS fsp FROM aus_women \
    UNION ALL \
    SELECT "Player2" AS name,"FSP.2" AS fsp FROM aus_women \
    UNION ALL \
    SELECT "Player1" AS name,"FSP.1" AS fsp FROM us_men \
    UNION ALL \
    SELECT "Player2" AS name, "FSP.2" AS fsp FROM us_men \
    UNION ALL \
    SELECT "Player 1" AS name,"FSP.1" AS fsp FROM us_women \
    UNION ALL \
    SELECT "Player 2" AS name, "FSP.2" AS fsp FROM us_women) \
    SELECT name, fsp \
        FROM serves \
        ORDER BY fsp DESC;'''

__S Errani__ has the highest FSP at 93

__Question 4:__ What are the unforced error percentages of the top three players with the most wins? (Unforced error percentage is % of points lost due to unforced errors. In a match, you have fields for number of points won by each player, and number of unforced errors for each field.)

'''
WITH wins AS (\
    SELECT "Player1" AS name, "Result" AS result, "UFE.1" AS ufe FROM french_womens WHERE "Result" =1 \
    UNION ALL \
    SELECT "Player2" AS name, "Result" AS result, "UFE.2" AS ufe FROM french_womens WHERE "Result" =0 \
    UNION ALL \
    SELECT "Player1" AS name, "Result" AS result, "UFE.1" AS ufe FROM french_men WHERE "Result" =1 \
    UNION ALL \
    SELECT "Player2" AS name, "Result" AS result, "UFE.2" AS ufe FROM french_men WHERE "Result" =0 \
    UNION ALL \
    SELECT "Player1" AS name, "Result" AS result, "UFE.1" AS ufe FROM aus_men WHERE "Result" =1 \
    UNION ALL \
    SELECT "Player2" AS name, "Result" AS result, "UFE.2" AS ufe FROM aus_men WHERE "Result" =0 \
    UNION ALL \
    SELECT "Player1" AS name, "Result" AS result, "UFE.1" AS ufe FROM aus_women WHERE "Result" =1 \
    UNION ALL \
    SELECT "Player2" AS name, "Result" AS result, "UFE.2" AS ufe FROM aus_women WHERE "Result" =0 \
    UNION ALL \
    SELECT "Player1" AS name, "Result" AS result, "UFE.1" AS ufe FROM us_men WHERE "Result" =1 \
    UNION ALL \
    SELECT "Player2" AS name, "Result" AS result, "UFE.2" AS ufe FROM us_men WHERE "Result" =0 \
    UNION ALL \
    SELECT "Player 1" AS name, "Result" AS result, "UFE.1" AS ufe FROM us_women WHERE "Result" =1 \
    UNION ALL \
    SELECT "Player 2" AS name, "Result" AS result, "UFE.2" AS ufe FROM us_women WHERE "Result" =0) \
    SELECT name, COUNT(result) AS num_wins, AVG(ufe) AS avg_ufe \
        FROM wins \
        GROUP BY name \
        ORDER BY COUNT(result) DESC;'''

__Rafael Nadal, Stanislas Wawrinka, Novak Djokovic__ are the players with the most wins with avg ufe of __27.7, 41.9 and 25.7__ respectively
