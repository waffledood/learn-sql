# Exercises (Mode.com)

## Basic 



## Intermediate

### Outer Joins

_Question_
Write a query that displays player names, school names and conferences for schools in the "FBS (Division I-A Teams)" division.

_My Attempt_
```sql
SELECT player_name,
       players.school_name AS "School Name",
       conference
FROM benn.college_football_players players
JOIN benn.college_football_teams teams
ON teams.school_name = players.school_name
WHERE division = 'FBS (Division I-A Teams)';```

_Sample Answer_
```sql
SELECT players.player_name,
       players.school_name,
       teams.conference
  FROM benn.college_football_players players
  JOIN benn.college_football_teams teams
    ON teams.school_name = players.school_name
 WHERE teams.division = 'FBS (Division I-A Teams)'```

**_Feedback_**
- Try to make it a habit to explicitly label which table a column being selected is from, i.e. `players.player_name` instead of just `player_name`

### Left Join

_Question_
Write a query that performs an inner join between the tutorial.crunchbase_acquisitions table and the tutorial.crunchbase_companies table, but instead of listing individual rows, count the number of non-null rows in each table.

_My Attempt_
SELECT COUNT(companies),
       COUNT(acquisitions)
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink

_Sample Answer_
SELECT COUNT(companies.permalink) AS companies_rowcount,
       COUNT(acquisitions.company_permalink) AS acquisitions_rowcount
  FROM tutorial.crunchbase_companies companies
  JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink

**_Feedback_**
I feel that the question is a bit misleading, saying to count the number of rows in each table, but doesn't specify to do so for each table respectively (either before the join, or after the join)

## Advanced