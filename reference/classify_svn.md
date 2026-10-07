# Classify small vulnerable newborns in `data.frame`-like objects with the INTERGROWTH-21^(st) weight-for-gestational age standard

Classify small vulnerable newborns in `data.frame`-like objects with the
INTERGROWTH-21^(st) weight-for-gestational age standard

## Usage

``` r
classify_svn(
  .data,
  weight_kg,
  gest_days,
  sex,
  .new = c("birthweight_centile", "svn")
)
```

## Arguments

- .data:

  A `data.frame`-like tabular object with one or more rows. Must be
  permissible by
  [`checkmate::assert_data_frame()`](https://mllg.github.io/checkmate/reference/checkDataFrame.html),
  so you can also supply a `tibble`, `data.table`, or similar.

- weight_kg:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of birth
  weight values in kg. It is assumed that weight measurements provided
  to this function are birth weights recorded \<12 hours after an
  infant's birth.

- gest_days:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of
  gestational age(s) at birth in days between `168` and `300`. By
  default, gigs will warn you about elements of this vector which are
  outside these bounds, are `NA`, or `Inf`. You can customise this
  behaviour using the [GIGS package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- sex:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a case-sensitive character
  vector of sexes, either `"M"` (male) or `"F"` (female). By default,
  gigs will warn you if any elements of `sex` are not `"M"` or `"F"`, or
  are missing (`NA`). You can customise this behaviour using the [GIGS
  package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- .new:

  A two-length character vector with names for the output columns. These
  inputs will be repaired if necessary using
  [`vctrs::vec_as_names()`](https://vctrs.r-lib.org/reference/vec_as_names.html),
  which will print any changes to the console. If any elements in `.new`
  are the same as elements in `colnames(.data)`, the function will throw
  an error. Default = `c("birthweight_centile", "svn")`.

## Value

A tabular object of the same class that was provided as `.data`, with
two new columns named according to `.new`. These columns will be (from
left to right):

- `birthweight_centile` - Numeric vector of birthweight centiles from
  the INTERGROWTH-21^(st) Newborn Size standard for weight-for-GA

- `svn` - Factor of small vulnerable newborn (SVN) categories

## Details

Cut-offs for small, vulnerable newborn categorisations are:

|  |  |  |  |
|----|----|----|----|
| **SVN category** | **Factor level** | **Centile bounds** | **Gestational age range** |
| Preterm-SGA | `"Preterm SGA"` | `p` \< 0.1 | `gest_days` \< 259 |
| Preterm-AGA | `"Preterm AGA"` | 0.1 =\< `p` =\< 0.9 | `gest_days` \< 259 |
| Preterm-LGA | `"Preterm LGA"` | `p` \> 0.9 | `gest_days` \< 259 |
| Term-SGA | `"Term SGA"` | `p` \< 0.1 | `gest_days` \>= 259 |
| Term-AGA | `"Term AGA"` | 0.1 =\< `p` =\< 0.9 | `gest_days` \>= 259 |
| Term-LGA | `"Term LGA"` | `p` \> 0.9 | `gest_days` \>= 259 |

*Abbreviations:* SGA, small-for-gestational age; AGA,
appropriate-for-gestational age; LGA, large-for-gestational age.

## Note

Categorical (factor) columns produced here may contain unused factor
levels. By default, gigs will inform you if these columns have unused
factor levels. You can change this behaviour using the [GIGS
package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## References

WHO. **Physical status: the use and interpretation of anthropometry.
Report of a WHO Expert Committee.** *World Health Organisation Technical
Report Series 1995,* **854: 1–452**

Royal College of Obstetricians and Gynaecologists. **The Investigation
and Management of the Small-for-Gestational-Age Fetus: Green-top
Guideline No. 31.** *Technical report, Royal College of Obstetricians
and Gynaecologists, London, 2013.*

## See also

See
[`classify_sfga()`](https://docs.ropensci.org/gigs/reference/classify_sfga.md)
for size-for-GA classifications which are not stratified by whether a
newborn is term. See
[`classify_growth()`](https://docs.ropensci.org/gigs/reference/classify_growth.md)
to run this analysis and others at the same time.

## Examples

``` r
data <- data.frame(
  wt_kg = c(1.5, 2.6, 2.6, 3.5),
  gestage = c(235, 257, 275, 295),
  sex = c("F", "M", "F", "M")
)

data |>
  classify_svn(weight_kg = wt_kg,
               gest_days = gestage,
               sex = sex)
#> ! Unused factor levels kept after small vulnerable newborn categorisation:
#> "Preterm LGA" and "Term LGA".
#>   wt_kg gestage sex birthweight_centile         svn
#> 1   1.5     235   F          0.07039106 Preterm SGA
#> 2   2.6     257   M          0.27470460 Preterm AGA
#> 3   2.6     275   F          0.06389942    Term SGA
#> 4   3.5     295   M          0.36209260    Term AGA
```
