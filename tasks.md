# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
<!-- Copy solution here -->
SELECT * FROM public.matches WHERE season = 2017;

```

2) Find all the matches featuring Barcelona.

```sql
<!-- Copy solution here -->
SELECT * FROM public.matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona';

```

3) What are the names of the Scottish divisions included?

```sql
<!-- Copy solution here -->
-- if you want all the data from the Scottish divisions:
SELECT name FROM public.divisions WHERE country = 'Scotland';
-- if you just want the names:
SELECT name, country FROM public.divisions WHERE country = 'Scotland';
```

4) Find the division code for the Bundesliga. Use that code to find out how many matches Freiburg have played in the Bundesliga since the data started being collected.

```sql
<!-- Copy solution here -->
SELECT code, name FROM public.divisions where name = 'Bundesliga';
SELECT COUNT(*) FROM public.matches WHERE division_code = 'D1' AND hometeam = 'Freiburg' awayteam = 'Freiburg';

```

5) Find the unique names of the teams which include the word "City" in their name (as entered in the database)

```sql
<!-- Copy solution here -->
-- gives you all the information on teams with the word city in their name:
SELECT * FROM public.matches WHERE hometeam LIKE '%City%' OR awayteam LIKE '%City%';

SELECT DISTINCT hometeam, awayteam FROM matches WHERE hometeam LIKE '%City%' OR awayteam LIKE '%City%';

-- for only home team:
SELECT DISTINCT hometeam FROM matches WHERE hometeam LIKE '%City%' 

```

6) How many different teams have played in matches recorded in a French division?

```sql
<!-- Copy solution here -->

SELECT COUNT(DISTINCT hometeam) FROM matches WHERE division_code = 'F1' OR division_code = 'F2';

```

7) Have Huddersfield played Swansea in the period covered?

```sql
<!-- Copy solution here -->

SELECT * FROM matches WHERE(hometeam = 'Huddersfield' OR awayteam 'Huddersfield') AND (hometeam = 'Swansea' OR awayteam = 'Swansea');

-- could also have: (same thing)
SELECT * FROM matches WHERE (hometeam = 'Huddersfield' AND awayteam = 'Swansea') OR (hometeam = 'Swansea' AND awayteam = 'Huddersfield');
```


8) How many draws were there in the Eredivisie between 2010 and 2015?

```sql
<!-- Copy solution here -->
select code from division where name = 'Eredivisie';
select count(*) from matches where division_code = 'N1' and ftr = 'D' and season between 2010 and 2015; 

```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. Where there is a tie the match with more home goals should come first.

```sql
<!-- Copy solution here -->
select code from divisions where name 'Premier League'
select * from matches where division_code = 'E0' order by (fthg + ftag) DESC, fthg DESC;

```

10) In which division and which season were the most goals scored?

```sql
<!-- Copy solution here -->

Select division_code, season, sum(fthg + ftag) from matches group by division_code, season order by sum(fthg+ ftag) DESC limit 1


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)