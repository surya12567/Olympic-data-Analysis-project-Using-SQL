# SQL-Portfolio project-Olympic data Analysis-project

For this blog, I am going to showcase some beginner MySQL skills with a data set I have of Olympic statistics. Normally, I start off a blog post with a question and try and answer that question by combing through the data. This time, and mostly because I want to showcase how to use MySQL queries, I will be asking several small questions about the data, then writing some code to try and see if we can answer it. I think this Olympic data set is interesting, so we should be able to pull out some fun group-bys and aggregations.


1.write a sql query to find in which sport or event india has won the highest medals?

    SELECT event,COUNT(medal)
    FROM oly_event
    WHERE team='India'
    AND medal <> 'NA'
    GROUP BY event
    ORDER BY COUNT(medal) DESC;

 2.How many events are held in olympics?

    SELECT DISTINCT COUNT(event)
    FROM oly_event;

3.Ientify the sport or event which was played most consecutively in the summer Olympics games?
    
    SELECT event, COUNT( event)
    FROM oly_event
    WHERE season='Summer'
    GROUP BY event
    ORDER BY COUNT(event) DESC;

 4.write the sql query to fetch the details of the all countries which have won most number of silver and bronze medals and at least one gold medal?
     
     SELECT team,SUM(Silver),
                 SUM(Bronze),
                 SUM(Gold)
    FROM (SELECT *,
    CASE medal WHEN 'Silver' THEN 1 ELSE 0 END AS Silver,
    CASE medal WHEN 'Bronze' THEN 1 ELSE 0 END AS Bronze,
    CASE medal WHEN 'Gold' THEN 1 ELSE 0 END AS Gold,
    FROM oly_event
    )innerT
    GROUP BY team
    HAVING MAX(Gold)>0
    ORDER BY COUNT(silver) DESC;

5.Which Countries have won most medals?
   
    SELECT noc,COUNT(medal)
    FROM oly_event
    WHERE medal<> 'NA'
    GROUP BY noc
    ORDER BY COUNT(medal) desc;

6.Which cities have hosted most Olympics. Find top 5 cities?

    SELECT city,COUNT(DISTINCT year ) AS dy
    FROM oly_event
    GROUP BY city
    ORDER BY dy DESC
    LIMIT 5;

7.Which cities have hosted most Olympics. Find top 5 cities?

    SELECT sport ,COUNT(sex) AS cs
    FROM oly_event
    WHERE sex='F'
    GROUP BY sport 
    ORDER BY  cs desc
    LIMIT 5;

8.Which player has won max number of gold medals?

    SELECT fname,SUM(gold)
    FROM
    (SELECT *,
     CASE medal WHEN 'Gold' THEN 1 ELSE 0 END AS Gold

     FROM oly_event
    )xyz
     GROUP BY fname 
     HAVING MAX(Gold)>0
     ORDER BY SUM(gold) DESC;


9.which sport has maximum events ?
 
    SELECT sport, COUNT(DISTINCT event)
    FROM oly_event
    GROUP BY sport
    ORDER BY COUNT(sport) desc;


10.Which countries won maximum medal in one year and in which year?

    SELECT noc, year, COUNT(medal) AS total_medals
    FROM Oly_event
    WHERE medal <> 'NA'
    GROUP BY noc, year
    ORDER BY total_medals DESC
    LIMIT 1;

12.To find the sports conducted how many times in the given year of 2000 and 2016

    SELECT sport, COUNT(*)sport
    FROM oly_event
    WHERE year BETWEEN 2000 AND 2016
    GROUP BY sport
    ORDER BY COUNT(sport) DESC;

13.To find the sports conducted how many times in this year

    SELECT sport, COUNT(*)sport
    FROM oly_event
    GROUP BY sport
    ORDER BY COUNT(sport) DESC;
