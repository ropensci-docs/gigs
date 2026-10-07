# Classify stunting in `data.frame`-like objects with GIGS-recommended growth standards

Classify stunting in `data.frame`-like objects with GIGS-recommended
growth standards

## Usage

``` r
classify_stunting(
  .data,
  lenht_cm,
  age_days,
  gest_days,
  sex,
  id = NULL,
  .new = c("lhaz", "stunting", "stunting_outliers")
)
```

## Arguments

- .data:

  A `data.frame`-like tabular object with one or more rows. Must be
  permissible by
  [`checkmate::assert_data_frame()`](https://mllg.github.io/checkmate/reference/checkDataFrame.html),
  so you can also supply a `tibble`, `data.table`, or similar.

- lenht_cm:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of
  length/height values in cm.

- age_days:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of age
  values in days.

- gest_days:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of
  gestational age(s) at birth in days. This column, in conjunction with
  the column referred to by `age_days`, is used to select which growth
  standard to use for each observation.

- sex:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a case-sensitive character
  vector of sexes, either `"M"` (male) or `"F"` (female). By default,
  gigs will warn you if any elements of `sex` are not `"M"` or `"F"`, or
  are missing (`NA`). You can customise this behaviour using the [GIGS
  package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- id:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a factor variable with IDs
  for each observation. When not `NULL`, this variable is used to ensure
  that only the first measurement taken from each infant is used as a
  birth measure. If all your data is from one individual, leave this
  parameter as `NULL`. Default = `NULL`.

- .new:

  A three-length character vector with names for the output columns.
  These inputs will be repaired if necessary using
  [`vctrs::vec_as_names()`](https://vctrs.r-lib.org/reference/vec_as_names.html),
  which will print any changes to the console. If any elements in `.new`
  are the same as elements in `colnames(.data)`, the function will throw
  an error. Default = `c("lhaz", "stunting", "stunting_outliers")`.

## Value

A tabular object of the same class that was provided as `.data`, with
three new columns named according to `.new`. These columns will be (from
left to right):

- `lhaz` - Numeric vector of length/height-for-age zscores

- `stunting` - Factor of stunting categories without outlier flagging

- `stunting_outliers` - Factor of stunting categories with outlier
  flagging

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

Categorical (factor) columns produced here may contain unused factor
levels. By default, gigs will inform you if these columns have unused
factor levels. You can change this behaviour using the [GIGS
package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

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

## See also

See
[`classify_growth()`](https://docs.ropensci.org/gigs/reference/classify_growth.md)
to run this analysis and others at the same time. See
[`gigs_waz()`](https://docs.ropensci.org/gigs/reference/gigs_zscoring.md)
to learn which growth standard will be used for different combinations
of gestational/chronological age.

## Examples

``` r
# This dummy dataset contains data from two people, from birth (<3 days) to
# 500 days of age.
data <- data.frame(
  child = factor(rep.int(c("A", "B"), c(3, 3))),
  agedays = c(0, 100, 500, 2, 100, 500),
  gestage  = c(rep(35 * 7, 3), rep(40 * 7, 3)),
  sex = rep.int(c("M", "F"), c(3, 3)),
  length_cm = rep.int(c(52.2, 60.4, 75), 2)
)

# Use the `id` argument to ensure that `classify_stunting` uses the correct
# standard for each observation
data |>
  classify_stunting(lenht_cm = length_cm,
                    age_days = agedays,
                    gest_days = gestage,
                    sex = sex,
                    id = child)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
#> ! Unused factor levels kept after stunting categorisation: "stunting_severe".
#> ! Unused factor levels kept after stunting categorisation: "stunting_severe"
#> and "outlier".
#>   child agedays gestage sex length_cm        lhaz     stunting
#> 1     A       0     245   M      52.2  2.82368563 not_stunting
#> 2     A     100     245   M      60.4  0.88764438 not_stunting
#> 3     A     500     245   M      75.0 -2.16900825     stunting
#> 4     B       2     280   F      52.2  1.86816342 not_stunting
#> 5     B     100     280   F      60.4 -0.04512913 not_stunting
#> 6     B     500     280   F      75.0 -1.44230628 not_stunting
#>   stunting_outliers
#> 1      not_stunting
#> 2      not_stunting
#> 3          stunting
#> 4      not_stunting
#> 5      not_stunting
#> 6      not_stunting

# If you don't specify `id`, `classify_stunting` will assume data is from one
# child only
data |>
  classify_stunting(lenht_cm = length_cm,
                    age_days = agedays,
                    gest_days = gestage,
                    sex = sex)
#> ! Unused factor levels kept after stunting categorisation: "stunting_severe".
#> ! Unused factor levels kept after stunting categorisation: "stunting_severe"
#> and "outlier".
#>   child agedays gestage sex length_cm        lhaz     stunting
#> 1     A       0     245   M      52.2  2.82368563 not_stunting
#> 2     A     100     245   M      60.4  0.88764438 not_stunting
#> 3     A     500     245   M      75.0 -2.16900825     stunting
#> 4     B       2     280   F      52.2  1.45276970 not_stunting
#> 5     B     100     280   F      60.4 -0.04512913 not_stunting
#> 6     B     500     280   F      75.0 -1.44230628 not_stunting
#>   stunting_outliers
#> 1      not_stunting
#> 2      not_stunting
#> 3          stunting
#> 4      not_stunting
#> 5      not_stunting
#> 6      not_stunting
```
