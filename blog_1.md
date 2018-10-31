# a blog post 

a not quite point in polygon summary.
final:
```SQL
select commercialdivision,pl.feedername, parish, constituen, division,  count(sl.*) light_count, sum(wattage) wattage from voluminous.streetlamp_data_20180528aaa sl
cross join lateral (
  select * from livewire.primarylines pl
  order by sl.g <-> pl.g
  limit 1
) as pl
cross join lateral (
  select * from base.parishcouncils pc
  order by pc.geom <-> sl.g
  limit 1
) as pc

--left join base.parishcouncils pc on st_intersects(sl.g,pc.geom)
left join base.feeders f on f.feedername = pl.feedername
group by 1,2,3,4,5
order by 1,2,3,4,5
```
first:

```SQL
select commercialdivision,pl.feedername, parish, constituen, division,  count(sl.*) light_count, sum(wattage) wattage from voluminous.streetlamp_data_20180528aaa sl
cross join lateral (
  select * from livewire.primarylines pl
  order by sl.g <-> pl.g
  limit 1
) as pl
join base.parishcouncils pc on st_intersects(sl.g,pc.geom)
left join base.feeders f on f.feedername = pl.feedername
group by 1,2,3,4,5
order by 1,2,3,4,5
```



second:
```SQL
select commercialdivision,pl.feedername, parish, constituen, division,  count(sl.*) light_count, sum(wattage) wattage from voluminous.streetlamp_data_20180528aaa sl
cross join lateral (
  select * from livewire.primarylines pl
  order by sl.g <-> pl.g
  limit 1
) as pl
left join base.parishcouncils pc on st_intersects(sl.g,pc.geom)
left join base.feeders f on f.feedername = pl.feedername
group by 1,2,3,4,5
order by 1,2,3,4,5
```



