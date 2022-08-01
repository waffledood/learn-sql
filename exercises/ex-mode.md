# Exercises (Mode.com)

## Basic 



## Intermediate

### Outer Joins

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

_Feedback_
- Try to make it a habit to explicitly label which table a column being selected is from, i.e. `players.player_name` instead of just `player_name`

## Advanced
