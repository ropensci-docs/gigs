# Data extract from the Low birthweight Infant Feeding Exploration (LIFE) study

A subset of anthropometric data for 300 singleton infants enrolled in
the Low birthweight Infant Feeding Exploration (LIFE) study. The
variables are as follows:

## Format

A data frame with 2,191 rows and 10 variables:

- `id`::

  Unique ID for each infant in the dataset (1–300).

- `visitweek`::

  Chronological age in weeks (±1) when study visit occurred (0–26).

- `sex`::

  Sex of the infant as a factor (`"M"` = Male; `"F"` = Female).

- `gestage`::

  Best obstetric estimate of gestational age in days (181–291).

- `age_days`::

  Chronological age in days at each visit; equal to `pma - gestage`
  (0–242).

- `pma`::

  Post-menstrual age in days (182–528).

- `wt_kg`::

  Mean weight in kg (1.24–9.40667).

- `len_cm`::

  Mean length in cm (37.37–72.93).

- `headcirc_cm`::

  Mean head circumference in cm (23.20–44.87).

- `muac_cm`::

  Mean mid-upper arm circumference in cm (6.30–16.83).

## Note

We subsetted the full LIFE 6 month dataset for
[gigs](https://docs.ropensci.org/gigs/reference/gigs-package.md). As
such, this extract only includes data from 300 singleton pregnancies
where the best estimate of gestational age was \>168 days. We also
removed rows corresponding to visit weeks where no measurement data was
taken due to non-attendance of the visit.

## References

Vesel L, Bellad RM, Manji K, Saidi F, Velasquez E, Sudfeld C, et al.
**Feeding practices and growth patterns of moderately low birthweight
infants in resource-limited settings: results from a multisite,
longitudinal observational study.** *BMJ Open* 2023, **13(2):e067316.**
[doi:10.1136/BMJOPEN-2022-067316](https://doi.org/10.1136/BMJOPEN-2022-067316)

## Examples

``` r
head(gigs::life6mo)
#>   id gestage sex visitweek pma age_days    wt_kg   len_cm headcirc_cm   muac_cm
#> 1  1     273   M         0 273        0 2.300000 42.06667    33.26667  9.433333
#> 2  1     273   M         1 280        7 2.185000 42.13333    33.33333  9.566667
#> 3  1     273   M         2 288       15 2.325000 43.66667    35.06667  9.633334
#> 4  1     273   M         4 301       28 2.575000 47.46667    37.66667  9.933333
#> 5  1     273   M         6 316       43 3.410000 49.00000    39.00000 11.400000
#> 6  1     273   M        10 344       71 4.262333 55.03333    41.03333 13.466667
```
