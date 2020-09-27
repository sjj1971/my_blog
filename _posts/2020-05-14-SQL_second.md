---
title: "SQL using postgres! part 2"
date: 2020-05-14 23:00:00 
categories: programming
---

Join table
```sql
select table_1.column_1, table_2.column_2
from table_1
inner join table_2
on table_1.column_x = table_2.column_y
```
Aggregation (count, sum, avg, min, max) & sorting
```sql
select column_1, AVG(column_2), MIN(column_3)
from table_name
group by column_1
order by avg(column_2)
limit 5;
```
Subquery
```sql
select column_1 from table_1
where column_2 in
(
select column_2 from table_2
where column_3 = value
)
```
Join and Aggregation
```sql
select table_1.column_1, avg(table2.column_2)
from table_1
inner join table_2
using (column_3)
group by table_1.column_1;
```
Foreign Key
```sql
create table table_name(
    id serial primary key,
    column_2 data_type,
    foreign key(column_2) references table_1(primary key)
);
```
Union (it is showing at the same output table)
```sql
select toy_id from toys
union # or 'union all' to show duplicated rows also
select game_id from games;
```

### ERD
https://www.quickdatabasediagrams.com/


