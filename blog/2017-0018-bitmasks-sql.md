extends: post.liquid
title: Bitmasks in SQL
date: 1 Jul 2017 18:27:29 +0100
path: 2017/bitmasks-sql
tags: oracle, sql, bitmasks
---

bitmasks are really handy way to express predicates without becoming overly
verbose with parens and logical operators (`AND` and `OR`). Assume we have the 
following table.

```
| what        | wanted |
|-------------|--------|
| need me too | 4      |
| alpha       | 1      |
| beta        | 2      |

with data as
(
select 'appears_in_both', 4 as wanted from dual
union all
select 'alpha', 1 as wanted from dual
union all
select 'beta', 2 as wanted from dual
)
...
```

## Get "need me too" and "alpha" together

```sql
...
select * 
from data
where bitand(wanted, 5) <> 0; -- (4 + 1)
```

## Get "need me too" and "beta" together

```sql
...
select * 
from data
where bitand(wanted, 6) <> 0; -- (4 + 2)
```