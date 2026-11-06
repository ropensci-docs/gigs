# Classify head size in `data.frame`-like objects with GIGS-recommended growth standards

Classify head size in `data.frame`-like objects with GIGS-recommended
growth standards

## Usage

``` r
classify_headsize(
  .data,
  headcirc_cm,
  age_days,
  gest_days,
  sex,
  id = NULL,
  .new = c("hcaz", "headsize")
)
```

## Arguments

- .data:

  A `data.frame`-like tabular object with one or more rows. Must be
  permissible by
  [`checkmate::assert_data_frame()`](https://mllg.github.io/checkmate/reference/checkDataFrame.html),
  so you can also supply a `tibble`, `data.table`, or similar.

- headcirc_cm:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of head
  circumference values in cm.

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
  an error. Default = `c("hcaz", "headsize")`.

## Value

A tabular object of the same class that was provided as `.data`, with
three new columns named according to `.new`. These columns will be (from
left to right):

- `hcaz` - Numeric vector of weight-for-length/height zscores

- `headsize` - Factor of head size categories

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

## Note

Categorical (factor) columns produced here may contain unused factor
levels. By default, gigs will inform you if these columns have unused
factor levels. You can change this behaviour using the [GIGS
package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## References

Victora CG, Schuler-Faccini L, Matijasevich A, Ribeiro E, Pessoa A,
Barros FC. **Microcephaly in Brazil: how to interpret reported
numbers?** *The Lancet* 2016, *387(10019):621-624*
[doi:10.1016/S0140-6736(16)00273-7](https://doi.org/10.1016/S0140-6736%2816%2900273-7)

Accogli A, Geraldo AF, Piccolo G, Riva A, Scala M, Balagura G, et al.
**Diagnostic Approach to Macrocephaly in Children**. *Frontiers in
Paediatrics* 2022, *9:794069*
[doi:10.3389/fped.2021.794069](https://doi.org/10.3389/fped.2021.794069)

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
  gestage  = c(rep(35 * 7, 3), rep(35 * 7, 3)),
  sex = rep.int(c("M", "F"), c(3, 3)),
  headcirc_cm = rep.int(c(40, 50, 60), 2)
)

# Use the `id` argument to ensure that `classify_headsize()` uses the correct
# standard for each observation
data |>
  classify_headsize(headcirc_cm = headcirc_cm,
                    age_days = agedays,
                    gest_days = gestage,
                    sex = sex,
                    id = child)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
#> ! Unused factor levels kept after head size categorisation:
#> "microcephaly_severe", "microcephaly", "normal_headcirc", and "macrocephaly".
#>   child agedays gestage sex headcirc_cm      hcaz            headsize
#> 1     A       0     245   M          40  4.759628 macrocephaly_severe
#> 2     A     100     245   M          50 10.907943 macrocephaly_severe
#> 3     A     500     245   M          60  9.804805 macrocephaly_severe
#> 4     B       2     245   F          40  4.807734 macrocephaly_severe
#> 5     B     100     245   F          50 11.700306 macrocephaly_severe
#> 6     B     500     245   F          60 10.202535 macrocephaly_severe

# If you don't specify `id`, `classify_headsize()` will assume data is from
# one child only
data |>
  classify_headsize(headcirc_cm = headcirc_cm,
                    age_days = agedays,
                    gest_days = gestage,
                    sex = sex)
#> ! Unused factor levels kept after head size categorisation:
#> "microcephaly_severe", "microcephaly", "normal_headcirc", and "macrocephaly".
#>   child agedays gestage sex headcirc_cm      hcaz            headsize
#> 1     A       0     245   M          40  4.759628 macrocephaly_severe
#> 2     A     100     245   M          50 10.907943 macrocephaly_severe
#> 3     A     500     245   M          60  9.804805 macrocephaly_severe
#> 4     B       2     245   F          40  7.961152 macrocephaly_severe
#> 5     B     100     245   F          50 11.700306 macrocephaly_severe
#> 6     B     500     245   F          60 10.202535 macrocephaly_severe
```
