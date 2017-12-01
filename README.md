Day 1
-----

(Star 1 omitted, as it's a simplified version of star 2.)

```SQL
select sum(d) from (
    select
        d::int,
        (lead(d, length($1) / 2) over (order by ord))::int as next,
        row_number() over (order by ord) <= length($1) as include
    from regexp_split_to_table(repeat($1, 2), '') with ordinality as r(d, ord)
) ss
where include and d = next
```
