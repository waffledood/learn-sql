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
WHERE division = 'FBS (Division I-A Teams)';
```

_Sample Answer_
```sql
SELECT players.player_name,
       players.school_name,
       teams.conference
  FROM benn.college_football_players players
  JOIN benn.college_football_teams teams
    ON teams.school_name = players.school_name
 WHERE teams.division = 'FBS (Division I-A Teams)';
 ```

**_Feedback_**
- Try to make it a habit to explicitly label which table a column being selected is from, i.e. `players.player_name` instead of just `player_name`

### Left Join

_Question_
Write a query that performs an inner join between the tutorial.crunchbase_acquisitions table and the tutorial.crunchbase_companies table, but instead of listing individual rows, count the number of non-null rows in each table.

_My Attempt_
```sql
SELECT COUNT(companies),
       COUNT(acquisitions)
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink;
```

_Sample Answer_
```sql
SELECT COUNT(companies.permalink) AS companies_rowcount,
       COUNT(acquisitions.company_permalink) AS acquisitions_rowcount
  FROM tutorial.crunchbase_companies companies
  JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink;
```

**_Feedback_**
I feel that the question is a bit misleading, saying to count the number of rows in each table, but doesn't specify to do so for each table respectively (either before the join, or after the join)

_Question_
Count the number of unique companies (don't double-count companies) and unique acquired companies by state. Do not include results for which there is no state data, and order by the number of acquired companies from highest to lowest.

_My Attempt_
```sql
SELECT COUNT(DISTINCT companies.name) AS "Distinct Companies",
       COUNT(DISTINCT companies.permalink)
  FROM tutorial.crunchbase_companies companies
  JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
 WHERE state_code IS NOT NULL;
```

_Sample Answer_
```sql
SELECT companies.state_code,
       COUNT(DISTINCT companies.permalink) AS unique_companies,
       COUNT(DISTINCT acquisitions.company_permalink) AS unique_companies_acquired
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
 WHERE companies.state_code IS NOT NULL
 GROUP BY 1
 ORDER BY 3 DESC
```

_Feedback_
Totally misunderstood the question & hence came up with the wrong solutions. After looking at the sample answer, I understand the question is asking for the number of companies in each state & the number of companies in each state that got acquired, hence the 3 columns.

### Right Join

_Question_
Rewrite the previous practice query in which you counted total and acquired companies by state, but with a RIGHT JOIN instead of a LEFT JOIN. The goal is to produce the exact same results.

_My Attempt_
```sql
SELECT companies.state_code,
       COUNT(DISTINCT companies.permalink) AS "Number of Companies",
       COUNT(DISTINCT acquisitions.acquirer_permalink) AS "Number of Companies (Acquired)"
FROM tutorial.crunchbase_acquisitions acquisitions
RIGHT JOIN tutorial.crunchbase_companies companies
ON companies.permalink = acquisitions.company_permalink
WHERE companies.state_code IS NOT NULL
GROUP BY companies.state_code;
```

_Sample Answer_
```sql
SELECT companies.state_code,
       COUNT(DISTINCT companies.permalink) AS unique_companies,
       COUNT(DISTINCT acquisitions.company_permalink) AS acquired_companies
  FROM tutorial.crunchbase_acquisitions acquisitions
 RIGHT JOIN tutorial.crunchbase_companies companies
    ON companies.permalink = acquisitions.company_permalink
 WHERE companies.state_code IS NOT NULL
 GROUP BY 1
 ORDER BY 3 DESC
```

### Filtering in the ON or WHERE clause

_Question_
Write a query that shows a company's name, "status" (found in the Companies table), and the number of unique investors in that company. Order by the number of investors from most to fewest. Limit to only companies in the state of New York.

_My Attempt_
```sql
SELECT companies.name,
       companies.status,
       COUNT(DISTINCT investments.investor_permalink) AS "No. Of Unique Investors"
FROM tutorial.crunchbase_companies companies
JOIN tutorial.crunchbase_investments investments 
ON companies.permalink = investments.company_permalink
WHERE companies.state_code = 'NY'
GROUP BY companies.name, companies.status
ORDER BY "No. Of Unique Investors";
```

_Sample Answer_
```sql
SELECT companies.name AS company_name,
       companies.status,
       COUNT(DISTINCT investments.investor_name) AS unqiue_investors
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments investments
    ON companies.permalink = investments.company_permalink
 WHERE companies.state_code = 'NY'
 GROUP BY 1,2
 ORDER BY 3 DESC
```

_Feedback_
Using _just_ `JOIN` leaves out companies that don't have any investors. A `LEFT JOIN` would have been more appropriate & in line with what the question asked. 


## Advanced
