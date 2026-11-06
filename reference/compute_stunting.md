# Get stunting categories using multiple vectors and GIGS-recommended growth standards

Get stunting categories using multiple vectors and GIGS-recommended
growth standards

## Usage

``` r
compute_stunting(
  lenht_cm,
  age_days,
  gest_days,
  sex,
  id = NULL,
  outliers = FALSE
)
```

## Arguments

- lenht_cm:

  Numeric vector of length one or more with length/height measurement(s)
  in cm.

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

- outliers:

  A single `TRUE` or `FALSE` value specifying whether implausible
  z-score thresholds should be applied. Default = `FALSE`.

## Value

An object of class factor with the same length as the longest input
vector, containing stunting classifications. Its levels are
`c("stunting_severe", "stunting", "not_stunting")` if `outliers = FALSE`
(the default), else
`c("stunting_severe", "stunting", "not_stunting", "outlier")`. By
default, gigs will inform you this object contains unused factor levels.
You can change this behaviour using the [GIGS package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## Details

Cut-offs for stunting categories are:

|                 |                     |                     |
|-----------------|---------------------|---------------------|
| **Category**    | **Factor level**    | **Z-score bounds**  |
| Severe stunting | `"stunting_severe"` | `lhaz` =\< -3       |
| Stunting        | `"stunting"`        | -3 \< `lhaz` =\< -2 |
| No stunting     | `"not_stunting"`    | `lhaz` \> -2        |
| Outlier         | `"outlier"`         | `abs(lhaz)` \> 6    |

## Note

This function assumes that your measurements were taken according to WHO
guidelines, which stipulate that recumbent length should not be measured
after 730 days. Instead, standing height should be used. Implausible
z-score bounds are sourced from the referenced WHO report, and
classification cut-offs from the DHS manual.

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
compute_stunting(
  lenht_cm = c(52.2, 60.4, 75, 52.2, 60.4, 75),
  age_days = c(0, 100, 500, 2, 100, 500),
  gest_days = c(245, 245, 245, 280, 280, 280),
  sex = c("M", "M", "M", "F", "F", "F"),
  id = factor(c("A", "A", "A", "B", "B", "B"))
)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
#> ! Unused factor levels kept after stunting categorisation: "stunting_severe".
#> [1] not_stunting not_stunting stunting     not_stunting not_stunting
#> [6] not_stunting
#> Levels: stunting_severe stunting not_stunting

# With outlier flagging:
compute_stunting(
  lenht_cm = c(52.2, 75.4, 63.1),
  age_days = c(357, 375, 250),
  gest_days = c(196, 287, 266),
  sex = c("M", "M", "F"),
  id = factor(c("A", "B", "C")),
  outliers = TRUE
)
#> ! Unused factor levels kept after stunting categorisation: "stunting_severe".
#> [1] outlier      not_stunting stunting    
#> Levels: stunting_severe stunting not_stunting outlier

# If you don't specify `id`, the function will not identify that the fourth
# data point is a birth measurement, and will categorise it as severe
# stunting instead of not stunting
compute_stunting(
  lenht_cm = c(40.0, 60.4, 75, 40.0, 60.4, 75),
  age_days = c(0.45, 100, 500, 0.5, 100, 500),
  gest_days = c(245, 245, 245, 280, 280, 280),
  sex = c("M", "M", "M", "F", "F", "F")
)
#> [1] stunting        not_stunting    stunting        stunting_severe
#> [5] not_stunting    not_stunting   
#> Levels: stunting_severe stunting not_stunting
```
