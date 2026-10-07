# Get head size categories using multiple vectors and GIGS-recommended growth standards

Get head size categories using multiple vectors and GIGS-recommended
growth standards

## Usage

``` r
compute_headsize(headcirc_cm, age_days, gest_days, sex, id = NULL)
```

## Arguments

- headcirc_cm:

  Numeric vector of length one or more with head circumference
  measurement(s) in cm.

- age_days:

  Numeric vector of length one or more with age(s) in days for each
  child. Should be between `0` to `1856` days. By default, gigs will
  replace out-of-bounds elements in `age_days` with `NA` and warn you.
  This behaviour can be customised using the functions in
  [gigs_options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- gest_days:

  Numeric vector with gestational age(s) at birth in days.

- sex:

  Character vector of length one or more with sex(es), either `"M"`
  (male) or `"F"` (female). This argument is case-sensitive. By default,
  gigs will replace elements of `sex` which are not `"M"` or `"F"` with
  `NA` and warn you. You can customise this behaviour using the [GIGS
  package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- id:

  A factor of length one or more with an ID for each observation, either
  ordered or unordered, containing no missing (`NA`) values. When
  supplied, `id` is used to ensure that only the earliest measurement
  for each individual is used as a birth measure. Leave this argument as
  `NULL` if all your data comes from the same individual. Default =
  `NULL`.

## Value

An object of class factor with the same length as `wlz`, containing
wasting classifications. Its levels are
`c("wasting_severe", "wasting", "not_wasting", "overweight")` if
`outliers = FALSE` (the default), else
`c("wasting_severe", "wasting", "not_wasting", "overweight", "outlier")`.
By default, gigs will inform you this object contains unused factor
levels. You can change this behaviour using the [GIGS package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## Details

Cut-offs for head size categories are:

|                           |                         |                     |
|---------------------------|-------------------------|---------------------|
| **Category**              | **Factor level**        | **Z-score bounds**  |
| Severe microcephaly       | `"microcephaly_severe"` | `hcaz` =\< -3       |
| Microcephaly              | `"microcephaly"`        | -3 \< `hcaz` =\< -2 |
| Normal head circumference | `"normal_headcirc"`     | `abs(hcaz)` \< 2    |
| Macrocephaly              | `"macrocephaly"`        | `hcaz` \>= 2        |
| Severe macrocephaly       | `"macrocephaly_severe"` | `hcaz` \>= 3        |

## References

**'Implausible z-score values'** *in* World Health Organization (ed.)
*Recommendations for data collection, analysis and reporting on
anthropometric indicators in children under 5 years old*. Geneva: World
Health Organization and the United Nations Children's Fund UNICEF,
(2019). pp. 64-65.

**'Percentage of children stunted, wasted, and underweight, and mean
z-scores for stunting, wasting and underweight'** *in* *Guide to DHS
Statistics DHS-7* Rockville, Maryland, USA: ICF (2020). pp. 431-435.
<https://dhsprogram.com/data/Guide-to-DHS-Statistics/Nutritional_Status.htm>

## Examples

``` r
# The first observation for each infant in `id` uses the INTERGROWTH-21st
#  Newborn Size standards; the next two use either the INTERGROWTH-21st
# Postnatal Growth standards or WHO Child Growth Standards.
compute_headsize(
  headcirc_cm = c(31.6, 40, 50, 31.6, 40, 50),
  age_days = c(0, 100, 500, 2, 100, 500),
  gest_days = c(245, 245, 245, 280, 280, 280),
  sex = c("M", "M", "M", "F", "F", "F"),
  id = factor(c("A", "A", "A", "B", "B", "B"))
)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
#> ! Unused factor levels kept after head size categorisation:
#> "microcephaly_severe", "microcephaly", and "macrocephaly_severe".
#> [1] normal_headcirc normal_headcirc macrocephaly    normal_headcirc
#> [5] normal_headcirc macrocephaly   
#> 5 Levels: microcephaly_severe microcephaly normal_headcirc ... macrocephaly_severe

# If you don't specify `id`, the function will not identify that the fourth
# data point is a birth measurement, and will categorise it as microcephalic
# instead of normal
compute_headsize(
  headcirc_cm = c(31.6, 40, 50, 31.6, 40, 50),
  age_days = c(0, 100, 500, 2, 100, 500),
  gest_days = c(245, 245, 245, 280, 280, 280),
  sex = c("M", "M", "M", "F", "F", "F")
)
#> ! Unused factor levels kept after head size categorisation:
#> "microcephaly_severe" and "macrocephaly_severe".
#> [1] normal_headcirc normal_headcirc macrocephaly    microcephaly   
#> [5] normal_headcirc macrocephaly   
#> 5 Levels: microcephaly_severe microcephaly normal_headcirc ... macrocephaly_severe
```
