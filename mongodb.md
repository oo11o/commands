### Range

```
population_range[`$lt`] = 1000000;
population_range[`$gt`] = 10000;

db.towns.find(
  {population: population_range}
)
```
