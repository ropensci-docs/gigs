# Classify size-for-gestational age in `data.frame`-like objects with the INTERGROWTH-21^(st) weight-for-gestational age standard

Classify size-for-gestational age in `data.frame`-like objects with the
INTERGROWTH-21^(st) weight-for-gestational age standard

## Usage

``` r
classify_sfga(
  .data,
  weight_kg,
  gest_days,
  sex,
  .new = c("birthweight_centile", "sfga", "sfga_severe")
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

  A three-length character vector with names for the output columns.
  These inputs will be repaired if necessary using
  [`vctrs::vec_as_names()`](https://vctrs.r-lib.org/reference/vec_as_names.html),
  which will print any changes to the console. If any elements in `.new`
  are the same as elements in `colnames(.data)`, the function will throw
  an error. Default = `c("birthweight_centile", "sfga", "sfga_severe")`.

## Value

A tabular object of the same class that was provided as `.data`, with
three new columns named according to `.new`. These columns will be (from
left to right):

- `birthweight_centile` - Numeric vector of birthweight centiles from
  the INTERGROWTH-21^(st) Newborn Size standard for weight-for-GA

- `sfga` - Factor of size-for-GA categories without severe small-for-GA
  classification

- `sfga_severe` - Factor of size-for-GA categories with severe
  small-for-GA classification

## Details

Cut-offs for size-for-gestational age categorisations are:

|                       |                  |                     |
|-----------------------|------------------|---------------------|
| **Category**          | **Factor level** | **Centile bounds**  |
| Severely small-for-GA | `"SGA(<3)"`      | `p` \< 0.03         |
| Small-for-GA          | `"SGA"`          | `p` \< 0.1          |
| Appropriate-for-GA    | `"AGA"`          | 0.1 =\< `p` =\< 0.9 |
| Large-for-GA          | `"LGA"`          | `p` \> 0.9          |

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
[`classify_svn()`](https://docs.ropensci.org/gigs/reference/classify_svn.md)
for size-for-GA classifications which are stratified by whether a
newborn is term. See
[`classify_growth()`](https://docs.ropensci.org/gigs/reference/classify_growth.md)
to run this analysis and others at the same time.

## Examples

``` r
data <- data.frame(
 wt_kg = c(2.2, 2.5, 3.3, 4.0),
 gestage = 266:269,
 sex = c("F", "M", "F", "M")
)

data |>
  classify_sfga(weight_kg = wt_kg,
                gest_days = gestage,
                sex = sex)
#>   wt_kg gestage sex birthweight_centile sfga sfga_severe
#> 1   2.2     266   F          0.01890983  SGA     SGA(<3)
#> 2   2.5     267   M          0.06485308  SGA         SGA
#> 3   3.3     268   F          0.75655402  AGA         AGA
#> 4   4.0     269   M          0.97108564  LGA         LGA
```
